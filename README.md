# Hebrew lyrics for Spotify

A static site that shows the Hebrew lyrics and an English translation of whatever is playing on your Spotify account, with both texts filling in green as the song advances. Works on GitHub Pages with no backend.

## 1. Put it on GitHub Pages

1. Create a new public repo on GitHub (for example `hebrew-lyrics`).
2. Upload `index.html`, `songs.json` and this `README.md` to the root of the repo.
3. Repo → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
4. After a minute your site is live at `https://YOUR-USERNAME.github.io/hebrew-lyrics/` (note the trailing slash).

## 2. Create a Spotify app

1. Go to https://developer.spotify.com/dashboard and log in with your Spotify account.
2. Create an app. Any name works. Under "Redirect URIs" add **exactly** the address of your site, e.g. `https://YOUR-USERNAME.github.io/hebrew-lyrics/` (the site's Settings page shows the exact string to paste). Tick "Web API". Save.
3. Copy the **Client ID** (you do not need the client secret).
4. Open your site → Settings → paste the Client ID → "Save and connect Spotify". Log in and approve.

Notes:
- Reading what's playing works with any Spotify account. The Play/Pause button on the site needs Spotify Premium.
- Spotify apps start in "development mode": only the account that created the app (plus up to 25 users you add in the dashboard) can log in. That's fine for personal use.
- Play music in any Spotify app (phone, desktop, web) — the site just follows along.

## 3. Add lyrics for a song

Spotify doesn't provide lyrics through its API, so you add them yourself:

1. Play the song. The site shows "No lyrics yet" with the track ID, and a button "Add and sync lyrics".
2. In the sync editor, paste the Hebrew lines in the left box and the English lines in the right box (one line per row, same order).
3. Press "Start tapping", restart the song in Spotify, and tap **Now** (or press Space) at the moment each line begins.
4. Copy the JSON it produces and paste it into `songs.json` in your repo (commit the change). The site also previews it immediately.

`songs.json` format — one entry per Spotify track ID:

```json
{
  "3n3Ppam7vgaVa1iaRUc9Lp": {
    "title": "Song title",
    "artist": "Artist",
    "lines": [
      { "t": 12.4, "he": "שורה בעברית", "en": "The line in English" },
      { "t": 16.0, "he": "…", "en": "…", "end": 19.5 }
    ]
  }
}
```

- `t` is the start time of the line in seconds.
- A line fills from its `t` until the next line's `t`. Add `"end"` to stop the fill earlier (useful before an instrumental break or on the last line).
- The track ID is the part after `track/` in a Spotify share link, e.g. `https://open.spotify.com/track/3n3Ppam7vgaVa1iaRUc9Lp`.
- If the lyrics run slightly early or late, use the per-song offset in Settings.

The included sample is Hatikvah (public domain). Its timings are placeholders — replace `REPLACE_WITH_SPOTIFY_TRACK_ID` with the ID of whichever recording you use and retime it with the sync editor. "Try a demo without Spotify" on the home screen plays the first song in `songs.json` on a local timer so you can see the effect before connecting.
