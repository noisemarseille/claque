# CLAQUE — Press Kit

Static HTML press kit for **CLAQUE**, a noise rock trio from Marseille.  
Served as a single `index.html` file with all assets under `claque/`.

---

## Project Structure

```
claque/
├── index.html                  # Main press kit page
├── generate_manifest.sh        # Helper: regenerates pics/manifest.json
└── claque/
    ├── Photo.jpg               # Hero / main background photo
    ├── FT.png                  # Fische Technique image
    ├── claque_logo.png         # Band logo (used in hero, inverted to white)
    ├── claque_logo_original.png
    ├── logo.png                # Favicon / nav logo
    ├── logo32.png              # 32×32 favicon
    ├── logo32_bw.png
    ├── logo32_color.png
    ├── description.json        # Bilingual band bio
    ├── performances.json       # Live show history
    ├── albums/
    │   └── xanax paradise/
    │       └── album.jpg       # Album artwork
    └── pics/
        ├── manifest.json       # Auto-generated list of photo filenames
        └── *.jpg               # Band photos (live, promo, etc.)
```

---

## Key Assets

### `claque/Photo.jpg`
The **main hero background photo**. Displayed full-screen behind the band name on page load, with a dark overlay and monochrome radial gradients for atmosphere.

### `claque/FT.png`
The **Fische Technique** image. Used as a visual element in the press kit to represent the band's sonic approach / methodology.

---

## JSON Files

All JSON files live under `claque/` and drive the dynamic content of the page — no CMS, no backend.

### `claque/description.json`
Bilingual band biography. The page reads both fields and renders them in their respective language sections.

```json
{
  "fr": "Bio en français...",
  "en": "Bio in English..."
}
```

**Used by:** the Biography section of `index.html`.

---

### `claque/performances.json`
Array of live performance entries. Each object has:

| Field | Type | Description |
|---|---|---|
| `venue` | string | Venue name and city |
| `year` | string | Year of the performance |
| `description` | string | Short note about the show |

```json
[
  {
    "venue": "L'Embobineuse, Marseille",
    "year": "2025",
    "description": "Release party !!! with friends."
  }
]
```

**Used by:** the Live / Performances section of `index.html`.

---

### `claque/pics/manifest.json`
Auto-generated list of filenames in the `pics/` folder. The photo grid fetches this file at runtime, Fisher-Yates shuffles the list, and picks 6 random images to display on each page load.

```json
["DSC4098-Modifier-2-Modifier-3.jpg", "DSC4104-Modifier-Modifier-2.jpg", "..."]
```

**Used by:** the Visions photo grid in `index.html`.  
**Do not edit manually** — regenerate it instead:

```bash
./generate_manifest.sh
```

Run this script from the repo root whenever you **add or remove photos** from `claque/pics/`. It scans for all `.jpg`, `.jpeg`, `.png`, and `.webp` files and rewrites `manifest.json` automatically.

> ⚠️ The photo grid uses `fetch()` and requires the page to be served over HTTP — it will not work when opened directly as a `file://` URL.

---

## Adding New Photos

1. Drop the image file into `claque/pics/`
2. Run `./generate_manifest.sh` from the repo root
3. The grid will automatically include the new photo in its random rotation

---

## Logo

The hero logo is currently rendered as an `<h1>CLAQUE</h1>` with a white glitch/glow animation.  
A commented-out `<img>` tag is ready in `index.html` — just drop `claque_logo.png` in `claque/` and uncomment it:

```html
<!-- <img src="claque/claque_logo.png" alt="CLAQUE"
     style="max-width: clamp(200px, 40vw, 500px);
            filter: brightness(0) invert(1);
            animation: glitch 0.3s infinite;"> -->
```
