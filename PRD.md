# PassForge — Product Requirements Document

**Product:** PassForge  
**Type:** Web Application  
**Version:** 1.0 MVP  
**Status:** In Development

---

## 1. Overview

PassForge is a lightweight web application that enables event organizers to create branded digital event passes with scannable QR codes. It targets small to medium-sized events — meetups, weddings, workshops, conferences, and private gatherings — where organizers need professional-looking passes without requiring advanced design skills or a dedicated backend.

The application covers the full pass lifecycle: event setup, attendee onboarding, pass issuance, export and sharing, and real-time entry verification.

---

## 2. Problem Statement

Event organizers today face a fragmented workflow: design tools for the pass visual, spreadsheets for the attendee list, a separate QR generator, and no standardized way to verify passes at the door. For small and mid-size events, dedicated ticketing platforms are overkill and often expensive.

**PassForge consolidates this into one focused workspace:**
- Generate unique, scannable QR passes per attendee
- Brand passes to match the event's visual identity
- Export passes in formats attendees can receive and print
- Validate entry in real time without a dedicated scanning device or backend

---

## 3. Goals

| Goal | Description |
|------|-------------|
| Speed to first pass | An organizer should be able to create an event and generate a pass in under 2 minutes |
| Zero setup friction | No installation, account creation required to start; runs in any modern browser |
| Professional output | Exported passes should look polished enough to send to attendees directly |
| Reliable verification | Verifiers should be able to confirm a pass's validity and mark it used from any device |
| Multi-event support | Organizers running multiple events simultaneously should not experience data bleed between them |

---

## 4. Users

### 4.1 Primary — Event Organizer
Creates and manages events, adds or imports attendees, customizes pass design, and exports or shares passes. May also perform verification duties at the door.

### 4.2 Secondary — Door Staff / Verifier
Uses the verification interface at the event entrance to validate QR payloads and mark passes as used. Does not need to manage events or attendees.

---

## 5. User Stories

### Organizer
- As an organizer, I want to create a new event with a name, date, time, and venue so that I can start generating passes for it.
- As an organizer, I want to customize the pass brand color and template so that passes reflect my event's visual identity.
- As an organizer, I want to upload a banner image so that the pass has a custom cover section.
- As an organizer, I want to add attendees one at a time or import them from a CSV so that I can handle both small lists and large ones efficiently.
- As an organizer, I want to assign ticket types (General Admission, VIP, Speaker, Staff, Guest) so that passes clearly indicate what access level an attendee has.
- As an organizer, I want to preview the pass in real time as I edit event details so that I can see exactly what attendees will receive.
- As an organizer, I want to download a pass as PNG or PDF so that I can send it to the attendee.
- As an organizer, I want to copy a shareable verification link so that I can share the pass via any messaging channel.
- As an organizer, I want to open an email pre-filled with the attendee's pass link so that I can distribute passes from my existing email client.
- As an organizer, I want to regenerate a pass so that I can invalidate a compromised or lost pass and issue a fresh one.
- As an organizer, I want to manage multiple events from the same workspace so that I don't have to reset the app between events.
- As an organizer, I want a dashboard showing key metrics (events, attendees, issued passes, used passes) so that I can monitor pass issuance at a glance.

### Verifier
- As a verifier, I want to paste a QR payload or pass ID and instantly see whether the pass is valid so that I can make fast entry decisions.
- As a verifier, I want to see clear visual feedback (green/amber/red) on verification outcome so that I can read the result at a glance under any lighting conditions.
- As a verifier, I want to mark a valid pass as used with one action so that duplicate entries are prevented.
- As a verifier, I want the app to auto-verify a pass when I open a shared verification link so that I can verify passes from messaging apps without manual input.
- As a verifier, I want expired and revoked passes to be clearly distinguished from simply-used ones so that I can communicate the right message to the attendee.

---

## 6. Feature Requirements

### 6.1 Authentication

| # | Requirement |
|---|-------------|
| AUTH-1 | The application must present a login screen before granting access to the workspace |
| AUTH-2 | The login form must accept an email and password |
| AUTH-3 | Invalid credentials must display a clear inline error message |
| AUTH-4 | Successful login must transition directly to the dashboard with a confirmation toast |
| AUTH-5 | The prototype may persist the local authentication flag with settings; production authentication must replace this with a real session model |
| AUTH-6 | The user must be able to sign out from both the sidebar and the Settings view |
| AUTH-7 | The organizer profile name and email must be user-editable and must persist in local storage |

### 6.2 Dashboard

| # | Requirement |
|---|-------------|
| DASH-1 | The dashboard must display four summary metrics: total events, total attendees, issued pass count, used pass count |
| DASH-2 | The dashboard must list all events in a searchable, paginated table (6 rows per page) |
| DASH-3 | Event rows must show event name, venue, date/time, total attendees, and used pass count |
| DASH-4 | Each event row must provide a direct link to open that event's management view |
| DASH-5 | A selected-event detail panel must show organizer, venue, description, and quick-action links to Attendees and Verify |
| DASH-6 | When no events exist, the events panel must show a contextual empty state with a "Create event" call to action |

### 6.3 Event Management

| # | Requirement |
|---|-------------|
| EVT-1 | The user must be able to create a new event from the top navigation bar on any view |
| EVT-2 | New events must be created with default values and immediately opened in the Event view for editing |
| EVT-3 | Event fields: name, organizer, start date (date picker), start time (time picker), end date (date picker), end time (time picker), venue/location (text), description (textarea) |
| EVT-4 | Branding and state fields: brand color (color picker), pass template selector (Classic / Ribbon / Compact / Formal), event status selector (Active / Expired) |
| EVT-5 | The user must be able to upload an optional banner/cover image (PNG, JPG, or WebP); stored as base64 |
| EVT-6 | All field changes must update the pass preview in real time with no save action required |
| EVT-7 | The user must be able to remove the banner image via a dedicated remove action with a confirmation dialog |
| EVT-8 | The user must be able to delete an event; deletion must cascade to all associated attendees |
| EVT-9 | Event deletion must require a confirmation dialog before executing |
| EVT-10 | The active event must be selectable from a dropdown in the top navigation bar visible on all views |

### 6.4 Attendee Management

| # | Requirement |
|---|-------------|
| ATT-1 | The user must be able to add an attendee with: full name (required), email address (optional), ticket type |
| ATT-2 | Ticket types available: General Admission, VIP Access, Speaker, Staff, Guest |
| ATT-3 | Each new attendee must be automatically assigned a unique pass ID (format: `PASS-XXXXXX`) and a status of Issued |
| ATT-4 | The attendee list must be searchable by name, email, ticket type, or pass ID |
| ATT-5 | The attendee list must be paginated at 6 per page with prev/next navigation |
| ATT-6 | Selecting an attendee from the list must populate the details panel for editing |
| ATT-7 | The user must be able to edit an attendee's name, email, ticket type, and status in-place |
| ATT-8 | Pass status must be manually settable to: Issued, Used, Expired, Revoked |
| ATT-9 | The user must be able to delete an attendee after confirmation |
| ATT-10 | The application must support bulk CSV import using the format: `Name, Email, Type` |
| ATT-11 | CSV import must skip a header row if present; `Type` defaults to General Admission if omitted |
| ATT-12 | Post-import, a toast must confirm how many attendees were added |
| ATT-13 | When no attendees exist, the view must show an empty state with an "Add sample attendee" shortcut |

### 6.5 Pass Generation & Export

| # | Requirement |
|---|-------------|
| PASS-1 | Each attendee must have a unique QR pass generated automatically upon creation |
| PASS-2 | The QR code payload must follow the format: `PF\|event:{id}\|attendee:{id}\|pass:{passId}` |
| PASS-3 | The pass preview must render: event banner (if set), brand color header, organizer, event name, date, time, venue, attendee name, email, ticket type, QR code, pass ID, and status badge |
| PASS-4 | Pass templates must alter the card's border-radius and footer treatment (Classic, Ribbon, Compact, Formal) |
| PASS-5 | The QR code must update any time the pass ID or event data changes |
| PASS-6 | The user must be able to download the pass as a PNG at 3× retina resolution |
| PASS-7 | The user must be able to download the pass as a PDF sized to match the pass card dimensions |
| PASS-8 | The user must be able to copy a shareable verification URL to the clipboard |
| PASS-9 | The shareable URL must encode the QR payload in the URL hash so recipients can open it directly to a verified state |
| PASS-10 | The user must be able to trigger an email compose window pre-filled with the attendee name, event name, pass link, and pass ID |
| PASS-11 | The user must be able to regenerate a pass, which creates a new passId and resets status to Issued |
| PASS-12 | The pass list table must be searchable by name, email, ticket type, status, pass ID, or verification link |

### 6.6 QR Verification

| # | Requirement |
|---|-------------|
| VER-1 | The verification interface must accept a full QR payload or a bare pass ID as input |
| VER-2 | On page load, if the URL hash contains `#verify=<payload>`, the app must run verification automatically; signed-in organizers are routed to the Verify view, while signed-out users see a public verification panel |
| VER-3 | Verification result — Valid: green state, attendee name, event name and ticket type, "Mark as used" button |
| VER-4 | Verification result — Already Used: amber warning state, attendee name, event and ticket type, timestamp of when it was used |
| VER-5 | Verification result — Expired: red error state; if the event end date/time has passed, or the event is manually set to Expired, passes that are not Revoked must fail verification |
| VER-6 | Verification result — Revoked: red error state with "Invalid" label |
| VER-7 | Verification result — Not Found/Unavailable: red error state explaining that no local attendee record matches the submitted payload or pass ID |
| VER-8 | "Mark as used" must set the attendee's status to Used, record the current timestamp, and immediately re-verify to refresh the displayed state |
| VER-9 | A "Try Current Pass" shortcut must pre-fill the input with the currently selected attendee's payload |
| VER-10 | The selected attendee's pass preview must be visible alongside the verification form |

### 6.7 Settings

| # | Requirement |
|---|-------------|
| SET-1 | The user must be able to switch between Light, Dark, and System themes |
| SET-2 | Theme preference must persist in local storage and be applied on page load |
| SET-3 | System theme must respond to `prefers-color-scheme` changes dynamically |
| SET-4 | The user must be able to edit their organizer profile name |
| SET-5 | The user must be able to edit the login email associated with the profile |
| SET-6 | The user must be able to reset the entire workspace (clears all events and attendees) from the sidebar |

---

## 7. Navigation & Layout

| Requirement | Description |
|-------------|-------------|
| NAV-1 | On large screens (≥1024px), a fixed left sidebar must show the PassForge brand mark, navigation links, user profile, Sign out, and Reset workspace |
| NAV-2 | On small screens (<1024px), navigation must be rendered as a fixed bottom tab bar with Dashboard, Event, Attendees, Passes, Verify, and More |
| NAV-3 | The top bar must always show the active page title, an event selector dropdown when events exist, a create-event button labeled "Event", and a theme toggle |
| NAV-4 | Navigation links: Dashboard, Event, Attendees, Passes, Verify, Settings |
| NAV-5 | View transitions must use a fade + vertical slide animation |

---

## 8. Data Model

### Event
| Field | Type | Notes |
|-------|------|-------|
| `id` | String | `EVT-XXXXXX` (random base-36) |
| `name` | String | |
| `organizer` | String | |
| `date` | String | `YYYY-MM-DD` |
| `time` | String | `HH:MM` |
| `endDate` | String | `YYYY-MM-DD`; defaults to the event date |
| `endTime` | String | `HH:MM`; defaults to `23:59` |
| `status` | String | `Active` \| `Expired` |
| `location` | String | |
| `description` | String | |
| `color` | String | Hex color, default `#6C4CF1` |
| `template` | String | `Classic` \| `Ribbon` \| `Compact` \| `Formal` |
| `banner` | String | Base64 data URI or empty string |

### Attendee
| Field | Type | Notes |
|-------|------|-------|
| `id` | String | `ATT-XXXXXX` |
| `eventId` | String | Foreign key → Event.id |
| `name` | String | Required |
| `email` | String | Optional |
| `type` | String | `General Admission` \| `VIP Access` \| `Speaker` \| `Staff` \| `Guest` |
| `status` | String | `Issued` \| `Used` \| `Expired` \| `Revoked` |
| `passId` | String | `PASS-XXXXXX` |
| `usedAt` | String | Locale timestamp string, or empty string |

### Settings (persisted)
| Field | Type | Notes |
|-------|------|-------|
| `theme` | String | `Light` \| `Dark` \| `System` |
| `profileName` | String | |
| `profileEmail` | String | |
| `authenticated` | Boolean | Prototype-only local auth flag persisted with settings |

---

## 9. Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| Performance | Pass preview and QR code must re-render within 300ms of any input change |
| Responsiveness | All views must be fully usable on mobile (≥320px width) and desktop |
| Accessibility | All interactive elements must be keyboard-accessible; form fields must have visible labels; reduced motion must be respected |
| Persistence | All event and attendee data must survive page refresh via localStorage |
| Theme | Dark mode must apply to all surfaces without visual regressions |
| Export quality | PNG export must render at 3× (retina) resolution with a white background |
| Animation | View transitions, card entrances, and pass animations must be suppressed when `prefers-reduced-motion` is set |

---

## 10. Pass Templates

| Template | Border Radius | Footer |
|----------|--------------|--------|
| Classic | 24px all corners | Primary-subtle (light purple) |
| Ribbon | 24px top / 8px bottom | Primary-subtle |
| Compact | 12px all corners | Primary-subtle |
| Formal | 4px all corners | Light grey (`#F7F8FC`) |

---

## 11. QR Payload Specification

**Encoded payload:**
```
PF|event:{eventId}|attendee:{attendeeId}|pass:{passId}
```

**Shareable verification URL:**
```
{origin}{pathname}#verify={encodeURIComponent(payload)}
```

On page load, if the URL hash matches `/verify=(.+)$/`, the application must decode it, navigate to the Verify view, and execute verification automatically.

---

## 12. Pass Status Lifecycle

```
[Created] -> Issued
Issued -> Used        (scanned and marked used at entry)
Issued -> Expired     (manually invalidated by organizer or set by status controls)
Issued -> Revoked     (manually invalidated by organizer)
Used   -> (terminal)
Expired -> (terminal)
Revoked -> (terminal)
```

Event-level expiry: during verification, if the event end date/time is in the past or the event status is set to Expired, the pass fails with an expired result unless the attendee pass is Revoked.

---

## 13. Tech Stack

| Library | Version | Role |
|---------|---------|------|
| Vue 3 | latest | UI framework, Composition API |
| Tailwind CSS | latest | Utility-first styling |
| QRCode.js | 1.0.0 | QR code canvas rendering |
| html2canvas | 1.4.1 | Pass card screenshot for export |
| jsPDF | 2.5.1 | PDF generation from canvas |
| Inter (Google Fonts) | — | Primary typeface |

All dependencies loaded via CDN. No build toolchain required.

---

## 14. Out of Scope — v1.0

The following are explicitly excluded from this version and may be considered for a future release:

- Backend persistence or cloud sync
- Real email delivery (current implementation opens `mailto:` only)
- Camera-based QR scanning
- Bulk pass export (download all attendees at once)
- Role-based access control or multi-user collaboration
- Attendee self-service check-in portal
- Analytics beyond the four dashboard metrics
- Offline-first / PWA support
