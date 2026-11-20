# Tech stack

Draft. Filled in further as rounds progress.

| Area | Choice | Status |
|---|---|---|
| Language | Swift 6, strict concurrency | Decided |
| UI | SwiftUI, Apple Music style | Decided (D5) |
| Minimum iOS | 17.0; iOS 26+ features (Liquid Glass) behind `#available` | Decided (D11) |
| Dev device | iPhone on iOS 27 | Known |
| API | YouTube Music InnerTube (unofficial), JSON over HTTPS with `URLSession` | Decided (D3) |
| Stream extraction | Native Swift port of the parts of yt-dlp we need; YouTube player JS run through JavaScriptCore | Decided (D13) |
| Sign-in | `WKWebView` Google login, cookies stored in the Keychain; device-code OAuth fallback | Decided (D14) |
| Playback | AVFoundation (`AVPlayer` / `AVQueuePlayer`), `MPNowPlayingInfoCenter`, `MPRemoteCommandCenter` | Proposed |
| Local storage | SwiftData or GRDB | Pending |
| Project generation | XcodeGen or Tuist | Pending |
| CI | GitHub Actions, `xcode-27` runner label | Decided (D7, D9) |
| Install | iloader on Windows → SideStore on iPhone | Decided (D10) |

## Porting rule

If a feature already exists in another language (yt-dlp in Python, NewPipe/InnerTune/Metrolist in Kotlin, ytmusicapi in Python), we read it and rewrite it in Swift. No embedded interpreters, no extra runtimes. The one exception is YouTube's own player JavaScript, which must run as JS.
