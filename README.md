# Salsa/Bachata DJ — Android-first

A single-page, phone-first Spotify set generator.

Features: Spotify search, local song pool, four categories (Salsa Fast / Salsa Medium / Bachata Slow / Bachata Medium), energy 1–5, BPM, song weights, Fast→Medium→Slow→Medium rotation, artist spacing, song cooldown, energy progression, BPM smoothing, 30 min–4 h sets, and private Spotify playlist creation.

## Android setup

1. Host this folder on an HTTPS static site.
2. In Spotify Developer Dashboard create an app and add the exact hosted URL as a Redirect URI.
3. Open the hosted URL in Chrome on Android.
4. Paste the Spotify Client ID and tap Connect Spotify.
5. Search/add songs and tag them.
6. Generate and create the playlist.

Do not put a Spotify Client Secret in this app. Spotify recommends Authorization Code with PKCE for browser/mobile apps where a secret cannot be safely stored.

The app uses the current playlist endpoints: POST /me/playlists and POST /playlists/{playlist_id}/items.

## Importing a song list (JSON)

Instead of adding songs one by one, paste or upload a JSON array in the "Import songs" card (requires being connected to Spotify first — each entry is looked up via Spotify search to get its track ID/URI/duration).

Each item can have:

- `title` + `artist` — searched as `"{title} {artist}"` — **or** a single `query` string instead
- `category` (required) — one of `SALSA_FAST`, `SALSA_MEDIUM`, `BACHATA_SLOW`, `BACHATA_MEDIUM` (case-insensitive)
- `energy` — 1–5, defaults to 3
- `weight` — relative pick frequency, 1 = normal, 2 = frequent, 0.5 = rare, defaults to 1
- `bpm` — optional, enables BPM smoothing for that track

Example (`example-songs.json`):

```json
[
  {"title": "Obsesión", "artist": "Aventura", "category": "BACHATA_SLOW", "energy": 2, "bpm": 124},
  {"title": "Vivir Mi Vida", "artist": "Marc Anthony", "category": "SALSA_MEDIUM", "energy": 3, "bpm": 195},
  {"query": "El Cantante Hector Lavoe", "category": "SALSA_MEDIUM", "energy": 3}
]
```

Duplicates already in the pool and songs with no Spotify match are skipped and listed after import. This is a good use case for an LLM: ask it to generate a JSON list like this for a given set/vibe (with real song and artist names), then paste the result straight into the Import box.
