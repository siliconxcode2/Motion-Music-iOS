# Question rounds

Planning runs as about 8 rounds of 6 questions. Before each round the planner researches the topic, then asks. Answers are logged here and folded into the other docs.

## Round 0: kickoff (answered)

| # | Question | Answer |
|---|---|---|
| 0.1 | Who is the app for? | Only the owner, sideloaded |
| 0.2 | Account login? | Sign in with Google for the full YouTube Music feature set (InnerTube + yt-dlp) |
| 0.3 | Must-have features? | Everything possible, built in phases |
| 0.4 | Data source? | Unofficial YouTube Music API |
| 0.5 | Look and feel? | Apple Music style, native SwiftUI |
| 0.6 | Experience / tools? | Building with Claude Code, on a Windows PC, relying on GitHub CI/CD for all macOS steps |

## Round 1: build setup, sign-in and extraction (answered)

| # | Question | Answer |
|---|---|---|
| 1.1 | Repo public or private? | Public, so others can try it |
| 1.2 | Apple ID type and sideload tool? | Free Apple ID; tool left to planner (chose iloader + SideStore, D10) |
| 1.3 | iPhone / iOS version? | iOS 27 on device; agreed to iOS 17+ minimum |
| 1.4 | CI screenshots and snapshot tests enough? | Yes |
| 1.5 | Stream extraction approach? | Native Swift, and port/translate everything written in other languages to Swift |
| 1.6 | Google sign-in? | In-app web login (cookies), device-code OAuth as fallback |

## Round 2: features and phases (answered)

| # | Question | Answer |
|---|---|---|
| 2.1 | Phase 1 scope? | Agreed to the proposed list (D15) |
| 2.2 | Offline downloads? | Yes, best audio available |
| 2.3 | Lyrics? | Apple Music style word-by-word, with fallbacks |
| 2.4 | Audio options? | Quality (default Highest) and all of gapless, crossfade, EQ, normalization |
| 2.5 | Video? | Yes to all: videos, Song/Video toggle, PiP |
| 2.6 | Extras? | Live Activity / Dynamic Island only |

## Round 3: UI, look and account (answered)

| # | Question | Answer |
|---|---|---|
| 3.1 | Tab bar? | Home / Explore / Library / Search, agreed |
| 3.2 | Now Playing? | Agreed to proposal |
| 3.3 | Theme? | Follow system; accent from artwork |
| 3.4 | iOS 27 artist/album pages? | Yes |
| 3.5 | Name and icon? | "Motion Music" is final; icon ready |
| 3.6 | Premium? | No. Support both free and Premium |

## Round 4: architecture and code

Asked 2026-11-20. Answers pending.

1. Project generator: XcodeGen or Tuist?
2. Local database: GRDB or SwiftData?
3. Code layout: app target plus local Swift packages?
4. License (affects porting from GPL projects)?
5. Third-party package policy?
6. Remote config file for quick fixes when YouTube changes things?
