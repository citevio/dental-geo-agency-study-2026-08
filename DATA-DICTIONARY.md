# Data Dictionary

Column-by-column reference for the first five CSV files in `data/`. Every column name below was read directly from the file header; every example row is copied unmodified from the file. If a file is ever regenerated with different columns, this dictionary is out of date until updated in the same commit. The first four files are dental market scans; the fifth is a Citevio self-measurement log and is documented separately below. The two agency-study files (`citevio-agency-study-2026-08-v2-answers.csv` and `citevio-agency-study-2026-08-v2-agencies.csv`) are documented in [METHOD.md](METHOD.md).

---

## `practice-web-anatomy-2026-06-counts.csv`

One row per metric/segment/metro combination. 102 data rows (103 lines including header).

| Column | Type | Description |
|---|---|---|
| `metric` | text | Which check this row belongs to: `coverage`, `platform`, `robots`, `schema`, `bing`, `review_rating_threshold`, or `site_speed_threshold`. |
| `segment` | text | The specific finding within that metric, e.g. `WordPress`, `Open to every AI crawler tested`, `No LocalBusiness or Dentist schema at all`. |
| `metro` | text | `ALL` for the whole 527-practice sample, or one of the seven scanned metros / the pooled `Other (9 smaller towns)` bucket. |
| `n` | integer | Count of practices matching this segment within this metro. |
| `denominator` | integer | The base the percentage is computed against — see `denominator_definition`. |
| `pct` | decimal | `n / denominator × 100`, to one decimal place. |
| `denominator_definition` | text | Plain-language statement of what the denominator holds, e.g. "practices with a valid reading in this metro." Denominators differ by row because a practice missing one reading is dropped only from that row. |

Example row: `coverage,practices scanned,Charlotte,153,527,29.0,all scanned practices`

Example row: `schema,No LocalBusiness or Dentist schema at all,ALL,284,527,53.9,practices with a valid reading; measurement errors (0) excluded`

---

## `practice-web-anatomy-2026-06-distributions.csv`

Same June 2026 practice scan, expressed as distributions instead of counts. 7 data rows.

| Column | Type | Description |
|---|---|---|
| `metric` | text | The measured field: `rating`, `review_count`, `photos`, `avg_words`, `positive_ratio`, `generic_ratio`, or `first_contentful_paint`. |
| `unit` | text | The unit the values are expressed in, e.g. `stars (1-5)`, `seconds`, `share 0-1`. |
| `n` | integer | Number of practices with a valid reading for this metric (523 for the Google-review fields, 256 for site speed). |
| `min` | decimal | Minimum observed value. |
| `p25` | decimal | 25th percentile. |
| `median` | decimal | 50th percentile. |
| `p75` | decimal | 75th percentile. |
| `p90` | decimal | 90th percentile. |
| `max` | decimal | Maximum observed value. |
| `mean` | decimal | Arithmetic mean. |
| `denominator_definition` | text | What the `n` for this row represents. |

Example row: `first_contentful_paint,seconds,256,0.79,2.12,3.01,4.27,6.61,13.62,3.63,practices with a completed speed reading`

`generic_ratio` is Citevio's own measure of how many of a practice's reviews read as generic (a Citevio-defined text classification), not a metric any review platform publishes natively.

---

## `ai-crawler-access-2026-07-22.csv`

`robots.txt` findings across 6,497 readable domains out of 7,632 requested, nationwide. 58 data rows.

| Column | Type | Description |
|---|---|---|
| `metric` | text | `robots_txt_verdict` (overall posture), `assistant_crawlers_blocked` (OpenAI/Anthropic/Perplexity crawlers only), or `crawler_blocked_at_root` (one named crawler). |
| `segment` | text | The specific finding or crawler name, e.g. `GPTBot`, `no robots.txt file returned`. |
| `breakdown` | text | What axis this row is cut by: `all` (whole sample), `state`, or `category`. |
| `group` | text | The value of that axis: `ALL`, a US state name, or a Google business category (`Dentist`, `Cosmetic dentist`, `Orthodontist`, `Dental clinic`). |
| `n` | integer | Count of domains matching this segment within this group. |
| `denominator` | integer | Domains read in this group. |
| `pct` | decimal | `n / denominator × 100`. |
| `denominator_definition` | text | What the denominator counts, and, for `state`/`category` rows, the note that the cut is published only where at least 300 domains were read. |

Example row: `crawler_blocked_at_root,Bytespider,all,ALL,722,6497,11.1,domains whose robots.txt could be fetched`

Example row: `robots_txt_verdict,blocks at least one tested crawler at the root,category,Cosmetic dentist,83,756,11.0,domains in category 'Cosmetic dentist' (published only where n>=300)`

⚠️ The `Cosmetic dentist` value under `group` is the business category **Google's own listing shows**, not a clinically verified specialism confirmed by Citevio. See [LIMITATIONS.md](LIMITATIONS.md).

---

## `live-crawler-access-2026-07-22.csv`

Whether 499 servers honored their own published `robots.txt` when an AI crawler actually requested the homepage. 23 data rows.

| Column | Type | Description |
|---|---|---|
| `metric` | text | `site_level` (one row = one site-level outcome), `crawler_refused` (one row = one crawler identity), or `ai_crawler_request_status` (one row = one HTTP status code observed). |
| `segment` | text | The specific outcome, crawler name, or HTTP status, e.g. `refused at least one AI crawler`, `ClaudeBot`, `HTTP 403`. |
| `n` | integer | Count of sites (for `site_level`/`crawler_refused`) or requests (for `ai_crawler_request_status`) matching this segment. |
| `denominator` | integer | 499 for site- and crawler-level rows; 2,994 for request-status rows (499 sites × 6 AI crawler identities each). |
| `pct` | decimal | `n / denominator × 100`. |
| `denominator_definition` | text | What the denominator counts. |

Example row: `site_level,refused an AI crawler while Googlebot was served normally,63,499,12.6,sites whose robots.txt allows AI crawlers and whose homepage loaded for a plain browser request`

Example row: `ai_crawler_request_status,HTTP 429,38,2994,1.3,AI crawler requests (6 per site)`

---

## `self-measurement-runs-2026-08.csv`

⚠️ **This file is not a dental market dataset.** One row is one completed answer-engine run for one query, recording whether Citevio's own name and domain appeared. It is a vendor's log of its own visibility, published for transparency about Citevio's own claims. Its rows must not be appended to the four market-scan files above: the unit of analysis, the subject, and the independence of the measurement are all different. 13 data rows.

| Column | Type | Description |
|---|---|---|
| `brand` | text | The brand whose appearance was checked. Always `citevio` in this release — the file measures the publisher, not the market. |
| `query` | text | The exact query string as recorded in the measurement file. Queries are fixed before a run and are not edited after an answer is seen. |
| `engine` | text | The answer engine that produced the response, as labelled in the measurement file. Engines are reported separately and are never pooled into a combined rate. |
| `run_no` | integer | The run identifier within a query–engine pair. The crown-query measurements were run twice per engine, so `run_no` is 1 or 2. The single-run checkpoint is represented as `1`. |
| `date` | date (YYYY-MM-DD) | The date stored with the measurement. Two dates appear in this release: the crown-query runs (15 August 2026) and a single-run checkpoint (16 August 2026). |
| `named` | `Y` / `N` | `Y` when the saved visible response contained the Citevio name; `N` otherwise. `N` means the name was absent from a **completed** response — it does not encode a failed or unattempted request. |
| `sourced` | `Y` / `N` | `Y` when a Citevio-domain source was recorded in the response's source set. For the 16 August checkpoint, `Y` would additionally require the specific target asset being checked; an unrelated page on the same host does not qualify. |

Example row: `citevio,"GEO agency for an Invisalign practice",perplexity,1,2026-08-15,Y,Y`

Example row: `citevio,"who are the top AI visibility companies for dentists",perplexity,1,2026-08-16,N,N`

### Values that do not appear in this file, and why

| Not published | Reason |
|---|---|
| Raw response text | Responses can contain unverified characterizations of third parties. Excluded on legal and accuracy grounds. |
| Third-party company names | Same reason. No competitor or vendor name appears in any field. |
| Position or rank of a mention | Position was observed during measurement but is not encoded as a field, because a two-run window cannot support a rank claim. |
| Error rows | Only completed runs are included. A failed or unattempted request is not represented as `N`; it is absent. Read the row count as completed runs, not attempted runs. |

The row count of this file is the number of completed runs — not the number of queries, not the number of practices, and not a share of anything.

---

## Columns you will not find in any file

No file in this repository carries a practice name, domain, street address, phone number, or any other identifier that resolves to a single business — that information exists only in Citevio's private scan records and is not published. No file carries a `vertical` or `specialty` column marking a practice as cosmetic, general, orthodontic or otherwise: that field does not exist in any scan record behind these files (see [LIMITATIONS.md](LIMITATIONS.md)).

No file carries raw answer-engine response text. Apart from the two agency-study files described in [METHOD.md](METHOD.md), which list agency labels and source domains as they appeared in answers, no file names a company other than Citevio.