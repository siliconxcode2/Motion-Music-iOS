# Open questions

Questions that are not settled yet. Move each one to [decisions.md](decisions.md) once answered.

## Build and install

- XcodeGen or Tuist to generate the Xcode project in CI?
- License for the public repo (MIT, GPL-3.0, or none)?
- Bundle ID (name is final: Motion Music).
- App icon: owner to add a 1024×1024 PNG at `design/AppIcon-1024.png`.

## Stream extraction

- Signature and `n` parameter deciphering need YouTube's player JavaScript to run. "All Swift" still means running that JS through Apple's JavaScriptCore; we port the yt-dlp logic that finds and calls those functions, not YouTube's own JS.
- PO tokens: YouTube requires them for some clients. The iOS client's HLS formats reportedly don't need one for playback today. If that changes, generating a token through BotGuard in a hidden `WKWebView` is the likely route. Track this.
- Which InnerTube clients to use (iOS, web remix, Android music, TV) and in what fallback order.

## Free Apple ID limits to check

- A free Apple ID allows 3 active sideloaded apps (SideStore itself is one) and roughly 10 app IDs per 7 days. Each app extension (widget, Live Activity, share extension) needs its own app ID, so extensions eat into this.
- Some capabilities don't work with free signing (push notifications, iCloud, CarPlay entitlement). Features that depend on them may be dropped or kept optional.

## Research notes

- No current open-source SwiftUI YouTube Music client for iOS was found. Closest: [Kaset](https://raw.githubusercontent.com/sozercan/kaset/main/README.md) (SwiftUI, macOS only), [YTLite](https://github.com/d1y/YTLite) (UIKit, iOS), [YouTubeKit](https://github.com/alexeichhorn/YouTubeKit/blob/0.2.2) (Swift stream extraction), [YoutubeDL-iOS](https://swiftpackageregistry.com/kewlbear/YoutubeDL-iOS) (yt-dlp in an iOS app), [yt-dlp PO Token Guide](https://github.com/yt-dlp/yt-dlp/wiki/PO-Token-Guide).
- Recent official YouTube Music features (2026): AI playlist generator, Ask Music, song recognition by humming, Now Playing comments, Speed dial on Home, custom playlist thumbnails, redesigned artist pages ([PhoneArena](https://www.phonearena.com/news/youtube-music-shares-a-long-list-of-features-it-has-rolled-out-since-march-for-its-users_id160964), [9to5Google](https://9to5google.com/guides/youtube-music), [Tom's Guide](https://tomsguide.com/ai/youtube-music-adding-ai-generated-playlists-and-shazam-like-tool-heres-how-they-work)).
