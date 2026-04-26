# Tempo3D — Project Page

Static project page for the SIGGRAPH 2026 paper
**Tempo3D: Efficient Temporal-Aware Fine-Tuning and Multi-View Latent Aggregation for 3D Generation**.

## Structure

```
project_page/
├── index.html                # main page
├── README.md
└── static/
    ├── css/style.css         # custom theme
    ├── js/                   # (reserved for future interactive demos)
    ├── images/               # put exported paper figures here
    └── videos/               # (reserved for the paper video / supplementary clips)
```

## Required figure assets

Drop the following exports from the paper into `static/images/` (file names must match):

| File | Source in paper | Notes |
| --- | --- | --- |
| `teaser.png`        | Fig. 1  | hero strip, both (A) generation and (B) editing |
| `pipeline.png`      | Fig. 3  | full Tempo3D pipeline |
| `architecture.png`  | Fig. 4  | DiT block + TS-LoRA |
| `projection.png`    | Fig. 8  | FTP vs. Soft FTP |
| `aggregation.png`   | Fig. 9  | naive vs. Soft FTP vs. SVFA |
| `qual_classical.png`| Fig. 10 | classical-image comparison grid |
| `qual_aigen.png`    | Fig. 11 | AI-generated comparison grid |
| `editing.png`       | Fig. 12 | language-driven editing examples |
| `abl_tslora.png`    | Fig. 13 | TS-LoRA ablation |
| `abl_svfa.png`      | Fig. 14 | Soft FTP / SVFA ablation |
| `abl_gamma.png`     | Fig. 16 | γ sweep curve |
| `user_study.png`    | Fig. 17 | 2AFC win rate chart |

Quick way to extract them on Windows:

```bash
# 1. Convert each page to PNG (requires poppler — `pip install pdf2image` + the poppler binaries)
python -c "from pdf2image import convert_from_path; \
[img.save(f'page_{i+1}.png') for i, img in enumerate(convert_from_path('../SIGGRAPH2026_CR.pdf', dpi=200))]"

# 2. Crop the figure regions in any image editor (Photoshop / GIMP / paint.net).
```

Or, if you have the original figure source (TikZ / PSD / PNG masters), drop those in directly.

## Local preview

Any static server works:

```bash
cd project_page
python -m http.server 8000
# open http://localhost:8000
```

## Updating the placeholder links

`index.html` currently links the PDF locally (`../SIGGRAPH2026_CR.pdf`) and uses `#` for arXiv / GitHub /
dataset / video. Replace those `href="#"` entries with the real URLs once available.

## Deployment (GitHub Pages)

1. Push `project_page/` to a repo (e.g. `tempo3d-page`).
2. In repo Settings → Pages, choose `main` branch and `/project_page` as the source.
3. Custom domain via `static/CNAME` if needed.