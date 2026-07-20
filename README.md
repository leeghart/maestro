# Maestro Ear Trainer — native SwiftUI version

A native iOS port of the Maestro web game: same mechanics (era picker, 5-second
streamed piano fragments, 12-second answer window with the fill-up metronome,
3 choices, 5 rounds, score tiers, 3-second auto-advance), same 93-track deck.

## Files

| File | Contents |
|---|---|
| `MaestroApp.swift` | App entry point + all SwiftUI views (root, era picker, game, summary, how-to) and the theme |
| `Models.swift` | `Era`, `Track` (incl. Commons streaming-URL resolution), `Tier`, `RoundResult` |
| `Deck.swift` | The full 93-track repertoire |
| `GameViewModel.swift` | The whole game state machine: playback, timers, scoring, round flow |
| `MetronomeView.swift` | The signature metronome (Canvas-drawn case, fill timer, swinging pendulum) |

## Building it (on your Mac)

1. Open **Xcode** (15 or newer) → **File → New → Project…** → **iOS → App**.
   - Product Name: `Maestro` (or anything)
   - Interface: **SwiftUI**, Language: **Swift**
   - Minimum deployment target: **iOS 16** or later (the code uses `Task.sleep(for:)` and `NavigationStack`).
2. In the new project, **delete** the generated `ContentView.swift` and the generated `<YourApp>App.swift` (Move to Trash).
3. Drag all five `.swift` files from this folder into the project navigator (check *"Copy items if needed"* and make sure your app target is ticked).
4. Build & run (⌘R) on the simulator or your iPhone. No third-party dependencies, no configuration needed — audio streams over plain HTTPS, which iOS allows by default.

To run on your own iPhone you'll need to be signed into Xcode with any Apple ID
(free is fine) and select your phone as the run destination; the free
provisioning profile lasts 7 days per install. For anything longer-lived or for
TestFlight/App Store, you'd need the paid Apple Developer Program.

## One important technical note: audio formats

iOS's `AVPlayer` **cannot decode Ogg Vorbis**, and most of the deck's source
files on Wikimedia Commons are `.ogg`. The app solves this by streaming the
**MP3 transcodes** Commons generates automatically for every audio upload.
Those live at deterministic URLs derived from the MD5 hash of the filename —
see `Track.streamURL` in `Models.swift`. `.mp3` and `.flac` originals play
natively and use their original URLs.

Practical consequence: if you add tracks to `Deck.swift`, just use the exact
Commons filename (as with the web game) and the URL logic handles the rest —
but a brand-new Commons upload may take a little while before its MP3
transcode exists.

## Parity with the web version

Deliberately identical: timings (5s audio / 12s window / 3s verdict), scoring
formula (`1000 − 70·seconds`, floor 100), tier thresholds, choice-building
rules (distractors from the same era, deduplicated by title), random fragment
start (8–40s, clamped for short recordings).

Not carried over (yet): nothing — this is the full game. Natural next steps if
you want them: haptics on correct/wrong answers, a persistent best-score per
era via `@AppStorage`, and Game Center leaderboards.
