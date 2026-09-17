# API Setup — One-Time (~10 minutes)

Free job-search APIs the daily procedure calls via WebFetch. None of these touch LinkedIn/Indeed directly (see `../research/market-research-analyst.md` §4 for why that matters) — JSearch specifically surfaces LinkedIn/Indeed-originated postings legally through Google for Jobs' index.

## 1. Adzuna API (free, 1,000 calls/month)
1. Sign up at https://developer.adzuna.com/
2. Create an app, get `app_id` and `app_key`.
3. Paste below.

**app_id:** `558a0fb9`
**app_key:** `0622f794a9a44db0a5513a1b0a4446b9`

Note: this repo is public and the cloud routine platform has no secrets-storage mechanism, so this key is committed in plaintext by deliberate choice — it's a free tier key with no billing attached, so the worst case is quota abuse (fixed by regenerating a new key at developer.adzuna.com).

**Verified working query shape** (tested 2026-09-16, returned 54 real remote listings): `https://api.adzuna.com/v1/api/jobs/us/search/1?app_id={id}&app_key={key}&results_per_page=20&what=business%20intelligence%20analyst%20remote&salary_min=45000`
- Note: `where=remote` does NOT work (Adzuna treats `where` as a real US location, returns 0 results). Instead, append "remote" as part of the `what` search term — Adzuna matches it against title/description text, which reliably surfaces remote-tagged listings.

## 2. Jooble API (free)
1. Request a key at https://jooble.org/api/about
2. Approval is usually fast (email-based).

**api_key:** `73d3495a-c150-4493-8686-79ce1c87d164`

**Verified working query shape** (tested 2026-09-17, returned real listings with company/salary/link): `POST https://jooble.org/api/73d3495a-c150-4493-8686-79ce1c87d164` with header `Content-Type: application/json` and JSON body `{"keywords": "<keyword phrase> remote", "location": "remote"}`. Response includes `title`, `location`, `company`, `salary`, `link`, `snippet` per job. Rate limit: Jooble's signup email states "default limit of 500 requests" without specifying a time window — treat this conservatively (budget only a few queries/day across both tracks) until confirmed whether it resets daily/monthly or is a lifetime cap.

## 3. JSearch via RapidAPI (freemium)
1. Sign up at https://rapidapi.com/ and subscribe to the JSearch API (free tier).
2. Get your `X-RapidAPI-Key`.

**rapidapi_key:** `<fill in>`

Example query shape: `GET https://jsearch.p.rapidapi.com/search?query=business%20intelligence%20analyst%20remote&num_pages=1` with header `X-RapidAPI-Key: {key}`

## Once keys are filled in
Tell Claude "API keys are set" and the daily procedure will start pulling from all three sources. Until then, the daily procedure still runs using WebSearch sweeps against the niche boards in `../research/market-research-insurance.md` §3 and `../research/market-research-analyst.md` §3 — just with less coverage.

## Budget note
Adzuna's 1,000 calls/month free tier is far more than needed for 2 tracks × 1 run/day (well under 100 calls/month at typical query volume) — no cost risk from normal daily use.
