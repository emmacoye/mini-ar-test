# mini-ar-test

A minimal MindAR.js image-tracking test project.  
Use this to verify image tracking works in your local Cursor setup **before** converting the JetZero project.

---

## What it does

- Opens the camera
- Scans for a **compiled image target** (`targets.mind`)
- Renders a **spinning orange 3D box** on top of the target using Three.js

---

## Setup

### 1. Install a local server (if you don't have one)

```bash
npm install -g serve
# or use the Live Server extension in VS Code / Cursor
```

### 2. Generate your target image + `.mind` file

MindAR needs a compiled `.mind` file (not a raw image).  
Use the **MindAR Image Target Compiler**:

👉 https://hiukim.github.io/mind-ar-js-doc/tools/compile

Steps:
1. Open the compiler in your browser
2. Upload **any image** you want to use as your AR target  
   (high-contrast images with lots of detail work best — logos, posters, etc.)
3. Click **Compile**
4. Download the `.mind` file
5. **Also save the source image** as `target-image.png` — you'll point your camera at this

Put both files in this folder:
```
mini-ar-test/
  index.html
  targets.mind          ← compiled file from compiler
  target-image.png      ← the image you compiled (print it or open on another screen)
```

### 3. Run

```bash
cd mini-ar-test
serve .
# Then open http://localhost:3000 on your phone or desktop browser
```

> ⚠️ Camera access requires **HTTPS or localhost**.  
> `serve` on localhost works fine. For mobile testing, use ngrok or deploy to GitHub Pages.

---

## Testing on mobile

```bash
npm install -g ngrok
ngrok http 3000
# Use the https:// URL ngrok gives you — open it on your phone
```

---

## Project structure

```
index.html          ← main AR scene (MindAR + Three.js via CDN)
targets.mind        ← YOU generate this (see step 2 above)
target-image.png    ← the image to point your camera at
README.md
```

---

## Next step: JetZero conversion

Once this mini test works, the JetZero conversion follows the same pattern:

| Current (Zappar/Mattercraft)         | New (MindAR)                          |
|--------------------------------------|---------------------------------------|
| `InstantWorldTracker` (plane)        | `MindARThree` + image target          |
| `@zcomponent/zappar-three`           | `mind-ar` CDN or npm package          |
| `.zcomp` scene file                  | Plain `index.html` + `index.js`       |
| Placement tap gesture                | Auto-anchors when target detected     |
| `plane.glb` / `main-building.glb`   | Same `.glb` files via `GLTFLoader`    |

The JetZero target image would typically be a **printed card or brochure** with the JetZero logo — something you'd place on a table.

---

## Resources

- [MindAR docs](https://hiukim.github.io/mind-ar-js-doc/)
- [Image target compiler](https://hiukim.github.io/mind-ar-js-doc/tools/compile)
- [MindAR GitHub](https://github.com/hiukim/mind-ar-js)
- [AR.js (alternative)](https://github.com/AR-js-org/AR.js)
