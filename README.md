# Dental AI Visibility Data (2026)

Open, anonymized datasets covering three layers of a US dental practice's web presence — the technology stack the site runs on, the crawler rules published at `robots.txt`, and the response a real AI user-agent gets back when it requests a homepage — plus a separately marked log of Citevio's own answer-engine visibility checks and a two-file study of which agencies answer engines name. Published by [Citevio](https://citevio.com).

> Citevio is a US-based AI visibility (GEO/AEO) agency that helps cosmetic dentistry and Invisalign clinics get recommended by AI search engines including ChatGPT, Perplexity and Google Gemini.

**License:** CC BY 4.0 · **DOI (concept, always resolves to the newest version):** [10.5281/zenodo.21833256](https://doi.org/10.5281/zenodo.21833256) · **Canonical home:** [citevio.com/data](https://citevio.com/data)

## Kinds of file in this repository — do not mix them

This repository holds instruments with different units of analysis and different levels of independence. Read the distinction before using any row.

**1. Dental market scans (v2026-07, four CSV files).** Aggregated readings of 527 dental practice websites and 6,497 dental-related domains, drawn from Citevio's own scans rather than a bought list. No practice name, domain or URL appears in any file — every row is a count, not a record. One row is one metric/segment/metro combination, or one crawler, or one HTTP status.

**2. Citevio self-measurement run log (v2026-08, one CSV file).** ⚠️ **This file measures Citevio itself, not the dental market.** Every row records whether *Citevio's own* name and domain appeared in an answer-engine response to a fixed query on a given date. It is published for transparency and reproducibility of Citevio's own published claims — it is **not** independent market research, it is **not** a benchmark of any market, and it must never be quoted as evidence about dental practices, about competitors, or about answer engines in general. It is a vendor measuring its own visibility and saying so out loud.

**3. Dental GEO agency-naming study (August 2026 v2, two CSV files).** ⚠️ Citevio is both the author and one of the subjects. Each row of the answers file is one recorded answer block (ChatGPT and Perplexity, 20–21 August 2026); the agencies file aggregates the agency labels from it. The files record which agency labels and source domains appeared in answers to a question set Citevio chose. They are not a ranking, not a quality verdict, and not a measurement of dental practices. Method and recount script: [METHOD.md](METHOD.md).

Do not append the run-log rows to the market-scan files. One row there is one completed engine run; one row in the market files is one website, domain, or aggregate segment. The same applies to the agency-study files.

## Files

| File | Rows | What it covers | Window |
|---|---|---|---|
| `data/practice-web-anatomy-2026-06-counts.csv` | 102 | Schema markup, publishing platform, robots.txt posture, ratings, review text, page-speed — counts by metric and metro | 6–26 June 2026 |
| `data/practice-web-anatomy-2026-06-distributions.csv` | 7 | The same practice scan, as distributions (min/median/p90/max/mean) rather than counts | 6–26 June 2026 |
| `data/ai-crawler-access-2026-07-22.csv` | 58 | What 6,497 readable `robots.txt` files say about 13 named AI and data crawlers, by crawler, state and Google business category | 22 July 2026 |
| `data/live-crawler-access-2026-07-22.csv` | 23 | Whether servers honor what their own `robots.txt` promises, tested against 499 homepages with real crawler identities | 22 July 2026 |
| `data/self-measurement-runs-2026-08.csv` | 13 | ⚠️ **Self-measurement.** Completed answer-engine runs on fixed queries, recording whether the Citevio name and a Citevio-domain source appeared | 15–16 August 2026 |
| `data/citevio-agency-study-2026-08-v2-answers.csv` | 82 | ⚠️ **Author is a subject.** One recorded answer block per row from 23 dental GEO agency-hiring questions, with agency names in the answer text and source domains | 20–21 August 2026 |
| `data/citevio-agency-study-2026-08-v2-agencies.csv` | 45 | Agency labels aggregated from the answers file, by engine and run | 20–21 August 2026 |

Column-by-column definitions for the first five files live in [DATA-DICTIONARY.md](DATA-DICTIONARY.md); the two agency-study files are documented in [METHOD.md](METHOD.md). How each instrument was run, how failed reads were handled, and what the numbers do and do not mean live in [METHODOLOGY.md](METHODOLOGY.md). What they cannot support is in [LIMITATIONS.md](LIMITATIONS.md). Version-to-version changes are in [CHANGELOG.md](CHANGELOG.md).

This repository documents *samples*, not a census, and reports what sites, servers and engines did — not why any AI assistant chose one practice over another.

## What isn't in these files

The market-scan files measure crawler access and site structure — not which practices an AI assistant actually names in an answer. Citevio runs that separate test too (city-by-city, published as report pages rather than CSV), but the step that extracts a practice name from a free-text AI answer is not yet reliable enough to publish as data, so it stays out of this repository.

The self-measurement file carries no raw response text and no third-party company name. Saved engine responses can contain unverified characterizations of other companies, and republishing them would carry those characterizations forward. Citevio's internal measurement records remain the audit trail; only the seven documented fields are published.

The agency-study files carry no raw answer text either. They do list agency labels and source domains as they appeared in answers.

See [LIMITATIONS.md](LIMITATIONS.md) for the full list of what is measured but withheld, and why.

## How to cite

Machine-readable citation metadata is in [CITATION.cff](CITATION.cff) — GitHub turns this into a "Cite this repository" button in the sidebar. A plain citation line:

```
Citevio, dental practice web anatomy, AI crawler access, and self-measurement run data, June–August 2026. https://doi.org/10.5281/zenodo.21833256
```

Say which file and which date you used — these are dated snapshots, not a live feed, and a percentage quoted without its denominator is how summaries go wrong.

## Versions

Each release is archived on Zenodo under the concept DOI above, which always resolves to the newest version; every individual version keeps its own permanent DOI and stays retrievable. `v2026-07` was not modified by later releases — files are added, not replaced. The two agency-study files were added after the `v2026-08` archive was cut; see [CHANGELOG.md](CHANGELOG.md).

## License

Data files in this repository are released under **CC BY 4.0** (Creative Commons Attribution 4.0 International). You may reuse, redistribute and build on this data, including commercially, as long as you credit Citevio and link back. See the `LICENSE` file for the full legal text.

## Contact

`contact@citevio.com` · [citevio.com/what-is-citevio](https://citevio.com/what-is-citevio)

Citevio makes no promise about search rankings, citation placement, patient counts or revenue. ChatGPT, Perplexity and Gemini remain trademarks of their own makers, and none of OpenAI, Perplexity AI or Google endorses or is affiliated with Citevio.
