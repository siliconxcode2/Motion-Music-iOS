# Architecture

Draft, growing each round.

## Module layout (D29)

The app is a thin iOS app target plus local Swift packages under `Packages/`. The split is chosen for a Windows developer using Claude Code: the core packages import only Foundation, so they compile and run their tests on Linux (a fast, free GitHub Actions job, and Claude Code cloud sessions) and, with the Swift for Windows toolchain, on the Windows PC. Only the Apple-only packages need the macOS runner.

| Package | Imports | Builds on | Holds |
|---|---|---|---|
| `MMCore` | Foundation | Linux, Windows, macOS | Shared models (Song, Album, Artist, Playlist), errors, logging |
| `InnerTube` | Foundation, MMCore | Linux, Windows, macOS | Request building, client profiles, JSON response parsing, remote config schema |
| `Extractor` | Foundation, InnerTube | Linux, Windows, macOS (logic) | Format selection, signature and `n` decipher logic. The JS runner is a protocol; the JavaScriptCore implementation lives in `AppleBridges` |
| `Lyrics` | Foundation, MMCore | Linux, Windows, macOS | Lyrics providers, TTML/LRC/word-sync parsers, fallback chain |
| `Storage` | GRDB, MMCore | macOS (Linux possible) | Database schema, migrations, library cache, downloads index |
| `AppleBridges` | JavaScriptCore, WebKit, Security | macOS only | JS runner, web sign-in, Keychain |
| `Playback` | AVFoundation, MediaPlayer | macOS only | Playback engine, Now Playing info, remote commands, downloads |
| `UI` | SwiftUI, Nuke | macOS only | All screens and components |

Rules:

- Core packages never import Apple-only frameworks. Anything platform-specific goes behind a protocol and is injected from the app.
- Tests in core packages use recorded JSON fixtures, not live network calls. That makes them fast, repeatable, and safe on Windows, where `URLSession` support is still unreliable.
- A separate, manually triggered CI job runs a few live "canary" calls against YouTube to catch API changes early.

## Remote config (D32)

`config/remote-config.json` in this repo holds values YouTube changes often: InnerTube client names and versions, API keys, user agents, player JS regex patterns, client fallback order. The app fetches it from the repo at launch, checks its schema version, and falls back to the copy bundled in the app if the fetch fails.

## Audio engine

Round 2 asked for gapless, crossfade, an equalizer and normalization together. Plain `AVPlayer` can't do all of these:

- Crossfade needs two players running at once with their volumes ramped.
- An equalizer needs access to the audio samples, which means either an `MTAudioProcessingTap` on the `AVPlayerItem` or playing through `AVAudioEngine` with an `AVAudioUnitEQ`.
- Gapless needs the next item prepared before the current one ends.

Likely design: a `PlaybackEngine` that owns two `AVPlayer` instances (A/B) for crossfade and gapless, with a processing tap on each item for EQ and normalization gain. Video uses the same `AVPlayer`, shown through `AVPlayerLayer`, which also gives Picture in Picture. To decide in the architecture round.

## Stream formats

- AVFoundation does not play WebM. Prefer AAC in MP4 (`.m4a`) for audio and HLS for the iOS client.
- Best audio is itag 141 (AAC 256 kbps), which YouTube serves only to Premium accounts. Without Premium the best AAC is itag 140 (128 kbps).

## Free and Premium accounts (D26)

- At sign-in, read the account's Premium status from InnerTube and store it.
- Stream selection asks "best format this account can get", so the same code serves both.
- Downloads record the bitrate they were saved at. If a free user later gets Premium, the app can offer to re-download at higher quality.
- Our client plays streams directly, so the official app's free-tier limits on background play don't apply here. Some regional or catalogue limits might still show up in InnerTube responses; handle those as playback errors with a clear message.

## Live Activity

Needs a Widget extension using ActivityKit. Now Playing state is pushed to it locally (no push server, which free signing couldn't use anyway).
