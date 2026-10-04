# Limitations

What this data does not show. Read this before quoting a number from these files — it is the difference between an honest citation and a misleading one. If you are using `data/self-measurement-runs-2026-08.csv`, read **§11 first** — it is a different instrument with a different subject, and the sections below were written about the four market-scan files.

## 1. This is not a "cosmetic dentistry" dataset

Citevio's own positioning is narrow (cosmetic dentistry and Invisalign clinics). The scanned clinic lists behind these files are not: they are **every dental practice** Citevio's crawler found in a given metro or domain frame — general dentistry, orthodontics, prosthodontics, pediatric dentistry, all of it. In a name-based check limited to two of the seven scanned metros, roughly 4% of practices carried a word like "cosmetic" or "aesthetic" in their business name — an approximate, name-only read (not a clinical audit), and not necessarily representative of the other five metros. The overwhelming majority of scanned practices are ordinary general or specialty clinics with no cosmetic branding at all.

Two consequences follow directly:

- **A "cosmetic dentists" sample does not exist here.** No file in this repository, and no page on citevio.com, should ever be read as "N cosmetic dentists were scanned." The correct description is "N dental practices."
- **A cosmetic-specific rate cannot be computed from these files.** A statement like "X% of cosmetic dental clinics are invisible to AI" is not supported by this data, because there is no verified clinical-specialty field to divide by. The `Cosmetic dentist` value that appears under `group` in `ai-crawler-access-2026-07-22.csv` is the business category **Google's own listing shows** for that domain — a self-reported directory label, not a clinical verification that the practice performs cosmetic work. Do not treat the two as equivalent.

A field meant to classify each scanned practice by treatment focus (cosmetic / orthodontic / specialist / general practice, detected from the practice's own homepage text) exists in Citevio's scanner code, but it is not present in any of the 640 scan records collected so far (counted directly from the scan archive) — it was added after those scans ran and will only appear in future scan rounds. Until then, no clinically verified cosmetic-only cut is possible from any file Citevio has published or will publish from the current scan archive.

## 2. Sample, not census

The June 2026 practice-web-anatomy dataset covers seven US metros (led by Charlotte and Austin) plus nine smaller nearby towns — 527 practices in total. It supports statements about "this sample" or "these seven metros." It does not support a national claim about US dental practices as a whole.

The July 2026 crawler-access study is wider (6,497 readable domains nationwide) but not evenly spread: a small number of states supply a large share of the readable domains. That is why state-level and category-level breakdowns in `ai-crawler-access-2026-07-22.csv` are published only where at least 300 domains were read in that cut — below that floor, a percentage moves too easily on a handful of sites to be worth publishing.

## 3. One website is one row, not one location

Where two business listings shared a single website, the scan combined them into one row. That is correct when the thing being studied is a website — and wrong the moment you want a count of individual clinics or physical locations. A group with several offices publishing from one shared domain contributes a single entry, and any review or rating number attached to that entry reflects the one listing actually read, not the group's combined patient base.

## 4. Partial bases — a missing reading is not a negative result

Three fields in the June scan did not complete for every practice, and the gap is handled the same way every time: the practice is dropped from that specific row's denominator, not counted as a "no."

- **Site speed (First Contentful Paint):** a valid reading exists for 256 of the 527 scanned practices. The remaining 271 carry no value at all for this metric — there is no basis for guessing whether that missing group skews faster or slower, so no guess is made.
- **Bing index status:** a usable reading came back for 291 of 527 practices. The other 236 failed on Citevio's own request side — the large majority timed out on a provider rate limit, a smaller number failed outright — and are excluded rather than counted as "weak" or "not indexed." A rate-limited request describes a failed check, not a finding.
- **Bing index status by metro:** for the same reason, no per-metro Bing breakdown is published — the readable base per metro would be too thin after excluding the failures.

## 5. Two crawler-blocking rates, and they are not interchangeable

The June practice scan checks `robots.txt` against six named AI crawlers inside a 527-practice regional sample. The July study checks it against 13 named crawlers across 6,497 domains nationwide. They describe different instruments on different samples a month apart, and their headline blocking rates should never be swapped for each other or averaged together. Where a citation needs "the" blocking rate, the July file is the wider-powered instrument for that question; the June figure belongs with the rest of that regional scan.

## 6. Two different July numbers, and the qualifier is load-bearing

`ai-crawler-access-2026-07-22.csv` publishes both an all-13-crawlers blocking rate and a narrower rate counting only crawlers operated by OpenAI, Anthropic and Perplexity. These two figures answer different questions and are not substitutes for one another — a sentence that states one number while describing the other's crawler set is inaccurate regardless of which number is technically correct.

## 7. What Citevio measures but does not publish, and why

| Held back | Why |
|---|---|
| Foursquare listing match | The matching step returned unrelated businesses (hotels, gyms) for dental search terms in testing, so any count built on it describes the wrong businesses. Withheld entirely — no figure from this check appears anywhere. |
| Which specific practices an AI assistant names | The step that extracts a business name from a free-text AI answer still returns non-answers (phrases instead of practice names) often enough that a structured, publishable count is not yet possible. |
| A verified cosmetic-dentistry-only cut | No file in the current scan archive carries a verified clinical-specialty field. See §1. |
| Bing index status broken out by metro | The per-metro base is too thin once rate-limited and timed-out requests are excluded. See §4. |

Each of these will be published, dated, once the underlying instrument is fixed — not before.

## 8. Description, not cause

Nothing in these files tests whether a missing schema tag, a slow homepage, or a blocked crawler *causes* a practice to go unrecommended by an AI assistant. These datasets describe what a site or a server does. Any relationship visible across rows in a single dataset is an association, not a controlled experiment, and should be read and cited as such.

## 9. Deduplication is a best effort, not a guarantee

Before publication, scan records that were not dental practices at all were removed, and repeat scans of the same website (sometimes filed under two spellings of the same practice name) were collapsed into a single row. That process matches on domain, so it can miss cases where one practice genuinely runs two separate websites under two different names — a small number of such pairs were found and manually corrected in one metro during quality review, and it is possible (not confirmed) that a few more exist uncaught elsewhere in the archive. Where a citation needs an exact practice count for a single metro, treat the published figure as very slightly high for this reason rather than exact to the unit.

## 10. Point-in-time, not a live feed

Every file in this repository carries the scan window it was built from, in its own name and in `DATA-DICTIONARY.md`. None of it updates in real time. If a figure matters to a decision, check the scan date against today before relying on it — bot-blocking rules on hosting platforms in particular are known to change without much notice.

## 11. ⚠️ The self-measurement file measures Citevio, not the market

`data/self-measurement-runs-2026-08.csv` records whether *Citevio's own* name and domain appeared in answer-engine responses to a fixed set of queries on two dates. It is published so that Citevio's own public claims can be checked against dated rows rather than screenshots. Everything below applies to that file.

- **It is not independent.** The publisher chose the queries, ran the checks, and is the subject being counted. Treat it as a vendor's self-report — useful for verifying what Citevio says about itself, and not evidence about anything else.
- **It says nothing about dental practices.** No row describes a practice, a market, a competitor, or an industry pattern. A rate computed from these rows is a statement about one company's visibility on 15–16 August 2026 and nothing more.
- **It is a snapshot, not a trend.** Thirteen completed runs across two dates cannot establish durability, rank, persistence, or general visibility. A later run may differ with nothing having changed.
- **`named` and `sourced` are narrow string-and-source checks.** They do not measure recommendation strength, sentiment, position within an answer, or commercial effect. `Y` does not mean "recommended"; it means a name or a domain source was present in a saved response.
- **API observation is not a consumer interface.** These runs were collected through engine APIs and are not assumed to reproduce what a person sees in a consumer product, under personalization, in another geography, or from another account.
- **Only completed runs appear.** A failed or unattempted request is absent, not recorded as a miss. Read the row count as completed runs, not attempted runs.
- **Nothing here establishes a publication effect.** The 16 August row is a single recorded observation taken after an asset was published; one observation cannot attribute a result to that publication.
- **Raw responses are not published**, because saved engine responses can contain unverified characterizations of third parties.
- **Do not merge it with the market-scan files.** One is a run log; the others are site-reading datasets. They share no unit of analysis.
