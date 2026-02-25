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
- **Perspective flatten** — straighten photos taken at an angle using homography-based perspective correction
- **Save All** — download every photo at once

## How to Use

### On a Computer (Easiest)

1. Open `index.html` directly in Chrome, Firefox, or Edge
2. No server needed — just double-click the file

### On iPhone / iPad

iPhones can't open local HTML files directly. You need to serve the app over HTTP using **one** of these options:

**Option A: GitHub Pages (recommended — no computer needed after setup)**

1. Push this folder to a GitHub repository
2. Go to **Settings > Pages** and set Source to your main branch
3. Your app will be live at `https://yourusername.github.io/TeacherPhoto/`
4. Open that URL in Safari on your iPhone
5. Tap the Share button > **Add to Home Screen** to install as an app

**Option B: Serve from your computer (quick for testing)**

1. On your Mac/PC, open Terminal and navigate to this folder
2. Run: `python3 -m http.server 8000`
3. Find your computer's local IP (e.g., `192.168.1.100`)
4. On your iPhone, open Safari and go to `http://192.168.1.100:8000`
5. Both devices must be on the same Wi-Fi network

**Option C: Drag-and-drop hosting**

1. Go to [Netlify Drop](https://app.netlify.com/drop) in any browser
2. Drag the entire `TeacherPhoto` folder onto the page
3. You'll get a public URL — open it on your iPhone

### Using the App

1. Tap **Take Photo** to snap a picture, or **Upload Photos** to pick from your gallery
2. Each photo opens in the editor with AI auto-crop running automatically
3. Tap **Accept** to keep the suggested crop, **Adjust** to tweak it, or **Skip** to leave as-is
4. Name the photo, rotate if needed, then swipe to the next one
5. Use **Flatten** to straighten photos taken at an angle
6. Back in the gallery, tap **Auto Crop All** to batch-process remaining photos
7. When done, tap **Save All**
8. On iPhone, if Save doesn't download directly, the image will open — long-press it and tap **Save Image**

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
