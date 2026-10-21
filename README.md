# 3dsvgok

## About this derivative

This repository is a personal derivative of [renatoworks/3dsvg](https://github.com/renatoworks/3dsvg), originally created by Renato Costa under the MIT license. The upstream author and license are preserved.

The [`3dsvg` npm package](https://www.npmjs.com/package/3dsvg) and [3dsvg.design](https://3dsvg.design) referenced below belong to the upstream project. This repository does not publish a separate npm package or operate that website. Its current focus is maintaining the copied editor and its deployment configuration.

See [CONTRIBUTING.md](CONTRIBUTING.md) for local checks and how to propose a change.

![3dsvg](.github/assets/demo.png)

The easiest way to turn SVGs into interactive 3D.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![npm](https://img.shields.io/npm/v/3dsvg)](https://www.npmjs.com/package/3dsvg)

## Overview

This is a monorepo with two packages:

| Package | Description |
|---------|-------------|
| [`packages/engine`](packages/engine/) | Embeddable `<SVG3D>` React component — published to npm as [`3dsvg`](https://www.npmjs.com/package/3dsvg) |
| [`packages/web`](packages/web/) | Visual editor at [3dsvg.design](https://3dsvg.design) — design 3D objects and export as images, video, 3D models, or embed code |

The web editor renders the engine's `<SVG3D>` component directly — what you see in the editor is exactly what you get with the embed.

## Quick Start

Use **Node.js 20.9 or newer** and npm. The web workspace uses Next.js 16, whose minimum Node.js version is 20.9; Node.js 18 is not supported. CI checks the project on Node.js 24, on Linux and Windows.

```bash
npm ci --ignore-scripts
npm run build:engine
npm run dev:web
```

Open [http://localhost:3000](http://localhost:3000).

## Development checks

From the repository root, run:

```bash
npm run check
```

This builds the engine, including its TypeScript declarations, before type-checking the web workspace against the local engine. It does not start a server, deploy the app, publish to npm, or require an API key.

The same command runs in GitHub Actions for pushes and pull requests. A passing check covers compilation and types; it does not replace testing the editor and its exports in a browser.

## Embed

```bash
npm install 3dsvg
```

```tsx
import { SVG3D } from "3dsvg";

<SVG3D text="Hello" animate="spin" />
<SVG3D svg="/logo.svg" material="gold" />
```

See the full [engine docs](packages/engine/README.md) for all props.

## Web Editor Features

- **4 input methods** — Text (10 Google Fonts), Pixel Editor, SVG Code, File Upload
- **10 material presets** — Default, Plastic, Metal, Glass, Rubber, Chrome, Gold, Clay, Emissive, Holographic
- **7 animations** — Spin, Float, Pulse, Wobble, Swing, Spin+Float, or static
- **Textures** — 10 procedural presets or upload your own
- **Configurable lighting** — Key light position/intensity, ambient, shadows
- **PNG export** — Transparent or with background, up to 4K resolution
- **Video export** — 60fps capture with iOS-style trim UI, MP4 (via FFmpeg WASM) or WebM, quality control
- **3D model export** — Download the scene as GLB (color + materials preserved), STL (3D printing), OBJ, or PLY
- **Camera mode** — iPhone-style shutter button, aspect ratio picker, viewfinder overlay
- **Interactive canvas** — Drag rotation with momentum, scroll zoom, cursor-follow orbit
- **Responsive** — Auto-zooms on narrow/portrait viewports to keep the 3D object visible
- **Embed code export** — Copy-ready `<SVG3D>` JSX snippet with all props from the current editor state
- **Drag & drop** — Drop SVG files anywhere on the page to load them

## Project Structure

```
3dsvg/
├── packages/
│   ├── engine/                 # npm package "3dsvg"
│   │   └── src/
│   │       ├── index.tsx       # SVG3D component (public API)
│   │       ├── scene.tsx       # 3D scene, ExtrudedSVG, Canvas
│   │       ├── controls.tsx    # Animations, smooth controls
│   │       ├── materials.ts    # 10 PBR material presets
│   │       ├── types.ts        # SVG3DProps, defaults
│   │       └── use-font.ts     # Google Font loading
│   └── web/                    # Next.js editor app
│       └── src/
│           ├── app/            # Pages
│           ├── components/     # Editor UI, export bar
│           └── lib/            # Textures, FFmpeg, utilities
└── package.json                # npm workspaces root
```

## Tech Stack

| Library | Purpose |
|---------|---------|
| [Next.js 16](https://nextjs.org/) | App framework (web) |
| [React Three Fiber](https://docs.pmnd.rs/react-three-fiber) | Declarative Three.js |
| [Three.js](https://threejs.org/) | 3D rendering |
| [tsup](https://tsup.egoist.dev/) | Engine bundler |
| [opentype.js](https://opentype.js.org/) | Font to vector paths |
| [FFmpeg WASM](https://ffmpegwasm.netlify.app/) | Video conversion (web) |
| [shadcn/ui](https://ui.shadcn.com/) | UI components (web) |
| [Tailwind CSS v4](https://tailwindcss.com/) | Styling (web) |

## License

MIT — [Renato Costa](https://renato.works)

Made in [Blueberry](https://meetblueberry.com) 🫐
