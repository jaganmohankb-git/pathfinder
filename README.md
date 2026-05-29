# PathFinder India 🧭

**Free, private, AI-guided career guidance for students completing 10th & 12th in India**

→ **Live tool:** https://jaganmohankb-git.github.io/pathfinder/

---

## What it does

PathFinder helps students and parents make a better career decision at the two most critical moments in Indian education:

- **After 10th:** Science / Commerce / Arts / Diploma — which stream and why
- **After 12th:** Which course, which college tier, which field — backed by real job market data

It combines:
- Subject marks (band-based, approximate is fine)
- RIASEC psychometric interest profile (Holland's model — 60 years of validated research)
- Extracurricular inputs (sports, arts, community work, awards)
- Family context (city tier, parent profession, budget)
- **Live job market signals** (Naukri JobSpeak 2025–26 data, NASSCOM data)

Output: 3 ranked career paths with honest job market notes, salary ranges, and a parent-friendly summary.

---

## Key design decisions

- **Zero backend.** Everything runs in the browser. No data is stored, no login required, no server costs.
- **Printable / saveable as PDF.** One click → `Ctrl+P` → Save as PDF. Parents can keep it, share it with teachers.
- **WhatsApp share button** on the result — built for Indian distribution.
- **GA4 analytics** for basic click/view tracking. Replace `G-XXXXXXXXXX` with your Measurement ID.
- **RIASEC is public domain.** No licensing fee. Backed by decades of peer-reviewed research.

---

## How to deploy to GitHub Pages (5 minutes)

1. Create a new GitHub repo named `pathfinder` (or any name)
2. Upload `index.html` to the root
3. Go to **Settings → Pages → Source → main branch → / (root)**
4. Your tool is live at `https://YOUR-USERNAME.github.io/pathfinder/`

That's it. No npm, no build step, no dependencies.

---

## How to add GA4 tracking

1. Go to [analytics.google.com](https://analytics.google.com)
2. Create a new Property → Web → enter your GitHub Pages URL
3. Copy your **Measurement ID** (starts with `G-`)
4. In `index.html`, replace both occurrences of `G-XXXXXXXXXX` with your Measurement ID

Events already tracked:
- `select_class` — when student picks 10th or 12th
- `step_view` — every step navigation
- `select_stream_12` — stream selection for 12th students
- `psycho_answered` — each psychometric response
- `result_generated` — final output view (with class level, RIASEC type, avg marks)
- `print_result` — print/PDF save

---

## Updating job market data

The job market data is hardcoded in two places:
1. The visual market strip in the result section (HTML near bottom of file)
2. The `hiring` and `risk` fields inside the `allPaths` arrays in the JavaScript

Update quarterly. Sources to use:
- [Naukri JobSpeak](https://www.naukri.com/blog/category/market-trends/)
- [NASSCOM reports](https://nasscom.in/knowledge-center/publications)
- [IndiaSpend jobs coverage](https://www.indiaspend.com)

---

## Roadmap

- [ ] Tamil language version (huge for TN distribution)
- [ ] Claude API integration for personalised paragraph generation
- [ ] Feedback form (Was this helpful? Y/N)
- [ ] Entrance exam calendar widget
- [ ] College search by state + marks + budget

---

## Built by

[Jaganmohan KB](https://linkedin.com/in/jaganmohankb) · [JK Advisory](https://jkadvisory.in)

Feedback: jagan@jkadvisory.in

---

*Free to use. Free to fork. Built for Indian students who deserve better career guidance.*
