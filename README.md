````md
# Project Organizer

Desktop project launcher for managing **After Effects** and **development projects** in one searchable library.  
UI is rendered via **PyQt6 WebEngine** (local HTML) with **GSAP** animations and a subtle **Three.js** background.

## Features

### Projects
- Add projects by selecting a folder
- Automatic type detection:
  - After Effects: `.aep` / `.aepx` (newest file becomes `main_file`)
  - Coding: `.git`, `package.json`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `build.gradle`, `CMakeLists.txt`, …
  - Video / 3D / Design (basic detection), fallback to `Other`
- Fast search across title, tags, notes, path, type
- Filters (type + status)
- Grid/List view
- Detail panel: edit title, type, status, tags, notes
- Quick actions: open folder, open project (main file), copy path, delete

### Ideas
- Separate Ideas tab for notes/concepts
- Create, edit, search, delete

### Settings
- Themes: Dark / Light / Purple Dark
- Optional backup sync (mirror projects into a backup folder)

## Requirements

- Python 3.10+ recommended
- Dependencies:
  - `PyQt6`
  - `PyQt6-WebEngine`

Install:

```bash
pip install PyQt6 PyQt6-WebEngine
````

## Run

Make sure these files are in the same directory:

* `Launcher.py`
* `Launcher.html`

Start:

```bash
python Launcher.py
```

## Data Storage

All data is stored locally in `./data/`:

* `data/projects.db` — SQLite (projects + ideas)
* `data/settings.json` — UI/theme/view/filters + backup folder
* Optional JSON exports (if used)

## Backup Sync

If a backup folder is configured in Settings, the app can mirror each project folder into:

```
<backupRoot>/<projectTitle>_<hash>/
```

Behavior:

* Copies only changed files (size/mtime comparison)
* Removes files/folders in backup that no longer exist in the source (mirror)
* Prevents recursion if the backup folder is inside a project directory

## Configuration

Detection and scan behavior can be adjusted in `Launcher.py`:

* `MAX_SCAN_DEPTH` — folder scan depth (default: 4)
* Marker sets:

  * `CODING_MARKERS`
  * `VIDEO_EXTS`
  * `THREE_D_EXTS`
  * `DESIGN_EXTS`

## Platform Notes

Opening folders/files:

* Windows: `os.startfile`
* macOS: `open`
* Linux: `xdg-open`

Drag & drop folder paths can be limited by Qt WebEngine depending on OS; the folder picker is the reliable method.

## License
/
