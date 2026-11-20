# Decision log

Each entry records what was decided and why. Newest at the bottom.

| # | Date | Decision | Reason |
|---|---|---|---|
| D1 | 2026-11-20 | Personal use only, installed by sideloading | No App Store review, no other users to support |
| D2 | 2026-11-20 | Sign in with Google for full YouTube Music features | Library, playlists, likes and personalised feeds need an account |
| D3 | 2026-11-20 | Data from the unofficial InnerTube API, with yt-dlp as the reference for stream extraction | No official public API covers YouTube Music playback |
| D4 | 2026-11-20 | Build every feature possible, delivered in phases | Large scope; phases keep each release usable |
| D5 | 2026-11-20 | Native SwiftUI app with Apple Music style design | Native feel and performance; familiar layout |
| D6 | 2026-11-20 | Code written with Claude Code | Owner's chosen workflow |
| D7 | 2026-11-20 | Development on Windows; all macOS work (build, test, package) runs on GitHub Actions | No Mac available |
| D8 | 2026-11-20 | Planning done as Markdown in `docs/`, pushed after each question round | Keeps a written record before coding starts |
| D9 | 2026-11-20 | Public GitHub repo, so others can try the app | Free standard macOS runners for public repos; others can fork and build |
| D10 | 2026-11-20 | Free Apple ID signing. Install with iloader (Windows) to put SideStore on the phone, then SideStore refreshes and updates the app on the device | No 7-day trip back to the PC; SideStore can also read a source feed for updates |
| D11 | 2026-11-20 | Minimum iOS 17. Dev device runs iOS 27. Newer APIs (iOS 26 Liquid Glass and later) used behind `#available` checks | Owner agreed to iOS 17+; wider reach now the repo is public |
| D12 | 2026-11-20 | CI simulator screenshots and snapshot tests are the way to review UI before installing | No Mac or simulator on Windows |
| D13 | 2026-11-20 | Stream extraction fully native Swift. Port and translate every non-Swift piece we rely on (yt-dlp logic, other-language clients) into Swift. YouTubeKit may be used or studied | One language, no embedded Python, no server |
| D14 | 2026-11-20 | Google sign-in: in-app web login that captures session cookies; TV device-code OAuth as fallback | Web login gives full access; device code is restricted but useful as backup |
