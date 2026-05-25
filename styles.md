# PassForge — Design System & Style Guide

> **Version:** 1.0
> **Theme:** Modern · Elegant · Premium

All styles live in the `<style>` block of `index.html`. There is no external stylesheet. Tailwind CSS (CDN) handles utility classes; custom classes handle design-system components.

---

## Design Philosophy

PassForge is built on one principle: **clarity commands trust.**

Every visual decision — spacing, type weight, color hierarchy — exists to make the organizer feel in control and the attendee feel valued. The UI is deliberately restrained. No gradients, no decoration for its own sake. Strength comes from proportion, contrast, intentional whitespace, and very limited overlay shadow.

The aesthetic is **corporate-premium without being cold** — the kind of interface you'd expect from a well-funded product, not a weekend project.

---

## Typography

### Typeface

**Inter** is the sole typeface across the entire product.

Inter was chosen for its exceptional legibility at small sizes, its neutral authority at large sizes, and its variable font support. The OpenType features below enable disambiguated characters (0 vs O, 1 vs l) and a cleaner lowercase `a` — important for a product dealing with alphanumeric IDs and pass tokens.

```css
font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11';
```

All `button`, `input`, `select`, and `textarea` elements inherit `font: inherit`.

---

### Type Scale

| Token | Size | Weight | Line Height | Letter Spacing | Usage |
|-------|------|--------|-------------|----------------|-------|
| `display` | 48px | 700 | 1.1 | 0em | Hero, landing |
| `heading-1` | 36px | 700 | 1.15 | 0em | Page titles |
| `heading-2` | 24px | 600 | 1.25 | 0em | Section headers |
| `heading-3` | 18px | 600 | 1.35 | 0em | Card titles, panel headers |
| `heading-4` | 13px | 600 | 1.4 | 0.07em | Labels, eyebrows (uppercase) |
| `body-lg` | 16px | 400 | 1.7 | 0em | Primary body copy |
| `body` | 15px | 400 | 1.7 | 0em | Default UI text |
| `body-sm` | 13px | 400 | 1.6 | 0em | Secondary text, hints |
| `caption` | 11px | 500 | 1.5 | 0.09em | Tags, timestamps (uppercase) |
| `mono` | 13px | 400 | 1.6 | 0em | IDs, tokens, pass codes |

### Rules

- **No negative tracking.** Letter spacing is either `0` for normal text or positive for uppercase labels/captions.
- **Two weights for UI text: 400 and 600.** Weight 500 is permitted for numeric values and emphasized inline text only. Avoid 700 in UI components — it is a display/title weight.
- **Uppercase is a tool, not a style.** Use uppercase only for `heading-4` labels and `caption` elements. Never uppercase body copy.
- **No italic in UI.** Italic is permitted in marketing or editorial copy only — never in dashboard, forms, or data contexts.
- **Minimum size: 11px.** Nothing below this in any context.

---

## Color

### Palette

```css
:root {
  /* Primary */
  --primary:         #6C4CF1;
  --primary-hover:   #5A3DD4;
  --primary-active:  #4A2FB8;
  --primary-subtle:  #EDE9FD;
  --primary-border:  #C4B5FA;

  /* Accent */
  --accent:          #FFB5A7;
  --accent-subtle:   #FFF0ED;
  --accent-border:   #FFCFC7;

  /* Backgrounds */
  --bg:              #F7F8FC;
  --surface:         #FFFFFF;
  --surface-soft:    #F7F8FC;
  --sunken:          #EDEEF4;

  /* Text */
  --text:            #101828;
  --text-secondary:  #344054;
  --muted:           #667085;
  --disabled:        #98A2B3;

  /* Borders */
  --border:          #E4E7EC;
  --border-strong:   #D0D5DD;

  /* Semantic — Success */
  --success:         #027A48;
  --success-bg:      #ECFDF3;
  --success-border:  #ABEFC6;
  --success-dot:     #12B76A;

  /* Semantic — Warning */
  --warning:         #B54708;
  --warning-bg:      #FFFAEB;
  --warning-border:  #FEDF89;
  --warning-dot:     #F79009;

  /* Semantic — Error */
  --error:           #B42318;
  --error-bg:        #FEF3F2;
  --error-border:    #FECDCA;
  --error-dot:       #F04438;

  /* Semantic — Info */
  --info:            #1D4ED8;
  --info-bg:         #EFF6FF;
  --info-border:     #BFDBFE;
}
```

### Dark Mode (`.dark` on `<html>`)

| Token | Value |
|-------|-------|
| `--bg` | `#0B1020` |
| `--surface` | `#111827` |
| `--surface-soft` | `#151D2E` |
| `--sunken` | `#172033` |
| `--text` | `#F8FAFC` |
| `--text-secondary` | `#D5DBE8` |
| `--muted` | `#A7B0C3` |
| `--border` | `#293244` |
| `--border-strong` | `#3A455A` |

Semantic color tokens (success/warning/error/primary) are overridden in dark mode via per-component rules (e.g. `.dark .badge-issued`, `.dark .btn-danger`).

---

### Color Roles

| Token | Hex | Role |
|-------|-----|------|
| `--primary` | `#6C4CF1` | CTAs, active states, focus rings, brand identity |
| `--primary-subtle` | `#EDE9FD` | Badge backgrounds, selected row highlights |
| `--accent` | `#FFB5A7` | Pass template accents, decorative highlights |
| `--accent-subtle` | `#FFF0ED` | Soft backgrounds for accent-adjacent content |
| `--bg` | `#F7F8FC` | Page background |
| `--surface` | `#FFFFFF` | Cards, modals, inputs |
| `--sunken` | `#EDEEF4` | Inset panels, table alt rows, code blocks |
| `--text` | `#101828` | All headings, primary body text |
| `--text-secondary` | `#344054` | Supporting body text, descriptions |
| `--muted` | `#667085` | Placeholders, hints, metadata |
| `--disabled` | `#98A2B3` | Disabled inputs and buttons |
| `--border` | `#E4E7EC` | Default borders on cards, inputs, dividers |
| `--border-strong` | `#D0D5DD` | Emphasized borders, table headers |

### Color Usage Rules

- **Primary is for action.** `#6C4CF1` signals something the user can or should do. Never use it decoratively on non-interactive elements.
- **Accent is for warmth.** `#FFB5A7` should appear sparingly — in pass template design or as a visual counterpoint to primary. Never use it for functional text.
- **Backgrounds create depth without shadows.** The three-level background system (`--bg`, `--surface`, `--sunken`) replaces elevation shadows entirely. Cards on `--surface` (#FFFFFF) against `--bg` (#F7F8FC) create perceived lift through contrast alone.
- **Text hierarchy is non-negotiable.** Primary (#101828), secondary (#344054), and muted (#667085) must be used at the correct hierarchy level. Mixing them incorrectly destroys visual structure.
- **Never use color alone to communicate state.** Always pair color with a text label, icon, or shape change.

---

## Spacing

### Base Unit

All spacing is derived from a **4px base unit**. All values must be multiples of 4.

### Scale

| Token | Value | Common Use |
|-------|-------|------------|
| `space-1` | 4px | Icon gaps, tight inline spacing |
| `space-2` | 8px | Between label and input hint |
| `space-3` | 12px | Internal component padding (sm) |
| `space-4` | 16px | Default component padding |
| `space-5` | 20px | Between sibling components |
| `space-6` | 24px | Card padding, section gaps |
| `space-8` | 32px | Between card groups |
| `space-10` | 40px | Section top padding |
| `space-12` | 48px | Section vertical rhythm |
| `space-16` | 64px | Major section breaks |
| `space-24` | 96px | Page-level breathing room |

### Layout Dimensions

| Property | Value |
|----------|-------|
| Sidebar width | 240px (fixed, full height) |
| Content max-width | 1280px (Tailwind `max-w-7xl`) |
| Content horizontal padding | 32px desktop / 16px mobile |
| Card padding | 20–24px |
| Form field gap | 20px |

---

## Border Radius

Radius communicates containment and softness.

| Token | Value | Usage |
|-------|-------|-------|
| `radius-xs` | 4px | Tags, code chips, formal pass card |
| `radius-sm` | 6px | Badges, small buttons |
| `radius-md` | 8px | Inputs, buttons, attendee items |
| `radius-lg` | 12px | Cards, panels, compact pass card |
| `radius-xl` | 16px | Modals, verify result panels |
| `radius-2xl` | 24px | Pass card (Classic, Ribbon top) |
| `radius-full` | 9999px | Status pills, avatar circles, spinners |

---

## Borders

Borders carry most of the responsibility for defining component edges and hierarchy.

```css
/* Default — cards, inputs, dividers */
border: 1px solid var(--border);          /* #E4E7EC */

/* Strong — table headers, emphasized panels */
border: 1px solid var(--border-strong);   /* #D0D5DD */

/* Focus ring — interactive elements */
border-color: var(--primary);             /* #6C4CF1 */
outline: 3px solid var(--primary-subtle); /* #EDE9FD */

/* Primary tint — selected states, info panels */
border: 1px solid var(--primary-border);  /* #C4B5FA */
```

### Rules

- **Every elevated surface has a border.** Cards, inputs, dropdowns, and modals all carry `1px solid var(--border)`. Borders provide the primary edge contrast.
- **Focus must be primary color.** All interactive elements use `#6C4CF1` as the focus ring color. Never use browser defaults.
- **Use shadows only for overlays or transient emphasis.** Standard cards, inputs, tables, and panels use background contrast and borders. Fixed mobile overlays and the compact destructive attendee action may use a small shadow for separation.

---

## Elevation System

PassForge uses shadows sparingly. Elevation is usually communicated through background color contrast and border definition; shadows are reserved for fixed mobile overlays and small destructive-action emphasis.

| Level | Background | Border | Use |
|-------|-----------|--------|-----|
| Sunken | `#EDEEF4` | none | Inset panels, login product panel, settings sections |
| Base | `#F7F8FC` | none | Page background |
| Elevated | `#FFFFFF` | `1px solid #E4E7EC` | Cards, inputs, dropdowns |
| Overlay | `#FFFFFF` | `1px solid #D0D5DD` | Modals, confirmation dialogs, mobile menu panels |

---

## Motion

Subtle, purposeful, never decorative. Motion confirms state changes and guides attention — it never entertains.

### Transitions

```css
/* Instant — hover color/border changes */
transition: all 150ms ease;

/* Default — background fills, opacity */
transition: all 200ms ease-out;

/* Reveal — panels, modals appearing */
transition: all 250ms cubic-bezier(0.16, 1, 0.3, 1);

/* Gentle — page-level view transitions */
transition: all 300ms ease-in-out;
```

### Keyframe Animations

| Name | Trigger | Effect |
|------|---------|--------|
| `fade-up` | `.card`, `.attendee-item` | Fade in + translate Y from 8px, 280ms ease-out |
| `pass-in` | `.pass-card`, `.confirm-dialog` | Fade in + translate Y + scale from 0.98, 360ms cubic-bezier |
| `spin` | `.spinner` | 360° rotation, 700ms linear infinite |
| `view-fade` | Vue `<transition>` on view changes | Fade + Y translate between views, 300ms |

### Rules

- **No bounce on UI chrome.** Use restrained ease curves; pass-card creation may use the slightly more expressive `cubic-bezier(.16, 1, .3, 1)`.
- **Max duration: 360ms.** Any longer and the interface feels sluggish.
- **No looping animations in production UI.** Loading spinners are the only exception.
- **Prefer opacity + transform over layout animations.** Never animate `width`, `height`, `padding`, or `margin`.
- **Respect reduced motion.** `@media (prefers-reduced-motion: reduce)` collapses all animation/transition durations to `0.01ms`.

---

## Layout Classes

### App Shell

| Class | Description |
|-------|-------------|
| `.sidebar` | Fixed left sidebar, 240px wide, visible `lg:` and up |
| `.topbar` | Sticky header, glassmorphism blur (`backdrop-filter: blur(16px)`) |
| `.brand-mark` | 36×36 purple rounded square with "PF" initials |
| `.mobile-bottom-nav` | Fixed bottom tab bar used below `1024px` |
| `.mobile-tab` | Compact icon + label navigation item |
| `.mobile-tab-avatar` | Profile initials shown in the More tab |
| `.mobile-menu-panel` | Floating mobile account/actions panel |
| `.mobile-menu-profile` | Account identity row inside the mobile panel |
| `.mobile-menu-actions` | Grid of Profile, Reset workspace, and Sign out actions |

### Login

| Class | Description |
|-------|-------------|
| `.login-screen` | Full-viewport grid, centered |
| `.login-panel` | Two-column card (max 920px): product panel + form panel |
| `.login-product` | Left panel — sunken bg, feature list |
| `.login-form-panel` | Right panel — form, centered vertically |
| `.login-feature` | Feature row with icon + text, top border divider |
| `.login-feature-icon` | 36×36 bordered square icon container |
| `.login-error` | Red error message box |
| `.credential-hint` | `<details>` element for demo credentials |
| `.public-verify-panel` | Standalone shared-pass verification panel |
| `.public-verify-header` | Icon + heading row for public verification |
| `.public-verify-mark` | 44×44 primary-tinted verification icon container |
| `.public-pass-code` | Sunken panel containing the shared pass input |

### Content Panels

| Class | Description |
|-------|-------------|
| `.card` | White surface, 1px border, 14px radius, `fade-up` entrance animation |
| `.soft-panel` | Light surface, 1px border, 12px radius |
| `.listing-card` | Flex column card for searchable list views |
| `.listing-header` | Two-column header: title + search input |
| `.listing-search` | Search field aligned to end of header |
| `.listing-body` | Flex 1 area for list content |
| `.pager` | Bottom pagination bar: count + prev/next buttons |
| `.metric-card` | Dashboard stat card, 116px min height |
| `.metric-icon` | 36×36 primary-subtle rounded icon |

### Attendee List

| Class | Description |
|-------|-------------|
| `.attendee-list` | Grid of attendee cards, 6px gap |
| `.attendee-item` | Two-column card (name/email + type badge); hover lifts -1px |
| `.attendee-item.active` | Primary border + primary-subtle background |

---

## Component Specifications

### Buttons (`.btn`)

Base: `min-height: 40px`, inline-flex, 8px radius, 14px font, 600 weight, 8px gap, `8px 14px` padding. The current app uses one button size and varies emphasis through color variants.

#### Variants

| Class | Appearance |
|-------|-----------|
| `.btn-primary` | Purple fill (`#6C4CF1`), white text |
| `.btn-secondary` | White surface, secondary text, strong border |
| `.btn-ghost` | Transparent, muted text; hover shows sunken bg |
| `.btn-danger` | Error-tinted bg, red text and border |

Hover/active states step through `--primary-hover` (#5A3DD4) → `--primary-active` (#4A2FB8).
Disabled state: `opacity: 0.45`, `cursor: not-allowed`.

---

### Inputs (`.input`)

```css
.input {
  min-height: 40px;
  padding: 8px 12px;
  border: 1px solid var(--border-strong);
  border-radius: 8px;
  color: var(--text);
  background: var(--surface);
  outline: none;
  transition: border-color 150ms ease, outline 150ms ease, background 250ms ease;
}
.input:focus        { border-color: var(--primary); outline: 3px solid var(--primary-subtle); }
```

**Table variant**: transparent border + soft bg at rest; restores surface border on focus.

Date and time inputs set `color-scheme` for light/dark mode and adjust WebKit picker indicators so native controls remain readable.

### Select (`.select-input`)

Extends `.input`. Custom SVG chevron background image; hides native OS arrow (`-webkit-appearance: none`). Right padding expanded to 40px for chevron clearance.

### Labels (`.label`)

11px, 600 weight, uppercase, 0.09em letter-spacing, `--muted` color, 6px bottom margin.

---

### Badges (`.badge`)

Pill shape (9999px radius), 22px min height, 11px/600 text, 6×6px colored dot.

| Class | Background | Text | Border | Dot |
|-------|-----------|------|--------|-----|
| `.badge-issued` | `--primary-subtle` | `--primary-active` | `--primary-border` | `#6C4CF1` |
| `.badge-used` | `--success-bg` | `--success` | `--success-border` | `#12B76A` |
| `.badge-revoked` / `.badge-expired` | `--error-bg` | `--error` | `--error-border` | `#F04438` |
| `.badge-draft` | `--surface-soft` | `--muted` | `--border` | `#98A2B3` |

---

### Cards (`.card`)

```css
.card {
  background: var(--surface);    /* #FFFFFF */
  border: 1px solid var(--border);
  border-radius: 14px;
  overflow: hidden;
  animation: fade-up 280ms ease-out both;
}
```

**Card sub-structure:**

| Element | Padding | Border |
|---------|---------|--------|
| Card header | 20px 24px | `border-bottom: 1px solid var(--border)` |
| Card body | 20–24px | — |
| Card footer | 16px 24px | `border-top: 1px solid var(--border)`, soft bg |

---

### Tables (`.table`)

- Full width, `border-collapse: collapse`
- `th`: 11px/600, uppercase, 0.08em tracking, soft bg, muted text, `white-space: nowrap`
- `td`: 14px, 14px vertical padding, `vertical-align: middle`
- `tbody tr:hover`: soft background transition (150ms)
- Mobile (`max-width: 767px`): table minimum width 640px with horizontal scroll wrapper (`.mobile-scroll`)

---

### State Panels (`.state-panel`)

Centered grid, 180px min height, 28px vertical padding. Used for empty states throughout the app.

| Class | Description |
|-------|-------------|
| `.state-icon` | 44×44 circle, sunken bg, primary icon color |

---

### Modals

| Class | Description |
|-------|-------------|
| `.modal-backdrop` | Fixed full-screen, `rgba(15, 23, 42, 0.48)` overlay, `z-80` |
| `.confirm-dialog` | Card, 420px max width, `pass-in` entrance animation |

---

### Toast

Fixed bottom-center, `z-50`, auto-dismisses after 2600ms.

| Class | Appearance |
|-------|-----------|
| `.toast` | Surface bg, border, primary text |
| `.toast-error` | Error bg/border/text |
| `.toast-success` | Success bg/border/text |

---

### Upload

| Class | Description |
|-------|-------------|
| `.upload-dropzone` | 3-column grid, dashed border; hover turns primary-tinted |
| `.upload-dropzone.has-file` | Solid primary border + primary-subtle bg |
| `.upload-icon` | 40×40 icon box, surface bg, primary icon color |
| `.upload-preview` | 72×44 thumbnail, 8px radius |

---

### Verification Results

| Class | Appearance |
|-------|-----------|
| `.verify-success` | `--success-bg` / `--success-border` / `--success` text |
| `.verify-warning` | `--warning-bg` / `--warning-border` / `--warning` text |
| `.verify-error` | `--error-bg` / `--error-border` / `--error` text |

Full state specifications:

| State | Background | Heading | Icon |
|-------|-----------|---------|------|
| Valid | `#ECFDF3` | `#027A48` | Circle checkmark, `#12B76A` |
| Already Used | `#FFFAEB` | `#B54708` | Warning triangle, `#F79009` |
| Expired / Revoked / Invalid | `#FEF3F2` | `#B42318` | X circle, `#F04438` |

- State label: 11px, uppercase, 0.12em tracking
- Attendee name: 24px/600, `--text`
- Event + ticket type: 14px, `--muted`
- Timestamp (if used): 12px mono, `--muted`

---

## Pass Card

The exportable pass uses **hardcoded light-mode values** (not CSS variables) so PNG/PDF export renders correctly regardless of app theme.

```css
.pass-card {
  width: min(100%, 400px);
  background: #fff;
  color: #101828;
  border-radius: 24px;
  overflow: hidden;
}
```

### Templates

| Class modifier | Border Radius | Footer bg |
|---------------|--------------|-----------|
| (none) Classic | 24px all | `#EDE9FD` primary-subtle |
| `.compact` | 12px all | `#EDE9FD` |
| `.ribbon` | 24px top / 8px bottom | `#EDE9FD` |
| `.formal` | 4px all | `#F7F8FC` light grey |

### Pass Card Zones

1. **Banner** — optional cover image, 112px height, `background-cover`
2. **Header band** — brand color background, organizer in white/75, event name Inter 700, date/time/venue in 2-column grid
3. **Pass holder section** — attendee name (20px/600), email (14px slate-500)
4. **Divider** — dashed `#D0D5DD` with cut-circle notches (`::before` / `::after`) on each edge
5. **QR zone** — 116×116px QR code (QRCode.js), pass ID in mono 12px, status badge
6. **Footer band** — "Scan to verify entry" left-aligned, "PassForge" right-aligned, 12px/600

At export: html2canvas captures at `scale: 3` (1200px effective width), `backgroundColor: #FFFFFF`.

---

## Navigation

### Sidebar (`.sidebar`)

```css
.sidebar {
  background: var(--surface);
  border-right: 1px solid var(--border);
}
```

### Nav Button (`.nav-button`)

Full-width minus 24px margin, 10px padding, 8px radius, 14px text.

```css
.nav-button         { color: var(--muted); }
.nav-button:hover   { background: var(--sunken); color: var(--text); }
.nav-button.active  { background: var(--primary); color: #fff; }
```

### Top Bar (`.topbar`)

```css
.topbar {
  background: color-mix(in srgb, var(--surface) 92%, transparent);
  border-bottom: 1px solid var(--border);
  backdrop-filter: blur(16px);
  position: sticky;
  top: 0;
  z-index: 40;
}
```

### Mobile Bottom Navigation

Below `1024px`, primary navigation moves to `.mobile-bottom-nav`, a fixed bottom tab bar with six equal columns: five primary workspace tabs plus a More tab for account actions. The More tab opens `.mobile-menu-panel`, which contains profile identity, Settings/Profile, Reset workspace, and Sign out.

---

## Iconography

**Style:** Lucide-inspired inline SVG, outline style only. Icons are embedded directly in `index.html` rather than loaded from an icon package.

- **Default size:** 16px inline, 20px for standalone action icons
- **Stroke width:** 1.5px throughout — never 2px, never filled variants
- **Color:** always `currentColor` — never hardcoded
- **No filled icons** in any context except the verified-entry checkmark on the QR confirmation page

```html
<svg width="16" height="16" viewBox="0 0 24 24" fill="none"
     stroke="currentColor" stroke-width="1.5"
     stroke-linecap="round" stroke-linejoin="round">
  ...
</svg>
```

---

## Visual Hierarchy Principles

Five rules that must never be broken:

1. **One H1 per screen.** Every page has a single, unambiguous primary heading. If you are tempted to use two H1s, you have two pages.

2. **Contrast before size.** A 13px label in `#101828` reads as more important than a 16px label in `#98A2B3`. Use weight and color to lead the eye before reaching for larger type.

3. **Empty space is structure.** Whitespace between elements communicates grouping. Elements that belong together have less space between them than elements that do not. This is more reliable than borders or dividers.

4. **Primary color is a promise.** When users see `#6C4CF1`, they know they can act. If a purple element is not interactive, it breaks trust. Purple means clickable.

5. **Status must be immediately readable.** Pass status (issued / used / revoked) must be visible without reading — the badge dot color alone should communicate state at a glance. The text confirms; the color announces.

---

## Responsive Breakpoints

| Name | Width | Layout |
|------|-------|--------|
| Mobile | < 640px | Single column, fixed bottom tabs, stacked forms |
| Tablet | 641px–1023px | Two columns where space allows, no sidebar, fixed bottom tabs |
| Desktop | ≥ 1024px (`lg:`) | Full 240px fixed sidebar, multi-column content |
| Wide | ≥ 1280px | Max-width 1280px content centered |

Specific breakpoint behaviors:

| Breakpoint | Changes |
|-----------|---------|
| `max-width: 1023px` | Fixed bottom navigation appears; main content gets extra bottom padding |
| `max-width: 860px` | Login panel stacks to single column |
| `max-width: 767px` | Listing header stacks; attendee item stacks; pager stacks; table gets horizontal scroll |
| `max-width: 640px` | Upload dropzone collapses to 2-column; top action controls stack into a two-column/mobile-friendly grid; public verification panel gets tighter padding |

---

## Do & Don't

| Do | Don't |
|----|-------|
| Use Inter at defined weights (400, 500, 600, 700) | Mix system fonts or use weights outside the scale |
| Use `#6C4CF1` only for interactive elements | Use primary purple decoratively on non-interactive UI |
| Use `#FFB5A7` accent sparingly in pass design | Apply accent color to text or functional UI elements |
| Communicate standard elevation through background contrast and borders | Add decorative shadows to cards or layout sections |
| Use 1px borders on all elevated surfaces | Use borderless cards on a white page background |
| Pair every status badge color with a text label | Use color alone to communicate state |
| Maintain 4px spacing multiples throughout | Use arbitrary values like 7px, 11px, 13px for spacing |
| Use positive letter-spacing only for uppercase labels/captions | Apply negative tracking to any text |
| Suppress all animation when `prefers-reduced-motion` is set | Ignore reduced-motion preferences |

---

## CSS Custom Properties — Quick Reference

```css
/* Backgrounds */
--bg:              #F7F8FC;   /* Page */
--surface:         #FFFFFF;   /* Cards, inputs */
--surface-soft:    #F7F8FC;   /* Table header, soft input bg */
--sunken:          #EDEEF4;   /* Inset panels */

/* Text */
--text:            #101828;
--text-secondary:  #344054;
--muted:           #667085;
--disabled:        #98A2B3;

/* Primary */
--primary:         #6C4CF1;
--primary-hover:   #5A3DD4;
--primary-active:  #4A2FB8;
--primary-subtle:  #EDE9FD;
--primary-border:  #C4B5FA;

/* Accent */
--accent:          #FFB5A7;
--accent-subtle:   #FFF0ED;
--accent-border:   #FFCFC7;

/* Borders */
--border:          #E4E7EC;
--border-strong:   #D0D5DD;

/* Semantic */
--success:         #027A48;   --success-bg: #ECFDF3;   --success-border: #ABEFC6;   --success-dot: #12B76A;
--warning:         #B54708;   --warning-bg: #FFFAEB;   --warning-border: #FEDF89;   --warning-dot: #F79009;
--error:           #B42318;   --error-bg:   #FEF3F2;   --error-border:   #FECDCA;   --error-dot:   #F04438;
--info:            #1D4ED8;   --info-bg:    #EFF6FF;   --info-border:    #BFDBFE;
```

---

*PassForge Design System · v1.0 · Quiet surfaces. Clear hierarchy.*
