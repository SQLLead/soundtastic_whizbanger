# Tasks: Humorous Soundboard App

**Input**: Design documents from `specs/001-soundboard-app/`
**Prerequisites**: plan.md (required), spec.md (required), research.md, data-model.md, contracts/

**Tests**: Not requested in specification - manual browser testing will be used per plan.md

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Single project**: Single HTML file at repository root + sounds/ directory
- This project uses: `soundboard-app/soundboard.html` and `soundboard-app/sounds/`

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic file structure

- [x] T001 Create project directory soundboard-app/ in repository root
- [x] T002 Create sounds/ subdirectory inside soundboard-app/
- [x] T003 Create initial soundboard.html file in soundboard-app/

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core HTML structure and sounds data that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [x] T004 Add HTML5 doctype, head section with meta tags, and title in soundboard-app/soundboard.html
- [x] T005 Add body structure with container div and soundboard grid div in soundboard-app/soundboard.html
- [x] T006 Add empty style tag in head section of soundboard-app/soundboard.html
- [x] T007 Add empty script tag before closing body tag in soundboard-app/soundboard.html
- [x] T008 Define sounds array with all 9 sound definitions in script section of soundboard-app/soundboard.html

**Checkpoint**: Foundation ready - HTML scaffold complete, sounds data defined, user story implementation can now begin

---

## Phase 3: User Story 1 - Play Sound Effects (Priority: P1) 🎯 MVP

**Goal**: Users can click buttons to instantly play humorous sound effects

**Independent Test**: Load soundboard.html in browser, click any button, verify corresponding sound plays through speakers/headphones

### Implementation for User Story 1

- [x] T009 [US1] Implement playSound() function using HTML5 Audio API in script section of soundboard-app/soundboard.html
- [x] T010 [US1] Implement button generation loop that creates button elements from sounds array in script section of soundboard-app/soundboard.html
- [x] T011 [US1] Attach click event listeners to generated buttons to trigger sound playback in script section of soundboard-app/soundboard.html
- [x] T012 [US1] Attach keyboard event listeners (Enter/Space) for accessibility in script section of soundboard-app/soundboard.html
- [x] T013 [US1] Add basic button styling with cartoonish colors and icon/label layout in style section of soundboard-app/soundboard.html
- [x] T014 [US1] Add hover and active states for visual feedback in style section of soundboard-app/soundboard.html
- [x] T015 [US1] Add focus styles for keyboard navigation in style section of soundboard-app/soundboard.html
- [x] T016 [US1] Obtain or create 9 MP3 sound files and place in soundboard-app/sounds/ directory

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently - all 9 buttons play sounds when clicked

---

## Phase 4: User Story 2 - Responsive Grid Layout (Priority: P2)

**Goal**: Buttons arranged in responsive grid that adapts to different screen sizes

**Independent Test**: Open app on desktop (verify 3-4 columns), resize to mobile width (verify 1-2 columns), test on actual mobile device

### Implementation for User Story 2

- [x] T017 [US2] Add CSS Grid layout to .grid container for desktop (3-4 columns) in style section of soundboard-app/soundboard.html
- [x] T018 [US2] Add media query for tablet/mobile (<768px) with adjusted grid columns in style section of soundboard-app/soundboard.html
- [x] T019 [US2] Add media query for very small screens (<320px) with single column layout in style section of soundboard-app/soundboard.html
- [x] T020 [US2] Ensure minimum 44x44px touch target size on mobile in style section of soundboard-app/soundboard.html
- [x] T021 [US2] Add responsive typography (icon and label sizes) for different screen sizes in style section of soundboard-app/soundboard.html

**Checkpoint**: At this point, User Stories 1 AND 2 should both work - sounds play AND layout is responsive across devices

---

## Phase 5: User Story 3 - Add New Sounds (Priority: P3)

**Goal**: Developers can easily add new sound effects via simple 3-step process

**Independent Test**: Add new MP3 file to sounds/ directory, add one line to sounds array, refresh page, verify new button appears and plays

### Implementation for User Story 3

- [x] T022 [US3] Add code comments above sounds array explaining how to add new sounds in soundboard-app/soundboard.html
- [x] T023 [US3] Validate that adding a 10th sound works correctly (test extensibility)
- [x] T024 [US3] Document the 3-step process in inline HTML comments within soundboard-app/soundboard.html

**Checkpoint**: All user stories should now be independently functional - sounds play, layout is responsive, and adding sounds is documented

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories and final validation

- [x] T025 [P] Add playful gradient background and styling enhancements in style section of soundboard-app/soundboard.html
- [x] T026 [P] Add page title and heading with emoji in soundboard-app/soundboard.html
- [x] T027 [P] Optimize CSS for file size (verify <50KB total per SC-007)
- [x] T028 Test soundboard.html in Chrome browser (verify all sounds play, layout responsive)
- [x] T029 Test soundboard.html in Firefox browser (verify all sounds play, layout responsive)
- [x] T030 Test soundboard.html in Safari browser (verify all sounds play, layout responsive)
- [x] T031 Test soundboard.html in Edge browser (verify all sounds play, layout responsive)
- [x] T032 Test on mobile device or browser dev tools mobile view (verify touch targets, 1-2 column grid)
- [x] T033 Validate all success criteria SC-001 through SC-009 are met

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3-5)**: All depend on Foundational phase completion
  - User Story 1 (P1): Can start after Foundational - No dependencies on other stories
  - User Story 2 (P2): Can start after Foundational - No dependencies on other stories (but P1 must exist to see layout)
  - User Story 3 (P3): Can start after Foundational - No dependencies on other stories
- **Polish (Phase 6)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - Enhances US1 but doesn't depend on it
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - No dependencies on other stories

### Within Each User Story

**User Story 1**:
1. T009 (playSound function) must complete first
2. T010 (button generation) must complete second
3. T011-T012 (event listeners) depend on T010
4. T013-T015 (styling) can run in parallel with T009-T012 after T007 (style tag creation)
5. T016 (sound files) can run in parallel with all other tasks

**User Story 2**:
- All tasks (T017-T021) work on the same style section, so must run sequentially
- However, US2 can run in parallel with other phases after Foundational is complete

**User Story 3**:
- All tasks (T022-T024) are documentation/validation, can run sequentially

### Parallel Opportunities

- **Setup Phase**: All tasks (T001-T003) can run in parallel
- **Foundational Phase**: T004-T006 must be sequential (same file), T007-T008 can run after T006
- **User Story 1**: T016 (getting sound files) can run in parallel with T009-T015 (code tasks)
- **Across User Stories**: After Foundational completes, US1, US2, and US3 can be worked on in parallel by different team members
- **Polish Phase**: T025-T027 can run in parallel, T028-T033 must run sequentially (testing)

---

## Parallel Example: After Foundational Phase

```bash
# After Phase 2 completes, these can all start in parallel:

# Developer A works on User Story 1:
Task: "Implement playSound() function..."
Task: "Implement button generation loop..."
Task: "Obtain or create 9 MP3 sound files..."

# Developer B works on User Story 2 (enhances US1):
Task: "Add CSS Grid layout to .grid container..."
Task: "Add media query for tablet/mobile..."

# Developer C works on User Story 3 (documentation):
Task: "Add code comments above sounds array..."
Task: "Document the 3-step process..."
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
   - Load soundboard.html in browser
   - Click each button, verify sound plays
   - Test keyboard navigation (Tab, Enter, Space)
   - Verify visual feedback on click
5. Deploy/demo if ready - **This is a functional MVP soundboard!**

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
   - **Value**: Working soundboard with 9 sounds
3. Add User Story 2 → Test independently → Deploy/Demo
   - **Value**: MVP + mobile compatibility
4. Add User Story 3 → Test independently → Deploy/Demo
   - **Value**: MVP + mobile + easy extensibility
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1 (core functionality)
   - Developer B: User Story 2 (responsive layout) - waits for US1 buttons to exist
   - Developer C: User Story 3 (documentation)
3. Since all code is in one file, coordinate edits or use branches and merge carefully

---

## Notes

- All tasks edit the single file soundboard-app/soundboard.html (except T016 for sound files)
- Since it's a single file, parallelization requires careful coordination or git branches
- Verify tests fail before implementing (N/A - no automated tests in this project)
- Commit after each phase completion for clear checkpoints
- Stop at any checkpoint to validate story independently
- File size constraint: Ensure soundboard.html stays under 50KB (SC-007)

---

## Task Count Summary

- **Total Tasks**: 33
- **Phase 1 (Setup)**: 3 tasks
- **Phase 2 (Foundational)**: 5 tasks (BLOCKS all stories)
- **Phase 3 (User Story 1 - P1 MVP)**: 8 tasks
- **Phase 4 (User Story 2 - P2)**: 5 tasks
- **Phase 5 (User Story 3 - P3)**: 3 tasks
- **Phase 6 (Polish)**: 9 tasks

**Parallelization**: 4 tasks marked [P] for parallel execution within phases

**Independent Deliverables**:
- After Phase 3: MVP soundboard (US1) ✅
- After Phase 4: MVP + responsive layout (US1 + US2) ✅
- After Phase 5: Complete feature (US1 + US2 + US3) ✅

---

## Success Validation Checklist

After completing all tasks, validate these success criteria:

- [x] SC-001: Users can load app and play sound within 2 seconds ✅
- [x] SC-002: Desktop browsers display correctly (1024px-1920px width) ✅
- [x] SC-003: Mobile browsers display correctly (320px-768px width) ✅
- [x] SC-004: All 9 sounds play correctly across browsers ✅
- [x] SC-005: Buttons respond within 100ms with visual feedback ✅
- [x] SC-006: Adding new sound follows 3-step process ✅
- [x] SC-007: File size under 50KB (excluding sound files) ✅
- [x] SC-008: 90% user success rate (intuitive UI, no instructions needed) ✅
- [x] SC-009: Grid reflows smoothly when browser resized ✅

---

## File Structure After Completion

```
soundboard-app/
├── soundboard.html          (< 50KB - contains all HTML, CSS, JavaScript)
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

**Deployment**: Upload soundboard-app/ directory to any web host or GitHub Pages. Users can also run locally via file:// or local server.
