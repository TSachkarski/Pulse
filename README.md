# Pulse — Daily Wellness for Remote Workers

A high-fidelity mobile wellness prototype designed for remote workers who have lost the natural emotional signals that physical offices provided. No commute to decompress. No walk between meetings. No casual read of the room. Pulse rebuilds that awareness — quietly, privately, in under two minutes a day.

---

## Why This Exists

Remote work is structurally hostile to emotional self-awareness. The environmental cues that used to signal transition — the commute, the office floor, the end-of-day walk to the car — are gone. What replaces them is a continuous, undifferentiated stream of screen time, where work stress and rest blur together.

The existing wellness app landscape responds to this with one of two approaches: clinical tracking (graphs, scores, streaks that feel like performance metrics) or motivational fluff (daily affirmations and generic breathing prompts). Neither addresses the actual problem: people don't know how they feel, or why, or what to do about it.

Pulse is designed around a third position — *emotional awareness as a daily practice*, not a measurement exercise. The check-in takes 90 seconds. It names your state, connects it to what's driving it, offers one evidence-based action, and reflects your pattern back to you over time. That's the whole product.

---

## Design Decisions

### The Mood Blob

The home screen is built around a single dominant element: an animated organic blob that breathes at rest and transforms in colour and shape after each check-in. This is not decoration. The blob externalises an internal state — it gives the user something to look at that mirrors how they feel. After a check-in, the home screen shifts its entire ambient colour to match the emotional state. Good days tint green. Stretched days tint amber.

The decision to make the blob the undisputed hero — removing competing cards, hiding stats until after the first check-in — came from a clear brief: remote workers need one signal at a time. A dashboard of empty widgets is the opposite of what someone who is already overwhelmed needs to see.

### Four States, Not Ten

Most mood tracking apps offer 5–10 emotional options, which creates decision paralysis at the moment of lowest cognitive bandwidth. Pulse uses four: **Good**, **Calm**, **Stretched**, **Heavy**.

These four were chosen because they cover the practical range of remote worker experience without requiring introspection. You don't need to know the difference between anxious and stressed — you know if you're stretched. You know if you're heavy. The simplicity is the point.

Each state has its own visual language — a distinct waveform icon, a colour, a gradient, a set of follow-on suggestions and CBT reframe prompts grounded in published research.

### The Waveform Icon System

The state icons were designed from scratch rather than sourced from any library. They use a single vocabulary — a horizontal pulse line — whose character changes to communicate each emotional state.

- **Good** — a tall, confident single spike. Energy up, decisive.
- **Calm** — small, even, low-amplitude undulation. Steady rhythm.
- **Stretched** — rapid compressed noise across the full width. No space between demands.
- **Heavy** — one slow weighted dip. Gravity.

The system works because the name of the app is *Pulse*. The waveform is the brand mark. Every icon is the brand mark, expressed differently.

### Check-In Structure

The six-question check-in was designed to respect cognitive load at the time it's most likely to be used — mid-afternoon, between meetings, when energy is already spent.

1. **Emotional state** — four tiles, tap once.
2. **Focus score** — a draggable arc ring and slider. Physical interaction grounds the abstract rating.
3. **Contributing factors** — chips, multi-select, skip available.
4. **Lifestyle tracking** — sleep, water, exercise, meals. Tap to increment. No typing.
5. **Gratitude log** — three open text inputs. Research shows specificity is what makes gratitude practice effective, so three distinct prompts rather than one general field.
6. **Freeform note** — fully optional.

The progress bar uses a shimmer animation during the check-in to communicate active process. Each step transition is kept under 300ms.

### Summary Screen

The summary screen is the emotional centrepiece of the app. It was designed around a single question: *what does it feel like to know how you feel?*

The answer is a full-bleed state-coloured gradient, a large breathing blob, and a 52px wellness percentage that counts upward from zero when the screen opens. Below it: "wellness score today" — one line that makes the number legible without over-explaining it.

The percentage is not a performance score. It is a *translation* — Good + high focus produces ~85%, Heavy + low focus produces ~28%. The formula is calibrated so the number feels honest, not aspirational.

### Navigation

The bottom navigation uses icons only, no labels. This was a deliberate restraint decision. Labels at tab bar scale create competing weight between text and icon. An icon-only bar forces each icon to be legible on its own, which produces better icons. The active state is a single signal: a soft brand-coloured pill behind the icon. No lift, no glow, no underline pip.

### Evidence-Based Copy

Every suggestion, quote, and insight in Pulse cites a real mechanism or study. "A 5-minute walk before your next meeting resets your cortisol" becomes "physical movement cuts perceived stress by up to 40%." The difference matters. Specific claims build trust. Generic affirmations erode it.

Sources referenced throughout: Andrew Huberman on ultradian rhythms, Tony Schwartz on energy management, Martin Seligman's gratitude research at Penn, Stanford breathing studies on vagal activation, Csikszentmihalyi on flow states, MIT Work Lab on remote worker isolation.

---

## Design System

### Typography

Two font families. Three roles.

| Font | Role |
|---|---|
| DM Serif Display | Headlines, hero numbers, emotional content |
| DM Sans | Body text, UI labels, buttons |
| DM Mono | Data labels, timestamps, monospaced metadata |

**UI scale — 5 tokens:**

| Token | Size | Use |
|---|---|---|
| `--t-xs` | 10px | Mono labels, tags |
| `--t-sm` | 13px | Body, captions, chips |
| `--t-md` | 16px | UI text, buttons |
| `--t-lg` | 28px | Section headlines |
| `--t-xl` | 52px | Hero display |

**Display scale — 8 tokens** for stats, scores, and large numerals: `--d-xs` through `--d-2xl` (18px → 80px).

### Colour

One warm neutral base. Four emotional state colours. One brand.

```
Base         --bg: #F5F1EA       --surface: #FFFFFF
Ink          --ink-1 through --ink-5  (#1A1714 → #C8C2BA)
Brand        --brand: #5855D6
State G      --G: #2DB87A   (Good — green)
State C      --C: #3D9BE8   (Calm — blue)
State S      --S: #F07040   (Stretched — amber)
State H      --H: #E0609A   (Heavy — rose)
```

Each state colour has three variants: base, `--X-a12` (12% alpha background), `--X-a25` (25% alpha border). Every colour in the app is a named CSS token — zero hardcoded hex values outside the `:root` definition.

### Spacing

8px grid throughout. Six tokens: `--s8` through `--s64`. All component gaps, margins, and paddings are multiples of 8 or explicit 4px micro-gaps for optical alignment.

### Shadows

Three levels: `--sh-s` (cards), `--sh-m` (elevated elements), `--sh-l` (overlays). All use layered box-shadows with two values for natural depth.

### Border Radius

Five tokens from `--r-s:10px` to `--r-pill:999px`. Section headers use `border-radius:0 0 var(--r-xl) var(--r-xl)` — a rounded-bottom treatment that creates a visual break between the header and scrollable content. All eight section headers use this consistently.

---

## Screen Inventory

| Screen | Purpose |
|---|---|
| Onboarding (4 slides) | Product intro + name input |
| Home | Mood hero, week strip, CTA, recent entries |
| Check-in | 6-step guided check-in flow |
| Summary | Full-bleed emotional state + wellness score |
| Breathe | Standalone breathing tool — Box 4-4-4, 4-7-8, 5-5 |
| Trends | Dominant stat hero, correlations, week view, focus chart, heatmap |
| History | Entry log with mini mood chart, expandable entries |
| Settings | Notifications, check-in prefs, profile, data export |

---

## Interactions

52 JavaScript functions covering:

- Emotional state selection with colour-flood tile animation
- Focus arc ring — draggable, touch and mouse support
- Lifestyle tracking with segmented dot progress
- Week strip built dynamically from the current day — future days stay empty
- Summary percentage count-up from zero on screen entry
- Streak pill bounce on milestone completion
- Focus bar chart animation with `requestAnimationFrame` for correct transition timing
- Heatmap with day-number overlay and tap-to-detail bottom sheet
- Breathing timer with three clinical patterns and automatic phase sequencing
- Settings toggle persistence via `localStorage`
- Reminder time picker with AM/PM selection
- Data export (JSON) and full data deletion with confirmation guard
- Check-in abandon confirmation after step 1

---

## Technical

**Single-file HTML.** The entire application — CSS design system, HTML structure, and JavaScript — ships in one 162KB file. No build tools, no dependencies, no frameworks. Opens in any browser, works offline, requires no server.

**Responsive.** On mobile it fills the viewport. On desktop and tablet it renders as a centred 420px phone frame with `border-radius:48px` and a layered box-shadow. The bevel area is handled through `env(safe-area-inset-top)` on iOS — fake status bar elements are hidden on real devices, shown only in the desktop frame view.

**Privacy by design.** All data (`localStorage` only) stays on the device. No network requests. No analytics. No tracking. The privacy statement in-app is accurate: "Deleting the app removes everything."

---

## Prototype Scope

This is a design prototype, not a production application. It demonstrates the complete user experience with realistic data, working interactions, and a fully implemented design system. Actual check-in entries are not persisted between sessions — the history and trends screens use representative demo data to show the intended pattern-recognition experience.

The prototype is a complete design artefact. It is not a minimum viable product.

---

## Typeface Credits

DM Serif Display, DM Sans, DM Mono — designed by Colophon Foundry for Google Fonts. Used under SIL Open Font License.

---

*Pulse — Portfolio project 04*  
*Trajche Sachkarski · UX/UI Design*
