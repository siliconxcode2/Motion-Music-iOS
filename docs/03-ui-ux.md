# UI and UX

Apple Music style, native SwiftUI (D5). Follows Apple's current design language, including iOS 26+ Liquid Glass where available.

## Navigation

Tab bar with four tabs:

| Tab | Content |
|---|---|
| Home | YouTube Music home feed: Speed dial / quick picks, mixes, recommendations |
| Explore | New releases, charts, moods and genres |
| Library | Playlists, liked songs, albums, artists, downloads, history |
| Search | Search with suggestions and filters (songs, videos, albums, artists, playlists) |

The mini player sits above the tab bar on every tab. Tapping it opens Now Playing.

## Now Playing

- Full-screen sheet in the Apple Music style.
- Animated background tinted from the artwork's colours.
- Song/Video toggle at the top (D19). In Video mode the artwork area shows the video; Picture in Picture is available.
- Swipe or buttons to open lyrics and the queue.
- Lyrics view: word-by-word highlight (D17).
- Supports portrait and landscape, like Apple Music in iOS 27.

## Theme

- Follows the system light/dark setting.
- Accent colour is taken from the current song's artwork and updates as tracks change. A neutral default is used when nothing is playing.

## Artist and album pages

iOS 27 Apple Music style: large artist image that blends into the page, page colours drawn from the image, prominent Shuffle and Play buttons. Album pages follow the same treatment.

## App identity

- Home screen name: **Motion Music** (final).
- Icon: supplied by the owner. To add to the repo as a 1024×1024 PNG (see [open-questions.md](open-questions.md)).

## References

- [9to5Mac: Apple Music in iOS 27 design changes](https://9to5mac.com/2026/06/19/apple-music-in-ios-27-introduces-new-design-changes-in-two-key-areas/)
- [MacRumors: Apple Music in iOS 27](https://www.macrumors.com/2026/06/09/apple-music-gains-automix-upgrades-and-more-in-ios-27/)
