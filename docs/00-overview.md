# Overview

## What we are building

Motion Music is a native iOS client for YouTube Music. It signs in with the owner's Google account and gives access to the full YouTube Music library, recommendations and playback, inside an interface modelled on Apple Music.

## Who it is for

One person: the owner. The app is sideloaded onto their own iPhone. There is no App Store release, no other users, no analytics and no backend run for other people. This keeps legal and review concerns out of the design, but the app still has to survive YouTube changing its private API, so the code must make that easy to fix.

## Goals

1. Feature parity with the official YouTube Music app over time, built in phases.
2. A native SwiftUI interface that looks and behaves like Apple Music.
3. Signed-in access: library, liked songs, playlists, history, home feed, mixes.
4. Reliable background playback with lock screen and Control Center controls.
5. A build pipeline that works entirely from Windows through GitHub Actions.

## Non-goals (for now)

- App Store distribution.
- Android, macOS or web versions.
- Multi-user support.

## Data source

YouTube Music's unofficial internal API, InnerTube (the same JSON API the official apps and website use). yt-dlp is the reference for stream extraction and cipher handling. How much of yt-dlp runs in the app versus being ported to Swift is an open question; see [open-questions.md](open-questions.md).

## Key constraint

The owner develops on Windows with Claude Code. Every compile, test and package step runs on GitHub's macOS runners. See [05-build-and-ci.md](05-build-and-ci.md).
