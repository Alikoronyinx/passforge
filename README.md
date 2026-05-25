# PassForge

**Event QR Pass Generator** — create branded digital passes with scannable QR codes for any event. Manage attendees, customize pass design, export passes, and verify entry at the door from one focused workspace.

---

## Overview

PassForge is built for event organizers running small to mid-size events — meetups, workshops, conferences, weddings, private gatherings. It covers the full pass lifecycle end-to-end: event setup, attendee management, pass issuance and export, and real-time entry verification.

No installation. No build step. Works in any modern browser.

---

## Getting Started

Open `index.html` in your browser. Sign in with the demo credentials:

```
Email:    demo@passforge.app
Password: passforge123
```

From the **Dashboard**, create your first event with the **+ Event** button in the top bar. Add attendees, preview passes, and start verifying — all from the same screen.

---

## Features

### Event Management
- Create and manage multiple events simultaneously
- Per-event fields: name, organizer, start date/time, end date/time, event status, venue, description
- Brand color picker and pass template selector applied to all passes for that event
- Optional banner/cover image (PNG, JPG, or WebP)
- Live pass preview updates as you type — no save needed
- Delete events with full attendee cascade

### Attendee Management
- Add attendees individually: name, email, and ticket type
- Ticket types: General Admission, VIP Access, Speaker, Staff, Guest
- Edit or delete attendees in-place
- Manually override pass status: Issued, Used, Expired, Revoked
- Search attendees by name, email, ticket type, or pass ID
- Bulk CSV import — paste rows as `Name, Email, Type`

### QR Passes
- Every attendee gets a unique, scannable QR pass on creation
- Pass templates: Classic, Ribbon, Compact, Formal
- Download individual passes as **PNG** (3× retina) or **PDF**
- Copy a shareable **verification link** to clipboard
- Open a pre-filled **email composer** with the pass link and pass ID
- Regenerate a pass to invalidate the old one and issue a fresh ID

### Entry Verification
- Paste a QR payload or bare pass ID to verify entry instantly
- Open a shared verification URL to auto-verify on page load
- Outcomes: Valid · Already Used · Event Expired · Expired · Invalid · Unavailable
- "Mark as used" stamps the entry with a timestamp in one tap
- Event-level expiry is detected automatically during verification

### Workspace
- Dashboard with four summary metrics: events, attendees, issued passes, used passes
- Persistent storage — events and attendees survive page refresh
- Light, Dark, and System (auto) themes
- Reset workspace to clear all data and start fresh

---

## Views

| View | Purpose |
|------|---------|
| **Dashboard** | Metrics summary, event list with search and pagination, selected event detail |
| **Event** | Edit event details, branding, and pass template; live preview with export controls |
| **Attendees** | Add, edit, search, and import attendees; per-attendee status management |
| **Passes** | Full pass list with search; per-pass preview, export, share, email, and regenerate |
| **Verify** | QR payload input, verification result, mark as used |
| **Settings** | Theme selector, organizer profile |

---

## Pass Templates

| Template | Style |
|----------|-------|
| Classic | Fully rounded corners (24px), purple footer |
| Ribbon | Rounded top, squared bottom — good for lanyards |
| Compact | Smaller radius, tighter layout |
| Formal | Near-square corners (4px), neutral grey footer |

---

## CSV Import Format

```csv
Name,Email,Type
Ava Cole,ava@example.com,VIP Access
Ben Marsh,ben@example.com,General Admission
Sam Diaz,sam@example.com,Speaker
```

- Header row is detected and skipped automatically
- `Type` defaults to **General Admission** if the column is omitted
- `Email` is optional per row

---

## Verification URL

Each pass generates a shareable URL of the form:

```
https://yourhost/index.html#verify=PF%7Cevent%3A...
```

Opening this URL in any browser runs the check automatically. If the organizer workspace is already signed in, the app opens the Verify view with the pass preloaded. If the workspace is signed out, PassForge shows a public pass verification screen first.

Note: this MVP stores records locally in the organizer's browser. A shared verification link can only be fully validated in a browser that has the relevant PassForge workspace data.

---

## Ticket Status Lifecycle

```
Issued → Used       Scanned and marked at entry
Issued → Expired    Event has ended or was manually expired
Issued → Revoked    Manually invalidated by organizer
```

Event expiration is based on the event end date/time, or an event status manually set to **Expired**. Older saved events are normalized with an end time of `23:59` and status `Active`.

---

## Tech Stack

| Library | Purpose |
|---------|---------|
| [Vue 3](https://vuejs.org) | Reactive UI, Composition API |
| [Tailwind CSS](https://tailwindcss.com) | Utility-first styling |
| [QRCode.js](https://github.com/davidshimjs/qrcodejs) | QR code generation |
| [html2canvas](https://html2canvas.hertzen.com) | Pass card capture for export |
| [jsPDF](https://github.com/parallax/jsPDF) | PDF generation |
| Inter (Google Fonts) | Typography |

All libraries loaded from CDN. No package manager, no bundler.

---

## File Structure

```
passforge/
├── index.html    # Full application — HTML, CSS, and JavaScript
├── README.md     # This file
├── PRD.md        # Full product requirements document
└── styles.md     # Design system and CSS reference
```

---

## Storage

All data is stored in `localStorage` under the key `passforge-mvp-v2`. The current single-file prototype stores the local authentication flag alongside theme and profile settings, so a signed-in workspace may stay signed in across refreshes until the user signs out.

To clear all data: use **Reset workspace** in the sidebar, or run `localStorage.clear()` in the browser console.

Persisted shape:

```json
{
  "settings": {
    "theme": "System",
    "profileName": "Alex Rivers",
    "profileEmail": "demo@passforge.app",
    "authenticated": false
  },
  "selectedEventId": "EVT-XXXXXX",
  "selectedAttendeeId": "ATT-XXXXXX",
  "events": [],
  "attendees": []
}
```
