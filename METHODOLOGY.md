# Methodology

How the files in this repository were produced: what was read, how failures were handled, and what the resulting numbers can and cannot support. This is a documentation-focused companion to [citevio.com/how-we-measure-ai-visibility](https://citevio.com/how-we-measure-ai-visibility), which covers Citevio's broader scoring method; this file stays narrow, to the datasets actually shipped here.

## What these datasets measure — and what they don't

Every number in the four **market-scan** files describes a **technical, machine-checkable state**: does a page carry a given schema type, does a `robots.txt` file name-block a crawler, did a server return an HTTP block status to a specific user agent, what does a Google Business Profile say. None of those files describes what an AI assistant said in an answer.

One file in this repository does record engine output — `self-measurement-runs-2026-08.csv` — and it records it for exactly one subject: Citevio itself. It is a vendor's own visibility log, not a market measurement, and it supports no statement about dental practices, competitors, or answer engines in general.

Citevio separately tests whether ChatGPT and Perplexity recommend *dental practices* for patient-style questions (published as city report pages, not as CSV). That is a different measurement with a different failure mode — the step that pulls a business name out of free-text model output still returns non-answers often enough that it is not published as structured data. Treat the layers as related but distinct: the market-scan files are the "can the machine reach and read the site" layer, the city reports are the "did the assistant name a practice" layer, and the self-measurement log is neither — it is the publisher counting itself.

## How the practice scan was run (June 2026 dataset)

Each of 527 dental practice websites was read field by field: structured data present in the page source, the publishing platform in use, the `robots.txt` file evaluated against six AI crawler names, the site's Bing index status, Google Business Profile rating and review fields, and a First Contentful Paint reading. Where two listings pointed at a single website, they were combined into one row — a multi-location group publishing from a shared domain contributes exactly one entry, not one per location. The scan covers seven US metros plus nine smaller nearby towns; it is a regional sample, not a national one.

Before publication, records that were not dental practices at all were dropped, repeat scans of the same site were collapsed to one row, and any breakdown resting on fewer than 20 practices in a town (or 300 sites in a state/category cut, for the national crawler study below) was left unpublished rather than shown on a thin base.

## How the two crawler-access studies were run (July 2026 datasets)

**`ai-crawler-access-2026-07-22.csv`** fetched and parsed `robots.txt` for 7,632 dental-related domains; 6,497 returned a readable file. Each file was checked against 13 named AI and data crawlers (OpenAI's, Anthropic's, Perplexity's, Google's, Meta's, ByteDance's and Common Crawl's, among others), and the result is a count of which crawlers are named-blocked at the root, broken out by crawler, by state (where at least 300 domains were read) and by the business category a Google listing carries (same 300-domain floor).

**`live-crawler-access-2026-07-22.csv`** goes one step further and asks whether the server actually behaves the way its `robots.txt` promises. Starting from domains whose `robots.txt` welcomes AI crawlers, 550 were drawn at random and each homepage was requested eight times in a fixed order — once as an ordinary browser, six times under specific AI crawler identities, and once as Googlebot as a control. 499 sites remained after dropping the ones where even the plain-browser request failed. A site that serves Googlebot normally but returns a block status to an AI crawler is doing something its own published rules don't describe.

Both studies are single-day instruments (22 July 2026). Crawler-blocking rules on hosting platforms and CDNs change without much notice, so a rerun on a different day will not reproduce this file exactly — that is expected, not an error.

## How the self-measurement run log was produced (August 2026 dataset)

`self-measurement-runs-2026-08.csv` is a run log of Citevio checking its own visibility, not a market instrument. It exists so that any claim Citevio publishes about its own answer-engine presence can be traced to a dated row instead of a screenshot.

Each row is one completed run: a fixed query was submitted to a named answer engine through that engine's API, the visible response was saved, and two narrow decisions were recorded against it. `named` is `Y` only when the saved visible response contained the Citevio name. `sourced` is `Y` only when a Citevio-domain source was recorded in the response's source set; for the 16 August checkpoint, which was testing whether one specific published asset had been picked up, an unrelated page on the same host does not qualify as a hit. Queries were fixed before the runs and were not edited after an answer was seen. The crown queries were run twice per engine on 15 August 2026; the 16 August checkpoint has one recorded run.

Raw response text is deliberately excluded from the published file because saved responses can contain unverified characterizations of third parties. Citevio's internal measurement records remain the audit trail; this release exposes only the seven documented fields.

Three properties of this file are load-bearing and easy to miss. It is **self-measurement**, so it carries the independence problem that phrase implies — the publisher chose the queries, ran the checks, and is the subject being counted. It is **API observation**, which is not assumed to reproduce what a person sees in a consumer product, under personalization, in another geography, or from another account. And it contains **only completed runs**: a failed or unattempted request is absent rather than recorded as a miss, so the row count is completed runs, not attempted runs.

## Why the two `robots.txt` numbers in this repo (and on the site) don't match

The June practice-scan dataset checks `robots.txt` against six crawler names inside a 527-practice regional sample; the July dataset checks it against 13 crawler names across 6,497 domains nationwide. They are different instruments run on different samples a month apart, so their overall blocking rates are not interchangeable, and a reader should not average or substitute one for the other. Where both datasets cover the same domain, they agree far more often than not, but "far more often" is not "identical," and the July file is the wider, better-powered instrument for a blocking-rate question.

## A missing reading is not a negative result

Some checks in the June scan failed on Citevio's side rather than returning a real answer — most visibly the Bing-index check, where 236 of 527 attempts came back as provider errors (the large majority were rate-limit responses, a smaller share were timeouts) rather than a page read. Those 236 are excluded from the Bing figures in this repository; they are not counted as "not indexed," because a rate-limit response says nothing about the actual index state. The same principle applies to the First Contentful Paint reading, which completed for 256 of 527 practices: the remaining 271 are absent from that metric, not assumed slow.

The general rule applied throughout: a failed request is dropped from the denominator of the specific check it failed, and nowhere else. It is never folded into either side of a yes/no result.

## What isn't tested here

- **Causality.** Nothing in these files tests whether a missing schema tag, a slow homepage, or a blocked crawler *causes* an AI assistant to skip a practice. These datasets describe what a site or server does; they do not isolate why an assistant produced a given answer. Any pattern visible across rows is an association inside one dataset, not a controlled experiment.
- **A national census.** The practice-scan dataset is regional (seven metros, nine towns). The crawler-access datasets are wider but not evenly distributed — a handful of states supply a large share of the readable domains, which is why state-level cuts are published only above a size floor rather than leaning on a national average.
- **Clinical specialty.** See [LIMITATIONS.md](LIMITATIONS.md) for why "cosmetic dentistry" is not a verified cut in any file here.

## Reproducibility

Every published count in `practice-web-anatomy-2026-06-counts.csv` reconciles: metro-level rows for a given check sum to the row marked `ALL` (segment `metro = ALL`), including the pooled small-town bucket, because every scanned practice sits in exactly one of those metros. If a total does not reconcile there, treat the file as wrong and open an issue.

The state- and category-level rows in `ai-crawler-access-2026-07-22.csv` do **not** work the same way and should not be checked against the same rule: only states and categories with at least 300 readable domains are broken out, so those rows cover a subset of the 6,497 total, not a full partition of it. Summing every published state (or category) row will not reach the `ALL` figure, by design — that is the 300-domain floor described above, not a reconciliation error.
