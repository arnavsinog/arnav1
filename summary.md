# San Francisco capital-firm research: summary

**Result: 18 firms in `leads_sf.csv`, not 30.** 7 are `qualified`, 11 are `needs_check`. Two required checks (Google visibility, articles) could not be run as specified, so the visibility filter was not applied. Details below.

## What I could and could not do

| Requirement | Status | Why |
|---|---|---|
| Company-level data only, no people, no LinkedIn | Done | Only firm-level facts recorded. No LinkedIn URLs or people collected. LinkedIn pages were never fetched. |
| HQ San Francisco, founded 2015+ | Partly | Verified from search-result snippets and aggregator profiles (Crunchbase, PitchBook, Tracxn, etc.). Not confirmed from firms' own sites or SEC filings. |
| Seed-list firms verified | Done | All 5 seed firms confirmed as San Francisco based and founded in the stated years. |
| Candidates verified | Done | Each candidate checked once by search. Results in the table below. |
| robots.txt and rate limiting | Not applicable | The network egress proxy blocks every firm website I tried (centana.com, nexaequity.com, acrewcapital.com, plus several directory sites). No site was fetched, so nothing was scraped. |
| Google visibility check | Not done | I cannot run Google searches or read Google rankings from this environment. I only have a search tool that returns a list of results. |
| Articles check | Not done | Firm sites are blocked, so I could not look for `/insights`, `/news`, etc. or count posts. `articles_section_url` and `posts_last_12_months` are blank for every row. |
| Fabrication rule | Followed | Unknown fields are blank. Website is filled only where it came from the seed list or a source URL I saw. |

## Visibility check: what I did instead

I ran about a dozen sector-style queries through the search tool (for example "San Francisco growth equity fintech", "healthcare software growth equity San Francisco", "San Francisco boutique investment bank technology capital raise"). This is a proxy, not Google rankings.

- A firm's **own domain** appeared in a generic query only once: Vista Point Advisors (`vistapointadvisors.com`), which is excluded for being founded in 2011.
- Third-party pages naming firms from the list: Nexa Equity and Centana Growth Partners both appeared by name in a "fintech growth equity firm San Francisco" results page that carried a Spectrum/Turn-River/Mainsail listing; Invictus Growth Partners and Questa Capital appeared on a Clutch "Top Growth Equity Companies in San Francisco" page.
- Applying "keep only visibility_score ≥ 1" using this proxy would remove almost every firm, and the proxy doesn't measure what you asked for. So `visibility_score` is left **blank** for every row and no firm was dropped on that basis. Re-run this step with real Google data (or a SERP tool) before filtering.

## Candidate decisions

**Included (18):** Centana, Nexa Equity, Acrew Capital, Health Velocity Capital, Sansa Advisors, Peak Technology Partners, Invictus Growth Partners, Fin Capital, Tribe Capital, Flourish Ventures, Base10 Partners, Bloom Equity Partners, Metamora Growth Partners, Craft Ventures, Questa Capital, Camber Partners, Aphias Capital, Nfluence Partners.

**Excluded from your candidate list:**

| Firm | Reason |
|---|---|
| Madison Bay Capital Partners | Founded 2013 and HQ in New York (San Francisco is an office). |
| Cimbal Capital Group | Founded 2015 but HQ in Los Altos, and it does control buyouts in healthcare/industrial/defense tech. |
| Pilot Growth Equity | Founded 2011 (also offices in San Francisco and New York). |
| DBO Partners | Founded 2012 and acquired by Piper Sandler in 2022. |
| Vista Point Advisors | Founded 2011 (pre-2015). |
| Moorgate Capital Partners | Founded 2009/2010 and HQ in New York with a San Francisco office. |
| Serent Capital | Founded 2008, over $7B AUM, legacy scale. |
| Inhite Ventures | Founded 2004. |

**Excluded from my own searches:** PeakSpan Capital (HQ San Mateo), Redesign Health (not a San Francisco growth equity firm), Hustle Fund and CapitalX and Contrary Capital (pre-seed/seed, below the $5M+ mandate), Probitas Partners (founded 2001), Ridgecrest Capital Partners (2001), Banneker Partners (2010), Turn/River Capital (2012), Bregal Milestone (London), plus mega funds and legacy firms (Francisco Partners, Vista Equity, TPG, Genstar, Hellman & Friedman, GI Partners, Spectrum Equity, Mainsail).

**Could not verify, so left out:** Bradfield Capital, Encore Consumer Capital, Software Growth Partners, Arbor Advisors (Silicon Valley, not San Francisco), Atlas Technology Group.

## Calls I made

- A firm with a San Francisco office and another office is `needs_check` rather than `qualified`: Questa (Washington DC and San Francisco), Camber (San Francisco Bay Area city unconfirmed), Bloom Equity Partners (San Francisco versus New York conflict).
- VC firms whose stated mandate is seed/early (Acrew, Base10, Craft, Flourish) are kept as `needs_check`, since the $5M-$100M+ equity mandate may not fit.
- Nfluence Partners stays as `needs_check` because its founding year (2011, rebranded 2018) is borderline.
- Aggregator figures (AUM, headcount) are single-source and should not be treated as verified.

## Why not 30

Eighteen is the count that survives a reasonable HQ/founding filter using only search snippets. Getting to 30 would need either looser filters (older firms, non-San Francisco HQs) or direct access to sources I cannot reach from here.

## Next steps to finish the brief

1. Allow these hosts in the environment's network settings so I can read the firm sites and robots.txt: the 5 seed domains plus any candidates' domains, `crunchbase.com`, and `sec.gov` for Form ADV/Form D.
2. Run the Google visibility queries with a real SERP tool, then apply the ≥1 filter.
3. Run the articles check on each firm's site.
4. Fill the 12 remaining slots from the same SERP-driven searches.

The prompt you sent ended mid-sentence in the ARTICLES CHECK section ("Record the section URL, the post"), so I assumed the remaining fields were post titles and dates, and the CSV has columns for the section URL and 12-month post count only.

Files are in the repo directory and are not committed.
