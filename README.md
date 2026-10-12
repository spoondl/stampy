# Timeprint

A static, browser-based photo timestamp app. It adds retro digital-camera date stamps to new JPEG copies and supports batch export.

## Features
- Retro styles: Classic LCD, Red LED, Camcorder, Warm Film, Minimal, Green LCD
- EXIF capture date detection, preferring `DateTimeOriginal`
- Manual date/time override for the currently selected photo
- Multiple photo upload, queue, per-photo preview, batch ZIP export
- HEIC/HEIF conversion in-browser (via `heic2any`)
- Best-effort EXIF preservation for JPEG inputs (via `piexifjs`); EXIF Orientation is normalized to 1 because canvas output has already applied image orientation
- Local browser processing; photos are not uploaded to a server

## Run locally
Open `index.html` in a modern browser. The libraries load from jsDelivr, so an internet connection is required. For best HEIC compatibility, use a current desktop browser.

## Deploy
### Netlify Drop
1. Extract `timeprint-app.zip`.
2. Go to https://app.netlify.com/drop.
3. Drag the extracted `timeprint-app` folder onto the page.
4. Use the URL Netlify provides.

### GitHub Pages
Upload `index.html` to a repository, then go to **Settings → Pages** and deploy from the `main` branch root.

## Metadata notes
- The app reads EXIF from original JPEGs before conversion.
- Canvas export creates a new JPEG and does not naturally retain metadata. If enabled, Timeprint attempts to copy the original JPEG's EXIF block into the exported JPEG with `piexifjs`, and normalizes the Orientation tag to `1`.
- EXIF copying is best-effort. Proprietary MakerNotes, embedded thumbnails, uncommon tags, or unusual camera metadata may be missing or not remain valid. For non-JPEG input (including HEIC/HEIF), original EXIF is not currently reinserted into the exported JPEG.
- If a file has no EXIF capture date, no timestamp is guessed. Enter a manual date/time override for the selected photo before exporting.
- EXIF can include GPS coordinates and camera serial information. If you don't want those details in your output, uncheck **Preserve original EXIF metadata**.
- The timestamp uses the camera's recorded local date/time; timezone is not inferred unless you manually account for it.
