# playlist-tweaks

Play a YouTube playlist in any order: drag to reorder, or sort by title, upload date, shuffle or default order. Your order is saved per playlist in the browser.

- **Fill window** button: the video fills the whole browser tab. Esc or ✕ exits (F11 on top for real fullscreen). YouTube's keyboard shortcuts are off while filling so Esc always works.
- Dark theme built in; the page tells Dark Reader to leave it alone.
- SponsorBlock: not built in. The SponsorBlock browser extension works inside the embedded player.

## Run

```
docker run -d -p 8000:80 ghcr.io/niklas2233/playlist-tweaks:latest
```

Or build it yourself:

```
docker build -t playlist-tweaks .
docker run -d -p 8000:80 playlist-tweaks
```

Open http://localhost:8000 and paste a playlist URL.

### Updating

Every push to `main` publishes a new `:latest` image. `docker run` won't fetch it on its own, so pull and recreate:

```
docker pull ghcr.io/niklas2233/playlist-tweaks:latest
docker rm -f <container> && docker run -d -p 8000:80 ghcr.io/niklas2233/playlist-tweaks:latest
```

In Portainer: open the container → **Recreate** → turn on **Re-pull image**. Then hard-refresh the page (Ctrl+F5) in case the browser cached the old one.

Without Docker: `python -m http.server 8000` in this folder. (Opening `index.html` directly from disk breaks the YouTube embed.)

## Upload-date sorting

Needs a free YouTube Data API v3 key (Google Cloud Console → enable "YouTube Data API v3" → Credentials → API key). Paste it into the key field; it's saved as soon as you type it, and only in your browser (per browser and per address).

## Limits

- Only the first ~200 videos of a playlist (embed player limit).
- Titles come from noembed.com unless an API key is set.
