# WebGL Distortion Effect

An interactive WebGL demo that renders text on a fullscreen canvas and distorts it in real time with a custom GLSL fragment shader. Move your mouse over the text to trigger a magnifying lens distortion with subtle iridescence, scanlines, phosphor glow, and a CRT-style vignette — like an old cathode-ray tube breathing under your cursor.

## Features

- **Real-time WebGL distortion** — fullscreen canvas, raw WebGL (no three.js), custom vertex + fragment shaders written inline
- **Mouse-driven lens effect** — text magnifies and warps around the cursor position with a configurable radius
- **Iridescent color shift** — HSV-to-RGB shader math adds a subtle rainbow sheen inside the distortion zone
- **CRT aesthetic** — animated scanlines, phosphor glow, film-grain noise, and a soft vignette
- **Smooth animation loop** — `requestAnimationFrame` render loop with time-based shader uniforms
- **Dark, minimal UI** — shadcn/ui + Tailwind styling, theme provider with dark mode
- **Fully client-side** — `'use client'` component only; no API routes, no server actions, no database

## Tech Stack

| Layer    | Tech                                  |
|----------|---------------------------------------|
| Framework | Next.js 15 (App Router, static export) |
| Language | TypeScript                            |
| Rendering | Raw WebGL + custom GLSL shaders       |
| Styling  | Tailwind CSS 3, shadcn/ui (Radix UI)  |
| UI extras | lucide-react icons, next-themes      |
| Package manager | pnpm                             |

## Quick Start

```bash
# install dependencies
npm install
# or: pnpm install

# run the dev server
npm run dev

# open http://localhost:3000
```

### Build for production

```bash
npm run build
npm start        # serves the production build locally
```

## Project Structure

```
web-gl-distortion-effect/
├── app/
│   ├── page.tsx        # WebGL canvas + GLSL distortion shader (the whole demo)
│   ├── layout.tsx      # Root layout, fonts, theme provider
│   └── globals.css     # Tailwind + theme styles
├── components/
│   ├── theme-provider.tsx
│   └── ui/             # shadcn/ui primitives (buttons, dialogs, tooltips…)
├── lib/
│   └── utils.ts        # cn() class-name helper
├── public/             # placeholder images / logos
├── styles/             # extra stylesheets
├── next.config.mjs     # static export config (+ basePath for GitHub Pages)
└── tailwind.config.ts  # Tailwind theme config
```

## Environment Variables

None. The app is fully static — no secrets, API keys, or backend config required.

## Deployment

This app is statically exported (`output: 'export'` in `next.config.mjs`), so it can be hosted on any static host:

- **GitHub Pages** — the `gh-pages` branch of this repo is published at `https://girishlade111.github.io/web-gl-distortion-effect/`
- **Vercel / Netlify / Cloudflare Pages** — `npm run build` then serve the `out/` directory

> Note: `next.config.mjs` sets `basePath: '/web-gl-distortion-effect'` so assets resolve under the GitHub Pages subpath. Remove `basePath` if you deploy to a root domain (Vercel/Netlify).

## How the Shader Works

1. Text is drawn to an offscreen 2D canvas, which becomes a WebGL texture.
2. The vertex shader maps the texture to a fullscreen quad.
3. The fragment shader samples the texture with a radial displacement around the mouse cursor (`u_magnifyRadiusPixels`), then layers HSV iridescence, scanlines, phosphor glow, noise, and vignette before output.

## License

Free to use and learn from.

---

Built by Girish Lade · [ladestack.in](https://ladestack.in)
