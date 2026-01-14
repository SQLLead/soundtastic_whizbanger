# Research: Humorous Soundboard App

**Feature**: 001-soundboard-app
**Date**: 2026-01-11
**Purpose**: Technical research and decisions for single-file HTML soundboard implementation

## Technical Decisions

### Decision 1: HTML5 Audio API

**Decision**: Use HTML5 `<audio>` elements with JavaScript Audio API for sound playback

**Rationale**:
- Native browser support across all modern browsers (Chrome 4+, Firefox 3.5+, Safari 3.1+, Edge all versions)
- No external dependencies required (meets FR-008)
- Simple API: `new Audio(src)` and `.play()` method
- Supports MP3 format universally
- Handles preloading and buffering automatically
- Accessible via JavaScript event listeners

**Alternatives Considered**:
- **Web Audio API**: More powerful but overly complex for simple playback. Adds unnecessary code weight for basic sound effects.
- **`<audio>` tags in HTML**: Would require 9 audio elements in markup, less clean than dynamic creation. Chosen approach allows programmatic control.
- **Howler.js library**: Excellent cross-browser audio library but violates FR-008 (no external dependencies)

**Implementation Notes**:
- Create Audio objects dynamically: `const audio = new Audio('sounds/fart.mp3')`
- Use `.play()` to trigger playback
- Handle autoplay restrictions by initializing AudioContext on first user interaction
- Allow overlapping sounds (don't stop previous sound when new one starts)

---

### Decision 2: CSS Grid for Responsive Layout

**Decision**: Use CSS Grid Layout with media queries for responsive button grid

**Rationale**:
- Native CSS feature, no framework needed (meets FR-008)
- Perfect for 2D grid layouts with automatic wrapping
- Simple responsive breakpoints via media queries
- Excellent browser support (Chrome 57+, Firefox 52+, Safari 10.1+, Edge 16+)
- Handles dynamic content (can add buttons without layout changes)

**Alternatives Considered**:
- **Flexbox**: Good for 1D layouts but Grid is more suited for 2D grid of buttons. Flexbox would require more CSS to achieve same result.
- **Float-based layout**: Legacy approach, more CSS required, harder to maintain
- **Bootstrap/Tailwind**: Violates FR-008 (no external dependencies)

**Implementation Notes**:
- Desktop (≥768px): `grid-template-columns: repeat(auto-fit, minmax(150px, 1fr))` for 3-4 columns
- Mobile (<768px): `grid-template-columns: repeat(auto-fit, minmax(120px, 1fr))` for 1-2 columns
- Gap between buttons: `gap: 1rem`
- Auto-fit ensures responsive behavior without hardcoded column counts

---

### Decision 3: Emoji Icons

**Decision**: Use Unicode emoji characters for button icons (💨, 🤢, 💥, etc.)

**Rationale**:
- No external icon files needed (reduces complexity, meets FR-008)
- Universal support across all devices and browsers
- Playful and immediately recognizable
- Accessible (screen readers can interpret emoji)
- Zero file size impact (text characters)
- Matches "playful, cartoonish" design requirement (FR-013)

**Alternatives Considered**:
- **SVG icons**: Would require inline SVG code or external files. Adds complexity and file size.
- **Icon fonts (Font Awesome)**: Violates FR-008 (external dependency)
- **Image files (PNG/GIF)**: Requires 9 additional files, breaks "single HTML file" constraint (FR-007)

**Icon Mapping**:
- Fart: 💨 (dash symbol / wind)
- Burp: 🤢 (nauseated face)
- Knuckle Crack: 👊 (fisted hand)
- Neck Crunch: 🦴 (bone)
- Back Creak: 🧘 (person in lotus position)
- Head Bonk: 🤕 (face with head-bandage)
- Sproing: 🎯 or 🎪 (circus tent / playful)
- Cough: 😷 (face with medical mask)
- Sneeze: 🤧 (sneezing face)

---

### Decision 4: Vanilla JavaScript (ES6+)

**Decision**: Use modern vanilla JavaScript (ES6+) with no frameworks or build tools

**Rationale**:
- Meets FR-007 and FR-008 (single file, no dependencies)
- ES6 features (arrow functions, template literals, const/let) reduce code verbosity
- Array.map() for generating buttons from data structure
- Event delegation for efficient button handling
- All modern browsers support ES6 (Chrome 51+, Firefox 54+, Safari 10+, Edge 15+)

**Alternatives Considered**:
- **jQuery**: Unnecessary for simple DOM manipulation. Violates FR-008.
- **React/Vue**: Massive overkill for 9 buttons. Violates FR-007 and FR-008.
- **TypeScript**: Would require compilation step, can't be single HTML file

**Implementation Pattern**:
```javascript
const sounds = [
  { id: 'fart', label: 'Fart', icon: '💨', file: 'sounds/fart.mp3' },
  // ... more sounds
];

sounds.forEach(sound => {
  const button = document.createElement('button');
  button.innerHTML = `<span class="icon">${sound.icon}</span><span class="label">${sound.label}</span>`;
  button.onclick = () => new Audio(sound.file).play();
  container.appendChild(button);
});
```

---

### Decision 5: MP3 Audio Format

**Decision**: Use MP3 format for all sound files (44.1kHz, 128kbps stereo)

**Rationale**:
- Universal browser support (all browsers support MP3)
- Good compression ratio (small file sizes for 1-5 second clips)
- Widely available sound effect libraries use MP3
- Balances quality and file size (128kbps is sufficient for comedic sound effects)

**Alternatives Considered**:
- **WAV**: Uncompressed, much larger files (10x+ size). Unnecessary quality for humorous effects.
- **OGG Vorbis**: Better compression but not supported in Safari/iOS
- **AAC/M4A**: Good quality but inconsistent browser support
- **Multiple formats (MP3 + OGG fallback)**: Overcomplicated for this use case given universal MP3 support

**File Naming Convention**:
- Lowercase, hyphenated: `fart.mp3`, `knuckle-crack.mp3`, `neck-crunch.mp3`
- Stored in `/sounds/` subdirectory relative to HTML file
- Keep file sizes under 100KB each (typically 30-50KB for 2-3 second clips)

---

### Decision 6: CSS-in-HTML via `<style>` Tag

**Decision**: Embed all CSS within `<style>` tag in HTML `<head>`

**Rationale**:
- Meets FR-007 requirement (single HTML file)
- Cleaner separation than inline styles
- Allows use of media queries, pseudo-classes, animations
- Standard practice for single-file HTML applications
- Better readability and maintainability than inline styles

**Alternatives Considered**:
- **Inline styles**: Would clutter HTML, can't use media queries or pseudo-classes
- **External CSS file**: Violates FR-007 (must be single file)

**CSS Organization**:
- CSS reset/normalization (minimal)
- Layout styles (grid, container)
- Button styles (base, hover, active states)
- Media queries (mobile breakpoints)
- Animation/transition styles

---

### Decision 7: No Build Process

**Decision**: Write code that runs directly in browser without compilation or bundling

**Rationale**:
- Meets FR-007 and FR-008 (single file, no dependencies)
- Users can open file directly in browser (file:// protocol)
- Easy to deploy (just upload HTML + sounds folder)
- Simplifies development (no npm, webpack, babel, etc.)
- Meets SC-006 (easy to add new sounds by editing array)

**Alternatives Considered**:
- **Webpack/Parcel bundler**: Would allow modern tooling but requires build step, violates requirements
- **Minification**: Could reduce file size but adds complexity for minimal gain (target is <50KB which is easily achievable)

**Deployment Options**:
- Local: Open `soundboard.html` in browser (requires local web server for Chrome due to CORS on file://)
- Static hosting: Upload to any web host (GitHub Pages, Netlify, Vercel, S3)
- No server-side processing required

---

## Best Practices

### HTML5 Audio Best Practices
- Preload audio on page load: `audio.preload = 'auto'`
- Handle audio loading errors gracefully
- Respect user's browser autoplay policies
- Consider mobile data usage (9 sounds × 50KB = ~450KB total)

### Accessibility Best Practices
- Use semantic `<button>` elements (not `<div>` with onclick)
- Include proper ARIA labels if needed
- Ensure keyboard navigation (Tab key)
- Support Enter and Space key to activate buttons
- Sufficient color contrast (WCAG AA minimum)
- Touch target minimum 44×44px (FR-014)

### Performance Best Practices
- Lazy-load audio on first play instead of preloading all 9 files
- Use CSS animations (GPU accelerated) not JavaScript animations
- Minimize DOM manipulation (create buttons once on load)
- Debounce rapid clicks if needed (optional)

### Code Organization Best Practices
- Sounds array at top of `<script>` for easy editing (meets SC-006)
- Comments explaining extensibility
- Consistent naming conventions
- Separate concerns: HTML structure, CSS styling, JS behavior

---

## Technology Summary

| Component | Technology | Reason |
|-----------|-----------|---------|
| Audio Playback | HTML5 Audio API | Native, no dependencies, universal support |
| Layout | CSS Grid | Perfect for 2D responsive grids |
| Icons | Unicode Emoji | No external files, playful aesthetic |
| Scripting | Vanilla JS (ES6+) | No dependencies, modern syntax |
| Audio Format | MP3 (128kbps) | Universal support, good compression |
| Styling | Embedded CSS | Single-file requirement |
| Build | None | Direct browser execution |

---

## Open Questions & Decisions

**Q: Should sounds overlap or stop previous sound?**
**A**: Allow overlapping (funnier for rapid clicking, simpler code)

**Q: How to handle missing sound files?**
**A**: Log error to console, show visual error state on button (optional enhancement)

**Q: Preload all sounds or load on demand?**
**A**: Load on first click (reduces initial load time, acceptable delay for comedic timing)

**Q: Support keyboard shortcuts (e.g., number keys 1-9)?**
**A**: Not in MVP (P1), could add as enhancement if users request it

**Q: Volume controls?**
**A**: Not in MVP (users can use system volume), could add global volume slider as enhancement

---

## Risk Assessment

**Low Risk**:
- HTML5 Audio API support (mature, stable API)
- CSS Grid browser support (widely supported)
- Single-file deployment (simple, proven approach)

**Medium Risk**:
- Browser autoplay policies (mitigated: user must click button first)
- Sound file sourcing (assumption: user will provide or source files)

**No Risk**:
- No backend, database, or server requirements
- No user data, privacy, or security concerns
- No third-party dependencies to break or update
