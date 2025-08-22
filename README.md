# Static Website (GitHub Pages)

This repository hosts a simple static website (HTML + CSS, optional light JS) served directly via GitHub Pages. There is no backend, no database, and no build pipeline required. All content changes are requested through GitHub Issues and implemented by Copilot (or an automated assistant) via pull requests.

## Purpose
Keep the site ultra‑light, transparent, and easy to update without needing direct edits to `main` except through reviewed PRs generated from Issue requests.

## Tech Scope
- Static assets only: `index.html`, stylesheet(s), optional small JS for interactivity.
- No frameworks or bundlers unless explicitly introduced later via an Issue.
- No data persistence beyond the repository files.

## Content Change Workflow
1. Open a GitHub Issue (use a clear title describing the change).
2. Describe exactly what should change (sections to add/remove, text edits, links, styling tweaks). Provide final copy where possible.
3. (Optional) Add a label like `content` or `update` to help triage.
4. Copilot/automation generates a branch + pull request implementing the change.
5. Review the PR (focus on accuracy of content & simple HTML/CSS integrity) and merge.
6. GitHub Pages automatically redeploys from the configured branch (usually `main` or `docs`).

## Minimal Structure
```
index.html
assets/
  css/
    styles.css
  img/
    (images, favicons)
README.md
```
(Adjust or extend only through Issues.)

## Local Preview
You can simply open `index.html` in a browser. For cleaner relative path behavior (and if later adding JS modules), run a lightweight local server:
```bash
python -m http.server 8000  # or any static server
```
Then visit: http://localhost:8000

## Adding / Editing Content (What to Include in an Issue)
Provide:
- Section / file to change (e.g. "Add a Features section under the hero").
- Exact text / HTML snippet (or bullet list to be converted to markup).
- Any style adjustments (e.g. "Make heading centered" or color changes with hex codes).
- Asset needs (attach images or specify source URL).

## Non-Goals (Unless an Issue Approves a Change)
- No client-side frameworks.
- No server-side rendering.
- No databases or external CMS.
- No analytics/tracking scripts by default.

## Deployment
Configured via GitHub Pages. After merging to the published branch, changes propagate automatically (cache/CDN delays may be a few minutes). If Pages is not yet enabled: Settings → Pages → Select branch + root.

## Contribution Guidelines
- Never push directly to `main`.
- Every change originates from an Issue and lands via PR.
- Keep HTML semantic and accessible (use proper headings, alt text, landmarks).

## License
TBD. If you intend the site to be public/open, add a LICENSE file (MIT is a common simple choice). Until then, treat as All Rights Reserved.

---
To request the initial `index.html` + `assets` scaffold, open an Issue or ask directly.
