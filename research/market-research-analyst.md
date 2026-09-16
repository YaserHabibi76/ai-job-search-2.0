# Market Research — Remote BI / Data Analyst Roles (2026)

Researched 2026-09-16 to inform the job search plan.

## 1. Market demand & competitiveness
- BI Analyst demand projected +21% growth 2018-2028; some sources cite 30-40% YoY growth for data/business analyst roles, partly AI-adjacent-analytics driven.
- Entry-level (0-2 yrs) data analyst roles are ~5.1% of postings — real but a minority share.
- Core skills match Yaser's profile well: SQL (~95% of postings), a BI tool — Tableau/Power BI/Looker (~72%), Python (~78%). Skills fit is not the bottleneck.
- Market framed as "low-hire, low-fire" for 2026: fewer openings, but also fewer layoffs — high selectivity per role rather than mass churn.
- Entry-level candidates increasingly struggle to convert applications to offers even with matching skills — attributed to AI-driven application-volume flooding recruiters and "entry-level" postings quietly asking for 1-3 yrs.

**Remote-only realism — the key headwind:**
- Direction since 2023-2024 is away from remote-only, toward hybrid/onsite. Robert Half Q2 2026: ~87% fully on-site postings, ~10% hybrid, ~3% fully remote.
- Broader "data analytics field" remote-or-hybrid figure: ~34% — much higher than "fully remote," implying hybrid absorbed most of what used to be remote.
- Counter-signal: FlexJobs reports remote postings grew 22% in Q2 2026 (second consecutive quarterly increase) — partial rebound, not pure decline.
- Tech/legal/marketing/finance (where BI/data roles sit) show the highest remote/hybrid share of any sector — comparatively well-positioned vs. healthcare/admin.
- **Bottom line: expect roughly 1 truly-remote listing for every 5-8 hybrid/onsite listings in this title space** — remote-only is realistic but narrows the pool and puts you in national (not just local) competition. Plan for a volume-application strategy, not a handful of targeted applications.
- No sign of BI/data-analyst-specific mass layoffs distinct from general tech layoffs — market framed as stable-but-selective.

## 2. Highest-signal job titles/keywords
- Business Intelligence Analyst / Associate Business Intelligence Analyst
- Data Analyst / Junior Data Analyst / Entry Level Data Analyst
- Reporting Analyst
- BI Developer / Business Intelligence Developer (I/II)
- Analytics Associate / Business Data Analyst
- Data & Reporting Analyst
- Given Baylis Medical background (forecasting/financial modeling): also try "Financial Analyst" + Power BI, "FP&A Analyst" — BI-to-FP&A crossover postings often list similar toolsets.
- Search as exact-phrase + "remote": `"Business Intelligence Analyst"`, `"Data Analyst"`, `"Reporting Analyst"`, `"BI Developer"`, `"Analytics Associate"`, `"Power BI Analyst"`, `"Tableau Analyst"`.

## 3. Job boards beyond LinkedIn/Indeed
- **Built In** — dedicated remote + data-analytics + BI filter: builtin.com/jobs/remote/data-analytics/business-intelligence
- **We Work Remotely** — strong remote-only inventory, frequently recommended for data roles
- **Wellfound** (formerly AngelList Talent) — startup-focused, dedicated data-analyst page; good for early-career since startups often accept less experience
- **Outer Join** — boutique board specifically for remote data science/analytics/data-engineering (outerjoin.us)
- **DataAnalyst.com / DataJobs.com / Dynamite Jobs** — smaller niche boards, lower volume, worth a pass
- **Dice** — more IT-infra-leaning but returns real remote BI results
- **Welcome to the Jungle** (absorbed Otta) — large, active
- **RemoteOK, Himalayas** — generalist remote boards, reasonable secondary sources
- **FlexJobs** — paid but hand-vetted, good for scam-filtering

## 4. Automation feasibility (drives the technical design of this system)
**No legal/technical path to query LinkedIn or Indeed search directly:**
- Indeed's Publisher API was deprecated in 2023; no public self-serve job-search API remains. Enterprise data partnerships are NDA-gated, sales-led, six-figure minimums.
- LinkedIn's official Job Posting API is for approved ATS/distribution partners *posting* jobs, not third parties *reading/searching*. No new data-extraction API access granted to third parties since ~2018.
- **ToS**: LinkedIn explicitly bans scraping/bots/automated access (78.2M fake accounts blocked, 23.5M automated sessions flagged in one quarter per a 2026 transparency report). Indeed's ToS prohibits "robots, spiders, or other automated means" and automating Indeed Apply outside official vendor tooling.
- **Legal precedent**: hiQ Labs v. LinkedIn (9th Cir. 2022) found scraping *public* pages likely doesn't violate CFAA's "without authorization" clause — but the case still ended in **LinkedIn's favor on breach-of-contract grounds** (Nov 2022 summary judgment; Dec 2022 settlement: hiQ paid LinkedIn $500k, permanent injunction, data destruction). hiQ does NOT clear automated LinkedIn/Indeed use — it only narrows CFAA criminal exposure; ToS-based account bans remain a real risk.
- Practically: LinkedIn search-results pages sign-in-wall anonymous/automated visitors (truncated data, no pagination); Indeed runs Cloudflare + DataDome anti-bot with CAPTCHA challenges even at low request volume from a single IP.

**Legitimate alternatives that avoid touching LinkedIn/Indeed directly:**
- **Adzuna API** — free tier, 1,000 calls/month, instant self-serve signup, aggregates broadly.
- **Jooble API** — free (email approval, usually fast), aggregates 140,000+ sources.
- **JSearch (via RapidAPI)** — surfaces Google-for-Jobs-indexed results, which *includes* LinkedIn/Indeed/Glassdoor/ZipRecruiter postings — legal because it's built on Google's public index, not a direct scrape of linkedin.com/indeed.com. Freemium tier.
- **Greenhouse Job Board API** (`GET boards-api.greenhouse.io/v1/boards/{board_token}/jobs?content=true`) and **Lever Postings API** (`GET api.lever.co/v0/postings/{company}`) — public, unauthenticated, officially documented; 100% legitimate since it's the company's own public careers-page feed.
- USAJobs API — free, federal roles only, not relevant unless open to federal work.

**What a WebSearch/WebFetch-only agent can actually do:**
- Individual public job-posting URLs are sometimes readable via fetch, but increasingly hit sign-in walls / truncated content.
- Search-results pages on both LinkedIn and Indeed are unreliable for automated fetch (login walls, CAPTCHA) regardless of ToS.
- WebSearch (Claude's general web index) can surface links to LinkedIn/Indeed postings indexed by search engines — indirect, low-volume, doesn't hit either site's own search infrastructure, so no ToS conflict, but coverage is partial/stale vs. the sites' own real-time search.

**Bottom line:** Never build anything that scrapes/programmatically queries LinkedIn or Indeed search directly. Use Adzuna + Jooble + JSearch + targeted Greenhouse/Lever lookups for automated discovery (this gets de facto LinkedIn/Indeed coverage via JSearch's Google-for-Jobs index, legally). Treat LinkedIn/Indeed as manual-browse channels backed by the user's own native saved-search/alert features.
