# 🏓 Pong Tournament Rankings

A one-page site where people rank the tournament players 1→N and everyone sees a live overall leaderboard. No logins. One file (`index.html`), hosted free on GitHub Pages, with a free Firebase database for shared results.

Total setup: ~10 minutes.

---

## Step 1 — Add your players (1 min)

Open `index.html`, find the `PLAYERS` list near the top of the `<script>`, and replace the placeholders with the real names:

```js
const PLAYERS = [
  "Alex",
  "Sam",
  "Jordan",
  ...
];
```

You can have any number of players (the ballot adapts). Keep each name in `"quotes"` with a comma after it.

---

## Step 2 — Create a free Firebase database (~4 min)

This is what lets all 10 people see each other's rankings.

1. Go to **https://console.firebase.google.com** and sign in with your Google account.
2. Click **Add project** → give it any name (e.g. `pong`) → you can **disable** Google Analytics → **Create project**.
3. In the left menu, click **Build → Realtime Database** → **Create Database**.
   - Pick any location.
   - Choose **Start in test mode** → **Enable**.  
     *(Test mode = anyone can read/write. Perfect for a 1-day event. See cleanup below.)*
4. Get your config: click the **⚙️ gear → Project settings**. Scroll to **Your apps**, click the **web icon `</>`**, register an app (any nickname, no hosting needed). You'll see a `firebaseConfig` object.

---

## Step 3 — Paste the config into `index.html` (1 min)

Copy the values from `firebaseConfig` into the `FIREBASE_CONFIG` block in `index.html`:

```js
const FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "pong-xxxx.firebaseapp.com",
  databaseURL: "https://pong-xxxx-default-rtdb.firebaseio.com",
  projectId: "pong-xxxx"
};
```

⚠️ **The `databaseURL` must be present** (it looks like `https://...firebaseio.com`). If Firebase didn't show it in the snippet, grab it from the Realtime Database page you created in Step 2.

> It's safe that these keys are public — Firebase keys are meant to be in client code, and test-mode rules are what control access.

---

## Step 4 — Host on GitHub Pages (~3 min)

1. Create a new repository on GitHub (e.g. `pong-rankings`). Make it **Public**.
2. Upload `index.html` (drag-and-drop in the GitHub web UI → **Add file → Upload files → Commit**).
3. Go to the repo's **Settings → Pages**.
4. Under **Build and deployment**, set **Source = Deploy from a branch**, **Branch = `main`**, folder = `/ (root)` → **Save**.
5. Wait ~1 minute, then refresh. GitHub shows your live URL:  
   `https://<your-username>.github.io/pong-rankings/`
6. Share that link with your 10 people. Done. 🎉

---

## How it works

- Each voter types their name and drags players from best (1) to worst.
- **Overall standings** = each player's **average position** across all ballots (lower is better). Ties broken by the average.
- Re-submitting with the **same name** updates that person's ballot (no duplicates).
- Results update **live** for everyone.

## After the event (optional cleanup)

Since the database is in open test mode, just delete it when you're done: Firebase console → your project → **⚙️ → Project settings → delete project**, or delete the GitHub repo. Nothing to pay for either way (free tier).

## Testing locally first

Open `index.html` by double-clicking it, or run a local server from this folder:

```
python3 -m http.server 8000
```
then visit `http://localhost:8000`. Once your Firebase config is pasted in, submissions will save and sync.
