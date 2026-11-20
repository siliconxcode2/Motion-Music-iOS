# Motion Music (iOS)

A personal YouTube Music client for iPhone, written in SwiftUI with an Apple Music style interface. It is for one user (the owner) and is installed by sideloading. It will not be published on the App Store.

This repository is in the planning stage. All planning lives in [`docs/`](docs/). Some files below are filled in as the question rounds progress.

| File | What it holds |
|---|---|
| [docs/00-overview.md](docs/00-overview.md) | Purpose, goals, scope |
| [docs/01-features.md](docs/01-features.md) | Feature list and build phases |
| [docs/02-architecture.md](docs/02-architecture.md) | App structure, data layer, playback |
| [docs/03-ui-ux.md](docs/03-ui-ux.md) | Screens, navigation, visual style |
| [docs/04-tech-stack.md](docs/04-tech-stack.md) | Languages, frameworks, libraries |
| [docs/05-build-and-ci.md](docs/05-build-and-ci.md) | Windows workflow, GitHub Actions, sideloading |
| [docs/06-roadmap.md](docs/06-roadmap.md) | Phases and milestones |
| [docs/decisions.md](docs/decisions.md) | Decision log |
| [docs/open-questions.md](docs/open-questions.md) | Questions still to settle |
| [docs/question-rounds.md](docs/question-rounds.md) | Every planning question asked, with answers |

## Important: development happens on Windows

The owner builds this app from a Windows PC. There is no Mac, no local Xcode and no iOS Simulator on the dev machine. Every macOS step (compiling, running tests, simulator screenshots, packaging the `.ipa`) runs on GitHub Actions macOS runners. Code is written with Claude Code. See [docs/05-build-and-ci.md](docs/05-build-and-ci.md).
