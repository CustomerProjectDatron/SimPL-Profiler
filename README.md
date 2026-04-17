# Profiler Viewer

A zero-dependency, single-file HTML profiler viewer that runs entirely in the browser.
Load any JSON profiling trace by drag & drop or file picker — no server, no install required.

## Features

| Tab | Description |
|---|---|
| **⬡ Baum** (Tree) | Collapsible call tree with time bars, self-time overlay and call-count badges. Lazy DOM rendering handles 50 MB+ files smoothly. |
| **⬥ Hotspots** | Aggregated method list, sortable by total time, self time or call count. Shows average time per call. |
| **🔥 Flame Graph** | Canvas-based flame graph. Click any block to zoom in; use *Back* / *Reset* to navigate. Hover for tooltip. |
| **↩ Bottom-up** | Every method listed with its callers. Searchable and sortable. |

## JSON format

The viewer expects an array (or a single object) at the root. Each node:

```json
{
  "name": "MyNamespace::MyMethod",
  "totalMs": 123.456,
  "selfMs": 12.34,
  "callCount": 5,
  "children": [ /* recursive */ ]
}
```

| Field | Type | Description |
|---|---|---|
| `name` | string | Display name; use `Namespace::Method` for colour grouping |
| `totalMs` | number | Inclusive (wall-clock) time in milliseconds |
| `selfMs` | number | Exclusive time (totalMs minus all children) |
| `callCount` | number | Number of invocations |
| `children` | array | Nested call nodes (optional) |

## 🚀 Deploy to GitHub Pages

### 1 — Create a new GitHub repository

Go to <https://github.com/new> and create an **empty public** repository
(no README, no .gitignore).

### 2 — Push the files

```bash
cd C:\Repos\profiler-viewer

git init
git add index.html README.md
git commit -m "chore: initial release"

# Replace USERNAME and REPO with your values
git remote add origin https://github.com/USERNAME/REPO.git
git branch -M main
git push -u origin main
```

### 3 — Enable GitHub Pages

1. Open the repository on GitHub.
2. **Settings → Pages** (left sidebar).
3. Under *Build and deployment* choose **Deploy from a branch**.
4. Branch: `main` / Folder: `/ (root)` → **Save**.

After ~30 seconds the site is live at:

```
https://USERNAME.github.io/REPO/
```

---

## Local usage

Just open `index.html` in any modern browser — no build step, no server needed.

```bash
start index.html      # Windows
open  index.html      # macOS
xdg-open index.html   # Linux
```

## Performance notes

* JSON parsing runs in a **Web Worker** so the UI never freezes.
* Tree nodes are built **lazily** — only expanded nodes get DOM elements.
* Tested with files up to 50 MB / 100 000 nodes.

## License

MIT
