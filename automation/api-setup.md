# API Setup — One-Time (~10 minutes)

Free job-search APIs the daily procedure calls via WebFetch. None of these touch LinkedIn/Indeed directly (see `../research/market-research-analyst.md` §4 for why that matters) — JSearch specifically surfaces LinkedIn/Indeed-originated postings legally through Google for Jobs' index.

## 1. Adzuna API (free, 1,000 calls/month)
1. Sign up at https://developer.adzuna.com/
2. Create an app, get `app_id` and `app_key`.
3. Paste below.

**app_id:** `<fill in>`
**app_key:** `<fill in>`

Example query shape: `https://api.adzuna.com/v1/api/jobs/us/search/1?app_id={id}&app_key={key}&results_per_page=20&what=business%20intelligence%20analyst&where=remote&salary_min=45000`

## 2. Jooble API (free)
1. Request a key at https://jooble.org/api/about
2. Approval is usually fast (email-based).

**api_key:** `<fill in>`

Example query shape: `POST https://jooble.org/api/{api_key}` with JSON body `{"keywords": "business intelligence analyst", "location": "remote"}`

## 3. JSearch via RapidAPI (freemium)
1. Sign up at https://rapidapi.com/ and subscribe to the JSearch API (free tier).
2. Get your `X-RapidAPI-Key`.

**rapidapi_key:** `<fill in>`

Example query shape: `GET https://jsearch.p.rapidapi.com/search?query=business%20intelligence%20analyst%20remote&num_pages=1` with header `X-RapidAPI-Key: {key}`

## Once keys are filled in
Tell Claude "API keys are set" and the daily procedure will start pulling from all three sources. Until then, the daily procedure still runs using WebSearch sweeps against the niche boards in `../research/market-research-insurance.md` §3 and `../research/market-research-analyst.md` §3 — just with less coverage.

## Budget note
Adzuna's 1,000 calls/month free tier is far more than needed for 2 tracks × 1 run/day (well under 100 calls/month at typical query volume) — no cost risk from normal daily use.
