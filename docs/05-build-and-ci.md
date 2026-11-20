# Build and CI (Windows-first)

## The setup

The owner's development machine is a **Windows PC**. It has no macOS, no Xcode and no iOS Simulator. Code is written with Claude Code (in the terminal or in Claude Code cloud sessions). That means:

- Nothing iOS-specific can be compiled or run locally.
- **GitHub Actions on macOS runners is the build machine.** Every `xcodebuild`, `swift test`, simulator run and `.ipa` export happens there.
- The only thing done on Windows is installing the finished `.ipa` onto the iPhone.

Every plan in this repo must respect this. Any step that says "open Xcode" or "run on the simulator" needs a CI equivalent.

## Pipeline (draft)

1. Push to a branch, or open a pull request.
2. The GitHub Actions workflow starts on a `macos-latest` (or pinned `macos-15`/`macos-26`) runner.
3. It resolves Swift packages, builds the app, and runs unit tests on the iOS Simulator.
4. It builds an unsigned `.ipa` (`CODE_SIGNING_ALLOWED=NO`, then zip `Payload/MotionMusic.app`).
5. It uploads the `.ipa`, test results and simulator screenshots as workflow artifacts.
6. On Windows, download the `.ipa` and install it with Sideloadly (or AltStore/SideStore), which signs it with the owner's Apple ID.

## Project file without Xcode

A hand-edited `.xcodeproj` is fragile when nobody can open Xcode. The plan is to generate it in CI from a text spec, with XcodeGen (`project.yml`) or Tuist. The generated project is not committed. This also keeps diffs readable for Claude Code. (Final choice is pending; see [open-questions.md](open-questions.md).)

## Seeing the app without a Mac

- CI runs the app on the simulator and saves screenshots of key screens as artifacts.
- SwiftUI previews can't be viewed on Windows, so snapshot tests (rendering views to PNG in CI) stand in for them.
- Real behaviour (audio, background play, lock screen) is checked on the iPhone after sideloading.

## Things that affect cost and speed

- GitHub Actions minutes: macOS runners bill at 10x on private repos. Public repos get standard runners free. Repo visibility is pending.
- Build caching (SwiftPM cache, DerivedData) to keep runs short.
- Free Apple ID signing expires every 7 days; a paid developer account lasts a year. Pending.

## References

- [Build unsigned IPA to install via Sideloadly](https://dev.to/oivoodoo/build-unsigned-ios-ipa-to-install-via-sideloadly-236f)
- [Sideloadly how-to](https://www.idownloadblog.com/?p=898073)
