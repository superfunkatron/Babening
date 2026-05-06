Date: 6 May 2026

# **Bug Fixes**

**Venues tab restored to Edit Mode**

The venues tab button was missing entirely from the tab bar HTML — dropped during the April 28 UI redesign. The CSS and panel were intact; only the button itself was gone. Diagnosed by inspecting the .edit-only-tab CSS rule and then checking the HTML tab bar. Fixed by adding the missing button back after the Other tab:

<button class="tab-btn edit-only-tab" id="tab-venues" onclick="switchTab('venues')">

  <span class="tab-icon">🏠</span>

  <span class="tab-label">Venues</span>

  <span class="tab-check">&nbsp;</span>

</button>

**Duplicate Edit button removed from header**

Two identical Edit buttons were present in the header HTML, both with the same id (editToggleBtn) and both calling toggleEditMode(). Caught before committing. One was deleted, leaving a single valid button.

**Stale duplicate venues panel removed from history tab**

A full copy of the venues panel HTML (id="panel-venues") was sitting inside panel-history — a leftover from an earlier restructure. It was inert but added dead weight to the file. Removed entirely.

# **UI Redesign — History / Log Tab**

The history/log tab has been brought in line with the new design language established in the April 28 session. The approach was clean, readable, and utilitarian — matching the function of a log rather than competing with the workout cards for visual energy.

**Chart tabs**

Restyled to match the main tab bar — card-style with rounded corners, dark active state (#1a1a1a background with white text), Barlow font replacing DM Mono, emoji added to Sessions and Weekly/Monthly tabs. Neon green active state retired.

**Session entries**

Dark header bar (#1a1a1a) added to each session entry, matching the exercise card pattern. Day name moved to Barlow bold white, date in muted DM Mono. Stats row (Lifts / Total kg / Reps) given full-width treatment with dividing borders between stats rather than loose gap spacing. Exercise rows tightened with consistent border separators. PR entries retain gold colouring. Cardio entries retain orange colouring.

**PR list**

Dark header bar added to the PR wrap, matching session entry headers. PR title moved from Bebas Neue neon to Barlow bold gold. Row separators tightened to match session entry rows.

**Export / Import buttons**

Simplified — transparent background, muted border, no hover state (touch device). Active state gives subtle feedback. Clutter reduced.

# **Decisions Made**

- Diagnose before code — the missing venues tab was identified step by step (CSS check, then HTML check) before any fix was proposed. This approach is working well and will be maintained.

- Clean, readable, utilitarian — the design direction chosen for the history tab. Correct for a log. The workout cards carry the visual energy; the log should be easy to read.

- Raw GitHub URL for file access — established that the raw.githubusercontent.com URL can be used to fetch the current file directly, avoiding the need to paste large chunks. Note: GitHub's CDN can lag behind commits, so the fetched version may be slightly behind the latest commit.

**Date: 28 April 2026**

**Bug Fixes**

- Fixed updateProgress crashing on tab switch with a null guard — the function was firing before Supabase data had loaded, causing Cannot read properties of null errors on every tab change

- Fixed "null" value console error on number inputs by replacing || with ?? null coalescing across hero value inputs in buildCardHTML

**New Feature: Strength Progression Chart**

- Added renderStrengthChart() modelled directly on the existing cardio chart pattern

- Pulls all unique strength exercises from session history dynamically — only shows exercises you've actually logged

- Plots top weight per session over time with date labels

- Added as a new tab in the history/log section alongside the cardio chart

- Wired into switchHistoryTab() and added the HTML panel and tab button

**UI Redesign — Phase 1: Exercise Cards**

Full redesign of the exercise card component:

- Dark header with white exercise name, replacing the old inline neon text style

- Hero weight number dominates the card — large, immediately readable under gym lighting

- Sets/reps/volume condensed into a clean sub-line below the hero number

- Last session and suggested next weight shown as context chips

- PR gold strip at the top of the card when a personal record is active

- Tap card to activate — hero number becomes an inline editable input with +/− either side, no separate adjuster section

- ··· button opens the details panel for machine settings, how-to guide, edit fields, find swaps, rest timer

- Done state dims the card cleanly

- Cardio cards follow the same pattern with distance/watts as the hero number

- Pinch-to-zoom re-enabled by removing maximum-scale=1.0 from the viewport meta tag

- Old .card-content, .meta-pill, .card-main, .pr-badge etc. retired and replaced with new structure

**UI Redesign — Phase 2: Page Chrome**

- Header updated — stays dark/black across all themes, edit button becomes a solid pill style

- Tab bar redesigned — card-style tabs with emoji icon, label, and count; active tab goes dark to match card headers

- Day title redesigned — dropped the giant neon Bebas Neue treatment, replaced with clean bold Barlow title in body text colour

- Venue row updated — green dot replacing the pin emoji, cleaner label styling

- --muted colour values corrected in dark (#555 → #999) and dim (#2e2e2e → #666) themes — secondary text was near-invisible against dark backgrounds

**Decisions Made**

- Session consistency tracker (sessions per week chart) — removed from roadmap, adds no value over the existing log

- JSON export/import — kept as-is, reframed as an emergency escape hatch rather than a sync mechanism, no action needed

- 120-session history cap — still backlog, not urgent for several months yet

