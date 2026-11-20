# Open questions

Questions that are not settled yet. Move each one to [decisions.md](decisions.md) once answered.

## Build and install

- Is the GitHub repo public or private? This decides how many free macOS minutes we get.
- Free Apple ID (re-sign every 7 days, 3 app limit) or paid Apple Developer account (1 year)?
- XcodeGen or Tuist to generate the Xcode project in CI?

## Stream extraction

- yt-dlp is written in Python. Options for iOS: (a) port the needed logic to Swift, or use a Swift library such as YouTubeKit; (b) embed Python and run yt-dlp in the app (YoutubeDL-iOS does this, at the cost of size and startup time); (c) run yt-dlp on a small personal server.
- PO tokens: YouTube now requires them for some clients. The iOS client's HLS formats reportedly don't need one for playback today, but this changes often.

## Sign-in

- Google sign-in through an in-app web view that captures the session cookies, or the TV/device-code OAuth flow?

## Product

- Minimum iOS version (depends on the owner's iPhone).

## Research notes

- No current open-source SwiftUI YouTube Music client for iOS was found. Closest: [Kaset](https://raw.githubusercontent.com/sozercan/kaset/main/README.md) (SwiftUI, macOS only), [YTLite](https://github.com/d1y/YTLite) (UIKit, iOS), [YouTubeKit](https://github.com/alexeichhorn/YouTubeKit/blob/0.2.2) (Swift stream extraction), [YoutubeDL-iOS](https://swiftpackageregistry.com/kewlbear/YoutubeDL-iOS) (yt-dlp in an iOS app), [yt-dlp PO Token Guide](https://github.com/yt-dlp/yt-dlp/wiki/PO-Token-Guide).
