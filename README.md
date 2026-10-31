# Summit Studio

Mountains Lab (terrain editor / animation studio, Three.js 0.165) packaged as a Vite app.

## Develop
    npm install
    npm run dev      # http://localhost:5173
    npm run build    # outputs dist/
    npm run preview

## Structure
- `index.html` – page shell (element ids the script looks up must stay).
- `src/main.js` – entry; loads IBM Plex Sans, then the lab.
- `src/mountains-lab*.js`, `src/landform.js`, `src/mountains-lab.css` – the original lab assets (see `MOUNTAINS-LAB-README.md`).
- `three` is bundled from npm (pinned 0.165.0) – no CDN/import map.

## Font
IBM Plex Sans (300/400/500/600) is self-hosted via `@fontsource/ibm-plex-sans`, applied in the CSS `body` rule and the timeline `<canvas>` text. No other typography/layout changes.

## 3D export (Export → 3D model)
- **GLB with textures** – the mesh plus a baked base-colour texture (1K/2K/4K, contour lines optional) and, in hybrid/textured mode, a baked normal map. Roughness comes from the Render settings. Painterly break-up exports as alpha-mask cut-outs.
- **glTF / OBJ** – geometry only (positions, normals, UVs).
- **STL** – geometry only; by default a closed solid with walls and a floor, ready for slicing.
- **Heightmap 16-bit** – greyscale PNG at the terrain resolution; the filename carries the height range in metres (black → white). North (−Z) is the top row, matching the colour texture export.
- **Colour texture** – the baked colour map on its own, same orientation as the heightmap.

Meshes are in metres with the current vertical exaggeration and land transform applied. FBX isn't offered (no open exporter); Blender, Unity, Unreal and Godot all import GLB.

## Deploy to Vercel
1. Push this folder to `github.com/sahil639/Summit-Studio`.
2. Import the repo on Vercel – `vercel.json` sets the Vite preset, `npm run build`, output `dist`.
3. No environment variables are required. Node 18+.
Or via CLI: `npx vercel --prod`.

Notes: presets/library are stored in browser localStorage (`tibba.mountains.*`). Hashed assets get immutable cache headers.
