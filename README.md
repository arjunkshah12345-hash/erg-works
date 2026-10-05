# ERG Works — standalone recreation

A pixel-verified, fully standalone recreation of **"ERG Works"**, a public Claude artifact
concept site (a fictional desert holding company: Cairn, Sirocco, Tessera).

The site is a fixed WebGL canvas (Three.js r186) behind scroll-driven chapters —
hero → thesis → holdings → signal — with a loader, `.rise` reveal animation,
ambient sound toggle, and a warm paper/ink/ember palette.

> The companies are fictional. Design and content belong to the original artifact's
> author; this is a faithful standalone copy made for personal/educational use.

## Run it

Module scripts need HTTP (not `file://`):

```bash
cd erg-works
python3 -m http.server 8477
# open http://127.0.0.1:8477
```

## What's inside

| File | Notes |
|---|---|
| `index.html` | Verbatim artifact body (markup + all CSS) from the live artifact, plus a minimal `<head>` |
| `assets/app.js` | The artifact's own Vite/Three.js r186 bundle — byte-identical to the original (621,963 B) |
| `assets/geist-*.woff2` | 5 Geist Variable subsets (Google Fonts) matching the artifact's `@font-face` filenames — claude.ai 403s direct font downloads |

## Fidelity (measured, not vibes)

Original artifact and this recreation, same browser (real Chrome), same 722×940 viewport,
compared as 12×10 mean-RGB grid deltas (0–255 scale; `.` < 8, `o` < 20, `O` < 45, `X` ≥ 45):

| Chapter | Mean delta | Near-identical cells | Catastrophic cells |
|---|---|---|---|
| Hero (scroll 0) | 6.5 | 88 / 120 | 0 |
| Holdings (settled) | 7.7 | 74 / 120 | 0 |
| Signal (settled) | 3.6 | 104 / 120 | 0 |

Residual deltas are the intentionally stochastic dune terrain and font antialiasing.
Sky-gradient cells differ by 0–4 RGB points.

## How it was captured

1. Opened the artifact in a real browser; read the iframe's **served source** with the
   app bundle route-aborted so the DOM was captured pristine (a naive `content()` snapshot
   returns the post-init mutated DOM — the app deletes `#loader`, which crashes its own
   loop when re-run).
2. Confirmed the JS bundle is unchanged; pulled fonts from Google Fonts under the same
   subset filenames.
3. Verified interactively over CDP: zero console/page errors, wheel scrolling, nav
   `data-goto` jumps, CTA pills, sound toggle, loader lifecycle, chapter activation.
4. Grid-delta comparison scripts are in `../erg-works-verify/` along with the screenshots
   and reports backing the table above.
