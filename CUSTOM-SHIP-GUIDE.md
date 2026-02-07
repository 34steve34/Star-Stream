# Custom Ship Sprite Guide

## Changes Made

### 1. ✅ New Rotation Controls
- **Upper-left screen** = Clockwise (CW) rotation
- **Lower-left screen** = Counter-clockwise (CCW) rotation
- **Right side** = Fire bullets (unchanged)

No more double-tap! Just tap the area that matches the direction you want to spin.

### 2. ✅ PNG Ship Support Added
The game now supports using a custom PNG image for your ship instead of the vector drawing.

## How to Use a Custom Ship Image

### Step 1: Prepare Your Ship Image

**Requirements:**
- **Format:** PNG with transparent background (recommended)
- **Size:** 60x60 pixels is ideal (can be larger, will auto-scale)
- **Orientation:** Ship should point RIGHT (→) in the image
- **File name:** Name it `ship.png` (or whatever you prefer)

**Design Tips:**
- Keep it simple and recognizable
- Use bright colors (white, cyan, green work well against black space)
- Make sure the "front" of the ship points to the right
- Transparent background looks best

### Step 2: Upload to GitHub

1. Go to your repository: `https://github.com/YOUR-USERNAME/starstream`
2. Click **"Add file"** → **"Upload files"**
3. Upload your `ship.png` file
4. Commit the changes

### Step 3: Enable in Code

Open `index.html` and find this section (around line 327):

```javascript
startBtn.addEventListener("click", async () => {
    if (typeof DeviceMotionEvent !== 'undefined' && typeof DeviceMotionEvent.requestPermission === 'function') {
        try { await DeviceMotionEvent.requestPermission(); } catch(e) {}
    }
    
    // OPTIONAL: Uncomment these lines to use a custom ship PNG
    // Make sure to upload your ship image file to the same directory
    /*
    shipImage = new Image();
    shipImage.src = './ship.png'; // Replace with your ship image filename
    */
    
    startLevel(1);
});
```

**Uncomment and modify like this:**

```javascript
startBtn.addEventListener("click", async () => {
    if (typeof DeviceMotionEvent !== 'undefined' && typeof DeviceMotionEvent.requestPermission === 'function') {
        try { await DeviceMotionEvent.requestPermission(); } catch(e) {}
    }
    
    // Load custom ship sprite
    shipImage = new Image();
    shipImage.src = './ship.png'; // Your ship image filename
    
    startLevel(1);
});
```

### Step 4: Test

1. Commit and push changes
2. Wait for GitHub Pages to update (~1 minute)
3. Reload the game on your phone
4. Your custom ship should appear!

## Example Ship Images

Here are some ideas for ship designs:

### Classic Triangle (Current Default)
```
    /\
   /  \
  /    \
 /      \
|--------|  ← Points right
 \      /
  \    /
   \  /
    \/
```

### Sleek Spacecraft
- Streamlined body
- Pointed nose on right
- Fins/wings on sides
- Engine glow on left

### Retro Style
- Pixelated ship sprite
- Bright neon colors
- Simple geometric shapes

## Troubleshooting

### Ship doesn't appear
- Check console for errors (F12 → Console)
- Verify image file uploaded to repository root
- Make sure filename in code matches uploaded file exactly
- Check image loaded: Add `shipImage.onload = () => console.log('Ship loaded!');`

### Ship is too big/small
Change the size in the drawing code. Find this line in `index.html`:

```javascript
let w = shipImage.width || 60;
let h = shipImage.height || 60;
```

Change to scale:
```javascript
let w = (shipImage.width || 60) * 0.5; // 50% smaller
let h = (shipImage.height || 60) * 0.5;
```

### Ship points wrong direction
Your image needs to point RIGHT (→). If your ship PNG points up, you need to either:
1. Rotate the image file before uploading, OR
2. Add rotation offset in code:
   ```javascript
   ctx.rotate(ship.angle - Math.PI/2); // Adjusts 90° for upward-pointing sprite
   ```

## Reverting to Vector Ship

To go back to the default vector ship:
1. Comment out the shipImage lines again (add `//` or `/* */`)
2. Or just delete your ship.png file from the repository

The game automatically falls back to vector rendering if no image is loaded.

## Advanced: Animated Ship

Want your ship to have engine glow or animation? You can use a sprite sheet:

```javascript
// Load sprite sheet
shipImage = new Image();
shipImage.src = './ship-sprite.png';

// In draw function, use different frame based on game state
let frame = Math.floor(Date.now() / 100) % 4; // 4 frames
let frameWidth = 60;
ctx.drawImage(shipImage, 
    frame * frameWidth, 0, frameWidth, 60,  // Source
    -30, -30, 60, 60                        // Destination
);
```

---

## Summary of Controls

**Rotation:**
- Upper-left corner = Spin clockwise
- Lower-left corner = Spin counter-clockwise

**Movement:**
- Tilt device left/right/forward/back

**Fire:**
- Tap right side of screen

**Ship Sprite:**
- Default: Vector drawing (white triangle)
- Optional: Upload PNG and uncomment code to use custom sprite

Enjoy your improved controls! 🚀
