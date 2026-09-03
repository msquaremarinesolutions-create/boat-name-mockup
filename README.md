# boat-name-mockup

**See your boat name on your own transom.** Upload a photo of your boat, drag four corners onto the transom, and the name is rendered into the photo in perspective — in polished, brushed, black or gold finishes.

**Live:** https://mockup.msquaremarine.com

Everything runs in the browser. **The photo is never uploaded** — no server, no storage, no tracking. That is not a policy promise, it is how the tool is built: there is no backend to send it to.

## What it does

- **Perspective mapping** — a homography is fitted to the four corners you place, and the lettering is drawn through it with a 24×24 tile mesh, so it sits on a tilted or angled transom correctly.
- **Undistorted letterforms** — the name is fitted inside the marked area at its true aspect ratio rather than stretched, so the preview shows what the letters actually look like.
- **Material finishes** — polished 316L, brushed 316L (with grain), black and gold, each with a stand-off drop shadow, because cut letters sit proud of the hull.
- **Contrast check** — the tool samples the brightness of the marked area straight from your photo and warns when the chosen finish will be hard to read against that hull.
- **Download** as a PNG, labelled as a visualisation.

## Honesty

The output is clearly marked *digital visualisation*. It is a preview of a proposed job on the customer's own boat — never a photograph of finished work, and never a rendering of someone else's vessel.

## Run locally

One static HTML file, no build step, no dependencies:

```bash
npx http-server docs -p 8126
```

## How the perspective works

The four corner points define a quad. A 3×3 homography **H** is solved from the unit square to that quad (8 unknowns from 4 point pairs, Gaussian elimination). The lettering is rendered to an offscreen canvas cropped to its own bounding box, then drawn as a mesh of tiles: each tile's four corners are mapped through **H** and the tile is painted as two affine-textured triangles. Clip triangles are expanded by a fraction of a pixel so no seams appear between tiles.

## License

Code: [MIT](LICENSE). Fonts load from Google Fonts under the SIL Open Font License and are not redistributed here.

---

Made by [M.Square Marine](https://www.msquaremarine.com) — laser-cut 316L stainless steel boat lettering.
See also: [size calculator](https://size.msquaremarine.com) · [boat name rank](https://names.msquaremarine.com) · [boat-names-dataset](https://github.com/msquaremarinesolutions-create/boat-names-dataset)
