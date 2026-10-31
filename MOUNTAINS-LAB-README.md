# Mountains Lab

A terrain editor and animation studio for contour-drawn mountains (Three.js 0.165).

## Files
- `index.html` — the page: the canvas plus the empty panel/toolbar/timeline containers the script fills.
- `mountains-lab.js` — the editor (UI, sculpting, light, motion, export).
- `mountains-lab-terrain.js` — builds the heightfield mesh.
- `landform.js` — the landform generator and preset library.
- `mountains-lab.css` — the styles.

## Run
It uses ES modules, so serve the folder over http (opening the file directly won't work):

    npx serve .        # or: python3 -m http.server

## Adding it to another project
- Keep the four JS/CSS files together; they import each other by relative path.
- Three.js comes from unpkg through the import map in `index.html`. If your project already
  bundles `three`, delete the import map and the `import 'three'` lines resolve to yours.
- The script looks up these ids: `lab`, `panel`, `tools`, `timeline`, `hud`, `present-bar`,
  `busy`, `busy-t`, `busy-bar`, `busy-x`, `toast`. Keep them on the page.
- The CSS is written for a full-screen page (`html, body { overflow: hidden }`). To embed it in
  part of a page, scope those rules or put the lab in an iframe.
- Presets and the library are saved in localStorage under `tibba.mountains.*` keys; rename them
  in `mountains-lab.js` (`LIB_KEY`) and `landform.js` (`USE_KEY`) if you like.
- The font falls back to system-ui. The original site used F37 Analog (a trial licence, not included).
