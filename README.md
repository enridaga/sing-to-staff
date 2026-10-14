# Sing to Staff

Sing or hum a short tune into your phone and get the notes on a staff, as guitar tab, and as copyable ASCII tab.

**Use it:** https://enridaga.github.io/sing-to-staff/

## Install on your phone

- **Android (Chrome):** open the link, then menu ⋮ → *Install app* (or *Add to Home screen*).
- **iPhone (Safari):** open the link, tap Share → *Add to Home Screen*.

After the first visit it works offline. Allow microphone access when asked.

## How it works

Everything runs in the browser; no audio leaves the device.

1. Audio is resampled to 16 kHz and pitch-tracked frame by frame with the YIN algorithm.
2. Frames are smoothed and split into notes on pitch changes, silences and new syllables.
3. An optional tuning correction removes a constant sharp/flat offset in your singing.
4. Tempo is estimated from note spacing; durations are quantised to sixteenth notes, split at barlines with ties.
5. The key is estimated with the Krumhansl–Schmuckler profiles; notes are spelled for that key.
6. Guitar frets (standard tuning) are chosen to keep the hand in one area.
7. Notation and tab are engraved with [VexFlow](https://www.vexflow.com/) 4.2.5 (vendored in `vendor/`).

You can override tempo, time signature, clef (treble, bass, guitar 8vb), octave, key and tuning correction.

## My tunes

Name a tune and tap **Save tune** to keep it. Saved tunes are listed with date, key, note count and length; **Open** brings back the staff, tab, pitch view and playback with the settings you saved, and **Delete** (tap twice to confirm) removes it.

Tunes are stored only on this device, in the browser's IndexedDB (audio as 16 kHz 16-bit PCM, about 1 MB per 30 s). They are not uploaded anywhere. Clearing the site's data or uninstalling the app deletes them.

## Tips

- Sing on "da" or "ta" so repeated notes are separated.
- One voice, one note at a time; a quiet room helps.
- If the rhythm looks doubled or halved, set the tempo by hand.

## Development

Plain static files, no build step. Serve the folder locally (`python3 -m http.server`) and open `http://localhost:8000`; the microphone needs `localhost` or HTTPS.
Pushing to `main` deploys to GitHub Pages via `.github/workflows/pages.yml`. Bump `VERSION` in `sw.js` on each release so installed copies update.

## Licence

MIT for this project. VexFlow is MIT-licensed (see `vendor/VEXFLOW-LICENSE`).
