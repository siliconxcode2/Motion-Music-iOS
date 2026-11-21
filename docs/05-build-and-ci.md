# Build and CI (Windows-first)

## The setup

The owner's development machine is a **Windows PC**. It has no macOS, no Xcode and no iOS Simulator. Code is written with Claude Code (in the terminal or in Claude Code cloud sessions). That means:

- Nothing iOS-specific can be compiled or run locally.
- **GitHub Actions on macOS runners is the build machine.** Every `xcodebuild`, `swift test`, simulator run and `.ipa` export happens there.
- The only things done on Windows are installing SideStore once and, if needed, side-installing an `.ipa`.

Every plan in this repo must respect this. Any step that says "open Xcode" or "run on the simulator" needs a CI equivalent.

## Runner

- Use the `xcode-27` runner label. GitHub made the Xcode 27 image generally available in October 2026; it runs on macOS 27 and includes Xcode 27 and the Apple SDKs ([changelog](https://github.blog/changelog/2026-10-16-xcode-27-runner-image-generally-available/)). GitHub now names macOS images by Xcode major version.
- The repo is public (D9), so standard GitHub-hosted runners are free. Avoid the `-xlarge` label, which is billed.

## Pipeline (draft)

Two jobs run on every push:

- **Linux job** (`ubuntu-latest`, fast): `swift build` and `swift test` for the Foundation-only packages (`MMCore`, `InnerTube`, `Extractor` logic, `Lyrics`). Gives feedback in a few minutes.
- **macOS job** (`xcode-27`): the full app, as below.

macOS job steps:

1. Push to a branch, or open a pull request.
2. The workflow starts on an `xcode-27` runner.
3. Install the pinned Tuist version and run `tuist generate` (D27).
4. Resolve Swift packages, build, run unit and snapshot tests on the iOS Simulator.
5. Build an unsigned `.ipa` (`CODE_SIGNING_ALLOWED=NO`, then zip `Payload/MotionMusic.app`).
6. Upload the `.ipa`, test results and simulator screenshots as workflow artifacts.
7. On a tagged release, also attach the `.ipa` to a GitHub Release and update a SideStore source JSON in the repo.

## Installing on the iPhone (free Apple ID)

One-time setup on Windows:

1. Install iTunes (it provides the device drivers) and check that it sees the iPhone.
2. Install [iloader](https://github.com/nab138/iloader) from its GitHub repo or iloader.app (the only official sources).
3. In iloader, sign in with an Apple ID, choose the iPhone and install SideStore. Any free Apple ID works; it does not have to match the phone's iCloud account.
4. On the phone: trust the developer profile, turn on Developer Mode, install LocalDevVPN and connect it, then open SideStore and sign in.

After that, everything happens on the phone:

- Add the Motion Music SideStore source (URL from this repo), or install the `.ipa` from a GitHub Release.
- SideStore refreshes the 7-day signature in the background or on demand. LocalDevVPN must be connected while it refreshes or installs.

Free Apple ID limits: 3 active sideloaded apps (SideStore counts as one), and app extensions each use an app ID. See [open-questions.md](open-questions.md).

## Project file without Xcode

A hand-edited `.xcodeproj` is fragile when nobody can open Xcode. Tuist generates it in CI from Swift manifests (`Project.swift`, `Tuist.swift`). Tuist needs macOS and Xcode, so it never runs on Windows; Claude Code only edits the manifests. The generated project is not committed.

## Working loop with Claude Code on Windows

1. Claude Code edits code and pushes a branch.
2. The Linux job reports core test results within minutes; the macOS job follows with the full build, `.ipa` and screenshots.
3. Claude Code reads results with the `gh` CLI (`gh run watch`, `gh run view --log-failed`, `gh run download` for screenshots and the `.ipa`), so failures can be fixed without leaving the terminal.
4. Optional: install the Swift for Windows toolchain to run core package tests locally. Networking on Windows Swift is still unreliable, which is why tests use fixtures.
5. A `CLAUDE.md` at the repo root will spell out this loop and the "no Mac" rule for every future Claude Code session.

## Seeing the app without a Mac

- CI runs the app on the simulator and saves screenshots of key screens as artifacts.
- SwiftUI previews can't be viewed on Windows, so snapshot tests (rendering views to PNG in CI) stand in for them (D12).
- Real behaviour (audio, background play, lock screen) is checked on the iPhone after installing.

## Public repo rules

- No secrets, cookies, tokens or personal account data in the repo or in CI logs.
- Each user signs in with their own Google account inside the app.
- README gets an install guide for people who want to try it.

## References

- [iloader wiki](https://github.com/nab138/iloader/wiki)
- [SideStore guide (Gigazine, June 2026)](https://www.gigazine.net/gsc_news/en/20260628-sidestore-sideloading-ios)
- [Build unsigned IPA to install via Sideloadly](https://dev.to/oivoodoo/build-unsigned-ios-ipa-to-install-via-sideloadly-236f)
- [Xcode 27 runner image GA](https://github.blog/changelog/2026-10-16-xcode-27-runner-image-generally-available/)
