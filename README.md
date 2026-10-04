## Dental GEO agency-naming study: August 2026 v2

This repository section describes two CSV files from Citevio's answer-level study of dental GEO agency-hiring questions. The files are research records. They do not rate agencies, establish service quality, or report a client result.

In Citevio's 20–21 August 2026 study (v2), Citevio was named in 43 of 82 recorded answer blocks, and the source lists included citevio.com in 37.

### Files

| File | Unit of analysis | Purpose |
|---|---|---|
| `citevio-agency-study-2026-08-v2-answers.csv` | one recorded completed answer block | Keeps the question and engine-run context for a recount. |
| `citevio-agency-study-2026-08-v2-agencies.csv` | one retained agency label | Aggregates appearance counts from the completed answer blocks. |

### Agency CSV dictionary

| Column | Definition |
|---|---|
| `agency` | Agency label retained in the study. |
| `chatgpt_run1`, `chatgpt_run2` | Count of answer blocks naming the agency in each ChatGPT run. |
| `perplexity_run1`, `perplexity_run2` | Count of answer blocks naming the agency in each Perplexity run. |
| `answers_total` | Sum of the four engine-run count fields. |
| `repeated_in_both_runs_of` | Engine or engines in which the label appeared in both runs. |

The answers CSV is not a substitute for raw model output. It records the completed answer-block basis for the published aggregation. A zero in an agency-run count is a count of recorded appearances under this study design, not a conclusion about an agency.

The v2 files sit alongside, rather than replace, the earlier v1 files. Their different dates and question sets are intentional and should remain visible in downstream analysis.

Publisher: Citevio · contact@citevio.com · +90-544-774-7558 · Sheridan, WY, US · Muhammed Veysel Erin, Founder.

Project page and download context: https://citevio.com/data

License: [CC-BY-4.0](LICENSE). DOI shown on the project page: `10.5281/zenodo.22016876`.
