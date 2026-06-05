# Sardisan Map

Interactive game map with click-to-add markers, shared persistence via Firebase Realtime Database, and GitHub Pages hosting.

## Setup

### 1. Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com) and create a new project (free Spark plan is fine).
2. In the left sidebar: **Build → Realtime Database → Create database**.
3. Choose a region. Start in **test mode** (allows public read/write — tighten later).
4. Go to **Project Settings** (gear icon) → **Your apps** → click the `</>` Web icon → register the app.
5. Copy the `firebaseConfig` object shown.

### 2. Paste your config into `index.html`

Open `index.html` and find the `FIREBASE_CONFIG` block near the top of the `<script type="module">` section. Replace all `REPLACE_WITH_*` values with your copied config values.

```js
const FIREBASE_CONFIG = {
  apiKey:            "AIza...",
  authDomain:        "your-project.firebaseapp.com",
  databaseURL:       "https://your-project-default-rtdb.firebaseio.com",
  projectId:         "your-project",
  storageBucket:     "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123:web:abc123"
};
```

### 3. Enable GitHub Pages

In this repo: **Settings → Pages → Source: Deploy from a branch → main / root → Save**.

Your map will be live at `https://sardisanmap.github.io/<repo-name>/`.

### 4. Push the files

```bash
git init
git add index.html README.md
git commit -m "Initial map"
git remote add origin https://github.com/SardisanMap/<repo-name>.git
git push -u origin main
```

## Usage

- **View mode** (default): Click any marker to see its popup. Use the panel to search or filter by category.
- **+ Add mode**: Click the button, then click anywhere on the map to place a marker. The color is automatically set by the category you choose.
- **Hide**: Markers are never permanently deleted — hiding sets `hidden: true` in Firebase. You can restore them from the Firebase console by setting `hidden: false`.
- **Export JSON**: Downloads all current visible markers as `markers.json` (useful for backup or seeding a new DB).
- **Import JSON**: Upload a `markers.json` to bulk-add markers to Firebase.

## Categories & Colors

| Category | Color |
|---|---|
| Town / Settlement | Purple `#9b59b6` |
| Resource | Green `#27ae60` |
| Creature / Mob | Red `#e74c3c` |
| Point of Interest | Orange `#e67e22` |
| Dungeon / Cave | Gray `#95a5a6` |
| Structure / Building | Blue `#2980b9` |
| Waypoint | Teal `#1abc9c` |
| Other | Dark Gray `#7f8c8d` |

## Firebase Rules (recommended after testing)

Once you're done testing, replace the Realtime Database rules with something like:

```json
{
  "rules": {
    "markers": {
      ".read": true,
      ".write": true
    }
  }
}
```

Or add authentication if you want to restrict who can add/hide markers.
