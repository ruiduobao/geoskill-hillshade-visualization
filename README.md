# Hillshade Visualization (geoskill-hillshade-visualization)

> Multi-directional hillshade with vertical exaggeration and color overlay using the Horn algorithm

---

## 1. Overview

Computes hillshade using the Horn (1981) algorithm, supporting **multi-directional weighted compositing** (highlighting terrain textures of different orientations), vertical exaggeration via zfactor, and terrain color overlay. Multi-directional compositing computes hillshade for each azimuth angle and then combines them with weights (automatically normalized).

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-hillshade-visualization.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `color_shaded.png` | PNG | Color-overlay shaded relief (primary output) |
| `hillshade.tif` | GeoTIFF | Hillshade raster [0,1] (verifiable output) |
| `hillshade_meta.json` | JSON | Azimuth/weights/statistics |

Each run also produces `output-manifest.json` (run manifest).


## 6. Technical Principle

Horn 3×3 differences give dz/dx, dz/dy → slope/aspect → sin(alt)cos(slope)+cos(alt)sin(slope)cos(az-aspect); multi-directional is the normalized weighted sum of the per-azimuth hillshade values.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
