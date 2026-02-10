# Project Hub V2

A local-first desktop launcher to catalog and manage **After Effects** and **development projects** in one searchable workspace.  
Runs as a **PyQt6 WebEngine** app (Python backend + HTML UI) with **GSAP** motion and a subtle **Three.js** ambient layer.

## Highlights

- Folder-based project library with fast search and filtering
- Automatic project type detection (AE / Coding / Video / 3D / Design / Other)
- Project details panel (title, type, status, tags, notes)
- Quick actions (open folder, open main file, copy path, delete)
- Ideas tab for standalone notes/concepts
- Theme system (Dark / Light / Purple Dark)
- Optional backup sync to a user-selected folder

## Setup

### Requirements
- Python 3.10+ recommended

### Install
```bash
pip install PyQt6 PyQt6-WebEngine
````

## Run

Ensure both files are in the same directory:

* `Launcher.py`
* `Launcher.html`

Start:

```bash
python Launcher.py
```

## How it works

### Storage

Project Hub V2 stores everything locally in `./data/`:

* `data/projects.db` — SQLite database (projects + ideas)
* `data/settings.json` — theme, view, filters, backup settings
* Optional JSON exports (if used)

### Project type detection

During folder import the backend scans up to `MAX_SCAN_DEPTH` and assigns a type with this priority:

1. **AE** — `.aep` / `.aepx` (newest becomes `main_file`)
2. **Coding** — `.git` or common build markers (`package.json`, `pyproject.toml`, `requirements.txt`, `pom.xml`, `build.gradle`, `CMakeLists.txt`, …)
3. **Video** — common media/project markers
4. **3D** — `.blend`, `.fbx`, `.obj`, `.c4d`, …
5. **Design** — `.psd`, `.ai`, `.fig`, `.sketch`, …
6. **Other**

You can adjust markers and scan depth in `Launcher.py`.

### Backup Sync

If a backup folder is configured, Project Hub V2 can mirror each project folder into:

```
<backupRoot>/<projectTitle>_<hash>/
```

Behavior:

* Copies changed files (size/mtime comparison)
* Deletes files in the backup that no longer exist in the source (mirror)
* Prevents recursion if the backup folder is inside a project directory

## Platform notes

Opening files/folders uses native OS handlers:

* Windows: `os.startfile`
* macOS: `open`
* Linux: `xdg-open`

Drag & drop folder paths can be limited by Qt WebEngine depending on OS; the folder picker is the recommended method.

## License

Add a `LICENSE` file (e.g., MIT) if you plan to redistribute the project.

```
```
