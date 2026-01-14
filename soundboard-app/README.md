# 🎵 Humorous Soundboard App

A playful web-based soundboard that plays humorous sound effects when buttons are clicked. Features a responsive grid layout, cartoonish design, and works on both desktop and mobile devices.

## Features

- **9 Built-in Sounds**: Fart, Burp, Knuckle Pop, Neck Crunch, Back Creak, Head Bonk, Sproing, Cough, Sneeze
- **Responsive Design**: 3-4 columns on desktop, 1-2 columns on mobile
- **Playful UI**: Gradient background, emoji icons, smooth animations
- **Keyboard Accessible**: Tab navigation, Enter/Space to activate buttons
- **Easy to Extend**: Add new sounds with just 3 simple steps

## Quick Start

### Option 1: Open Directly in Browser

Simply double-click `soundboard.html` to open in your default browser.

**Note**: If sounds don't play in Chrome, use Option 2 below (Chrome blocks local file audio due to CORS).

### Option 2: Use a Local Server (Recommended)

**Python 3**:
```bash
python -m http.server 8000
```

**Python 2**:
```bash
python -m SimpleHTTPServer 8000
```

**Node.js**:
```bash
npx http-server -p 8000
```

Then open: `http://localhost:8000/soundboard.html`

## Adding New Sounds

Follow these 3 simple steps:

### Step 1: Add MP3 File
Place your sound file in the `sounds/` directory:
```
sounds/hiccup.mp3
```

### Step 2: Update the Array
Open `soundboard.html` and add ONE LINE to the `sounds` array:
```javascript
{ id: 'hiccup', label: 'Hiccup', icon: '🫧', file: 'sounds/hiccup.mp3' }
```

### Step 3: Refresh
Reload the page in your browser - your new button will appear automatically!

## File Structure

```
soundboard-app/
├── soundboard.html          (5.8 KB - all code in one file!)
├── README.md               (this file)
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

## Getting Sound Files

The placeholder MP3 files need to be replaced with actual sound effects. You can find royalty-free sounds at:

- **Freesound.org** - https://freesound.org/
- **Zapsplat.com** - https://www.zapsplat.com/
- **SoundBible.com** - http://soundbible.com/

Search for: "fart sound effect", "burp sound", "knuckle crack", etc.

## Browser Compatibility

- ✅ Chrome 51+
- ✅ Firefox 54+
- ✅ Safari 10+
- ✅ Edge 15+

All modern browsers from 2017+ are fully supported.

## Technical Details

- **No build process** - runs directly in the browser
- **No dependencies** - pure vanilla JavaScript, HTML5, CSS3
- **Single file** - all code in one HTML file (<50KB)
- **Responsive** - CSS Grid with media queries
- **Accessible** - keyboard navigation support
- **HTML5 Audio API** - for sound playback

## Deployment

### GitHub Pages
1. Create a GitHub repository
2. Upload the `soundboard-app/` directory
3. Enable GitHub Pages in repository settings
4. Access at: `https://username.github.io/repo-name/soundboard.html`

### Netlify
1. Drag and drop the `soundboard-app/` folder to netlify.com
2. Your soundboard will be live instantly!

### Any Web Host
Simply upload the `soundboard-app/` directory via FTP/SFTP.

## License

This project was created as part of the SpecKit workflow demonstration.

## Credits

Built with:
- HTML5 Audio API
- CSS Grid Layout
- Vanilla JavaScript (ES6+)
- Unicode Emoji Icons
