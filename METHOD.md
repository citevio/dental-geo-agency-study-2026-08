# METHOD — dental GEO agency-naming study, August 2026 (v2)

This document describes how the two v2 agency-study files in `data/` were produced, what each
column means, and how a third party can recount every published figure from the files alone.

It is a method record. It is not a ranking, not a benchmark of any agency, and not a client
outcome. Every count below describes what was recorded in a specific set of answers on a
specific pair of dates.

**Files described here**

| File | Rows (excl. header) | Unit of analysis |
|---|---|---|
| `data/citevio-agency-study-2026-08-v2-answers.csv` | 82 | one recorded answer block |
| `data/citevio-agency-study-2026-08-v2-agencies.csv` | 45 | one retained agency label |

**License:** CC BY 4.0 (see `LICENSE`) · **Archive DOI:** [10.5281/zenodo.23143214](https://doi.org/10.5281/zenodo.23143214)
· **Canonical download:** [citevio.com/data](https://citevio.com/data)

> The DOI above archives repository version `2026-10`, published 4 October 2026. It is the first archived version that contains the two v2 agency-study files. The canonical download is `citevio.com/data`.

---

## 1. Scope

| Item | Value |
|---|---|
| Question set | 23 questions, listed in §5 (`question_set` = `elle2026-08`) |
| Engines | ChatGPT, Perplexity |
| Runs per engine | 2 |
| Possible question × engine × run cells | 23 × 2 × 2 = **92** |
| Recorded answer blocks | **82** |
| Dates | ChatGPT runs: 2026-08-20 · Perplexity runs: 2026-08-21 |
| Collection | Manual. Each question was entered in the engine's own web interface and the returned answer read by hand |

Two engines and two runs each is the full scope of this study. Any wider scope — more engines,
daily frequency, longer windows — belongs to a different instrument and is not represented in
these files.

### Why 82 and not 92

The answers file records **completed answer blocks only**. Ten of the 92 possible cells produced
no recorded block and therefore have no row:

| Question (§5 number) | ChatGPT r1 | ChatGPT r2 | Perplexity r1 | Perplexity r2 |
|---|:--:|:--:|:--:|:--:|
| 7 · AI visibility agency for a dental implants and All-on-4 practice | ● | — | ● | ● |
| 9 · best digital smile design marketing agency | — | — | ● | ● |
| 15 · which agency can get my dental practice cited in ChatGPT answers | ● | ● | ● | — |
| 17 · What is Citevio and are they legitimate? | ● | — | ● | — |
| 18 · Citevio reviews | ● | — | ● | — |
| 22 · citevio vs dental geo | ● | — | ● | — |

Per-run totals: ChatGPT run 1 = 22, ChatGPT run 2 = 18, Perplexity run 1 = 23,
Perplexity run 2 = 19. Sum = 82.

⚠️ The files carry **no reason code** for an absent cell. A missing row means no completed answer
block was recorded for that combination; it does not record whether the engine refused, errored,
timed out, or was not run. An absent cell must not be treated as a zero, and must not be counted
as evidence about any agency named or not named.

---

## 2. Unit of analysis — what counts as one answer block

One row of the answers file is **one completed answer returned by one engine for one question on
one run**. A row exists only when a readable answer body was returned and read.

Within a block, two different events are recorded separately and are never merged:

- **Named in text** — the string appears as an agency name in the answer's own prose.
- **Cited as source** — the domain appears in the engine's source list for that answer.

A block can carry either, both, or neither. In this study 33 blocks carried both, 10 carried a
name without the domain in the source list, and 4 carried the domain in the source list without
the name in the prose.

---

## 3. Column definitions

### 3.1 `citevio-agency-study-2026-08-v2-answers.csv`

| Column | Type | Definition |
|---|---|---|
| `question` | text | The question as entered, verbatim. One of the 23 in §5 |
| `question_set` | text | Set identifier. `elle2026-08` for every row in this file (`elle` = manually collected) |
| `engine` | text | `chatgpt` or `perplexity` |
| `run` | integer | `1` or `2` — which of the two passes for that engine |
| `date` | ISO date | Date the answer was read (`2026-08-20` for ChatGPT, `2026-08-21` for Perplexity) |
| `search_calls` | text | Number of web-search calls the engine reported for this answer. `1` in 78 rows, `none` in 4 rows where the engine answered without a reported search call |
| `sources_returned` | integer | Count of entries in the engine's source list for this answer. Range 0–30; `0` in 10 rows |
| `source_domains` | text, `\|`-delimited | Registrable domains from that source list, alphabetically sorted, one entry per domain. Empty in the 10 rows where no source list was returned. In all 82 rows the entry count equals `sources_returned` |
| `agencies_named` | text, `\|`-delimited | Agency labels appearing in the answer prose, in the order read. Empty in 12 rows |
| `tools_named` | text, `\|`-delimited | Software/tool labels appearing in the answer prose. Empty in 75 rows — most answers named agencies rather than tools |
| `citevio_named_in_text` | 0/1 | `1` when `Citevio` appears as an agency name in the answer prose |
| `citevio_cited_as_source` | 0/1 | `1` when `citevio.com` appears in that answer's source list |

Notes that affect a recount:

- `source_domains` holds **domains, not URLs**. Where an engine cited several pages on one domain,
  the domain was recorded once and `sources_returned` was recorded on the same de-duplicated
  basis: across all 82 rows the two agree exactly.
- `agencies_named` records the label **as written by the engine**. In this study no spelling
  variants required consolidation — the 45 distinct labels in this column map one-to-one, and
  count-for-count, onto the 45 rows of the agency file.
- Neither flag column implies causation. A name or a domain appearing in an answer is an
  observation about that answer, not evidence that any page influenced the engine.

### 3.2 `citevio-agency-study-2026-08-v2-agencies.csv`

One row per agency label retained across the study. 45 rows.

| Column | Type | Definition |
|---|---|---|
| `agency` | text | The label for the company, as recorded in `agencies_named`. One row per distinct label |
| `chatgpt_run1` | integer | Answer blocks in ChatGPT run 1 whose prose named this agency |
| `chatgpt_run2` | integer | Same, ChatGPT run 2 |
| `perplexity_run1` | integer | Same, Perplexity run 1 |
| `perplexity_run2` | integer | Same, Perplexity run 2 |
| `answers_total` | integer | Sum of the four engine-run columns. Maximum possible value is 82 |
| `repeated_in_both_runs_of` | text | Engines in which the label appeared in **both** runs: `ChatGPT`, `Perplexity`, `ChatGPT+Perplexity`, or empty |

A `0` in an engine-run column is a count of recorded appearances under this study design. It is
not a statement about the agency, and it is not comparable to a count from the v1 study or from
any other question set.

---

## 4. The two published figures and how they were derived

> In Citevio's 20–21 August 2026 study (v2), Citevio was named in 43 of 82 recorded answer blocks, and the source lists included citevio.com in 37.

- **43** = rows where `citevio_named_in_text = 1` (answers file), which equals the sum of the four
  engine-run columns on the `Citevio` row of the agency file (14 + 8 + 13 + 8).
- **37** = rows where `citevio_cited_as_source = 1`, which equals the number of rows whose
  `source_domains` list contains `citevio.com`.
- Denominator for both is **82**, the number of recorded answer blocks — not 92, and not the
  number of questions.

The study author is also a subject in the study: Citevio selected the question set, ran the
queries, and published the files. A different question set, a different pair of dates, or a
different engine pair can produce different counts.

---

## 5. The 23 questions

Order below is first appearance in the answers file.

1. AI search visibility agency for cosmetic dentists in the United States
2. GEO agency for an Invisalign practice
3. AI visibility agency for a veneers and smile makeover practice
4. free tool to check if my dental practice appears in AI search
5. best AI visibility agency for cosmetic dentists
6. who should I hire to get my Invisalign practice recommended by ChatGPT
7. AI visibility agency for a dental implants and All-on-4 practice
8. does AI recommend AACD-accredited cosmetic dentists
9. best digital smile design marketing agency
10. cosmetic dentistry marketing agency vs general dental marketing agency
11. AI visibility agency for a multi-location cosmetic dental group
12. agency that helps cosmetic dentists get recommended by ChatGPT
13. best GEO agency for dental practices in 2026
14. who are the top AI visibility companies for dentists
15. which agency can get my dental practice cited in ChatGPT answers
16. GEO agency for dental practices
17. What is Citevio and are they legitimate?
18. Citevio reviews
19. best cosmetic dentistry marketing agency
20. AI visibility agency for aesthetic dental practices
21. who tracks how often ChatGPT recommends a dental practice
22. citevio vs dental geo
23. AI visibility agency for elective dental procedures

Six of the 23 name a company or compare named companies (17, 18, 22 explicitly; 4, 14, 21 ask for
providers or tools). The remaining questions are category questions. The set was written by
Citevio and is published here so that its composition can be argued with.

---

## 6. Recounting the published figures

Files needed: `data/citevio-agency-study-2026-08-v2-answers.csv` and
`data/citevio-agency-study-2026-08-v2-agencies.csv`. No other input is required.

```python
import csv, collections

rows = list(csv.DictReader(open("data/citevio-agency-study-2026-08-v2-answers.csv",
                                encoding="utf-8-sig")))

print(len(rows))                                                    # 82 answer blocks
print(len({r["question"] for r in rows}))                           # 23 questions
print(sorted(collections.Counter(
    (r["engine"], r["run"]) for r in rows).items()))                # per engine-run totals

print(sum(1 for r in rows if r["citevio_named_in_text"] == "1"))    # 43
print(sum(1 for r in rows if r["citevio_cited_as_source"] == "1"))  # 37

# 37 recomputed from the raw source lists rather than from the flag column
print(sum(1 for r in rows
          if "citevio.com" in [d.strip() for d in r["source_domains"].split("|")]))  # 37

ag = list(csv.DictReader(open("data/citevio-agency-study-2026-08-v2-agencies.csv",
                              encoding="utf-8-sig")))
print(len(ag))                                                      # 45 agency labels
c = next(r for r in ag if r["agency"] == "Citevio")
print(sum(int(c[k]) for k in
          ("chatgpt_run1", "chatgpt_run2", "perplexity_run1", "perplexity_run2")))   # 43
```

Cross-checks that should hold for any agency row, not just `Citevio`:

- `answers_total` equals the sum of the four engine-run columns.
- `answers_total` for any agency is ≤ 82.
- For every one of the 45 labels, the number of answers-file rows whose `agencies_named` contains
  that label equals that label's `answers_total`. The agency file is a pure aggregation of the
  answers file and adds no information of its own.

A recount that disagrees with a figure above is a finding worth reporting to
`contact@citevio.com`; the files, not the summary text, are the record.

---

## 7. What these files cannot support

- **They are not a quality ranking.** Being named more often is a property of the answers
  recorded, not of the work any company does.
- **They are not a causal record.** Nothing here identifies why an engine named one company.
- **They are not comparable to the v1 files.** The earlier August study used a different question
  set and different dates. The two studies stand side by side and must not be pooled or averaged.
- **They are not a live feed.** Engine behaviour changes. These are readings from 20–21 August
  2026 and will not reproduce exactly on a later date.
- **Absent cells are not zeros.** See §1.

---

## 8. Citation

```
Citevio (2026). Dental GEO agency-naming study, August 2026 (v2):
answer-level and agency-level records. CC BY 4.0.
https://doi.org/10.5281/zenodo.22016876
```

State which file and which date you used. A share quoted without its 82-block denominator is the
most likely way this data gets misreported.

Publisher: Citevio · contact@citevio.com · +90-544-774-7558 · Sheridan, WY, US ·
Muhammed Veysel Erin, Founder.
