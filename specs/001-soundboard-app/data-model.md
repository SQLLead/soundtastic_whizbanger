# Data Model: Humorous Soundboard App

**Feature**: 001-soundboard-app
**Date**: 2026-01-11
**Purpose**: Define data structures and relationships for soundboard application

## Overview

This soundboard application uses a simple, client-side data model with no backend storage or persistence. All data is defined in JavaScript arrays and objects within the single HTML file.

## Entities

### Sound Definition

Represents a single sound effect button in the soundboard.

**Attributes**:
- `id` (string, required): Unique identifier for the sound (lowercase, hyphenated)
  - Used for: DOM element IDs, tracking, debugging
  - Format: `^[a-z]+(-[a-z]+)*$`
  - Examples: `fart`, `knuckle-crack`, `neck-crunch`

- `label` (string, required): Human-readable name displayed on button
  - Used for: Button text, accessibility labels
  - Length: 3-20 characters
  - Examples: `"Fart"`, `"Burp"`, `"Knuckle Pop"`

- `icon` (string, required): Emoji character representing the sound
  - Used for: Visual button decoration
  - Format: Single Unicode emoji character
  - Examples: `"💨"`, `"🤢"`, `"👊"`

- `file` (string, required): Relative path to MP3 audio file
  - Used for: Audio source URL
  - Format: `sounds/{filename}.mp3`
  - Examples: `"sounds/fart.mp3"`, `"sounds/burp.mp3"`

**Type Definition** (TypeScript-style for clarity):
```typescript
interface SoundDefinition {
  id: string;           // Unique identifier (kebab-case)
  label: string;        // Display name
  icon: string;         // Emoji character
  file: string;         // Path to audio file
}
```

**JavaScript Implementation**:
```javascript
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
```

**Validation Rules**:
- All fields are required (no optional fields)
- `id` must be unique within the sounds array
- `id` must match filename (without .mp3 extension) for consistency
- `icon` should be a single emoji (not text or multiple characters)
- `file` path must point to existing MP3 file in sounds/ directory

**Relationships**:
- One-to-one: Each Sound Definition → One MP3 file
- One-to-one: Each Sound Definition → One button element (created dynamically)

---

### Audio Instance (Runtime)

Represents an HTML5 Audio object created at runtime when a sound is played.

**Attributes**:
- `src` (string): URL/path to the audio file
- `preload` (string): Preload strategy (`'none'`, `'metadata'`, `'auto'`)
- `currentTime` (number): Current playback position in seconds
- `duration` (number): Total audio duration in seconds (readonly)
- `paused` (boolean): Whether audio is currently paused (readonly)
- `volume` (number): Volume level (0.0 to 1.0)

**Methods**:
- `play()`: Start or resume playback (returns Promise)
- `pause()`: Pause playback
- `load()`: Reload the audio file

**Lifecycle**:
1. Created when button is clicked: `new Audio(soundDef.file)`
2. Played immediately: `audio.play()`
3. Garbage collected after playback completes (no references kept)

**Note**: Audio instances are ephemeral - created on-demand and not stored. This allows overlapping playback of the same sound.

---

### Button Element (DOM)

Represents the interactive button element in the DOM for each sound.

**Attributes**:
- `id` (attribute): Matches sound ID (e.g., `id="btn-fart"`)
- `class` (attribute): `"sound-button"` for styling
- `data-sound-id` (attribute): Reference to sound definition ID
- `aria-label` (attribute): Accessibility label (e.g., `"Play Fart sound"`)

**Structure**:
```html
<button id="btn-fart" class="sound-button" data-sound-id="fart" aria-label="Play Fart sound">
  <span class="icon">💨</span>
  <span class="label">Fart</span>
</button>
```

**Events**:
- `click`: Plays the associated sound
- `keydown` (Enter/Space): Plays the associated sound

**State** (CSS classes):
- `.sound-button`: Base state
- `.sound-button:hover`: Hover state
- `.sound-button:active`: Pressed state
- `.sound-button:focus`: Keyboard focus state
- `.sound-button.error`: Error state (if sound file fails to load)

---

## Data Relationships

```
Sound Definition (JavaScript Object)
    ↓ references
MP3 File (File System)

Sound Definition (JavaScript Object)
    ↓ generates
Button Element (DOM)
    ↓ creates on click
Audio Instance (Runtime)
    ↓ loads
MP3 File (File System)
```

**Key Points**:
- Sound Definitions are the source of truth
- Button elements are generated from Sound Definitions
- Audio instances are created transiently, not cached
- MP3 files are external assets referenced by path

---

## Data Flow

### Page Load
1. HTML parsed, `sounds` array defined in `<script>` tag
2. DOM ready event fires
3. For each sound in `sounds` array:
   - Create button element
   - Set icon and label from sound definition
   - Attach click event listener
   - Append to grid container

### Button Click
1. User clicks button (or presses Enter/Space)
2. Event handler retrieves sound definition via `data-sound-id`
3. Create new `Audio` instance with sound file path
4. Call `.play()` on audio instance
5. Audio loads and plays (browser handles buffering)
6. Add visual feedback (CSS `:active` state)
7. Audio completes, instance garbage collected

### Adding New Sound (Manual Edit)
1. Developer adds MP3 file to `sounds/` directory
2. Developer adds new object to `sounds` array:
   ```javascript
   { id: 'new-sound', label: 'New Sound', icon: '🔊', file: 'sounds/new-sound.mp3' }
   ```
3. Page refresh
4. New button automatically appears (generated from updated array)

---

## Storage Strategy

**Client-Side Only**:
- No database, no server, no persistence
- All data defined in JavaScript source code
- Sound files stored as static assets in `/sounds/` directory

**No State Management**:
- No need to track "played" sounds or usage statistics
- No user preferences or settings to persist
- Stateless application (each page load is fresh start)

**Advantages**:
- Simple deployment (static files only)
- No backend infrastructure required
- Fast load times (no API calls or database queries)
- Easy to understand and modify

**Limitations**:
- Cannot track user behavior or analytics (could add analytics library if needed)
- No personalization or favorites (acceptable for this use case)
- Sound collection is hard-coded (intentional per requirements)

---

## Extensibility

### Adding New Sounds

**Process** (per FR-012):
1. Add MP3 file to `sounds/` directory
2. Add entry to `sounds` array (1 line of code)
3. Refresh page

**Example**:
```javascript
// Add this line to the sounds array:
{ id: 'hiccup', label: 'Hiccup', icon: '🫧', file: 'sounds/hiccup.mp3' }
```

**No code changes needed**:
- Button rendering loop handles new entry automatically
- Grid layout adapts to additional buttons
- Event handling works without modification

### Removing Sounds

**Process**:
1. Remove entry from `sounds` array
2. (Optional) Delete MP3 file from `sounds/` directory
3. Refresh page

### Modifying Sounds

**Process**:
1. Replace MP3 file in `sounds/` directory (keep same filename)
2. No code changes needed

OR

1. Update `sounds` array entry (change label, icon, or file path)
2. Refresh page

---

## Schema Validation (Optional Enhancement)

While not implemented in MVP, the data structure could be validated:

```javascript
function validateSound(sound) {
  if (!sound.id || typeof sound.id !== 'string') return false;
  if (!sound.label || typeof sound.label !== 'string') return false;
  if (!sound.icon || typeof sound.icon !== 'string') return false;
  if (!sound.file || typeof sound.file !== 'string') return false;
  if (!sound.file.endsWith('.mp3')) return false;
  return true;
}

// Check for duplicate IDs
const ids = sounds.map(s => s.id);
const hasDuplicates = ids.length !== new Set(ids).size;
if (hasDuplicates) console.error('Duplicate sound IDs found!');
```

---

## Summary

The data model is intentionally minimal:
- **1 primary entity**: Sound Definition (JavaScript object)
- **2 derived entities**: Button Element (DOM), Audio Instance (runtime)
- **0 persistent storage**: All data in source code
- **Simple relationships**: One-to-one mappings

This simplicity aligns with:
- FR-007: Single HTML file (no external data files)
- FR-008: No external dependencies (no state management library)
- FR-012: Easy extensibility (add one line to array)
- SC-006: 3-step process to add sounds (file, array, refresh)
