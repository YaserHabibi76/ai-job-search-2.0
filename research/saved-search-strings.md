# Saved Search Strings & Native Alert Setup

Two purposes: (1) exact strings the automated daily procedure uses against Adzuna/Jooble/JSearch and in WebSearch sweeps, and (2) what Yaser should paste into LinkedIn's and Indeed's own search boxes to set up native daily alerts — this is the fully-compliant way to get LinkedIn/Indeed coverage, since the automation itself cannot query those two sites directly (see `market-research-analyst.md` §4).

## Insurance track — keyword strings
- `"Personal Lines Account Manager" remote`
- `"Personal Lines Insurance Advisor" remote`
- `"Licensed Insurance Producer" remote`
- `"Insurance Account Executive" remote`
- `"Remote Insurance Producer"`
- `"Licensed Insurance Sales Representative" remote`
- `"P&C licensed" remote personal lines`
- Add `-hybrid -"in office"` where the board supports negative keywords, to pre-filter.

## Analyst track — keyword strings
- `"Business Intelligence Analyst" remote`
- `"Data Analyst" remote entry level`
- `"Reporting Analyst" remote`
- `"BI Developer" remote`
- `"Analytics Associate" remote`
- `"Power BI Analyst" remote`
- `"Tableau Analyst" remote`

## LinkedIn — one-time manual setup (~10 min)
For each keyword string above:
1. Paste into LinkedIn Jobs search, set Location = "United States" (not a specific city), and filter Remote = "Remote."
2. Click "Create search alert" (bell icon) → set frequency to **Daily**, delivery to email + app notification.
3. Repeat for each of the ~13 strings above (or combine a few per alert if LinkedIn's search accepts OR logic — test with quotes/parentheses).

## Indeed — one-time manual setup (~10 min)
1. Run each keyword string in Indeed search with Location left blank or set to "Remote," and add the Remote filter.
2. Scroll to "Get new jobs for this search sent to your email" → enter email, set daily frequency.
3. Repeat per keyword string.

## Why this matters
Neither platform's search-results pages can be reliably or legally queried by the automated procedure (LinkedIn login-walls anonymous fetches; Indeed runs Cloudflare/DataDome anti-bot; both ToS explicitly forbid automated querying). Native alerts push results directly from LinkedIn/Indeed's own infrastructure to Yaser's inbox — zero ToS risk, zero technical fragility, and it's the only way to get first-party coverage of those two platforms. The automated daily procedure (Adzuna/Jooble/JSearch/WebSearch) fills in everything else.
