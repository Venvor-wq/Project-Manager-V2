# Project Organizer (PyQt6 + WebEngine)

A clean, offline **desktop launcher** to organize **After Effects** and **coding projects** (plus Video/3D/Design).  
Built with **PyQt6 WebEngine** as host + a modern **HTML/CSS/JS** UI with **GSAP** animations and a subtle **Three.js** background.

---

## ✨ Features

### Projects
- Add projects via **folder picker** (and best-effort Drag & Drop in Qt WebEngine)
- **Auto-detect project type**
  - After Effects: `.aep` / `.aepx` → picks newest as **main file**
  - Coding: `.git`, `package.json`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `build.gradle`, `CMakeLists.txt`, …
  - Video / 3D / Design (basic detection) or fallback: Other
- **Search** across title, tags, notes, path and type
- **Filters** by type + status
- **Grid / List** view toggle
- Detail panel:
  - Edit title
  - Change type + status
  - Tags (chips)
  - Notes
- Quick Actions:
  - Open folder
  - Open main file (or folder)
  - Copy path
  - Delete project

### Ideas
- Built-in **Ideas / Notes** tab
- Search + edit + delete
- Ctrl+Enter to save (optional)

### Settings
- Themes:
  - Dark (default)
  - Light
  - Purple Dark
- Backup Sync:
  - Select a backup folder
  - On startup: projects can be mirrored to that folder
  - “Run Sync Now” from settings

### UI / Visuals
- **GSAP** micro-interactions (staggered list loads, panel transitions, toasts)
- **Three.js** subtle background particles + wireframe orb (low-power)

---

## 🧱 Tech Stack

- **Python 3**
- **PyQt6**
- **PyQt6-WebEngine**
- Frontend: **HTML/CSS/JS**, **GSAP**, **Three.js**
- Storage: **SQLite** (`./data/projects.db`)
- Settings: JSON (`./data/settings.json`)

---

## ✅ Requirements

- Python **3.10+** recommended
- Windows / macOS / Linux (opening files uses OS-specific methods)

Install dependencies:

```bash
pip install PyQt6 PyQt6-WebEngine

🚀 Run

Make sure these files are in the same folder:

    Launcher.py

    Launcher.html

Start the app:

python Launcher.py

📁 Data / Files Created

On first run, a data/ folder will be created next to the script:

    data/projects.db → SQLite database (projects + ideas)

    data/settings.json → theme, view, filters, backup settings

    data/backup_*.json → optional export (if used)

🔍 Project Type Detection (Overview)

Detection priority:

    AE → finds .aep/.aepx (newest becomes main_file)

    Coding → detects .git or common build markers

    Video → common video/project extensions

    3D → .blend/.fbx/.obj/.c4d/...

    Design → .psd/.ai/.fig/.sketch/...

    Other

Max scan depth: MAX_SCAN_DEPTH = 4 (can be adjusted in Launcher.py)
🛠️ Backup Sync (How it works)

If you choose a backup folder in Settings → Backup Sync, the app can mirror each project folder into:

<backupRoot>/<projectTitle>_<hash>/

    Only changed files are copied (size/mtime comparison)

    Extra files in backup are removed (mirror behavior)

    The app avoids recursion (won’t back up if backup folder is inside the project)

    Tip: Put the backup folder on an external drive or cloud-synced directory if you want off-device redundancy.

🧩 Customize
Add more coding markers / file types

Edit these in Launcher.py:

    CODING_MARKERS

    VIDEO_EXTS

    THREE_D_EXTS

    DESIGN_EXTS

Adjust scan performance

    MAX_SCAN_DEPTH

🐞 Notes / Known Limitations

    Drag & Drop folder paths can be limited by Qt WebEngine depending on OS/permissions. The Add Folder button is always reliable.

    Three.js background is intentionally subtle and runs in low-power mode.

📜 License

Choose a license for your repo (MIT is a solid default).
Add a LICENSE file if you want it to be explicitly open-source.
📸 Screenshots

(Add screenshots/gifs here)

    Projects grid

    Detail panel

    Ideas tab

    Theme switching

🙌 Credits

    GSAP: GreenSock Animation Platform

    Three.js: 3D WebGL library

    PyQt6 WebEngine: Chromium-based embedded browser for desktop apps
