# STAR STREAM - Offline PWA Installation Guide

## Files Included
- `index.html` - Main game file (modified with PWA support)
- `manifest.json` - PWA manifest for app installation
- `sw.js` - Service worker for offline functionality
- `STARSTREAM-192.png` - App icon (192x192)
- `STARSTREAM0512.png` - App icon (512x512)

## Installation Methods

### Method 1: Simple File Access (Easiest)
1. Place all files in the same folder on your device
2. Open `index.html` directly in your mobile browser
3. The game will work immediately

### Method 2: Install as App (Recommended)
For full offline capabilities and app-like experience:

#### On Android (Chrome/Edge):
1. Host the files on a local web server OR use a file manager app that supports HTTP server
2. Open the game in Chrome browser
3. Tap the menu (⋮) and select "Install app" or "Add to Home Screen"
4. The game will install as a standalone app
5. Once installed, it works completely offline

#### On iOS (Safari):
1. Open `index.html` in Safari
2. Tap the Share button (square with arrow)
3. Scroll and tap "Add to Home Screen"
4. Name it "STAR STREAM" and tap "Add"
5. Launch from your home screen

### Method 3: Local Web Server (For Full PWA Features)
If you want the complete PWA experience with service worker caching:

#### Using Python (if installed):
```bash
# Navigate to the game folder
cd /path/to/starstream

# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

#### Using Node.js (if installed):
```bash
# Install http-server globally
npm install -g http-server

# Navigate to game folder and run
cd /path/to/starstream
http-server -p 8000
```

Then open `http://localhost:8000` in your browser.

## Troubleshooting

### Permission Issues
**Problem**: DeviceMotionEvent permission errors on iOS
**Solution**: The game will automatically request permissions when you tap "INITIATE TRIAL". Make sure to allow motion/orientation access.

### Service Worker Not Registering
**Problem**: Console shows "ServiceWorker registration failed"
**Solution**: Service workers require either:
- HTTPS connection (secure)
- localhost/127.0.0.1 (development)
- File:// protocol won't work for service workers, but the game itself will still function

### Game Won't Load Offline
**Problem**: Previously visited but won't load without internet
**Solution**: 
1. Clear browser cache
2. Reload the page while online once
3. The service worker will cache everything
4. After that, it works completely offline

### Icons Not Showing
**Problem**: App icon doesn't appear after installation
**Solution**: Ensure all PNG files are in the same directory as index.html

## How to Play
1. Hold device in **landscape mode**
2. **Left side of screen**: Tap to rotate ship (double-tap to reverse rotation)
3. **Right side of screen**: Tap to fire
4. **Tilt device**: Control ship drift (movement)
5. Stay close to the green target circle
6. Shoot the orange threat when it appears (3 hits to destroy)
7. Don't let the threat fully expand or you'll die
8. Score 150+ to advance to next level

## Technical Notes
- Game is completely self-contained (no external dependencies)
- Works 100% offline after first load (if using service worker)
- All game logic runs in browser JavaScript
- Uses HTML5 Canvas for rendering
- Requires devicemotion API for tilt controls
- Optimized for mobile landscape gameplay

## File Structure
```
starstream/
├── index.html              (Main game)
├── manifest.json          (PWA configuration)
├── sw.js                  (Service worker)
├── STARSTREAM-192.png     (Icon)
└── STARSTREAM0512.png     (Icon)
```

All files must be in the same directory!

## Browser Compatibility
- ✅ Chrome/Edge (Android) - Full support
- ✅ Safari (iOS) - Full support with motion permissions
- ✅ Firefox (Android) - Full support
- ⚠️ Desktop browsers - Works but tilt controls won't function (keyboard controls not implemented)

## Updates
To update the game:
1. Replace the files with new versions
2. Update the `CACHE_NAME` in `sw.js` (e.g., 'starstream-v2')
3. Clear browser cache or uninstall/reinstall the app

---

**Version**: 44.8
**Type**: Progressive Web App (PWA)
**Platform**: Mobile (Landscape)
**Offline**: Yes (with service worker)
