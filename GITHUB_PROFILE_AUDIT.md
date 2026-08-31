# GitHub Profile Audit

Self-review of `hichamagrad/hichamagrad`, written from the perspective of a cybersecurity recruiter, a technical recruiter, and a hiring engineer. Also documents every scope decision and trade-off made while building it, so nothing is a silent surprise.

## Would this make me want to open your repos?

**Yes.** In under 10 seconds a visitor sees: name, current role (cybersecurity intern at YAZAKI on an AI-risk mandate), and a concrete, credible flagship project (SecureWatch: 10 real vulnerabilities found and fixed, not a vague "security project"). That specificity is what separates this from a template profile.

## Content honesty checklist

- [x] No invented certifications, companies, job titles, or technologies. Every credential listed is a real, verifiable certificate (Oracle, Coursera).
- [x] No fabricated statistics. "Current Focus" bars are explicitly labeled as relative time investment, not a scored/fabricated skill percentage.
- [x] Every project listed has a real, working GitHub repository link (verified with a live HTTP check before publishing).
- [x] Experience descriptions rewritten from your portfolio/CV data, not copied verbatim from LinkedIn.
- [x] Skills list only includes technologies with direct evidence in your real repositories or portfolio (e.g., MITRE ATLAS and OWASP LLM Top 10 appear because SentinelLLM's code actually maps to them).

## Known issues at time of writing (2026-08-31)

1. **Portfolio live URL not yet included.** You said you'd send it; I used the GitHub repo link (`hicham-cybersecurity-portfolio`) as a placeholder everywhere a live link would go, rather than guess a `.vercel.app` address. **Once you give me the URL, these four spots need updating**: the "Portfolio" badge (top and bottom), the "About" section link, and the "Featured Projects" footnote.
2. **`aas-phones.vercel.app` is down (404).** It worked when the portfolio site was built, so the Vercel deployment appears to have gone stale since. I did not link it here. **This same dead link is currently live on your actual portfolio site** ("Secure E-commerce Platform" → "Live Demo"), worth fixing there too, either by redeploying or removing the demo link.
3. **Fixed: leftover Jekyll/Pages setup was failing on every push.** This repo had a stale `.github/workflows/jekyll-gh-pages.yml` (a GitHub-generated sample workflow) and GitHub Pages enabled with source `main`/`docs`, both left over from the 2022 coursework files at the repo root. Since no `/docs` folder exists, both that workflow and the legacy "pages build and deployment" job failed on every push, including the one that added this README, showing as red X's in the Actions tab. Removed the workflow file and disabled Pages via the API. Neither was serving any purpose (nothing links to the old `hichamagrad.github.io/hichamagrad/` Pages URL).
4. **`github-readme-stats.vercel.app` returned "DEPLOYMENT_PAUSED" (HTTP 503)** for both the stats card and top-languages card when I checked. This is a well-documented, recurring issue with that free shared instance hitting Vercel's usage quota, not something wrong with this profile's setup, and not a URL I invented. It usually comes back within hours to a couple of days. The streak-stats widget (a different service) was live and works now. If the stats cards are still broken when you check: the standard fix the community uses is deploying your own copy of the `github-readme-stats` repo to Vercel (you already have a Vercel account) and swapping the domain in the README's two `<img>` tags. Say the word and I'll set that up.

## Scope decisions and trade-offs

- **Binary portrait method**: built from your real reference photo using luminance-threshold silhouette extraction plus edge-detection for interior detail (glasses/hair boundaries), rendered as literal `0`/`1` characters, not a filter or generic face. Full detail requires the desktop PNG; the compact mobile version trades detail for size, as specified.
- **No true responsive image swap.** GitHub READMEs can't run media-query-based image switching for arbitrary raster images (only the `<picture>` + `prefers-color-scheme` trick, used here for the snake). So "desktop" and "mobile" portraits aren't shown/hidden by screen size; instead they're used in two different real contexts, the high-detail one as the main "Digital Identity" showcase, the compact one as the small avatar next to your name. Both files exist as deliverables either way.
- **Terminal section is a static formatted code block, not a per-keystroke typing animation.** True multi-line typing animation isn't reliably achievable in pure GitHub Markdown/SVG without an external always-on rendering service (which doesn't exist for multi-line terminal sessions the way it does for single-line rotating text). The single-line rotating job titles under your name *do* animate for real, via the widely-used `readme-typing-svg` service.
- **Animated binary portrait**: implemented as a real scramble-to-reveal GIF (random noise resolving into your portrait, then a subtle brightness pulse, looping), not a static placeholder, since Pillow made it genuinely achievable rather than a corner cut.
- **Skipped a separate `metrics.yml` action.** The brief's own instructions say "don't add unnecessary metrics" and "maximum 2-3 widgets." A `lowlighter/metrics` action would duplicate what the GitHub Stats and Streak cards already show, for the cost of a second scheduled Action to maintain. If you want a specific metrics plugin those cards don't cover (e.g., an isometric contribution calendar), tell me which one and I'll add it.
- **One reusable divider style**, not five different ones, per the brief's own "don't use too many" guidance.
- **SVG assets (hero/divider/footer) use a fixed dark background**, not a theme-adaptive transparent design. They'll look identical in GitHub's light and dark modes (like a fixed banner image would), rather than attempting the more complex dual-asset `<picture>` treatment for every decorative SVG. Only the snake graphic (where GitHub already expects theme variants) uses the `<picture>` dark/light split.

## Repository audit (recommendations only, nothing was modified)

Per your instructions, I did not touch any of your other repositories. For your own cleanup, in order of relevance:

**Worth featuring more (already good):**
- `securewatch`, `sentinelllm`: strong, well-documented, exactly the kind of repos a security recruiter wants to open.
- `Systeme-de-Reconnaissance-Faciale-avec-Django`: has a real README already.

**Could use a README:**
- `aasPhones`: currently only has Laravel's default boilerplate README, not one describing the actual e-commerce app you built on top of it.
- `NeoTrans` (TypeScript, logistics/tracking platform): has no description and isn't linked anywhere; if it's a substantial project, it's a good "full-stack breadth" addition to the portfolio.

**Likely candidates to archive or make private** (coursework/practice repos with no description, several unfinished or duplicate):
- `medical-office-management`, `currencyconverter`, `currencyconv` (near-duplicate of `currencyconverter`), `guessinggame1`, `gessinggameproject` (looks like a duplicate/typo of `guessinggame1`), `Gallery_Homework`, `horloge`, `DEV208`, `hichamagrad2`, `hichamagrad1`, `aas-phones` (an older TypeScript repo, distinct from the `aasPhones` Laravel one; the similar name is likely to confuse recruiters into thinking it's the same project).
- The `hichamagrad/hichamagrad` repo itself (this one) still has its original 2022 coursework files at the root (`pfm.html`, `style.css`, several `.ttf` fonts, an Unsplash stock photo, a few dated screenshots). I left them untouched since removing them wasn't necessary to make this README render as your profile page, but they'll show up if anyone browses the repo's file list. Worth deleting once you've reviewed them.

## Technical checklist

- [x] Valid Markdown, renders correctly.
- [x] All custom SVGs are self-contained (no external fonts/scripts), lightweight (hero 15KB, divider/footer <1KB each).
- [x] Binary portraits: desktop 15KB, mobile 7KB, animated GIF ~350KB.
- [x] Every external link HTTP-checked before publishing (see "Known issues" for the two that are genuinely down through no fault of this setup).
- [x] `snake.yml` configured with `workflow_dispatch` + push trigger, so it generates on first push rather than waiting for the next 03:00 UTC cron run.
