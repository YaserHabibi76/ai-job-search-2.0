# Daily Search Procedure

This is the exact recipe Claude follows each run — whether triggered by a scheduled cloud agent or manually by Yaser asking "run today's job search."

## Inputs
- `../profile.md` — constraints, salary floor, must-haves/no-gos
- `../research/saved-search-strings.md` — keyword strings per track
- `../automation/api-setup.md` — API keys (if filled in)
- `../pipeline/tracker.csv` — existing pipeline, for dedupe

## Steps
1. **Fetch new listings.**
   - If API keys are set: query Adzuna, Jooble, and JSearch via WebFetch for both tracks using the keyword strings, remote filter on, `salary_min` where the API supports it.
   - Always also run WebSearch sweeps against the niche boards listed in `../research/market-research-insurance.md` §3 (InsuranceJobs.com, iHireInsurance, Insurance Journal Jobs, Great Insurance Jobs) and `../research/market-research-analyst.md` §3 (Built In, We Work Remotely, Wellfound, Outer Join), plus general web search per keyword string.
   - **Never** query linkedin.com or indeed.com search endpoints directly — see research files for why. LinkedIn/Indeed coverage comes only from Yaser's own native alerts (he forwards/pastes anything interesting from those emails, or Claude reads an individual public posting URL he provides).

2. **Dedupe.** Skip any listing whose URL already exists in `tracker.csv`.

3. **Filter & tag.**
   - Reject: confirmed onsite/hybrid listings.
   - Tag `remote_verified = caution` for anything with residency/relocation language ("must reside in," "must relocate to," a specific state named in requirements despite a "Remote" title) — flag explicitly in notes, don't silently drop.
   - Tag `comp_type` = W2 or 1099 based on posting language.
   - Reject anything below the salary floor in `profile.md` if salary is stated; if unstated, keep and note `salary = unknown`.

4. **Rank.** Sort each track's new listings into Strong Match / Possible Match / Long Shot based on title match, skills match, and remote_verified confidence. Cap surfaced items at ~10-15 per track; anything past the cap goes to `pipeline/shortlist/backlog.md` instead.

5. **Tailor materials.** For each surfaced (non-backlog) listing: draft a 1-2 bullet resume adjustment (using the matching track's master resume as base) and a 2-3 sentence tailored cover-letter opener (using `resumes/cover-letter-base.md` as the skeleton), referencing something specific from the posting.

6. **Write outputs.**
   - Append new rows to `pipeline/tracker.csv` with status `New`.
   - Write `pipeline/shortlist/YYYY-MM-DD.md`: for each track, a ranked list with company/title/link/remote_verified/comp_type/salary, the tailored bullet + cover-letter opener, and a one-line "why this fits."
   - Append backlog overflow to `pipeline/shortlist/backlog.md`.

7. **Notify.** Send a Gmail digest to yaserhabibi27@gmail.com: counts of new Strong/Possible matches per track, and a link/pointer to today's shortlist file. If run in an active chat session, also summarize in chat.

## After Yaser applies
When told "I applied to X" (or tracker.csv is updated directly), flip that row's `status` to `Applied` and fill `date_applied`.

## Weekly retro (run once a week, e.g. Sunday)
Summarize from `tracker.csv`: applications sent, response rate, interviews booked — per track. If a track shows zero response after meaningful volume, flag it as a signal to revisit that track's resume/targeting rather than just sending more.
