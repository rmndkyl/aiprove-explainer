# AIProve — a 60-second explainer

Entry for the AIProve bounty **`explainer-video-aiprove`** — *"Sixty seconds that make a stranger understand AIProve: free to enter, graded in the open, paid in stock."*

Watch: **https://rmndkyl.github.io/aiprove-explainer/**

## What this is

A 60.00-second, 1920×1080, 30 fps explainer built entirely from code. Every pixel is rendered by Python (Pillow + numpy) and piped as raw RGB into ffmpeg:

- **Paper** — procedurally generated newsprint: low-frequency mottling, ~2 400 drawn paper fibres, ink specks, a vignette, then temporal grain added at encode time.
- **Type** — Georgia (headline / body) and Consolas (metadata) in ink `#141414` on newsprint `#F3EADC`, with a single accent `#B23A2F`. Kinetic reveals are driven by eased time curves, with clipped "rise into place" motion.
- **Art** — no photography, no stock, no generated footage. The owl plate in beat 7 is the mascot illustration from [`rmndkyl/aiprove-mascot`](https://github.com/rmndkyl/aiprove-mascot), multiplied into the page so it reads as a printed plate.
- **Voice** — edge-tts (`en-GB-RyanNeural`), eight lines, auto-fitted to their beat so no line overruns a cut.
- **Sound** — no licensed music. The bed is synthesised in numpy: brown-noise room tone, a page-rustle on every cut, typewriter ticks on every headline reveal, and a low drone that swells across the minute.
- **Edit** — eight beats × 7.50 s, page-slide transitions (0.45 s), encoded to H.264 yuv420p CRF 22.

## Specs

| | |
|---|---|
| Runtime | 60.000 s (1800 frames @ 30 fps) |
| Resolution | 1920 × 1080 |
| Video | H.264 High, yuv420p, CRF 22, `+faststart` |
| Audio | AAC 192 kbps, 48 kHz stereo |
| Size | 19.95 MB |
| Licence of audio | original (synthesised in numpy) |
| Third-party assets | mascot illustration (own work, MIT-style reuse) |

## Files

```
index.html                 player page (GitHub Pages)
poster.jpg                 still from 0:04
aiprove-explainer.mp4      the film
transcript.md              full spoken transcript + shot list
```

## Reproduce

The build lives in the author's working tree (`film.py`, `beats.py`, `render.py`, `build_audio.py`). Sequence:

```bash
python build_audio.py                                   # edge-tts lines + synthesised bed -> audio/mix.wav
python render.py --pipe out/aiprove-explainer.mp4 \
       --noise 1 --crf 22 --preset slow                 # 1800 frames -> ffmpeg
ffprobe -v error -show_entries format=duration,size -of default=nw=1 out/aiprove-explainer.mp4
```

Requires Python 3.11+, Pillow, numpy, edge-tts, and ffmpeg 8.x. Fonts: Georgia and Consolas (Windows).
