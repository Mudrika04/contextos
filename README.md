# ContextOS: My Context

A personal command-center dashboard that shows what is happening, what needs attention, why it matters, how items connect, and what to do next.

It is a static site (one HTML file, no build step, no dependencies). Data is stored in the browser's `localStorage`, so it is private to each browser and device.

## Features

- Attention radar and context orbit (click or tap any node)
- Prioritized "What needs your attention?" queue with a **Why?** explanation for every item
- Day and week timeline with conflict detection
- Context insights, context load (transparent formula), progress pulse, heatmap
- Focus mode with a 45-minute timer
- Quick capture (task, note, event, pasted text, image or PDF name) and search
- Light and dark themes, responsive layout, `prefers-reduced-motion` respected

## Run locally

```bash
python3 -m http.server -d public 8080
# open http://localhost:8080
```

## Deploy

**GitHub Pages (included workflow)**
1. Push this repo to GitHub (see below).
2. In the repo go to Settings, then Pages, and set Source to **GitHub Actions**.
3. Every push to `main` deploys. The URL is `https://<username>.github.io/<repo>/`.

**Netlify:** import the repo. `netlify.toml` already sets the publish folder to `public`.

**Vercel:** import the repo. `vercel.json` already sets the output folder to `public`.

**Docker or your own server**
```bash
docker build -t contextos .
docker run -d -p 80:80 --restart unless-stopped contextos
```
Or copy the contents of `public/` to any web root (nginx, Apache, S3 static hosting).

## Push to GitHub

```bash
git init -b main
git add .
git commit -m "Initial commit: ContextOS dashboard"
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

## Connecting a real backend

The functions in the `api` object in `public/index.html` (`summary`, `attention`, `timeline`, `graph`, `insights`, `progress`, `heatmap`) mirror these endpoints, and currently read from local storage:

```
GET /dashboard/summary      GET /dashboard/timeline     GET /dashboard/insights
GET /dashboard/attention    GET /dashboard/context-graph
GET /dashboard/progress     GET /dashboard/heatmap
```

To use a server, replace each function with a `fetch` call that returns the same shape and make `render()` async.

## License

MIT
