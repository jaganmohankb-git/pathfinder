# PathFinder India 🧭

**Free, private, multilingual career guidance for students completing 10th & 12th in India**

→ **Live tool:** https://jaganmohankb-git.github.io/pathfinder/

---

## What it does

PathFinder helps students and parents make a better career decision at the two most critical moments in Indian education:

- **After 10th:** Science / Commerce / Arts / Vocational / Diploma — which stream and why, including underexplored options like Actuarial Science and Psychology
- **After 12th:** Which course, which college (NIRF 2024 ranked, mark-filtered), which field — backed by real job market data

It combines:
- Subject marks (tap-card bands — approximate is fine)
- RIASEC psychometric interest profile (Holland's model — 60 years of validated research)
- Extracurricular inputs (sports, arts, community work, awards)
- Family context (city tier, parent profession, budget)
- State (for state-specific entrance exam names — TNEA, KCET, KEAM, etc.)
- **Live job market signals** (Naukri JobSpeak 2025–26 data, NASSCOM data)

Output: 3 ranked career paths with honest job market notes, mark-tier-appropriate salary ranges, NIRF 2024-based college suggestions, and a parent-friendly summary.

---

## Key features

- **Zero backend.** Everything runs in the browser. No data stored, no login, no server costs.
- **5 languages.** English, Tamil, Hindi, Kannada, Telugu — switch instantly via the globe icon. Career path content (courses, jobs, salary) stays in English by design, since technical terms are used in English even regionally.
- **Honest scoring.** Hard-excludes paths the student's marks can't realistically support (e.g. B.Tech CS/AI won't show for a 45% student). 3-layer fallback ensures every combination of marks + interests returns 3 meaningful paths — never an empty result.
- **NIRF 2024 college suggestions.** Filtered by marks into 4 tiers (95%+, 75-94%, 60-74%, <60%), with state-specific data for TN, KA, KL, AP, TS, MH, DL, WB. Clearly labelled "indicative" with links to official verification portals (NIRF, TNEA, KCET, JoSAA, MCC, CLAT).
- **"Before You Decide" explore box** (Class 10 only) — surfaces Actuarial Science or Psychology when a student's profile genuinely fits but Science/Commerce/Arts dominated their top 3. Addresses the "herd science group" pattern common in South India.
- **State-specific entrance exam names** — TNEA, KCET, KEAM, AP/TS EAMCET, MHT CET, WBJEE, etc.
- **Printable / saveable as PDF.** One click → "Save as PDF Report". Parents can keep it, share it with teachers/counsellors. Print CSS hides all UI chrome and adds attribution.
- **WhatsApp share** — both for sharing the tool itself (header button) and sharing personal results (result page).
- **GA4 analytics** — Measurement ID already configured (`G-QGZD0CKSJ6`). 12 events tracked (see below).
- **RIASEC is public domain.** No licensing fee. Backed by decades of peer-reviewed research.

---

## How to deploy to GitHub Pages (5 minutes)

1. Create a new GitHub repo named `pathfinder` (or any name)
2. Upload `index.html` to the root
3. Go to **Settings → Pages → Source → main branch → / (root)**
4. Your tool is live at `https://YOUR-USERNAME.github.io/pathfinder/`

No npm, no build step, no dependencies.

---

## GA4 analytics

Measurement ID is already set to `G-QGZD0CKSJ6` (3 occurrences in the file — async script tag, `gtag('config', ...)`, and a comment).

If forking for your own deployment, replace all 3 occurrences with your own Measurement ID from [analytics.google.com](https://analytics.google.com).

**Events tracked (12):**
- `select_class` — student picks 10th or 12th
- `step_view` — every step navigation
- `select_stream_12` — stream selection for 12th students
- `select_language` — language switch
- `psycho_answered` — each psychometric response
- `mark_selected` — each subject mark tap
- `extras_selected` — extracurricular selections
- `context_selected` — city tier / family context
- `result_generated` — final output view (class level, RIASEC type, avg marks, top path)
- `explore_box_shown` — when the "Before You Decide" box surfaces (Class 10)
- `print_result` — print/PDF save
- `whatsapp_share` — share button clicks (header and result)

⚠️ **Before any future full-file rebuild:** verify `G-QGZD0CKSJ6` is preserved — this has broken silently before (placeholder `G-XXXXXXXXXX` overwrote the real ID and tracking was dark for several days before being caught).

---

## Updating job market data

Hardcoded in two places:
1. The visual market strip in the result section (HTML near bottom of file)
2. The `hiring`, `risk`, and `salary` fields inside the `allPaths` arrays in `generatePaths10`, `generatePaths12`, and their `*Relaxed` variants

Update quarterly. Sources to use:
- [Naukri JobSpeak](https://www.naukri.com/blog/category/market-trends/)
- [NASSCOM reports](https://nasscom.in/knowledge-center/publications)
- [IndiaSpend jobs coverage](https://www.indiaspend.com)

## Updating NIRF college data

College suggestions are in the `getColleges()` function, organised by path ID → mark tier (`t1`–`t4`) → state. NIRF rankings are released annually (~August) at [nirfindia.org](https://www.nirfindia.org). When updating:
- Re-verify rank numbers cited inline (e.g. "NIT Trichy (NIRF #8)")
- Keep state-specific entries for TN, KA, KL, AP, TS, MH, DL, WB current
- `DEFAULT` entries apply to all other states

---

## Architecture notes (for future sessions)

- **Single HTML file**, ~4,000 lines, ~167KB. No build step.
- **Scoring logic:** `generatePaths10`/`generatePaths12` do hard exclusion (`score: -999`) when marks are >20 points below a path's `minMark`. If fewer than 3 paths survive, `generatePathsRelaxed` (no hard exclusion) fills gaps, then `getGenericLowMarkPaths` is the final fallback. This 3-layer fallback guarantees 3 results for any input — validated across 2,400 mark/RIASEC/stream combinations.
- **`generatePaths10` has an `includeAll` 11th parameter** — when `true`, returns all scored paths (not sliced to top 3). Used by the explore-box logic to check if Actuarial Science/Psychology scored ≥50 even if they didn't make top 3.
- **New paths (Actuarial Science, Psychology) are Class 10 only** — deliberately not added to 12th streams, since a 12th PCM/PCB/PCMB student would need to switch streams entirely, which would be misleading without heavy disclaimer work (a "pivot path" framing exercise, not yet done).
- **Vocational stream** has its own subject set (`marks12subjects.vocational`) — 4 subjects (Overall %, Vocational Theory, Vocational Practical, English). Validation threshold is dynamic (`Math.min(3, totalSubjects)`) to prevent future stream additions from hitting the same contradiction bug.

---

## Roadmap

- [x] Tamil, Hindi, Kannada, Telugu language versions
- [x] NIRF 2024-based college suggestions with mark filtering
- [x] Actuarial Science & Psychology paths (Class 10)
- [x] "Before You Decide" explore box for underexplored paths
- [ ] "Pivot path" framing for Psychology/Actuarial Science/Law/CA when a 12th student is already in PCM/PCB/PCMB
- [ ] Entrance exam score input (JEE/NEET percentile) to refine college tier beyond marks alone
- [ ] Claude API integration for personalised paragraph generation
- [ ] og-image.png — create from `/mnt/user-data/outputs/og-image.html` (1200×630 screenshot) and add to repo root
- [ ] College search by state + marks + budget

---

## Built by

[Jaganmohan KB](https://linkedin.com/in/jaganmohankb) · [JK Advisory](https://jkadvisory.in)

Feedback: jagan@jkadvisory.in

---

*Free to use. Free to fork. Built for Indian students who deserve better career guidance.*
