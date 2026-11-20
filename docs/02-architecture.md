# Architecture

Draft. The full architecture round comes later; this page records constraints found so far.

## Audio engine

Round 2 asked for gapless, crossfade, an equalizer and normalization together. Plain `AVPlayer` can't do all of these:

- Crossfade needs two players running at once with their volumes ramped.
- An equalizer needs access to the audio samples, which means either an `MTAudioProcessingTap` on the `AVPlayerItem` or playing through `AVAudioEngine` with an `AVAudioUnitEQ`.
- Gapless needs the next item prepared before the current one ends.

Likely design: a `PlaybackEngine` that owns two `AVPlayer` instances (A/B) for crossfade and gapless, with a processing tap on each item for EQ and normalization gain. Video uses the same `AVPlayer`, shown through `AVPlayerLayer`, which also gives Picture in Picture. To decide in the architecture round.

## Stream formats

- AVFoundation does not play WebM. Prefer AAC in MP4 (`.m4a`) for audio and HLS for the iOS client.
- Best audio is itag 141 (AAC 256 kbps), which YouTube serves only to Premium accounts. Without Premium the best AAC is itag 140 (128 kbps).

## Live Activity

Needs a Widget extension using ActivityKit. Now Playing state is pushed to it locally (no push server, which free signing couldn't use anyway).
