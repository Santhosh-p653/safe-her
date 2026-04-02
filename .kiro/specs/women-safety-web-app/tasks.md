# Implementation Plan: SafeHer / SheShield Women Safety Web App

## Overview

Build a single HTML file (`index.html`) with embedded CSS and JavaScript. All sections are implemented incrementally, wiring together into a complete SPA by the final task.

## Tasks

- [x] 1. Scaffold the single HTML file with base structure and CDN dependencies
  - Create `index.html` with `<head>` loading Bootstrap 5 CSS/JS, Bootstrap Icons, and Font Awesome via CDN
  - Add `<html style="scroll-behavior: smooth">` and CSS custom properties for the color palette (Deep Purple, Teal, Electric Blue/Orange)
  - Add empty section stubs with correct `id` attributes: `#home`, `#sos`, `#safety-tools`, `#blog`, `#community`, `#contact`
  - Add embedded `<style>` and `<script>` blocks (empty placeholders)
  - _Requirements: 1.1, 1.2, 1.3, 9.1_

- [x] 2. Implement the Navbar
  - [x] 2.1 Build the sticky Navbar with brand, nav links, language selector, and dark mode toggle button
    - Use Bootstrap `navbar navbar-expand-lg` with `position: sticky; top: 0`
    - Add links: Home, SOS, Safety Tools, Blog, Community, Contact (each `href` pointing to the corresponding section `id`)
    - Add Language Selector dropdown with English, Hindi, Spanish options
    - Add dark mode toggle button (moon/sun icon)
    - Apply glassmorphism styling via `backdrop-filter: blur()` and semi-transparent background
    - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5, 9.4, 11.1_

  - [x] 2.2 Implement Language Selector JS logic
    - On option click, update the dropdown label to the selected language; make no other DOM changes
    - _Requirements: 11.2_

  - [ ]* 2.3 Write property test for nav link → section id mapping (Property 1)
    - **Property 1: Nav links target existing sections**
    - **Validates: Requirements 1.4**
    - `// Feature: women-safety-web-app, Property 1: nav link hrefs map to existing section ids`

  - [ ]* 2.4 Write property test for language selector label update (Property 8)
    - **Property 8: Language selector updates label without altering content**
    - **Validates: Requirements 11.2**
    - `// Feature: women-safety-web-app, Property 8: label updates, no other DOM text changes`

- [x] 3. Implement the Hero Section
  - Add full-viewport-height section with CSS gradient background (Deep Purple → Teal)
  - Add headline "Your Safety, Your Power", subtext paragraph, and "Activate SOS" CTA button
  - Wire CTA button `onclick` to `document.querySelector('#sos').scrollIntoView({ behavior: 'smooth' })`
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5, 3.6, 9.5_

- [x] 4. Implement the SOS Section
  - [x] 4.1 Build SOS button with CSS pulse animation and result display areas
    - Add large centered SOS button with `@keyframes pulse` animation defined in CSS (no JS required for animation)
    - Add hidden coordinate display element and alert message element
    - Apply gradient background to the SOS section
    - _Requirements: 4.1, 4.7, 9.5_

  - [x] 4.2 Implement SOS button JS logic (geolocation)
    - On click, check `navigator.geolocation` support; if unsupported show "Geolocation is not supported by your browser."
    - Call `navigator.geolocation.getCurrentPosition()` on success: display lat/lng and "Location sent to emergency contacts"
    - On error: display "Location access was denied. Please enable location permissions." or "Location is currently unavailable. Please try again." based on error code
    - _Requirements: 4.2, 4.3, 4.4, 4.5, 4.6_

  - [ ]* 4.3 Write property test for geolocation success display (Property 2)
    - **Property 2: Geolocation success displays coordinates and alert message**
    - **Validates: Requirements 4.3, 4.4**
    - `// Feature: women-safety-web-app, Property 2: any lat/lng pair triggers coordinate display and alert message`

  - [ ]* 4.4 Write unit tests for geolocation error and unsupported paths
    - Test permission denied error message
    - Test unavailable error message
    - Test unsupported browser message
    - _Requirements: 4.5, 4.6_

- [x] 5. Checkpoint — Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.

- [x] 6. Implement the Safety Tools Section
  - [x] 6.1 Build three Bootstrap cards: Emergency Checklist, Nearby Help, Report Unsafe Area
    - Emergency Checklist: static list of preparedness items with Bootstrap Icons
    - Nearby Help: styled `<div>` map placeholder with "Map placeholder" label
    - Report Unsafe Area: form with location description textarea and incident type select field
    - Apply CSS hover effect: `transform: translateY(-4px)` + `box-shadow` transition on all cards
    - Apply glassmorphism styling on cards
    - _Requirements: 5.1, 5.2, 5.3, 5.4, 5.5, 9.3, 9.4_

  - [x] 6.2 Implement Report Unsafe Area form JS logic
    - Intercept form submit with `preventDefault()`; display inline client-side confirmation message; make no network requests
    - _Requirements: 5.6_

  - [ ]* 6.3 Write unit test for Report Unsafe Area form submission
    - Verify `preventDefault` called, confirmation message shown, no fetch/XHR triggered
    - _Requirements: 5.6_

- [x] 7. Implement the Blog Section
  - Build responsive Bootstrap grid (`col-md-4`) with minimum 3 blog cards
  - Each card: image placeholder (`<div>` styled as image), title, short description, "Read More" button
  - Topics: safety tips, awareness, real stories
  - Apply hover transition on cards; grid reflows to single column on mobile
  - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5, 9.3_

  - [ ]* 7.1 Write property test for blog card completeness (Property 3)
    - **Property 3: Blog cards are complete and sufficient**
    - **Validates: Requirements 6.1, 6.2**
    - `// Feature: women-safety-web-app, Property 3: all rendered blog cards contain image/placeholder, title, description, Read More button`

- [x] 8. Implement the Community Section
  - [x] 8.1 Build community feed with pre-populated sample posts and submission form
    - Render minimum 3 sample posts on page load (support tone, awareness content)
    - Add textarea + Submit button
    - _Requirements: 7.1, 7.3, 7.4_

  - [x] 8.2 Implement community post submission JS logic
    - On submit: trim input; if empty show "Please enter a message before posting." and do not add post
    - If valid: prepend new post card to feed, clear textarea, no page reload
    - _Requirements: 7.2, 7.5_

  - [ ]* 8.3 Write property test for valid community message submission (Property 4)
    - **Property 4: Valid community message appears in feed**
    - **Validates: Requirements 7.2**
    - `// Feature: women-safety-web-app, Property 4: any non-empty trimmed string submitted appears as new post in feed`

  - [ ]* 8.4 Write unit test for empty community message validation
    - Verify validation message shown and no post added when input is empty or whitespace
    - _Requirements: 7.5_

- [x] 9. Implement the Footer
  - Add quick nav links mirroring the Navbar
  - Add emergency helplines: Women Helpline 1091, Police 100, Ambulance 102
  - Add social media icons (Twitter/X, Instagram, Facebook) via icon CDN
  - Apply gradient/glassmorphism styling consistent with overall palette
  - _Requirements: 8.1, 8.2, 8.3, 8.4_

- [x] 10. Implement Dark Mode Toggle
  - [x] 10.1 Implement dark mode JS logic with localStorage persistence
    - On toggle: add/remove `dark` class on `<html>` element; write `'dark'` or `'light'` to `localStorage` key `'theme'`
    - On page load: read `localStorage.getItem('theme')` and apply stored preference before first paint
    - Update toggle button icon (moon ↔ sun) to reflect current state
    - _Requirements: 10.1, 10.2, 10.3, 10.4_

  - [x] 10.2 Add dark mode CSS rules
    - Define `html.dark` scoped CSS overrides for background, text, card, and navbar colors
    - _Requirements: 10.2, 10.3_

  - [ ]* 10.3 Write property test for dark mode round trip (Property 6)
    - **Property 6: Dark mode toggle is a round trip**
    - **Validates: Requirements 10.3**
    - `// Feature: women-safety-web-app, Property 6: toggle on then off restores original theme state`

  - [ ]* 10.4 Write property test for theme persistence (Property 7)
    - **Property 7: Theme preference persists across sessions**
    - **Validates: Requirements 10.4**
    - `// Feature: women-safety-web-app, Property 7: selected theme written to localStorage and re-applied on re-init`

- [x] 11. Implement scroll-triggered fade-in animations
  - Add `.fade-in` CSS class (opacity 0 → 1, translateY transition)
  - Use `IntersectionObserver` to add `.fade-in.visible` class when each section enters the viewport
  - Apply to all major sections
  - _Requirements: 9.2_

  - [ ]* 11.1 Write property test for hover transitions on interactive elements (Property 5)
    - **Property 5: Hover transitions applied to all interactive elements**
    - **Validates: Requirements 9.3**
    - `// Feature: women-safety-web-app, Property 5: every button and card element has a CSS transition property defined`

- [ ] 12. Final checkpoint — Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional and can be skipped for a faster MVP
- All property tests use **fast-check** with a minimum of 100 iterations per property
- All unit tests use **Jest + jsdom** (or Vitest + jsdom)
- Each property test must include the comment tag: `// Feature: women-safety-web-app, Property {N}: {property_text}`
- The entire application is delivered as a single `index.html` file — no build step required
