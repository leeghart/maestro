# 🎹 Maestro — Piano Ear Trainer

A browser-based, Hitster-style ear-training game: a short piano fragment plays, and you race the clock to pick the right composer and piece from three choices. Two files, no build step, no backend.

**Play it live:** `https://leeghart.github.io/maestro/`
*(update this link once GitHub Pages is enabled — see below)*

## Files

- **`index.html`** — the showcase/landing page. This is what visitors see first: a live embedded preview of the game, how-to-play, the repertoire by era, score tiers, and install instructions.
- **`game.html`** — the actual game. Linked from every "Play Now" button on the showcase page, and also the direct URL people should bookmark or add to their home screen.
- **`manifest.json`** + **`icons/`** — PWA install support (see below).

## How to play

1. Pick an era — Baroque, Classical, Romantic, Impressionist, or Mixed.
2. Press **Play Fragment** to hear a 5-second clip of a real piano recording.
3. Three possible answers appear immediately. Pick the composer & piece — the faster you're right, the more it's worth.
4. Watch the metronome case: it fills up (green → red) as your 12-second answer window runs out.
5. No idea, or want to move on? Hit **Skip** — it counts as wrong and advances.
6. The game runs for 5 rounds. Your final score depends on both accuracy and speed, and earns you a tier: Newbie → Apprentice → Expert → Maestro → Wizard.

Full rules are also available in-game via the **How to Play** button.

## Tech

- Two self-contained HTML files — HTML, CSS, and vanilla JS, no dependencies, no build tooling.
- Audio fragments are streamed directly from Wikimedia Commons / Musopen (public domain and Creative Commons piano recordings) via `Special:FilePath` links — no audio files are hosted in this repo.
- The showcase page (`index.html`) embeds `game.html` live in an iframe — it's not a screenshot or mockup, it's the actual playable game.
- Fonts loaded from Google Fonts (Spectral, Space Mono, Inter). Everything else runs entirely client-side.

## Installing to your home screen (PWA)

Open **`game.html`** in **Safari** on iPhone, tap the **Share** icon, then **Add to Home Screen**. You get a real icon and a full-screen launch with no browser chrome — no App Store required. This relies on `manifest.json` and the icon set in `icons/`, both already wired up in `game.html`'s `<head>`.

## Updating the track deck

The full track list lives in the `DECK` array near the top of the `<script>` block in `game.html`. Each entry looks like:

```js
{ composer:"Frédéric Chopin", era:"Romantic", title:"Nocturne in F minor, Op. 55 No. 1",
  url: cf("Chopin - Nocturne-op-55-no-1.ogg") }
```

`cf(name)` builds a Wikimedia Commons `Special:FilePath` URL from the exact file title on Commons — the easiest way to add a track is to find a public-domain/CC piano recording on [Wikimedia Commons](https://commons.wikimedia.org) or [Musopen](https://musopen.org), copy its exact filename, and add a new entry with the right `era` tag (Baroque / Classical / Romantic / Impressionist).

## Deploying updates

If you edit either file locally, you can push changes straight from the command line instead of using the GitHub web uploader:

```bash
git add index.html game.html manifest.json icons/
git commit -m "Update deck / showcase"
git push
```

GitHub Pages will redeploy automatically within a minute or so.

## License

The code in this repo is free to use and adapt. Audio recordings are not redistributed here — they're streamed live from Wikimedia Commons / Musopen under their original public domain or Creative Commons licenses (see each file's Commons page for exact terms; a few require attribution to the performer).
