# Changelog

Every release is archived on Zenodo under concept DOI [10.5281/zenodo.21833256](https://doi.org/10.5281/zenodo.21833256). Files are **added** between versions; earlier versions are never modified or withdrawn, and each keeps its own permanent DOI.

## Unreleased — added after the v2026-08 archive

**Added**

- `data/citevio-agency-study-2026-08-v2-answers.csv` (82 rows) and `data/citevio-agency-study-2026-08-v2-agencies.csv` (45 rows) — answer-level and agency-level records from Citevio's dental GEO agency-naming study, 20–21 August 2026 (ChatGPT and Perplexity, 23 questions, 2 runs each).
- `METHOD.md` — how the two files were produced, column definitions and a recount script.

**Boundaries**

Citevio chose the question set and is one of the subjects. The files list agency labels and source domains as they appeared in answers and contain no raw answer text.

## v2026-08 — 18 August 2026

**Added**

- `data/self-measurement-runs-2026-08.csv` — 13 completed answer-engine runs on fixed queries, 15–16 August 2026, recording whether the Citevio name and a Citevio-domain source appeared. Seven fields: `brand`, `query`, `engine`, `run_no`, `date`, `named`, `sourced`.
- `README.md`, published in the repository for the first time. Earlier releases carried the repository description only.
- `CHANGELOG.md` (this file) and `.zenodo.json` (archive metadata, so each release lands on Zenodo with the correct resource type, authors, licence and keywords without manual editing).

**Changed**

- `DATA-DICTIONARY.md`, `METHODOLOGY.md` and `LIMITATIONS.md` now document five files instead of four. The four market-scan sections are unchanged in substance; new sections cover the run log, and `LIMITATIONS.md` §11 states what it cannot support.
- `METHODOLOGY.md` — the opening section previously said that no file in the repository describes what an AI assistant said in an answer. That is still true of the four market-scan files and is no longer true of the repository as a whole, so the section now distinguishes the two.
- `CITATION.cff` — title, abstract, version and release date updated.

**Boundaries of the new file**

The run log measures **Citevio itself**, not the dental market. It is a vendor's self-report, published so that Citevio's own claims can be traced to dated rows. It is not independent research, it is not a benchmark, and its rows must not be appended to the market-scan files: the unit of analysis differs (one completed engine run, versus one website, domain, or aggregate segment). Raw engine response text is excluded because saved responses can contain unverified characterizations of third parties.

**Not changed**

The four market-scan CSV files are byte-identical to v2026-07. No figure previously published from them has been revised.

## v2026-07 — 7 August 2026

Initial release: four anonymized CSV files covering practice web anatomy (527 US dental practice websites, June 2026) and AI crawler access (6,497 domains nationwide plus 499 live crawler tests, July 2026), with methodology, limitations, data dictionary and citation metadata under CC BY 4.0.