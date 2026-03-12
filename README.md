<br>
<div align="center">

<img src="https://img.shields.io/badge/status-vibecoded-00d4aa?style=for-the-badge&labelColor=0e0e10" alt="Status: Vibecoded">
<img src="https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-adadb8?style=for-the-badge&labelColor=0e0e10" alt="Platform">
<img src="https://img.shields.io/badge/license-MIT-adadb8?style=for-the-badge&labelColor=0e0e10" alt="License">

<br><br>

```
██████  ██ ██   ██ ███████ ██            ██████  ██      ███████ ███████ ██████  
██   ██ ██  ██ ██  ██      ██            ██   ██ ██      ██      ██      ██   ██ 
██████  ██   ███   █████   ██      █████ ██████  ██      █████   █████   ██   ██ 
██      ██  ██ ██  ██      ██            ██   ██ ██      ██      ██      ██   ██ 
██      ██ ██   ██ ███████ ███████       ██████  ███████ ███████ ███████ ██████ 
```

**Edge-bleeding & PNG compression for Roblox images.**
<br>
*One page. No install. Just open and start.*

<br>

[Get Started](#-get-started) · [How It Works](#-how-it-works) · [Why This Exists](#-why-this-exists) · [Credits](#-credits)

</div>

<br>

---

<br>

## 🎯 Why This Exists

If you've made images or textures for Roblox, you've seen the problem: transparent edges bleed black (or wrong-colored) pixels when the engine filters your texture at a distance. The fix is **alpha bleeding** — flooding the RGB values of transparent pixels outward from opaque edges so that when Roblox samples across the boundary, it grabs the right color instead of garbage.

Tools like **[Chipng](https://rbxxaxa.github.io/chipng/)** and **[PixelFix](https://github.com/nickclaw/pixelfix)** solve this on Windows, but if you're on **macOS**, your options are limited. PixelBleed is a single HTML file that runs in any browser on any OS — no downloads, no installs, no dependencies.

It also borrows a trick from **[TinyPNG](https://tinypng.com/)**: after bleeding, it quantizes your image down to an indexed-color PNG, which can cut file sizes by 50–80% with virtually no visible quality loss. Smaller textures = faster load times for your game.

<br>

## 🚀 Get Started

```
1.  Download  pixelbleed.html or visit https://legendoj1.github.io/pixelbleed
2.  Drop in your PNGs
3.  Download the results
```

That's it. Everything runs client-side in your browser. No files are uploaded anywhere. As easy as 1-2-3.

<br>

## ⚙️ How It Works

### Alpha Bleeding

PixelBleed uses a **wavefront flood-fill** algorithm ported from [urraka/alpha-bleeding](https://github.com/urraka/alpha-bleeding). Instead of a fixed iteration count, it works in passes:

1. Every transparent pixel adjacent to an opaque pixel is added to a **pending queue**.
2. Each pending pixel averages the RGB of its opaque neighbors and gets filled (alpha stays 0).
3. Newly filled pixels promote their transparent neighbors into the next round.
4. This repeats until every transparent pixel in the image has been reached.

The result is a full bleed across the entire image — no guessing how many iterations you need.

### PNG Crush

After bleeding, PixelBleed optionally runs **UPNG.js color quantization** on the output. This is the same general technique TinyPNG uses: it reduces a 32-bit RGBA image to an indexed-color palette (256, 128, or 64 colors). The palette is chosen to minimize perceptual color difference, so for most Roblox textures the output is visually identical at a fraction of the file size.

You can toggle crush on/off and pick a palette size in the settings bar. Use 256 for detailed textures, drop to 64 for simple flat-color assets.

<br>

## 🖼️ Features

| | |
|---|---|
| **Batch processing** | Drop as many PNGs as you want — they process one by one with a live progress overlay |
| **Before / after toggle** | Click the eye icon on any card to flip between the original and bled result |
| **Size reporting** | Every card shows the original size, output size, and percentage savings |
| **Individual downloads** | Download button on each card for grabbing a single result |
| **ZIP export** | One-click download of all processed images in a ZIP archive |

<br>

## 🤝 Credits & Inspiration

This project stands on the shoulders of tools that came before it:

- **[Chipng](https://www.codeandweb.com/chipng)** — the original edge-padding tool many Roblox devs used on Windows
- **[PixelFix](https://github.com/nickclaw/pixelfix)** — another Windows-focused pixel bleeding utility
- **[urraka/alpha-bleeding](https://github.com/urraka/alpha-bleeding)** — the wavefront flood-fill algorithm this app is built on
- **[TinyPNG](https://tinypng.com/)** — the inspiration for the built-in PNG quantization/compression
- **[UPNG.js](https://github.com/nickclaw/UPNG.js)** — the library powering the PNG encoding and quantization
- **[JSZip](https://stuk.github.io/jszip/)** — ZIP generation in the browser

<br>

## ✨ Proudly Vibecoded

This project was vibecoded with [Claude](https://claude.ai). The entire app — algorithm port, UI, PNG compression pipeline — was built through conversation, not a traditional dev workflow. If it works well, that's the vibe. If something's off, PRs are welcome.

<br>

---

<div align="center">
<br>
<sub>Made for the Roblox dev community.</sub>
<br><br>
</div>
