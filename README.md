# playlist-tweaks

Play a YouTube playlist in any order: drag to reorder, or sort by title, upload date, shuffle or default order. Your order is saved per playlist in the browser.

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

Without Docker: `python -m http.server 8000` in this folder. (Opening `index.html` directly from disk breaks the YouTube embed.)

## Upload-date sorting

Needs a free YouTube Data API v3 key (Google Cloud Console → enable "YouTube Data API v3" → Credentials → API key). Paste it into the key field; it's stored only in your browser.

## Limits

- Only the first ~200 videos of a playlist (embed player limit).
- Titles come from noembed.com unless an API key is set.
