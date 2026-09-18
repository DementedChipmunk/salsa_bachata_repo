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
