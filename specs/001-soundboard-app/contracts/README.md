# Soundboard Contracts

**Feature**: 001-soundboard-app
**Date**: 2026-01-11
**Purpose**: Define data contracts and interfaces for the soundboard application

## Overview

This directory contains JSON Schema definitions that specify the structure and validation rules for data used in the soundboard application. While the app doesn't use JSON APIs (it's client-side only), these schemas document the expected format of the JavaScript data structures.

## Schemas

### sound-definition.schema.json

Defines the structure of a single sound effect definition.

**Purpose**: Validates individual sound objects in the `sounds` array

**Fields**:
- `id` (required, string): Unique identifier (kebab-case, 2-30 chars)
- `label` (required, string): Display name (3-20 chars)
- `icon` (required, string): Emoji character (1-4 chars for multi-byte emoji)
- `file` (required, string): Path to MP3 file matching pattern `sounds/*.mp3`

**Usage Example**:
```javascript
const sound = {
  id: 'fart',
  label: 'Fart',
  icon: '💨',
  file: 'sounds/fart.mp3'
};
```

**Validation Rules**:
- `id` must be lowercase letters with optional hyphens
- `id` should match the filename (without .mp3 extension)
- `file` path must start with `sounds/` and end with `.mp3`
- No additional properties allowed

---

### sounds-array.schema.json

Defines the structure of the complete sounds collection.

**Purpose**: Validates the entire `sounds` array in the JavaScript code

**Constraints**:
- Must be an array
- Minimum 1 sound, maximum 100 sounds
- All items must conform to sound-definition.schema.json
- All items must be unique (no duplicate sound definitions)

**Usage Example**:
```javascript
const sounds = [
  { id: 'fart', label: 'Fart', icon: '💨', file: 'sounds/fart.mp3' },
  { id: 'burp', label: 'Burp', icon: '🤢', file: 'sounds/burp.mp3' },
  { id: 'knuckle-crack', label: 'Knuckle Pop', icon: '👊', file: 'sounds/knuckle-crack.mp3' },
  // ... more sounds
];
```

---

## Validation (Optional)

These schemas are documentation/contracts only. The application doesn't validate at runtime (to keep file size small and avoid dependencies). However, you could validate during development:

### Using AJV (Node.js)

```bash
npm install ajv ajv-cli
ajv validate -s contracts/sounds-array.schema.json -d sounds-data.json
```

### Using Online Validator

1. Go to https://www.jsonschemavalidator.net/
2. Paste schema from `sounds-array.schema.json`
3. Paste your sounds array (as JSON)
4. Verify validation passes

---

## DOM Interface Contract

While not expressed as JSON Schema, the DOM interface follows this contract:

### Button Element Structure

```html
<button
  id="btn-{sound.id}"
  class="sound-button"
  data-sound-id="{sound.id}"
  aria-label="Play {sound.label} sound">
  <span class="icon">{sound.icon}</span>
  <span class="label">{sound.label}</span>
</button>
```

**Attributes**:
- `id`: Prefixed with `btn-` + sound ID
- `class`: Always `sound-button` (for CSS styling)
- `data-sound-id`: Reference to sound definition ID (for event handling)
- `aria-label`: Accessibility label for screen readers

**Child Elements**:
- `.icon` span: Contains emoji character
- `.label` span: Contains display text

**Events**:
- `click`: Triggers sound playback
- `keydown` (Enter/Space): Triggers sound playback

---

## CSS Class Contract

Buttons use these CSS classes:

```css
.sound-button          /* Base button styles */
.sound-button:hover    /* Mouse hover state */
.sound-button:active   /* Button pressed state */
.sound-button:focus    /* Keyboard focus state */
.sound-button .icon    /* Icon span styles */
.sound-button .label   /* Label span styles */
```

Optional error state (not in MVP):
```css
.sound-button.error    /* Error state (sound file failed to load) */
```

---

## File System Contract

**Directory Structure**:
```
soundboard.html          (root HTML file)
sounds/
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

**Audio File Requirements**:
- Format: MP3 (MPEG-1 Audio Layer 3)
- Bitrate: 128 kbps recommended (balance of quality and file size)
- Sample Rate: 44.1 kHz (CD quality)
- Channels: Stereo or mono
- Duration: 1-5 seconds typical (no hard limit)
- File size: <100KB per file recommended
- Naming: Lowercase, hyphenated, matching sound.id + `.mp3`

---

## Extensibility Contract

To add a new sound (per FR-012 and SC-006):

1. **Add MP3 file**: Place `new-sound.mp3` in `sounds/` directory
2. **Update array**: Add one line to `sounds` array in `<script>` section:
   ```javascript
   { id: 'new-sound', label: 'New Sound', icon: '🔊', file: 'sounds/new-sound.mp3' }
   ```
3. **Refresh page**: Reload browser to see new button

**Guarantees**:
- New button automatically appears in grid
- Grid layout adapts to additional button
- Click event handling works without modification
- No other code changes required

**Validation Checklist**:
- [ ] `id` is unique (not used by existing sounds)
- [ ] `id` matches filename (without .mp3)
- [ ] `id` is kebab-case (lowercase, hyphens only)
- [ ] `label` is descriptive and under 20 characters
- [ ] `icon` is a single emoji character
- [ ] `file` path is correct: `sounds/{id}.mp3`
- [ ] MP3 file exists at specified path
- [ ] Sound plays correctly when button clicked

---

## Backward Compatibility

These schemas define version 1.0 of the data contract. Future changes:

**Backward Compatible** (patch/minor version):
- Adding optional fields to Sound Definition
- Increasing maxItems limit on sounds array
- Relaxing pattern constraints

**Breaking Changes** (major version):
- Renaming required fields
- Changing field types
- Making optional fields required
- Changing file path structure

For this simple app, breaking changes are acceptable (users just update their HTML file). However, if this were used as a library or API, semantic versioning would apply.

---

## Summary

These contracts ensure:
- ✅ **Clarity** (Principle III): Explicit data structure specification
- ✅ **Simplicity** (FR-012): Adding sounds is a 3-step process
- ✅ **Validation**: Schemas enable optional validation during development
- ✅ **Documentation**: Clear reference for data format and constraints
- ✅ **Extensibility**: Well-defined interface for adding sounds
