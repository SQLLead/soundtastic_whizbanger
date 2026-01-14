# Quickstart Guide: Humorous Soundboard App

**Feature**: 001-soundboard-app
**Date**: 2026-01-11
**Purpose**: Step-by-step guide to build and deploy the soundboard application

## Prerequisites

- Text editor (VS Code, Sublime Text, Notepad++, or any editor)
- Web browser (Chrome, Firefox, Safari, or Edge)
- Basic HTML/CSS/JavaScript knowledge (helpful but not required)
- 9 MP3 sound effect files (or use temporary placeholder sounds)

**Time Estimate**: 30-60 minutes for complete implementation

---

## Step 1: Create Project Structure

Create a new directory and add the required files:

```bash
mkdir soundboard-app
cd soundboard-app
mkdir sounds
```

**Directory Structure**:
```
soundboard-app/
├── soundboard.html    (create in Step 2)
└── sounds/
    ├── fart.mp3
    ├── burp.mp3
    ├── knuckle-crack.mp3
    ├── neck-crunch.mp3
    ├── back-creak.mp3
    ├── head-bonk.mp3
    ├── sproing.mp3
    ├── cough.mp3
    └── sneeze.mp3
```

---

## Step 2: Create HTML File

Create `soundboard.html` with this basic structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Humorous Soundboard</title>
  <style>
    /* CSS will go here (Step 4) */
  </style>
</head>
<body>
  <div class="container">
    <h1>🎵 Humorous Soundboard</h1>
    <div id="soundboard" class="grid">
      <!-- Buttons will be generated here by JavaScript -->
    </div>
  </div>

  <script>
    // JavaScript will go here (Step 3)
  </script>
</body>
</html>
```

---

## Step 3: Add JavaScript (Sound Logic)

Replace the `<script>` section with this code:

```javascript
<script>
  // Define all sounds (add new sounds here!)
  const sounds = [
    { id: 'fart', label: 'Fart', icon: '💨', file: 'sounds/fart.mp3' },
    { id: 'burp', label: 'Burp', icon: '🤢', file: 'sounds/burp.mp3' },
    { id: 'knuckle-crack', label: 'Knuckle Pop', icon: '👊', file: 'sounds/knuckle-crack.mp3' },
    { id: 'neck-crunch', label: 'Neck Crunch', icon: '🦴', file: 'sounds/neck-crunch.mp3' },
    { id: 'back-creak', label: 'Back Creak', icon: '🧘', file: 'sounds/back-creak.mp3' },
    { id: 'head-bonk', label: 'Head Bonk', icon: '🤕', file: 'sounds/head-bonk.mp3' },
    { id: 'sproing', label: 'Sproing', icon: '🎯', file: 'sounds/sproing.mp3' },
    { id: 'cough', label: 'Cough', icon: '😷', file: 'sounds/cough.mp3' },
    { id: 'sneeze', label: 'Sneeze', icon: '🤧', file: 'sounds/sneeze.mp3' }
  ];

  // Function to play a sound
  function playSound(soundFile) {
    const audio = new Audio(soundFile);
    audio.play().catch(err => {
      console.error('Error playing sound:', err);
    });
  }

  // Generate buttons when page loads
  document.addEventListener('DOMContentLoaded', () => {
    const soundboard = document.getElementById('soundboard');

    sounds.forEach(sound => {
      // Create button element
      const button = document.createElement('button');
      button.id = `btn-${sound.id}`;
      button.className = 'sound-button';
      button.setAttribute('data-sound-id', sound.id);
      button.setAttribute('aria-label', `Play ${sound.label} sound`);

      // Create icon and label spans
      button.innerHTML = `
        <span class="icon">${sound.icon}</span>
        <span class="label">${sound.label}</span>
      `;

      // Add click event listener
      button.addEventListener('click', () => playSound(sound.file));

      // Add keyboard support (Enter and Space keys)
      button.addEventListener('keydown', (e) => {
        if (e.key === 'Enter' || e.key === ' ') {
          e.preventDefault();
          playSound(sound.file);
        }
      });

      // Add button to grid
      soundboard.appendChild(button);
    });
  });
</script>
```

---

## Step 4: Add CSS (Visual Styling)

Replace the `<style>` section with this code:

```css
<style>
  /* Reset and base styles */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Comic Sans MS', 'Chalkboard SE', 'Comic Neue', cursive, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  .container {
    max-width: 800px;
    width: 100%;
  }

  h1 {
    text-align: center;
    color: white;
    font-size: 2.5rem;
    margin-bottom: 30px;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  }

  /* Grid layout for buttons */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
    padding: 20px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    backdrop-filter: blur(10px);
  }

  /* Button styles */
  .sound-button {
    background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
    border: none;
    border-radius: 15px;
    padding: 20px;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    min-height: 120px;
    transition: all 0.2s ease;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    color: white;
    font-size: 1rem;
    font-weight: bold;
  }

  .sound-button:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 12px rgba(0,0,0,0.2);
    background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
  }

  .sound-button:active {
    transform: translateY(0);
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }

  .sound-button:focus {
    outline: 3px solid #fff;
    outline-offset: 2px;
  }

  .sound-button .icon {
    font-size: 3rem;
    line-height: 1;
  }

  .sound-button .label {
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  /* Mobile responsive (1-2 columns) */
  @media (max-width: 767px) {
    .grid {
      grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
      gap: 10px;
      padding: 15px;
    }

    .sound-button {
      min-height: 100px;
      padding: 15px;
    }

    .sound-button .icon {
      font-size: 2.5rem;
    }

    .sound-button .label {
      font-size: 0.8rem;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 20px;
    }
  }

  /* Very small screens (single column) */
  @media (max-width: 320px) {
    .grid {
      grid-template-columns: 1fr;
    }
  }
</style>
```

---

## Step 5: Add Sound Files

Place 9 MP3 files in the `sounds/` directory with these exact filenames:

- `fart.mp3`
- `burp.mp3`
- `knuckle-crack.mp3`
- `neck-crunch.mp3`
- `back-creak.mp3`
- `head-bonk.mp3`
- `sproing.mp3`
- `cough.mp3`
- `sneeze.mp3`

**Where to find sounds**:
- **Free sound libraries**: Freesound.org, Zapsplat.com, SoundBible.com
- **Search terms**: "fart sound effect", "burp sound", "knuckle crack", etc.
- **License**: Use royalty-free or Creative Commons sounds
- **Format**: Download as MP3 (or convert WAV to MP3 using online tools)

**Temporary Testing**:
If you don't have sounds yet, you can test with any MP3 file by duplicating it with different names, or use this online placeholder: `https://www.soundjay.com/button/beep-07.mp3` (change `file` paths temporarily)

---

## Step 6: Test the Application

### Local Testing (Simple Method)

1. Open `soundboard.html` directly in your browser (double-click the file)

**Note**: Some browsers (Chrome) may block audio loading from `file://` due to CORS restrictions. If sounds don't play, use the server method below.

### Local Testing (Server Method - Recommended)

**Option A: Python** (if installed):
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

Then open: `http://localhost:8000/soundboard.html`

**Option B: Node.js** (if installed):
```bash
npx http-server -p 8000
```

Then open: `http://localhost:8000/soundboard.html`

**Option C: VS Code Extension**:
- Install "Live Server" extension
- Right-click `soundboard.html` → "Open with Live Server"

### Testing Checklist

- [ ] Page loads without errors (check browser console F12)
- [ ] 9 buttons appear in a grid layout
- [ ] Each button shows an emoji icon and text label
- [ ] Clicking each button plays the correct sound
- [ ] Buttons show hover effect when mouse over
- [ ] Buttons show active/pressed effect when clicked
- [ ] Keyboard navigation works (Tab to button, Enter/Space to play)
- [ ] Layout is responsive (resize browser window to test)
- [ ] Works on mobile device (or browser dev tools mobile view)

---

## Step 7: Deploy (Optional)

### Option 1: GitHub Pages (Free)

1. Create GitHub repository
2. Upload `soundboard.html` and `sounds/` folder
3. Go to Settings → Pages
4. Select branch and folder
5. Your soundboard will be live at: `https://username.github.io/repo-name/soundboard.html`

### Option 2: Netlify (Free)

1. Sign up at netlify.com
2. Drag and drop your project folder
3. Your soundboard will be live instantly at a Netlify URL

### Option 3: Vercel (Free)

1. Sign up at vercel.com
2. Import your project from GitHub or upload directly
3. Your soundboard will be deployed automatically

### Option 4: Self-Hosted

Upload `soundboard.html` and `sounds/` folder to any web host via FTP/SFTP.

---

## Adding New Sounds (3-Step Process)

Per FR-012 and SC-006, adding a new sound is simple:

### Step 1: Add MP3 File
Place your new MP3 file in the `sounds/` directory, e.g., `sounds/hiccup.mp3`

### Step 2: Update Array
Open `soundboard.html` and find the `sounds` array. Add one line:

```javascript
const sounds = [
  { id: 'fart', label: 'Fart', icon: '💨', file: 'sounds/fart.mp3' },
  { id: 'burp', label: 'Burp', icon: '🤢', file: 'sounds/burp.mp3' },
  // ... existing sounds ...
  { id: 'hiccup', label: 'Hiccup', icon: '🫧', file: 'sounds/hiccup.mp3' } // NEW!
];
```

### Step 3: Refresh Page
Reload the page in your browser - the new button appears automatically!

**Tips**:
- Choose a unique `id` (kebab-case)
- Keep `label` short (under 20 characters)
- Pick an emoji that represents the sound
- Make sure `file` path is correct

---

## Troubleshooting

### Sounds Don't Play

**Problem**: Clicking buttons does nothing or shows an error

**Solutions**:
1. Check browser console (F12) for error messages
2. Verify MP3 files exist in `sounds/` directory
3. Check file names match exactly (case-sensitive on some servers)
4. Use local server instead of opening file directly (CORS issue)
5. Check browser autoplay policy (sounds should play after first click)

### Layout Looks Broken

**Problem**: Buttons not in grid or overlapping

**Solutions**:
1. Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R)
2. Check that all CSS is inside `<style>` tags
3. Verify no typos in class names (`sound-button`, `grid`, etc.)
4. Test in different browser (rule out browser-specific issue)

### Buttons Don't Appear

**Problem**: Page loads but no buttons show

**Solutions**:
1. Check browser console for JavaScript errors
2. Verify `sounds` array is defined before DOMContentLoaded
3. Ensure `<div id="soundboard">` exists in HTML
4. Check that JavaScript is inside `<script>` tags

### File Size Too Large

**Problem**: HTML file is over 50KB (SC-007)

**Solutions**:
1. Remove extra comments and whitespace (minify)
2. Shorten variable names if needed
3. Reduce CSS (remove unused styles)
4. The provided code should be well under 50KB (~10-15KB)

---

## Customization Ideas

### Change Colors
Edit the `background` gradients in CSS:
```css
body {
  background: linear-gradient(135deg, #your-color-1 0%, #your-color-2 100%);
}
```

### Change Font
Replace `Comic Sans MS` with your preferred font:
```css
body {
  font-family: 'Arial', sans-serif;
}
```

### Add Page Title/Description
Add text above the soundboard:
```html
<div class="container">
  <h1>🎵 Humorous Soundboard</h1>
  <p style="text-align:center; color:white; margin-bottom:20px;">
    Click buttons to play funny sounds!
  </p>
  <div id="soundboard" class="grid">
```

### Add More Sounds
Follow the 3-step process in "Adding New Sounds" section above.

---

## Success Validation

Verify your implementation meets all success criteria:

- **SC-001**: ✅ Users can load and play sounds within 2 seconds
- **SC-002**: ✅ Works on desktop (1024px-1920px) - test by resizing browser
- **SC-003**: ✅ Works on mobile (320px-768px) - test with device or dev tools
- **SC-004**: ✅ All 9 sounds play correctly
- **SC-005**: ✅ Buttons respond within 100ms with visual feedback
- **SC-006**: ✅ New sounds added via 3-step process
- **SC-007**: ✅ File size under 50KB (check file properties)
- **SC-008**: ✅ 90% of users can use without instructions (buttons are self-explanatory)
- **SC-009**: ✅ Layout reflows smoothly when resized

---

## Next Steps

1. **Share it**: Send the link to friends and family
2. **Customize it**: Add your own sounds and styling
3. **Extend it**: Add features like volume control, keyboard shortcuts, or sound categories
4. **Learn from it**: Study the code to understand HTML5 Audio API, CSS Grid, and DOM manipulation

---

## Resources

**Documentation**:
- [HTML5 Audio API - MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement)
- [CSS Grid - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [JavaScript Events - MDN](https://developer.mozilla.org/en-US/docs/Web/Events)

**Sound Libraries**:
- [Freesound.org](https://freesound.org/) - Community sound library
- [Zapsplat.com](https://www.zapsplat.com/) - Free sound effects
- [SoundBible.com](http://soundbible.com/) - Royalty-free sounds

**Emoji Reference**:
- [Emojipedia](https://emojipedia.org/) - Find emoji for your sounds

**Deployment**:
- [GitHub Pages Guide](https://pages.github.com/)
- [Netlify Docs](https://docs.netlify.com/)
- [Vercel Docs](https://vercel.com/docs)

---

## Support

If you encounter issues:
1. Check the Troubleshooting section above
2. Review browser console errors (F12)
3. Verify all files and code match this guide exactly
4. Test in a different browser to isolate the issue

Happy soundboarding! 🎵
