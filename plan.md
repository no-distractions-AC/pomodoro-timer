# Pomodoro Timer - Implementation Plan

## Project Overview
A Pomodoro productivity timer with task tracking, session history, statistics, and three themes. Pure HTML/CSS/JS with no build step, deployable to GitHub Pages.

## Clarified Requirements Summary
- **Branch**: `main` (GitHub Actions deployment)
- **Timer Controls**: Reset = restart current session, Stop = end entire cycle
- **Auto-start**: Only breaks auto-start; user manually starts work sessions
- **Task Association**: Sessions recorded even without task; no task change mid-session (toast warning)
- **Focus Theme**: Minimal view - timer, session indicator (1/4), task list only
- **Task Editing**: Double-click OR edit button
- **Help**: Full keyboard shortcuts modal
- **Mobile**: Bottom sheet for tasks (must-have), swipe gestures (without compromising desktop)
- **Streak**: At least 1 work session = day counts toward streak

---

## Phase 1: Project Setup & Foundation

### Task 1.1: Create File Structure
- [ ] Create `index.html` with semantic HTML5 boilerplate
- [ ] Create `styles.css` with CSS reset and variables
- [ ] Create `app.js` with IIFE structure
- [ ] Create `.gitignore` for web projects
- [ ] Update `README.md` with basic project info
- [ ] Create `LICENSE` (MIT)
- **Test**: Open `index.html` in browser, verify no errors in console
- **Commit**: "feat: initial project structure with HTML/CSS/JS files"

### Task 1.2: GitHub Actions Deployment
- [ ] Create `.github/workflows/deploy.yml`
- [ ] Configure for `main` branch deployment
- [ ] Add static HTML deployment steps
- **Test**: Push to GitHub, verify Actions workflow appears
- **Commit**: "ci: add GitHub Actions workflow for Pages deployment"

### Task 1.3: CSS Variables & Theme Foundation
- [ ] Define CSS variables for dark theme (default)
- [ ] Define CSS variables for light theme
- [ ] Define CSS variables for focus theme
- [ ] Add `data-theme` attribute support
- [ ] Add smooth transition for theme changes
- [ ] Add custom selection colors
- **Test**: Manually change `data-theme` in DevTools, verify colors change
- **Commit**: "feat: CSS variables and theme foundation for dark/light/focus"

### Task 1.4: Typography & Base Styles
- [ ] Import Space Mono / JetBrains Mono from Google Fonts
- [ ] Set base typography styles
- [ ] Add box-sizing reset
- [ ] Style body with theme variables
- [ ] Add `user-select: none` utility class
- **Test**: Verify font loads, text renders correctly
- **Commit**: "feat: typography setup with Space Mono font"

---

## Phase 2: Timer Core System

### Task 2.1: Timer State Management
- [ ] Create timer state object (duration, remaining, isRunning, sessionType, sessionCount)
- [ ] Create default durations object (work: 25, shortBreak: 5, longBreak: 15)
- [ ] Create localStorage helper functions (get, set, remove)
- [ ] Load/save timer preferences from localStorage
- **Test**: Set values in console, verify localStorage persistence
- **Commit**: "feat: timer state management and localStorage helpers"

### Task 2.2: Timer Display HTML
- [ ] Add timer container with circular progress ring (SVG)
- [ ] Add time display (MM:SS format)
- [ ] Add session type label ("Work" / "Short Break" / "Long Break")
- [ ] Add session progress indicator ("Session 2/4")
- [ ] Style timer display with theme variables
- **Test**: Verify timer display renders, progress ring visible
- **Commit**: "feat: timer display with circular progress ring"

### Task 2.3: Timer Countdown Logic
- [ ] Implement countdown using `performance.now()` for precision
- [ ] Update display every 100ms (not 1s for smoothness)
- [ ] Calculate remaining time accurately
- [ ] Handle timer completion
- [ ] Implement Visibility API for tab switching accuracy
- **Test**: Start timer, switch tabs, return - verify time is accurate
- **Commit**: "feat: precise timer countdown with performance.now()"

### Task 2.4: Timer Controls
- [ ] Add Start/Pause button (toggles state)
- [ ] Add Skip button (skip to next session)
- [ ] Add Reset button (reset current session)
- [ ] Add Stop button (end entire Pomodoro cycle)
- [ ] Style buttons with theme variables
- [ ] Add hover/active states
- **Test**: Click each button, verify correct behavior
- **Commit**: "feat: timer control buttons (start/pause/skip/reset/stop)"

### Task 2.5: Pomodoro Cycle Logic
- [ ] Implement session progression (work → short break → repeat)
- [ ] Track session count (1-4)
- [ ] Trigger long break after 4 work sessions
- [ ] Auto-start breaks after work sessions complete
- [ ] Reset cycle after long break
- [ ] Update progress ring based on elapsed time
- **Test**: Complete full Pomodoro cycle (use short durations for testing)
- **Commit**: "feat: complete Pomodoro cycle logic with auto-start breaks"

### Task 2.6: Session Calendar View
- [ ] Create 4-circle indicator showing position in cycle
- [ ] Fill circles based on completed sessions
- [ ] Different colors for work vs break
- [ ] Highlight current session
- **Test**: Progress through sessions, verify calendar updates
- **Commit**: "feat: session calendar view (1/4 visual indicator)"

---

## Phase 3: Sound System (Web Audio API)

### Task 3.1: Audio Context Setup
- [ ] Create AudioContext on first user interaction
- [ ] Create sound preference state (enabled/disabled)
- [ ] Load sound preference from localStorage
- [ ] Create master volume control with GainNode
- **Test**: Click page, verify AudioContext creates without error
- **Commit**: "feat: Web Audio API context setup"

### Task 3.2: Sound Generation Functions
- [ ] Create sine wave generator function
- [ ] Create triangle wave generator function
- [ ] Create square wave generator function
- [ ] Add envelope (attack, decay, sustain, release) for smooth sounds
- **Test**: Call functions in console, hear sounds
- **Commit**: "feat: oscillator-based sound generation functions"

### Task 3.3: Specific Sound Effects
- [ ] Timer start: soft ascending chime (3 sine notes)
- [ ] Timer pause: gentle click (triangle wave)
- [ ] Session complete: pleasant arpeggio (sine wave)
- [ ] Task check: subtle success tone
- [ ] Task uncheck: soft neutral tone
- [ ] Button click: minimal click (square wave, very short)
- [ ] Skip session: quick swoosh sound
- [ ] Last 10 seconds tick: subtle tick each second
- **Test**: Trigger each sound, verify they're gentle and under 200ms
- **Commit**: "feat: all sound effects using Web Audio API"

### Task 3.4: Sound Toggle
- [ ] Add sound toggle button (top-right, next to theme)
- [ ] Musical note icon when enabled, muted icon when disabled
- [ ] Persist preference in localStorage
- [ ] Respect preference for all sounds
- **Test**: Toggle sound, play sounds, verify mute works
- **Commit**: "feat: sound toggle with localStorage persistence"

---

## Phase 4: Task Management

### Task 4.1: Task Data Structure
- [ ] Define task object (id, text, completed, sessionsSpent, createdAt)
- [ ] Create tasks array in localStorage
- [ ] Create CRUD functions (create, read, update, delete)
- [ ] Create active task state
- **Test**: CRUD operations in console, verify localStorage
- **Commit**: "feat: task data structure and CRUD operations"

### Task 4.2: Task List UI
- [ ] Add task list container
- [ ] Render tasks with checkboxes
- [ ] Show sessions spent on each task
- [ ] Highlight active/selected task
- [ ] Style completed tasks (strikethrough)
- [ ] Mobile-responsive task list
- **Test**: View task list, verify rendering
- **Commit**: "feat: task list UI with sessions counter"

### Task 4.3: Add Task Functionality
- [ ] Add task input field with placeholder
- [ ] Add task on Enter key
- [ ] Validate input (no empty, character limit)
- [ ] Play task add sound
- [ ] Show toast on add
- [ ] Clear input after add
- **Test**: Add tasks, verify validation and localStorage
- **Commit**: "feat: add task with validation and feedback"

### Task 4.4: Task Completion (Checkbox)
- [ ] Toggle task completed state on checkbox click
- [ ] Apply strikethrough style
- [ ] Play check/uncheck sounds
- [ ] Keep task in list (don't remove)
- [ ] Update task in localStorage
- **Test**: Check/uncheck tasks, verify persistence
- **Commit**: "feat: task completion with strikethrough"

### Task 4.5: Task Editing
- [ ] Add edit button (small icon) next to each task
- [ ] Enable inline editing on double-click
- [ ] Save on Enter or blur
- [ ] Cancel on Escape
- [ ] Validate edited text
- [ ] Show toast on edit
- **Test**: Edit tasks both ways, verify persistence
- **Commit**: "feat: task editing via double-click and edit button"

### Task 4.6: Task Deletion
- [ ] Add delete button (small icon) next to each task
- [ ] Confirm deletion (or immediate with undo toast)
- [ ] Remove from localStorage
- [ ] Play deletion sound
- [ ] Show toast
- **Test**: Delete tasks, verify removal
- **Commit**: "feat: task deletion with confirmation"

### Task 4.7: Task Selection & Session Association
- [ ] Click task to select as active (visual indicator)
- [ ] Prevent task change while timer running (show toast)
- [ ] Associate completed work sessions with active task
- [ ] Increment sessionsSpent counter
- [ ] Allow no task selected (sessions still recorded)
- **Test**: Select task, complete session, verify counter increments
- **Commit**: "feat: task selection and session association"

---

## Phase 5: Session History

### Task 5.1: Session History Data Structure
- [ ] Define session object (id, date, startTime, endTime, duration, type, taskId, taskName)
- [ ] Create sessions array in localStorage
- [ ] Create add session function
- [ ] Create get sessions function (with date filtering)
- **Test**: Add sessions in console, verify localStorage
- **Commit**: "feat: session history data structure"

### Task 5.2: Record Sessions
- [ ] Record session on timer completion
- [ ] Include all required fields
- [ ] Associate with active task (if any)
- [ ] Handle work and break sessions differently
- **Test**: Complete sessions, verify recording
- **Commit**: "feat: automatic session recording on completion"

### Task 5.3: Session History UI
- [ ] Add history container (footer area)
- [ ] Display sessions in reverse chronological order
- [ ] Group by date with date headers
- [ ] Show session details (time, duration, type, task)
- [ ] Scrollable list
- [ ] Different styling for work vs break
- **Test**: View history, verify grouping and details
- **Commit**: "feat: session history display with date grouping"

### Task 5.4: History Collapsible on Mobile
- [ ] Make history section collapsible
- [ ] Collapsed by default on mobile
- [ ] Expand/collapse toggle
- [ ] Smooth animation
- **Test**: Test on mobile viewport, verify collapse works
- **Commit**: "feat: collapsible session history for mobile"

---

## Phase 6: Statistics Dashboard

### Task 6.1: Stats Calculation Functions
- [ ] Total sessions completed today
- [ ] Total focus time today (minutes)
- [ ] Total sessions all-time
- [ ] Total focus time all-time
- [ ] Longest streak (consecutive days)
- [ ] Average sessions per day
- [ ] Tasks completed today
- [ ] Tasks completed all-time
- [ ] Current session streak (1/4, 2/4, etc.)
- **Test**: Call functions with test data, verify calculations
- **Commit**: "feat: statistics calculation functions"

### Task 6.2: Stats Dashboard UI
- [ ] Create stats container with compact cards
- [ ] Display all stats with labels
- [ ] Update stats in real-time on session complete
- [ ] Style with theme variables
- [ ] Mobile-responsive (simplified view)
- **Test**: Complete sessions, verify stats update
- **Commit**: "feat: statistics dashboard UI"

### Task 6.3: Streak Calculation
- [ ] Calculate consecutive days with at least 1 session
- [ ] Track current streak
- [ ] Track longest streak ever
- [ ] Handle edge cases (first day, gap in history)
- **Test**: Create test data spanning multiple days, verify streaks
- **Commit**: "feat: streak calculation (current and longest)"

---

## Phase 7: Theming System

### Task 7.1: Theme Toggle Button
- [ ] Add circular button in top-right
- [ ] Display appropriate icon (moon/sun/target)
- [ ] Cycle through themes on click
- [ ] Add rotation and fade animation during transition
- **Test**: Click toggle, verify theme changes with animation
- **Commit**: "feat: theme toggle button with icons"

### Task 7.2: System Preference Detection
- [ ] Detect system color scheme preference
- [ ] Apply on first load (if no saved preference)
- [ ] Add media query listener for changes
- **Test**: Change system preference, verify theme updates
- **Commit**: "feat: respect system color scheme preference"

### Task 7.3: Theme Persistence
- [ ] Save theme choice to localStorage
- [ ] Load saved theme on page load
- [ ] Override system preference if user chose manually
- **Test**: Set theme, refresh page, verify persistence
- **Commit**: "feat: theme persistence in localStorage"

### Task 7.4: Focus Theme Minimal View
- [ ] Hide statistics dashboard in focus theme
- [ ] Hide session history in focus theme
- [ ] Show only: timer, session indicator, task list
- [ ] Minimal styling (pure black, bright red)
- [ ] Smooth transition when switching to/from focus
- **Test**: Switch to focus theme, verify minimal UI
- **Commit**: "feat: focus theme minimal view"

---

## Phase 8: Notifications

### Task 8.1: Browser Notification Setup
- [ ] Check notification permission status
- [ ] Request permission on first enable
- [ ] Create notification preference state
- [ ] Save preference to localStorage
- **Test**: Enable notifications, verify permission prompt
- **Commit**: "feat: browser notification permission handling"

### Task 8.2: Notification Toggle
- [ ] Add notification toggle in settings/header
- [ ] Show permission status
- [ ] Disable toggle if permission denied
- [ ] Persist preference
- **Test**: Toggle notifications, verify behavior
- **Commit**: "feat: notification toggle with permission status"

### Task 8.3: Session Completion Notifications
- [ ] Show notification when work session ends
- [ ] Show notification when break ends
- [ ] Include session info in notification
- [ ] Respect user preference
- [ ] Fallback to toast if notifications disabled/denied
- **Test**: Complete session with notifications enabled, verify
- **Commit**: "feat: browser notifications on session completion"

### Task 8.4: Screen Flash Animation
- [ ] Create screen flash effect on session complete
- [ ] Add toggle for flash preference
- [ ] Different flash colors for work vs break
- [ ] Persist preference
- **Test**: Complete session, verify flash effect
- **Commit**: "feat: screen flash animation on session complete"

---

## Phase 9: Toast Notifications

### Task 9.1: Toast System
- [ ] Create toast container (bottom center, fixed)
- [ ] Create showToast function (message, duration, type)
- [ ] Add fade in/out animations
- [ ] Auto-dismiss after 3 seconds
- [ ] Support multiple toasts (stack or replace)
- [ ] Style with monospace font
- **Test**: Call showToast with different messages
- **Commit**: "feat: toast notification system"

### Task 9.2: Toast Integration
- [ ] Session started/completed toasts
- [ ] Break started toasts
- [ ] Task added/deleted/edited toasts
- [ ] Settings changed toasts
- [ ] Keyboard shortcut used toasts
- [ ] Timer customization saved toasts
- [ ] Error toasts (different style)
- **Test**: Trigger each toast scenario
- **Commit**: "feat: toast notifications for all events"

---

## Phase 10: Customization Panel

### Task 10.1: Customization Modal UI
- [ ] Create modal/dropdown for customization
- [ ] Add number inputs for work duration
- [ ] Add number inputs for short break duration
- [ ] Add number inputs for long break duration
- [ ] Add save button
- [ ] Add cancel/close button
- [ ] Style with theme variables
- **Test**: Open modal, verify inputs render
- **Commit**: "feat: customization panel UI"

### Task 10.2: Duration Validation & Saving
- [ ] Validate inputs (min 1min, max 60min)
- [ ] Show validation errors
- [ ] Save to localStorage on confirm
- [ ] Apply to current timer (if not running)
- [ ] Show toast on save
- [ ] Reset to defaults option
- **Test**: Enter valid/invalid values, verify validation
- **Commit**: "feat: duration customization with validation"

### Task 10.3: Settings Toggles in Panel
- [ ] Add sound toggle
- [ ] Add notification toggle
- [ ] Add screen flash toggle
- [ ] Add auto-start breaks toggle (if desired)
- [ ] Persist all settings
- **Test**: Toggle each setting, verify persistence
- **Commit**: "feat: settings toggles in customization panel"

---

## Phase 11: Keyboard Shortcuts

### Task 11.1: Keyboard Event Handler
- [ ] Add global keydown event listener
- [ ] Prevent shortcuts when typing in input fields
- [ ] Create shortcut map object
- **Test**: Press keys, verify console logs
- **Commit**: "feat: keyboard event handler setup"

### Task 11.2: Timer Shortcuts
- [ ] Space: Start/Pause timer
- [ ] R: Reset current session
- [ ] N: Skip to next session
- [ ] S: Stop timer completely
- [ ] Show toast for each action
- **Test**: Use each shortcut, verify action
- **Commit**: "feat: timer keyboard shortcuts"

### Task 11.3: Task Shortcuts
- [ ] A: Focus add task input
- [ ] 1-9: Toggle task 1-9 checkbox
- [ ] Show toast for actions
- **Test**: Use each shortcut, verify action
- **Commit**: "feat: task keyboard shortcuts"

### Task 11.4: UI Shortcuts
- [ ] T: Toggle theme
- [ ] M: Toggle sound (mute)
- [ ] C: Open customization panel
- [ ] ?: Show help modal
- [ ] Detect "help" typed sequence
- **Test**: Use each shortcut, verify action
- **Commit**: "feat: UI keyboard shortcuts"

### Task 11.5: Help Modal
- [ ] Create modal with full keyboard shortcuts table
- [ ] Styled with theme variables
- [ ] Close on Escape or click outside
- [ ] Trigger with ? key or "help" typed
- **Test**: Open help modal, verify shortcuts list
- **Commit**: "feat: help modal with keyboard shortcuts reference"

---

## Phase 12: Mobile Responsiveness

### Task 12.1: Responsive Layout
- [ ] Add media queries for mobile breakpoints
- [ ] Stack layout vertically on mobile
- [ ] Timer remains prominent at top
- [ ] Larger touch targets (min 44px)
- [ ] Adjust font sizes for readability
- **Test**: Test on mobile viewport, verify layout
- **Commit**: "feat: mobile responsive layout"

### Task 12.2: Mobile Bottom Sheet for Tasks
- [ ] Create bottom sheet component
- [ ] Show task list in bottom sheet on mobile
- [ ] Drag handle for open/close
- [ ] Smooth slide animation
- [ ] Backdrop overlay
- [ ] Close on backdrop click
- **Test**: Test bottom sheet on mobile viewport
- **Commit**: "feat: mobile bottom sheet for task list"

### Task 12.3: Swipe Gestures
- [ ] Add touch event handlers
- [ ] Swipe left to skip session
- [ ] Swipe right to reset session
- [ ] Add visual feedback during swipe
- [ ] Ensure desktop mouse events still work
- [ ] Add gesture hints for first-time users
- **Test**: Test swipes on mobile, verify desktop unaffected
- **Commit**: "feat: swipe gestures for mobile"

### Task 12.4: Collapsible Sections
- [ ] Make stats section collapsible on mobile
- [ ] Make settings section collapsible
- [ ] Persist collapse state
- [ ] Smooth expand/collapse animation
- **Test**: Test collapsible sections on mobile
- **Commit**: "feat: collapsible sections for mobile"

---

## Phase 13: Accessibility

### Task 13.1: Semantic HTML & ARIA
- [ ] Use semantic HTML elements throughout
- [ ] Add ARIA labels to interactive elements
- [ ] Add ARIA live regions for timer updates
- [ ] Add role attributes where needed
- [ ] Ensure proper heading hierarchy
- **Test**: Run accessibility audit (Lighthouse)
- **Commit**: "feat: semantic HTML and ARIA labels"

### Task 13.2: Keyboard Navigation
- [ ] Ensure all controls are focusable
- [ ] Add visible focus indicators
- [ ] Implement logical tab order
- [ ] Support Enter/Space for buttons
- [ ] Escape to close modals
- **Test**: Navigate entire app with keyboard only
- **Commit**: "feat: full keyboard navigation support"

### Task 13.3: Screen Reader Support
- [ ] Add screen reader announcements for timer
- [ ] Announce session changes
- [ ] Announce task actions
- [ ] Test with VoiceOver/NVDA
- **Test**: Use screen reader to navigate app
- **Commit**: "feat: screen reader announcements"

---

## Phase 14: Error Handling

### Task 14.1: localStorage Error Handling
- [ ] Detect localStorage quota exceeded
- [ ] Show user-friendly error message
- [ ] Offer to clear old history
- [ ] Graceful fallback if localStorage unavailable
- **Test**: Fill localStorage, trigger error
- **Commit**: "feat: localStorage error handling"

### Task 14.2: Web Audio Error Handling
- [ ] Detect AudioContext creation failure
- [ ] Disable sounds gracefully
- [ ] Show message to user
- [ ] Continue app without sound
- **Test**: Block Web Audio API, verify graceful degradation
- **Commit**: "feat: Web Audio API error handling"

### Task 14.3: Notification Error Handling
- [ ] Handle permission denied gracefully
- [ ] Fall back to visual-only alerts
- [ ] Show helpful message
- [ ] Don't repeatedly ask for permission
- **Test**: Deny notification permission, verify fallback
- **Commit**: "feat: notification permission error handling"

### Task 14.4: Input Validation
- [ ] Validate all user inputs
- [ ] Show clear error messages
- [ ] Prevent invalid states
- [ ] Sanitize inputs before storage
- **Test**: Enter invalid inputs, verify validation
- **Commit**: "feat: comprehensive input validation"

---

## Phase 15: Polish & Optimization

### Task 15.1: Animation Polish
- [ ] Ensure all animations are 60fps
- [ ] Add will-change hints where needed
- [ ] Use transform/opacity for animations
- [ ] Add subtle micro-interactions
- [ ] Progress ring smooth animation
- **Test**: Profile animations in DevTools
- **Commit**: "feat: polished 60fps animations"

### Task 15.2: Performance Optimization
- [ ] Minimize reflows/repaints
- [ ] Debounce resize handlers
- [ ] Optimize localStorage access
- [ ] Lazy load non-critical features
- [ ] Verify under 100KB total size
- **Test**: Run Lighthouse performance audit
- **Commit**: "perf: optimize for fast loading"

### Task 15.3: Final UI Polish
- [ ] Review all spacing/alignment
- [ ] Ensure consistent styling
- [ ] Add loading states if needed
- [ ] Polish all three themes
- [ ] Test all interactions
- **Test**: Visual review of entire app
- **Commit**: "feat: final UI polish"

---

## Phase 16: Documentation & Deployment

### Task 16.1: README Documentation
- [ ] Add project description
- [ ] Add features list
- [ ] Add local setup instructions (just open index.html)
- [ ] Add keyboard shortcuts reference table
- [ ] Add how to customize timer durations
- [ ] Add how to enable notifications
- [ ] Add GitHub Pages deployment instructions
- [ ] Add screenshots/GIFs
- **Test**: Follow README instructions as new user
- **Commit**: "docs: comprehensive README"

### Task 16.2: Code Comments
- [ ] Add JSDoc comments to main functions
- [ ] Add section comments in CSS
- [ ] Add HTML section comments
- [ ] Document localStorage schema
- **Test**: Review code readability
- **Commit**: "docs: add code comments"

### Task 16.3: Final Testing
- [ ] Test full Pomodoro cycle
- [ ] Test all keyboard shortcuts
- [ ] Test all three themes
- [ ] Test on mobile devices
- [ ] Test accessibility
- [ ] Test localStorage persistence
- [ ] Test error scenarios
- [ ] Cross-browser testing (Chrome, Firefox, Safari)
- **Test**: Complete full test checklist
- **Commit**: "test: final testing complete"

### Task 16.4: Deployment Verification
- [ ] Push to GitHub
- [ ] Verify GitHub Actions runs
- [ ] Verify GitHub Pages deployment
- [ ] Test live URL
- [ ] Update README with live link
- **Test**: Visit deployed site, verify all features
- **Commit**: "deploy: verified GitHub Pages deployment"

---

## File Size Budget

| File | Target Size |
|------|-------------|
| index.html | ~10KB |
| styles.css | ~25KB |
| app.js | ~50KB |
| Total | <100KB |

---

## Testing Checklist

### Timer
- [ ] 25-minute work session counts down accurately
- [ ] 5-minute short break auto-starts
- [ ] 15-minute long break after 4 sessions
- [ ] Pause/resume maintains accuracy
- [ ] Tab switching doesn't break timer
- [ ] Reset restarts current session
- [ ] Stop ends entire cycle

### Tasks
- [ ] Add task works
- [ ] Edit task (double-click and button)
- [ ] Delete task works
- [ ] Checkbox toggles completion
- [ ] Strikethrough on complete
- [ ] Sessions counted per task
- [ ] Active task highlighting
- [ ] Cannot change task mid-session

### Themes
- [ ] Dark theme renders correctly
- [ ] Light theme renders correctly
- [ ] Focus theme renders correctly
- [ ] Smooth transitions between themes
- [ ] Persistence across refreshes
- [ ] System preference detection

### Sounds
- [ ] All sounds play correctly
- [ ] Sound toggle mutes all
- [ ] Sounds are gentle (<200ms)
- [ ] No audio file dependencies

### Shortcuts
- [ ] All shortcuts work
- [ ] No interference with inputs
- [ ] Help modal displays correctly

### Mobile
- [ ] Layout responsive
- [ ] Bottom sheet works
- [ ] Swipe gestures work
- [ ] Touch targets adequate
- [ ] Collapsible sections work

### Accessibility
- [ ] Keyboard navigation complete
- [ ] Screen reader announces
- [ ] Focus indicators visible
- [ ] ARIA labels present

---

## Commit Message Convention

Format: `<type>: <description>`

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting (no code change)
- `refactor`: Code restructuring
- `perf`: Performance improvement
- `test`: Testing
- `ci`: CI/CD changes
- `chore`: Maintenance

---

## Notes

- Keep JavaScript in single IIFE to avoid global pollution
- Use CSS custom properties for all theme colors
- Test on slow network to verify no external dependencies break app
- All times stored in localStorage as ISO strings
- Session IDs use timestamp + random suffix
- Task IDs use timestamp + random suffix
