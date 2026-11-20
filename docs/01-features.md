# Features and phases

The goal is everything YouTube Music offers that makes sense in a personal client, built in phases (D4). Phase numbers are a draft; the roadmap in [06-roadmap.md](06-roadmap.md) will set the order once all rounds are done.

## Phase 1: first installable build (agreed, round 2)

- Google sign-in (web login, device-code fallback)
- Home feed
- Search (songs, albums, artists, playlists, videos)
- Play songs, with a queue
- Background playback, lock screen and Control Center controls
- Library: playlists, liked songs, albums, artists
- Now Playing screen and mini player

## Later phases (agreed, not yet ordered)

### Downloads
- Offline downloads of songs, albums and playlists.
- Always the best audio available. Opus is not playable by AVFoundation inside WebM, so the likely format is AAC in `.m4a` (itag 141 at 256 kbps needs Premium; itag 140 at 128 kbps otherwise). To confirm in the architecture round.

### Lyrics
- Apple Music style word-by-word lyrics, with the current word lit up.
- Fallback chain: word-synced source → line-synced (YouTube Music or LRCLIB) → plain text from YouTube Music → "no lyrics".
- Candidate word-sync sources to study and port to Swift: LyricsPlus (used by [am-lyrics](https://github.com/binimum/am-lyrics)), [Lyrica](https://codeberg.org/willooper/Lyrica) (word and syllable level), [Karalyr](https://github.com/lemara98/karalyr) (word-synced database), [LRCLIB](https://docsearch.algolia.com/mcp/docs/repo/tranxuanthang/lrclib) (line-synced).

### Audio
- Quality setting, default Highest, separate values for Wi-Fi and cellular.
- Gapless playback.
- Crossfade (user-set length).
- Equalizer with presets and a custom curve.
- Volume normalization (YouTube's loudness data where available).

### Video
- Music videos playable, with a Song/Video toggle like YouTube Music.
- Picture in Picture.

### Extras
- Live Activity and Dynamic Island for Now Playing. Needs one widget extension, which uses one app ID on the free Apple ID.

## Not planned for now

Home screen widgets, Siri/Shortcuts, AirPlay-specific features (basic AirPlay comes free with AVFoundation), sleep timer, scrobbling, segment skipping, song recognition, comments, podcasts. Any of these can come back later.
