# 🎵 SpriteCut

A browser-based audio sprite editor for creating [Howler.js](https://howlerjs.com/) compatible sprite JSON files. Drop in an MP3, detect sounds automatically, name them, fine-tune boundaries, and export — no server, no install, just open the HTML file.

---

## What is an audio sprite?

An audio sprite packs multiple short sounds into a single MP3 file. Instead of loading dozens of individual files, you load one file and reference each sound by its start time and duration. Howler.js uses a JSON format like this:

```json
{
  "src": ["sprite.mp3"],
  "sprite": {
    "ko": [575050, 380],
    "bil": [619390, 460],
    "hund": [557090, 440]
  }
}
```

SpriteCut helps you build and maintain that JSON visually.

---

## Features

- **Drag & drop MP3** — load any MP3 directly in the browser, no upload needed
- **Auto-detection** — silence-based RMS detection finds sounds automatically with adjustable threshold, gap, and minimum duration
- **Import existing JSON** — paste a previous sprite JSON to load all named segments as locked entries, then detect only new sounds appended to the end of the audio
- **Virtual waveform rendering** — renders only the visible slice of the waveform, so even very long files (800s+) work at any zoom level without hitting browser canvas limits
- **Zoom in/out** — 10 zoom levels from 20px/sec to 800px/sec
- **Drag segment edges** — resize any segment boundary directly on the waveform
- **Split segments** — cut a detected sound into two pieces at any point
- **Merge segments** — select multiple segments and merge them into one
- **Lock/unlock segments** — lock segments to protect them from edits; unlock to modify
- **Rename inline** — click any segment name to rename it; the waveform label updates live
- **Resizable panel** — drag the divider between the waveform and segment list to resize
- **Export JSON** — copies Howler.js-compatible sprite JSON to clipboard or downloads as a file
- **No dependencies** — single HTML file, runs entirely in the browser

---

## Usage

### Starting fresh

1. Open `audio-sprite-editor.html` in any modern browser
2. Drop your MP3 onto the drop zone (or click **Choose File**)
3. Adjust **Threshold**, **Min Gap**, and **Min Dur** sliders if needed
4. Click **↺ Re-detect** to auto-detect sounds
5. Rename each segment by clicking its name in the list
6. Click **Export JSON ↗** to copy or download the sprite JSON

### Updating an existing sprite

1. Load the new version of your MP3 (with additional sounds appended at the end)
2. Click **⬆ Import JSON** and paste your existing sprite JSON
3. Click **Apply & Detect New Sounds** — existing entries load as locked segments, new sounds after the last entry are detected automatically
4. Name the new segments
5. Export the combined JSON

### Waveform controls

| Action | How |
|---|---|
| Scroll timeline | Scroll horizontally in the waveform area |
| Zoom in/out | Click **−** / **+** in the toolbar |
| Resize a segment | Drag the left or right edge handle on the waveform |
| Move a segment | Drag the segment body (unlocked only) |
| Split a segment | Click **✂** in the list, then click a point on the waveform |
| Seek playback | Click anywhere on the waveform |
| Play a segment | Click **▶** in the segment list |
| Lock / unlock | Click 🔒 or 🔓 next to any segment |

---

## Workflow for iterative sprite builds

SpriteCut is designed for a common workflow where you record new sounds and append them to an existing MP3 over time:

```
Session 1: Record 50 words → detect → name → export sprite.json
Session 2: Append 30 more words to MP3 → import sprite.json → detect new → name → export
Session 3: Append 20 more words → import sprite.json → detect new → name → export
```

Each session picks up exactly where the last one left off, without touching already-named segments.

---

## Detection settings

| Setting | What it does |
|---|---|
| **Threshold** | RMS amplitude level that counts as "sound". Lower = more sensitive |
| **Min Gap ms** | Silence duration required to end a segment. Higher = fewer splits |
| **Min Dur ms** | Minimum segment length to keep. Filters out clicks and noise |

---

## Export format

Exports standard Howler.js sprite JSON:

```json
{
  "src": ["your-file.mp3"],
  "sprite": {
    "segment-name": [startMs, durationMs]
  }
}
```

---

## Browser compatibility

Works in any browser with Web Audio API support — Chrome, Firefox, Safari, Edge.

---

## License

© Asif Mithawala 2026 — [mithawala.com](https://mithawala.com)
