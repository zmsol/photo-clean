# strip-c2pa

Strip C2PA Content Credentials and AI provenance metadata from images — locally, no uploads.

## What it does

Removes C2PA/JUMBF manifests, EXIF, XMP, IPTC, and AI generator tags (`digitalSourceType`, `trainedAlgorithmicMedia`, etc.) from JPG, PNG, WebP, HEIC, AVIF, and TIFF files using [exiftool](https://exiftool.org/).

## What's in this repo

| File | Purpose |
|------|---------|
| `strip-c2pa` | Command-line backend. Strips and verifies single files or whole directories. |
| `strip-c2pa-gui` | Drag-and-drop Tkinter GUI. Add files/folders, click **RUN**, watch progress in the log panel. |
| `strip-c2pa-gui.desktop` | Linux desktop shortcut (start menu entry). |

## Requirements

- Python 3
- [exiftool](https://exiftool.org/) — `sudo apt install libimage-exiftool-perl` (Debian/Ubuntu)

## Quick start

### GUI (recommended)

```bash
python3 strip-c2pa-gui
```

Or use the start menu shortcut `Strip C2PA Metadata` (install the `.desktop` file first).

1. Click **Add Files…** or **Add Folder…**
2. Choose options: Aggressive strip, In-place, Verify after
3. Click **▶ RUN — Strip C2PA Metadata**
4. Cleaned images land in `~/Downloads/strip-c2pa-out/` (unless in-place)

### CLI

```bash
# Single file
./strip-c2pa image.jpg
# → image_clean.jpg in the same folder

# Custom output
./strip-c2pa image.jpg -o clean.jpg

# Whole directory, recursive
./strip-c2pa -r ./assets/

# Strip ALL metadata (not just C2PA/AI)
./strip-c2pa --aggressive image.jpg

# Verify only, no changes
./strip-c2pa --verify-only image.jpg

# Overwrite original (creates .bak)
./strip-c2pa --in-place image.jpg
```

## GUI options

- **Aggressive** — strip *all* metadata, not just C2PA/AI tags
- **In-place** — overwrite originals (creates `.bak` backups)
- **Verify after** — re-scan output with exiftool to confirm no C2PA/AI metadata remains (recommended, on by default)

## Install the desktop shortcut

```bash
cp strip-c2pa-gui.desktop ~/.local/share/applications/
update-desktop-database ~/.local/share/applications/
```

Then launch "Strip C2PA Metadata" from your start menu.

## License

MIT. Privacy tool — runs locally, no data leaves your machine.
