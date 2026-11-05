# NCR Conquest — standalone website (GitHub Pages + Google Maps + Firebase)
 
This is the same branch-campaign tracker, rebuilt to run as a real website
instead of a Claude artifact: real Google Maps instead of the hand-drawn
map, and a Firebase database instead of Claude's built-in one. Hosting on
GitHub Pages is free; Google Maps and Firebase both have free tiers that
should fully cover normal use by a small team (see **Cost** at the bottom).
 
Everything (claiming branches, visit logs, the Victory Dashboard, CSV
export, admin add) works the same as before. The only new concept is that
**the shared password now also grants admin rights** (status override,
add-location, one-time data import) — there's no separate login system
on a plain static site, so it reuses the same gate that used to just
unlock the Monitor/download.
 
## What's in this folder
 
- `index.html` — the whole site (one file, inline CSS/JS).
- `data/branches.json` — the full 1,464-location master list (1,099 NCR +
  365 Lucknow), used only once, to seed the live database.
- `firestore.rules` — the database security rules (see step 3).
- `README.md` — this file.
## Step 1 — Put this on GitHub Pages
 
1. Create a new **public** repository on GitHub (private also works, but
   GitHub Pages on a private repo needs a paid GitHub plan).
2. Upload `index.html`, the `data/` folder, and `firestore.rules` to it
   (drag-and-drop on the GitHub web UI works fine, or `git push`).
3. In the repo, go to **Settings → Pages**. Under "Build and deployment",
   set Source to **Deploy from a branch**, branch **main**, folder **/
   (root)**. Save.
4. After a minute, GitHub shows your live URL — something like
   `https://yourusername.github.io/ncr-conquest/`. It will show the
   red "not configured" banner until you finish steps 2–4 below.
## Step 2 — Create a Firebase project (the shared database)
 
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
   and click **Add project**. Give it any name — this also creates a
   matching Google Cloud project behind the scenes, which you'll reuse
   in step 4.
2. In the new project, go to **Build → Firestore Database → Create
   database**. Choose **Production mode** and any nearby region (e.g.
   `asia-south1` for India).
3. Go to **Project settings** (gear icon) → **General** → scroll to
   "Your apps" → click the **</> (Web)** icon → give it a nickname →
   **Register app**. Firebase shows you a config object that looks like:
```js
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "your-project.firebaseapp.com",
     projectId: "your-project",
     storageBucket: "your-project.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };
```
4. Open `index.html`, find `FIREBASE_CONFIG` near the top, and paste
   those six values in (replacing the `YOUR_...` placeholders).
## Step 3 — Set the database rules
 
1. In Firebase Console, go to **Firestore Database → Rules**.
2. Replace the contents with everything in `firestore.rules` (also
   included in this folder), and click **Publish**.
3. Read the comment at the top of that file — it's a deliberately open,
   trust-based rule set (same model the original app used), not a
   production-grade lockdown. That's almost certainly fine for an
   internal team tool, but it does mean anyone with your site's URL
   could in principle write to the database directly, bypassing the
   password screen. If that's not acceptable, this is the one piece
   you'd want to revisit with Firebase Authentication later.
## Step 4 — Get a Google Maps API key
 
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
   and select the **same project** Firebase created for you in step 2
   (top-left project switcher).
2. You'll be asked to **link a billing account** (a payment method is
   required to use any Google Maps API, even within the free tier — see
   **Cost** below). Go to **Billing** and link or create one.
3. Go to **APIs & Services → Library**, search for **Maps JavaScript
   API**, and click **Enable**.
4. Go to **APIs & Services → Credentials → Create credentials → API
   key**. Copy the key (starts with `AIza...`).
5. Click the new key to edit it, and restrict it:
   - **Application restrictions** → **Websites** → add
     `yourusername.github.io/*` (and `localhost/*` if you want to test
     locally first).
   - **API restrictions** → **Restrict key** → select only **Maps
     JavaScript API**.
   - Save.
6. Open `index.html`, find `GOOGLE_MAPS_API_KEY` near the top, and paste
   your key in.
7. Optional but recommended: in Cloud Console, go to **IAM & Admin →
   Quotas** (or **APIs & Services → Maps JavaScript API → Quotas**) and
   set a daily request cap, since Google Maps has no built-in spending
   limit — see **Cost** below.
## Step 5 — Push your changes and seed the data
 
1. Commit and push your edited `index.html` (with both placeholders
   filled in) back to the GitHub repo. GitHub Pages redeploys
   automatically within a minute or two.
2. Open your live site. The red configuration banner should be gone and
   the map should load.
3. Click **Download master file** (or **Victory Dashboard**) and enter
   the shared password: **`NCRBranch@2026`**. This both opens that
   feature and unlocks admin controls for your browser.
4. A new **Import master data (one-time)** button appears next to
   Download. Click it, confirm, and wait for "Import complete" — this
   loads all 1,464 real branches from `data/branches.json` into your
   live Firestore database. It's safe to click again later if you ever
   need to re-sync the master list (it won't create duplicates).
5. That's it — the site is live. Share the URL with your team.
### Changing the password
 
The password's SHA-256 hash is hardcoded in `index.html` as
`APP_PASSWORD_HASH`. To change it, run this in any browser console (or
in a Node.js console) to get the new hash, then paste it in:
 
```js
crypto.subtle.digest("SHA-256", new TextEncoder().encode("YourNewPassword"))
  .then(buf => console.log([...new Uint8Array(buf)].map(b => b.toString(16).padStart(2,"0")).join("")));
```
 
## Cost
 
For a small internal team (a handful of commanders, ~1,500 branches,
checked a few hundred times a month), this should run entirely inside
free tiers:
 
- **GitHub Pages**: free, no limit relevant here.
- **Google Maps JavaScript API**: 10,000 free map loads per month, then
  $7 per 1,000 loads beyond that. There is **no automatic spending
  cap** — Google only emails a budget alert after charges happen — so
  set a quota (step 4.7) if you want a hard ceiling. A billing account
  with a payment method is required even to use the free tier.
- **Firebase Firestore (free Spark plan)**: 1 GiB stored data, 50,000
  reads/day, 20,000 writes/day, 10 GB/month network egress — all free.
- **Firebase Hosting isn't used here** (GitHub Pages hosts the file
  instead), so that free tier doesn't even come into play.
Realistic expected cost: **$0/month**, unless usage grows far beyond an
internal team tool (thousands of map loads a day, or a much larger
branch list).
 
## If something doesn't work
 
- **Red banner never goes away**: one of the two placeholders in
  `index.html` is still unfilled, or mistyped. Double-check
  `GOOGLE_MAPS_API_KEY` and all six `FIREBASE_CONFIG` fields.
- **Map area is blank/grey, console shows an auth error**: your Maps API
  key is missing, unbilled, or its website restriction doesn't match
  your actual GitHub Pages domain exactly (check for a trailing `/*`).
- **"Still waiting for the location list to load"**: Firestore rules
  weren't published (step 3), or `FIREBASE_CONFIG` has a typo.
- **Import button does nothing / "Import failed"**: open the browser
  console for the real error; most often this is a Firestore rules
  issue (step 3) or the site not being served from the repo root (so
  `data/branches.json` 404s).
 
