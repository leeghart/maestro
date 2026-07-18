[README.md](https://github.com/user-attachments/files/30155940/README.md)
# 🎹 Maestro — Piano Ear Trainer

A browser-based, Hitster-style ear-training game: a short piano fragment plays, and you race the clock to pick the right composer and piece from four choices. Single self-contained HTML file, no build step, no backend.

**Play it live:** `https://<your-username>.github.io/<repo-name>/`
*(update this link once GitHub Pages is enabled — see below)*

## How to play

1. Press **Play Fragment** to hear a 5-second clip of a real piano recording.
2. Four possible answers appear immediately. Pick the composer & piece — the faster you're right, the more it's worth.
3. Watch the metronome case: it fills up (green → red) as your 12-second answer window runs out.
4. No idea, or want to move on? Hit **Skip** — it counts as wrong and advances.
5. The game runs for 5 rounds. Your final score depends on both accuracy and speed, and earns you a tier: Newbie → Apprentice → Expert → Maestro → Wizard.

Full rules are also available in-app via the **How to Play** button.

## Tech

- Single `index.html` file — HTML, CSS, and vanilla JS, no dependencies, no build tooling.
- Audio fragments are streamed directly from Wikimedia Commons / Musopen (public domain and Creative Commons piano recordings) via `Special:FilePath` links — no audio files are hosted in this repo.
- Fonts loaded from Google Fonts (Spectral, Space Mono, Inter). Everything else runs entirely client-side.

## Updating the track deck

The full track list lives in the `DECK` array near the top of the `<script>` block in `index.html`. Each entry looks like:

```js
{ composer:"Frédéric Chopin", title:"Nocturne in F minor, Op. 55 No. 1",
  url: cf("Chopin - Nocturne-op-55-no-1.ogg") }
```

`cf(name)` builds a Wikimedia Commons `Special:FilePath` URL from the exact file title on Commons — the easiest way to add a track is to find a public-domain/CC piano recording on [Wikimedia Commons](https://commons.wikimedia.org) or [Musopen](https://musopen.org), copy its exact filename, and add a new entry.

## Deploying updates

If you edit `index.html` locally, you can push changes straight from the command line instead of using the GitHub web uploader:

```bash
git add index.html
git commit -m "Update deck"
git push
```

GitHub Pages will redeploy automatically within a minute or so.

## License

The code in this repo is free to use and adapt. Audio recordings are not redistributed here — they're streamed live from Wikimedia Commons / Musopen under their original public domain or Creative Commons licenses (see each file's Commons page for exact terms; a couple require attribution to the performer).
