---
name: geoskill-hillshade-visualization
description: 'Multi-directional hillshade with vertical exaggeration and color overlay using the Horn algorithm'
---

# 山体阴影可视化 | Hillshade Visualization

Computes hillshade using the Horn (1981) algorithm, with support for **multi-directional weighted compositing** (highlighting terrain textures of different orientations), vertical exaggeration via the zfactor, and terrain color overlay.

Multi-directional compositing computes the hillshade for each azimuth angle separately and then combines them with the given weights (automatically normalized).

## Core Algorithm / 核心算法

Horn 3×3 differencing yields dz/dx, dz/dy → slope/aspect → sin(alt)cos(slope)+cos(alt)sin(slope)cos(az-aspect); the multi-directional output is the normalized weighted sum of the per-azimuth hillshades.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (Synthetic Data, Offline)

```bash
python geoskill-hillshade-visualization.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (Custom Azimuths and Weights)

```bash
python geoskill-hillshade-visualization.py --input dem.tif --azimuths 315 270 --weights 0.7 0.3
```

### Example 3 (Lower Sun Angle for Sharper Relief)

```bash
python geoskill-hillshade-visualization.py --input dem.tif --altitude 30 --zfactor 2
```

### Example 4 (Grayscale Colormap)

```bash
python geoskill-hillshade-visualization.py --input dem.tif --cmap gray
```

### Example 5 (Synthetic Multi-ridge Terrain)

```bash
python geoskill-hillshade-visualization.py --bbox 116 39 117 40 --synthetic --zfactor 3
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `color_shaded.png` | PNG | Color-overlaid hillshade (primary output) |
| `hillshade.tif` | GeoTIFF | Hillshade raster [0,1] (verifiable output) |
| `hillshade_meta.json` | JSON | Azimuths/weights/statistics |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; user data is never uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
