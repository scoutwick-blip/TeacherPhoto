# Teacher Photo Editor

A mobile-first photo editor built for teachers who photograph student art projects in class. Snap, name, auto-crop, and save 30+ photos in one session.

## Features

- **Mobile-first** — designed for phones, works on tablets and desktops too
- **Installable PWA** — add to your home screen for an app-like experience
- **Camera integration** — "Take Photo" button opens your phone camera directly
- **Batch upload** — upload many photos at once from your gallery
- **AI auto-crop** — detects project edges using Gaussian blur, Sobel edge detection, adaptive thresholding, and connected component analysis
- **Batch Auto Crop All** — one-tap to auto-crop every uncropped photo with a progress bar
- **Accept / Adjust / Skip** — choose to accept the auto-crop, fine-tune it manually, or skip
- **Manual crop** — draw and drag a crop area with corner handles and rule-of-thirds grid
- **Rotate** — 90-degree left/right rotation
- **Undo / Reset** — revert any photo back to its original state
- **Name photos** — give each photo a name (used as the filename on save)
- **Swipe navigation** — swipe left/right to move between photos in the editor
- **Gallery view** — see all photos at a glance with cached thumbnails
- **Long-press select** — long-press in the gallery to select multiple photos for batch delete or save
- **Delete confirmation** — prevents accidental deletion
- **Save feedback** — toast notifications confirm saves and actions
- **Save All** — download every photo at once

## How to Use

1. Open `index.html` in any mobile browser (or desktop)
2. Tap **Add to Home Screen** in your browser menu to install as an app
3. Tap **Take Photo** to snap a picture, or **Upload Photos** to pick from your gallery
4. Each photo opens in the editor with AI auto-crop running automatically
5. Tap **Accept** to keep the suggested crop, **Adjust** to tweak it, or **Skip** to leave as-is
6. Name the photo, rotate if needed, then swipe to the next one
7. Back in the gallery, tap **Auto Crop All** to batch-process remaining photos
8. When done, tap **Save All**

No installation, server, or internet connection required.

## AI Auto-Crop Algorithm

The auto-crop uses pure client-side image processing (no external APIs):

1. Downsamples the image for speed
2. Converts to grayscale and applies Gaussian blur to reduce noise
3. Runs Sobel edge detection to find strong boundaries
4. Samples a wide border band to estimate the background color
5. Builds a foreground mask combining color distance (adaptive threshold) + edge strength
6. Applies morphological close/open operations to clean noise
7. Runs connected component analysis to isolate the largest foreground region
8. Returns the bounding box with padding as the suggested crop
