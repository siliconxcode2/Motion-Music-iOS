# Overview

## What we are building

Motion Music is a native iOS client for YouTube Music. It signs in with the owner's Google account and gives access to the full YouTube Music library, recommendations and playback, inside an interface modelled on Apple Music.

## Who it is for

Mainly the owner, who sideloads it onto their own iPhone. The repo is public so anyone else can build or install it too, each with their own Google account. There is no App Store release, no analytics and no backend server. The app still has to survive YouTube changing its private API, so the code must make that easy to fix.

## Goals

1. Feature parity with the official YouTube Music app over time, built in phases.
2. A native SwiftUI interface that looks and behaves like Apple Music.
3. Signed-in access: library, liked songs, playlists, history, home feed, mixes.
4. Reliable background playback with lock screen and Control Center controls.
5. A build pipeline that works entirely from Windows through GitHub Actions.

## Non-goals (for now)

- App Store distribution.
- Android, macOS or web versions.
- Multiple accounts on one install (may revisit).

## Data source

YouTube Music's unofficial internal API, InnerTube (the same JSON API the official apps and website use). Stream extraction is written in Swift, ported from yt-dlp and other open-source clients (D13).

## Key constraint

The owner develops on Windows with Claude Code. Every compile, test and package step runs on GitHub's macOS runners. See [05-build-and-ci.md](05-build-and-ci.md).
