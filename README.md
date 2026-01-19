# Charvi Khandelwal — Portfolio

High-polish personal site for Charvi Khandelwal built with React 19, Vite, Tailwind CSS, Framer Motion, and Lucide icons. The experience includes animated finance/astrophysics storytelling sections, theme toggling, and a dedicated projects route.

## Table of contents
1. [Tech stack](#tech-stack)
2. [Prerequisites](#prerequisites)
3. [Local development](#local-development)
4. [Available scripts](#available-scripts)
5. [Project structure](#project-structure)
6. [Builds & previews](#builds--previews)
7. [Deploying to GitHub Pages](#deploying-to-github-pages)

## Tech stack
- React 19 with hooks and React Router
- Vite 7 bundler + HMR
- Tailwind CSS 3 + custom theme tokens
- Framer Motion 12 for interactions
- gh-pages CLI for static hosting

## Prerequisites
- **Node.js 18+** (LTS recommended)
- **npm 9+** (ships with Node). If you use pnpm or yarn, make sure scripts match.
- GitHub repository at `kswork2001/CharviKhandelwal` (needed for Pages deploy target).

## Local development
```bash
# install dependencies (first run)
npm install

# start the Vite dev server on http://localhost:5173
npm run dev
```

The dev server provides hot-module reloading (HMR). Press `o` in the terminal to open the browser, or manually navigate to the printed URL.

## Available scripts
| Command | Description |
| --- | --- |
| `npm run dev` | Starts Vite in development mode with HMR. |
| `npm run build` | Produces a production bundle inside `dist/`. |
| `npm run preview` | Serves the latest production bundle locally (great QA check). |
| `npm run lint` | Runs ESLint against the whole project. |
| `npm run deploy` | Builds + publishes `dist/` to the `gh-pages` branch (see below). |

## Project structure
```
├── public/                # Static assets copied as-is
├── src/
│   ├── App.jsx            # Main UI + routes + sections
│   ├── assets/            # Static React assets
│   ├── index.css          # Tailwind layer + global resets
│   ├── App.css            # Component-specific styles (light usage)
│   └── main.jsx           # React entry point
├── tailwind.config.js     # Theme tokens, color palette
├── postcss.config.js      # Tailwind + autoprefixer pipeline
├── vite.config.js         # React plugin + base path for Pages
└── package.json           # Scripts + dependency manifest
```

## Builds & previews
1. `npm run build` emits optimized static assets in `dist/`.
2. `npm run preview` runs a tiny server so you can QA the exact bundle that will ship.
3. Clean up old artifacts by removing `dist/` if you need a fresh build.

## Deploying to GitHub Pages
This project already includes the wiring for GitHub Pages via the `gh-pages` package:

1. **Ensure config is correct**
   - `package.json > homepage` → `https://kswork2001.github.io/CharviKhandelwal/`
   - `vite.config.js > base` → `/CharviKhandelwal/`
2. **Authenticate once** (only needed locally):
   ```bash
   gh auth login  # or create a classic PAT and set it as origin credentials
   ```
3. **Deploy**
   ```bash
   npm run deploy
   ```
   The preconfigured `predeploy` hook runs `npm run build`, then `gh-pages -d dist` pushes to the `gh-pages` branch and updates the GitHub Pages site.

### Optional: GitHub Actions automation
If you prefer CI-based deployments, add an Action that runs `npm install`, `npm run build`, and then publishes `dist/` using `actions/upload-pages-artifact` + `actions/deploy-pages`. Keep the `base` and `homepage` values as above so asset paths stay correct.

## Troubleshooting
- **404s on refresh**: Ensure GitHub Pages is serving from the `gh-pages` branch and that `vite.config.js` has the correct `base` path.
- **Blank screen after deploy**: Usually caused by forgetting to run `npm run build` before serving or an incorrect `homepage` URL.
- **Permission errors on deploy**: Regenerate a GitHub personal access token or run `gh auth refresh -h github.com -s delete_repo,workflow`.
