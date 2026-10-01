<div align="center">

# 🏪 CX & Employee Intelligence Platform

### Operational intelligence platform for customer and employee support, with AI-powered auto-classification, sentiment analysis, and SLA prediction

<br>

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![XGBoost](https://img.shields.io/badge/XGBoost-SLA%20Predictor-FF6600?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Airflow](https://img.shields.io/badge/Apache-Airflow-017CEE?style=for-the-badge&logo=apacheairflow&logoColor=white)

<br>

> **Proof of Concept** — This project simulates the data architecture and AI models a nationwide retail company would need to transform its customer support operation from reactive to predictive.

<br>

[📊 Dashboards](#-dashboards) · [📐 Architecture](#-architecture) · [🤖 AI Models](#-ai-models) · [🩺 Diagnostics](#-diagnostics-and-lessons-from-the-process) · [🚀 Quick Start](#-quick-start) · [📁 Structure](#-project-structure)

</div>

---

## 🎯 The Problem

A convenience retail company with more than **20,000 points of sale** and millions of active customers faces an operational scale challenge that manual processes cannot solve:

| Symptom | Real-world impact |
|---|---|
| 6 support channels operating in silos | No unified customer view → inflated metrics |
| Manual ticket classification | Inconsistency across agents → unreliable data |
| Retroactive Excel reports | SLAs are missed before anyone sees it |
| No reincidence analysis | The same problem gets (badly) resolved over and over |
| Thousands of unprocessed social comments | Trends and crises detected days late |
| Internal tickets with no visibility | Employees don't know the status of their request |

**The consequence**: a reactive operation, rising costs, and a deterioration in customer and employee experience that can't be diagnosed precisely because the data isn't trustworthy.

---

## 💡 The Solution

An end-to-end data pipeline that turns operational chaos into actionable intelligence:

```
Raw data from 6+ channels  →  Validated ETL  →  Star-schema DWH  →  AI  →  Power BI
```

1. **Centralizes** external (customer) and internal (employee) tickets in a single DWH
2. **Validates** data quality at every layer before it reaches analysis
3. **Classifies** every ticket automatically with an NLP model trained on Spanish text
4. **Predicts** which tickets will breach their SLA 2+ hours in advance
5. **Analyzes** the sentiment of every interaction to detect dissatisfaction trends
6. **Exposes** everything in Power BI dashboards with drill-through, RLS, and automated alerts

---

## 📊 Dashboards
### Dashboard 1: CX Operations Board

*For Customer Experience managers and shift supervisors.*

**Page 1 — Executive Summary**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CX OPERATIONS BOARD            Today: Jun 18, 2025    [Updated: 14:32]     │
├───────────────┬───────────────┬──────────────┬──────────────┬───────────────┤
│ TICKETS TODAY │  SLA RESP %   │ SLA RESOL %  │    FCR %     │     NPS       │
│     1,847     │    96.2%  ✓  │   87.1%  ⚠️  │   71.4%  ✓  │    53.2   ✓  │
│  ▲ 43% vs avg │  target >95% │ target >90%  │ target >70%  │  target >50   │
├───────────────┴───────────────┴──────────────┴──────────────┴───────────────┤
│                                                                              │
│  SENTIMENT BY CHANNEL (today)                TICKETS AT SLA RISK            │
│                                                                              │
│  Facebook    ████████░░  0.62 😊           ┌────────────────────────────┐   │
│  Instagram   ██████░░░░  0.41 😐           │ CRITICAL (< 30 min)   ·  8 │   │
│  WhatsApp    ████░░░░░░ -0.18 😠 ⚠️         │ HIGH (30-2h, AI >70%) · 23 │   │
│  Email       ████████░░  0.55 😊           │ MEDIUM (2-4h, AI>50%) · 41 │   │
│  Chat        ███████░░░  0.48 😐           │ On time                ·  OK│   │
│                                             └────────────────────────────┘   │
│                                                                              │
│  VOLUME × HOUR OF DAY (today vs. Monday average)                            │
│                                                                              │
│  200 │                              ████                                     │
│  175 │                          ████████                                     │
│  150 │                      ████████████  ── today                          │
│  125 │              ████████████████████  ·· average                        │
│  100 │          ████████████████████████                                     │
│   75 │      ████████████████████████████                                     │
│       ────────────────────────────────────                                  │
│        6  7  8  9  10 11 12 13 14 15 16 17 18 19 20 21 22                  │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Page 2 — Channel Analysis**
Volume × hour heatmap · SLA % comparison across channels · Backlog waterfall

**Page 3 — Real-Time SLA Risk**
Table of tickets at high breach risk · AI score · Time remaining · Assigned agent

**Page 4 — Reincidence & Root Cause**
Categories with the highest reincidence · Average days between contacts · Failed-resolution analysis

**Page 5 — AI Performance Monitor**
Classifier accuracy by category · Confidence distribution · Tickets routed to human review

---

### Dashboard 2: Employee Service Dashboard

*For HR, IT, and operations coordinators.*

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  EMPLOYEE SERVICE DASHBOARD           [Updated: 14:32]                      │
├───────────────┬────────────────────┬──────────────────┬─────────────────────┤
│ TOTAL BACKLOG │   SLA COMPLIANCE   │    REINCIDENCE   │   BACKLOG > 30 DAYS │
│      247      │      82.3%  ⚠️     │     18.2%  ⚠️    │     12  🔴           │
├───────────────┴────────────────────┴──────────────────┴─────────────────────┤
│                                                                              │
│  BACKLOG AGING (open tickets)              TICKETS BY CATEGORY              │
│                                                                              │
│  0-7 days    ████████████████░   158 (64%)    Payroll / Pay     ████  89   │
│  8-15 days   ██████░░░░░░░░░░░    62 (25%)    IT Access          ███   71   │
│  16-30 days  ████░░░░░░░░░░░░░    15 (6%)     Uniforms           ██    48   │
│  > 30 days   ██░░░░░░░░░░░░░░░    12 (5%)  🔴 Credentials        ██    39   │
│                                                                              │
│  SLA COMPLIANCE BY RESPONSIBLE DEPARTMENT                                    │
│                                                                              │
│  Training       ████████████████░░  91%  ✓                                  │
│  Operations     ████████████████░░░  88%  ✓                                  │
│  HR             ██████████████░░░░░  79%  ⚠️                                 │
│  IT / Systems   ██████████░░░░░░░░░  63%  🔴 ← attention required           │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Notable DAX measures

```dax
// ── SLA Resolution Rate ──────────────────────────────────────────────────────
SLA Resolution % =
DIVIDE(
    CALCULATE(COUNTROWS(fact_tickets), fact_tickets[resolution_sla_met] = TRUE()),
    COUNTROWS(fact_tickets)
) * 100

// ── NPS Score ────────────────────────────────────────────────────────────────
NPS Score =
VAR Promoters  = CALCULATE(COUNTROWS(fact_tickets), fact_tickets[nps_score] >= 9)
VAR Detractors = CALCULATE(COUNTROWS(fact_tickets), fact_tickets[nps_score] <= 6)
VAR Total      = CALCULATE(COUNTROWS(fact_tickets), NOT ISBLANK(fact_tickets[nps_score]))
RETURN DIVIDE(Promoters - Detractors, Total) * 100

// ── Tickets at SLA Risk (for the real-time alert) ────────────────────────────
Tickets At Risk =
CALCULATE(
    COUNTROWS(fact_tickets),
    fact_tickets[sla_risk_level] IN {"CRITICAL_RISK", "HIGH_RISK"},
    fact_tickets[status] IN {"open", "in_progress", "pending"}
)

// ── Reincidence Rate ─────────────────────────────────────────────────────────
Reincidence Rate % =
DIVIDE(
    CALCULATE(COUNTROWS(fact_tickets), fact_tickets[is_reincidence] = TRUE()),
    COUNTROWS(fact_tickets)
) * 100

// ── WoW Change (previous-week comparison) ────────────────────────────────────
Tickets WoW % Change =
VAR ThisWeek  = CALCULATE(COUNTROWS(fact_tickets), DATESINPERIOD(dim_date[full_date], MAX(dim_date[full_date]), -7, DAY))
VAR LastWeek  = CALCULATE(COUNTROWS(fact_tickets), DATESINPERIOD(dim_date[full_date], MAX(dim_date[full_date]), -14, DAY))
RETURN DIVIDE(ThisWeek - LastWeek, LastWeek) * 100
```

---

## 📐 Architecture

![Platform architecture](./image/.Architecture_.png)

---

## 🤖 AI Models

### Module 1 — Ticket Classifier

Automatically classifies every ticket into the correct category at creation time, eliminating inconsistent manual classification.

```
Input:  Ticket text ("My payroll receipt from the 15th didn't arrive correctly")
Output: { category: "nomina_pago", confidence: 0.94, needs_review: false }
```

**Stack**: TF-IDF (ngram 1-2, 10K features) + Logistic Regression (class_weight balanced), calibrated with `CalibratedClassifierCV` (sigmoid/Platt)

**Low-confidence handling**: if `confidence < 0.50` → the ticket is flagged `needs_human_review = TRUE` and routed to manual review (threshold lowered from 0.75 on 2026-07-07, see below).

```
Real result (holdout by template, not a random split):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Macro F1-Score: 0.7203  (expanded corpus, 359 templates — was 0.4334 with 147)
Real accuracy:   73.64%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Why this number and not ~87%**: the first evaluation used a random
train/test split that left variants of the same message template on both
sides — the model learned to recognize the template, not the actual
category, and the measured F1 (~87%) reflected that data leakage, not real
generalization ability. Evaluated correctly with a holdout *by template*
(no template seen in train appears in test), the real macro F1 was 0.4334
with the original seed corpus (147 templates). After expanding the corpus
to 359 templates (prioritized by category according to the real measured
F1 — see `FASE_B_RESULTADOS.md`), the honest macro F1 rose to **0.7203**
and real accuracy to **73.64%**, measured with the same holdout
methodology.

**But expanding the corpus did not fix the confidence problem on its
own**: with the uncalibrated model, `low_confidence_rate` was still 99.4%
(previously 100%) — nearly every prediction remained below
`CONFIDENCE_THRESHOLD = 0.75`, even though the model was already correct
73.64% of the time. The cause: with 20 categories of partially
overlapping vocabulary, the softmax of an uncalibrated
`LogisticRegression` spreads probability across several plausible classes
even when it picks the right one — it isn't that the model is
untrustworthy, it's that its reported probability doesn't reflect its real
confidence.

**Fixed with `CalibratedClassifierCV`** (sigmoid/Platt): at the original
threshold (0.75), auto-classification coverage rose from **0.6% to
20.5%**, holding **95.7% accuracy** on those predictions — a ~34x increase
without sacrificing precision. Macro F1 also rose (0.7203 → 0.7503).

**[2026-07-07] Threshold lowered to 0.50** — a product decision made with
the sweep in `FASE_B_RESULTADOS.md §3.1` as evidence: accept slightly less
accuracy in exchange for substantially more coverage.

| | Threshold 0.75 | Threshold 0.50 (current) |
|---|---|---|
| Auto-classification coverage | 20.5% | **61.5%** |
| Accuracy on those predictions | 95.7% | **90.9%** |

`needs_human_review` now fires for ~38.5% of volume (previously ~79.5%
with the 0.75 threshold, ~99.4% uncalibrated). See
`FASE_B_RESULTADOS.md §3.1-3.2` for the full sweep (0.40-0.90) and the
details of this decision.

---

### Module 2 — Sentiment Analyzer

Analyzes the sentiment of every ticket interaction (customer messages).
The model in production **is not the Spanish BERT originally planned** —
it's a TF-IDF + Logistic Regression substitute, with the same
input/output contract.

```
Input:  "I've been waiting 3 days for a reply and nobody has contacted me, terrible service"
Output: { label: "negative", score: -0.91 }
```

**Actual model**: TF-IDF + Logistic Regression. **Why it isn't
`pysentimiento/robertuito-sentiment-analysis` (Spanish BERT) as planned**:
in the training sandbox, `huggingface.co` is outside the egress allowlist
(403 confirmed when attempting to download the model), and
`pysentimiento` pulls in `torch`+CUDA (~3.5 GB), which exhausted the
available disk halfway through installation. The inference wrapper is
compatible with both — migrating to the real BERT is a model change, not a
contract change, the day this runs on a machine with full internet and
disk.

**Real result**: macro F1 = **0.9898** on a holdout by template (it was
0.9515 with the original 147-template corpus; it rose after expanding to
359 for Phase B — see `FASE_C_RESULTADOS.md`) — unlike the classifier
(Module 1), this number already held up under correct evaluation even
before the corpus was expanded.

**Per-ticket aggregation**: recent interactions carry more weight. A
customer who starts out angry but ends up satisfied gets a different score
than one who starts well and ends up frustrated.

---

### Module 3 — SLA Breach Predictor

Predicts in real time which tickets have a high probability of breaching their SLA, enabling proactive agent reassignment.

```
Input:  Ticket features: channel, category, priority, hour of day,
        day of week, weekend flag, whether an agent is already assigned.

Output: { sla_breach_probability: 0.83, risk_level: "HIGH_RISK",
          minutes_to_breach: 47 }
```

**Stack**: XGBoost with `scale_pos_weight` computed from the real class imbalance

```
Real metric (model deployed today, 2026-07-07):
━━━━━━━━━━━━━━━━━━━━━━━━━━━
AUC-ROC: 0.6475
━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Why 0.65 and not 0.823, and why it isn't directly comparable to the
previous 0.56**: the first version of the model (*baseline* round)
measured AUC-ROC = 0.4862 — essentially chance — due to causal leakage in
the feature engineering. A later round (*causal_fix*) corrected that and
measured 0.5594, but **the code that applied that fix was lost entirely**
(not just the training script, but also the patch to the data generator) —
discovered while trying to improve the model today.
`data/synthetic/train_sla_model.py` was rebuilt with a new causal
structure (a reasonable reconstruction, not the original code) and
retrained: the model deployed today measures **0.6475**, but this number
**is not digit-for-digit comparable** to the historical 0.5594 — they're
different synthetic datasets. The 0.823 figure remains a number never
measured in this project.

**It was tested, with evidence, whether adding agent workload + SLA
history by category + message length would help** (see
`FASE_D_RESULTADOS.md §2.5`) — in a controlled 5-seed experiment, the
improvement averaged +0.0019 AUC: indistinguishable from noise. Those
three features **are not in the deployed model** (which is why they no
longer appear in the "Input" block above). It isn't that they were a bad
idea; the rest of the features already captured nearly all the signal
available in this data space.

---

### Module 4 — Executive Summary Generator

> **⚠️ Not implemented in this checkout** — there is no `ai/executive_summary/`
> nor any code for this module in the repo (confirmed 2026-07-06, see
> `ESTADO_REAL.md`). What follows is the planned specification, not a
> measured result or a working module, unlike Modules 1-3 (which do have
> code, trained models, and real metrics).

Planned: automatically generate the daily executive summary using an LLM, translating metrics into a decision-oriented narrative.

```python
# Example of the planned output (not generated by real code)
"""
CX EXECUTIVE SUMMARY — June 18, 2025

Overall status: ⚠️ A day under operational strain. Resolution SLA dropped
to 87% (target: 90%), driven mainly by WhatsApp, which processed 43% more
volume than expected starting at 14:00.

Critical channel: WhatsApp logged 1,847 tickets (vs. a 1,290 Monday average).
Resolution time was 4.2 hours, against a 2-hour SLA.
Probable cause: a spike of "incorrect charge" complaints in the Bajío region.

Highest reincidence: the "acceso_sistemas" category has a 28% reincidence
rate over 30 days, double the target. Resolution tickets record "access
restored" but employees report the same problem days later.

Sentiment: -0.21 (neutral-negative), consistent with last week.
No accelerated degradation, but no recovery either.

Priority actions for tomorrow:
1. Reinforce WhatsApp with 3 agents in the 13:00-17:00 window
2. Review the "acceso_sistemas" resolution protocol with the IT team
3. Investigate the cause of the Bajío spike (POS system issue?)
"""
```

---

## 🩺 Diagnostics and lessons from the process

- **Data leakage from a naive split (classifier)**: the original 87.4% came
  from a random train/test split that left variants of the same message
  template on both sides — the model memorized the template rather than
  learning the category. A holdout *by template* (leak-free) exposed the
  real number: macro F1 = 0.4334. The lesson isn't "the model is bad", it's
  that the split strategy determines whether the metric measures
  generalization or memorization.

- **0% real auto-classification, not 98.1% — and expanding the corpus
  wasn't enough to fix it; calibrating the model was**: measured under a
  holdout by template with the original corpus (147 templates), 100% of
  test predictions fell below the confidence threshold (0.75). The corpus
  was expanded to 359 templates (prioritized by each category's real F1)
  and macro F1 rose from 0.4334 to 0.7203 — a real, measured improvement.
  **But `low_confidence_rate` barely moved (100% → 99.4%)**: the model was
  already correct 73.64% of the time, yet with 20 categories of
  overlapping vocabulary the softmax of an uncalibrated
  `LogisticRegression` rarely exceeds 0.75 even when it's right. The root
  cause of the auto-classification symptom wasn't (only) corpus size — it
  was that the model's probability didn't reflect its real confidence.
  `CalibratedClassifierCV` (sigmoid) was applied over the same model:
  coverage rose from 0.6% to **20.5%** at the same 0.75 threshold, with
  95.7% accuracy on those predictions, and F1 also rose (0.72→0.75). The
  lesson: a reasonable hypothesis ("not enough data") can explain part of
  the problem (F1 did improve a lot) without explaining the symptom that
  motivated it (confidence barely changed) — you have to measure each
  effect separately, not assume that fixing one fixes the other. See
  `FASE_B_RESULTADOS.md` §3-3.1 for the full calibration analysis and the
  threshold sweep. **[2026-07-07]** That product decision has now been
  made: the threshold was lowered from 0.75 to 0.50, raising
  auto-classification coverage from 20.5% to **61.5%**, at the cost of
  dropping accuracy on those predictions from 95.7% to **90.9%** — the
  exact tradeoff already documented in the sweep before deciding. See
  `FASE_B_RESULTADOS.md` §3.2.

- **The SLA Predictor's "causal fix" code had also been lost — and the
  candidate features meant to improve it, tested with evidence, didn't
  help**: while trying to implement the improvements this very README
  recommended (agent workload, SLA history by category, message length), it
  turned out the patch connecting `resolution_sla_met` with peak
  hour/category/channel/weekend was never saved in `generate_data.py` —
  only the measured result (AUC 0.5594) survived, not the code. An
  equivalent causal generator was rebuilt and, with it, a controlled
  experiment: the 3 candidate features raised AUC by only +0.0019 on
  average across 5 seeds — within noise, not a real improvement. The
  decision was **not to deploy** that more complex model without a clear
  benefit. The lesson: a feature-engineering recommendation that sounds
  reasonable needs to be measured, not assumed — and "it didn't help" is
  also a valid result worth documenting, not just the ones that work. See
  `FASE_D_RESULTADOS.md §2.5` for the full experiment.

- **Audit log with hardcoded checks**: the synthetic data full-load writes a
  quality summary (`dq_checks_total/passed/failed`) as a fixed literal in the
  SQL, without computing it from the individual checks inserted in the same
  run. Auditing a real run confirmed the contradiction: the detail showed
  12/12 checks passed, the summary said 11/12. No validation ever failed —
  the summary number was simply never wired to a real calculation.

- **`ticket_id` collision incident**: a test sample (600 tickets) generated
  with the same synthetic generator as the production dataset unknowingly
  reused the same positional ID scheme. When loaded against the real
  database, the `UPSERT` (`ON CONFLICT DO UPDATE`) overwrote 600 real rows
  instead of inserting new ones. A scoped recovery search (volumes, backups,
  source data) found no way to restore them — they are considered
  permanently lost. It was fixed at the root on two fronts: sample IDs now
  use an exclusive prefix that never collides with production, and the
  loader now distinguishes and explicitly logs how many rows were real
  INSERTs vs. conflict-driven UPDATEs, so a future collision is immediately
  visible instead of silent.

- **The quality validation is not Great Expectations**: the pipeline
  implements by hand the same rules (not-null, range, uniqueness,
  duplicates) a GE suite would describe, without the dependency installed —
  a pragmatic decision to avoid tying the DAG to a heavy library,
  documented directly in the code.

- **A pipeline with an active cron keeps running between work sessions**:
  the DAG scheduled to run hourly did so autonomously during the time
  elapsed between manual validations, including a successful full load
  before anyone asked for it to be triggered by hand. The operational
  lesson: check the scheduler's pause state before assuming "nothing ran"
  just because nobody triggered it manually.

---

## 🎯 POC Results

With **13,000 synthetic tickets** simulating 90 days of operation:

| Metric | Result |
|---|---|
| Classifier F1-Score (macro, holdout by template) | **75.0%** (expanded corpus + calibrated; was 43.3%) |
| Classifier real accuracy (holdout by template) | **74.78%** |
| SLA Predictor AUC-ROC (model deployed 2026-07-07) | **0.65** (not digit-for-digit comparable to the previous `causal_fix` round, 0.56 — see `FASE_D_RESULTADOS.md` §2.5) |
| % auto-classified tickets (conf > 0.50) | **61.5%** (measured, calibrated + lowered threshold, see `FASE_B_RESULTADOS.md` §3.1-3.2) ⚠️ |
| Accuracy on auto-classified tickets | **90.9%** |
| Pipeline execution time (13K tickets) | 4m 32s * |
| Dashboard load time (Import Mode) | < 2s * |

⚠️ The 98.1% cited in the original version of this table came from the
split with template leakage (the same problem that inflated F1 to ~87%,
see Module 1). Measured under a holdout by template: expanding the corpus
(147→359 templates) raised F1 to 0.72 but left auto-classification
coverage at just 0.6% — the confidence threshold (designed for a simpler
problem than 20 categories with overlapping vocabulary) was almost never
exceeded, even though the model was already correct 73.64% of the time.
Calibrating the model (`CalibratedClassifierCV`) raised coverage to 20.5%
with 95.7% accuracy at the original threshold (0.75); lowering the
threshold to 0.50 (a product decision made on 2026-07-07, with the
threshold sweep as evidence) raised it further, to **61.5%** with **90.9%**
accuracy on those predictions. See "Diagnostics and lessons from the
process" below.

\* Figure from the original POC, not re-verified against a real run — see
"Diagnostics and lessons from the process" below.

### ⚠️ Illustrative simulation — not a measured result

The following table is a hypothetical projection of what the platform's
impact would look like **if the models reached the originally planned
metrics** (F1 87%, AUC 0.82). It is not a real measurement: there was no
instrumented "without platform" vs. "with platform" period, and the models
actually in production today (F1 0.75 for the classifier, AUC 0.65 for the
SLA predictor) perform well below what this simulation assumes. It is kept
as an illustration of the business case *if* those target metrics were
reached, not as evidence of a result.

| KPI | Without platform | With platform (hypothetical) | Δ |
|---|---|---|---|
| SLA Resolution % | 72% | 91% | +19pp |
| FCR Rate | 58% | 74% | +16pp |
| Reincidence Rate | 23% | 14% | -9pp |
| Manually classified tickets | 100% | 2% | -98% |
| Trend detection time | ~48 hours | < 2 hours | -96% |

---

## 🗃️ Data Model

A **star schema** architecture with 3 fact tables and 9 dimensions. Designed to support both complex analytical queries and Power BI loading in Import mode.

```
                          ┌───────────────┐
                          │   dim_date    │
                          │  date_key PK  │
                          └───────┬───────┘
                                  │
        ┌─────────────┐           │           ┌──────────────────┐
        │ dim_channel │           │           │   dim_category   │
        │channel_key  ├───────────┤           │  category_key PK │
        │channel_name │           │           │  sla_response_h  │
        │sla_defaults │           │           │  sla_resolution_h│
        └─────────────┘           │           └────────┬─────────┘
                                  │                    │
        ┌─────────────┐    ┌──────▼────────────────────▼──────┐    ┌─────────────┐
        │  dim_agent  │    │          fact_tickets             │    │dim_customer │
        │  agent_key  ├────┤                                   ├────│customer_key │
        │  team       │    │  ticket_key       PK              │    │(anonymized) │
        │  shift      │    │  ticket_id        natural key     │    └─────────────┘
        │  expertise  │    │  date_key         FK              │
        └─────────────┘    │  channel_key      FK              │    ┌─────────────┐
                           │  category_key     FK              │    │dim_employee │
        ┌─────────────┐    │  agent_key        FK              ├────│employee_key │
        │  dim_store  │    │  customer_key     FK (nullable)   │    │department   │
        │  store_key  ├────┤  employee_key     FK (nullable)   │    │region       │
        │  region     │    │  store_key        FK              │    └─────────────┘
        │  state      │    │                                   │
        └─────────────┘    │  — TIME METRICS —                 │
                           │  response_time_minutes            │
                           │  resolution_time_minutes          │
                           │  response_sla_met      BOOL       │
                           │  resolution_sla_met    BOOL       │
                           │  sla_breach_minutes    NUMERIC    │
                           │                                   │
                           │  — OPERATIONAL FLAGS —            │
                           │  is_reincidence        BOOL       │
                           │  escalated             BOOL       │
                           │  first_contact_resolved BOOL      │
                           │                                   │
                           │  — AI ENRICHMENT —                │
                           │  ai_predicted_category VARCHAR    │
                           │  ai_category_confidence NUMERIC   │
                           │  sentiment_score        NUMERIC   │
                           │  sentiment_label        VARCHAR   │
                           │  sla_breach_probability NUMERIC   │
                           │                                   │
                           │  — SATISFACTION —                 │
                           │  nps_score     INT                │
                           │  ces_score     INT                │
                           │  csat_score    INT                │
                           └───────────────────────────────────┘
```

### Fact tables

| Table | Grain | Estimated rows (90 days) |
|---|---|---|
| `fact_tickets` | 1 row per ticket | ~13,000 |
| `fact_interactions` | 1 row per message within the ticket | ~52,000 |
| `fact_daily_channel_metrics` | 1 row per channel per day (aggregated) | ~540 |

### Dimensions

| Dimension | Description | SCD Type |
|---|---|---|
| `dim_date` | Full calendar with Mexican holidays | Type 1 (static) |
| `dim_time` | Hourly granularity | Type 1 (static) |
| `dim_channel` | Support channels + SLA defaults | Type 1 |
| `dim_category` | Categories with SLA targets | Type 2 (SLAs change) |
| `dim_subcategory` | Hierarchical subcategories | Type 1 |
| `dim_agent` | Agents with team and shift | Type 2 (they change teams) |
| `dim_customer` | External customers (anonymized) | Type 1 |
| `dim_employee` | Internal employees | Type 2 |
| `dim_store` | Stores with region and state | Type 1 |

---

## 📈 Monitored KPIs

### External Customers

| KPI | Definition | Target | Source |
|---|---|---|---|
| **Volume by channel** | Tickets created per channel/day | Tracking | fact_tickets |
| **SLA Response %** | % of tickets with a first response on time | > 95% | fact_tickets |
| **SLA Resolution %** | % of tickets resolved on time | > 90% | fact_tickets |
| **FCR** | % resolved on first contact | > 70% | fact_tickets |
| **AHT** | Average handling time | < 30 min | fact_tickets |
| **Reincidence Rate** | % same customers, same problem, ≤30 days | < 15% | fact_tickets |
| **NPS** | Net Promoter Score | > 50 | fact_tickets |
| **Sentiment Score** | Average sentiment by channel | > 0.3 | fact_tickets + AI |
| **Escalation Rate** | % of escalated tickets | < 10% | fact_tickets |
| **AI Accuracy** | Classifier F1-score by category | > 85% | AI model |

### Internal Employees

| KPI | Target |
|---|---|
| **Backlog aging (> 30 days)** | 0% |
| **Internal SLA compliance** | > 85% |
| **Internal reincidence** | < 10% |
| **Duplicate tickets detected** | Tracking |
| **Resolution time by area** | Benchmark by category |

---

## 🚀 Quick Start

> This section was corrected on 2026-07-06 to reflect commands that
> actually exist in this checkout — the previous version referenced
> scripts and files that never existed here (`generate_external_tickets.py`,
> `scripts/init_db.py`, `etl/pipeline.py`, `requirements.txt`,
> `.env.example`, `ai/executive_summary/generator.py`). See `ESTADO_REAL.md`
> for the details of each correction.

### Prerequisites

```bash
Python 3.11+ (with faker, psycopg2-binary, numpy — for the data/synthetic/
              scripts, which run on the host, not in the containers)
Docker & Docker Compose
Power BI Desktop (if you want to build dashboards — there are no .pbix
                   files in this checkout, see Project Structure)
Git
```

### Installation

```bash
# 1. Clone the repository
git clone <repo-url>
cd airflow-docker

# 2. Environment variables
cp .env.example .env
# .env.example already includes AIRFLOW_UID and the postgres-oxxo credentials
# (DB_HOST, DB_NAME, DB_USER, DB_PASSWORD) that match
# docker-compose.yaml — nothing needs changing for the local environment.

# 3. Bring up the infrastructure
docker-compose up -d
# Starts: Airflow (scheduler + worker + apiserver + dag-processor +
#         triggerer) + Airflow metadata Postgres + postgres-oxxo
#         (the real DWH, oxxo_cx_intelligence) + Redis.
# Airflow available at http://localhost:8080

# 4. Install Python dependencies (to run scripts outside the containers)
pip install -r requirements-ai.txt
pip install faker psycopg2-binary numpy   # used by data/synthetic/, not in requirements-ai.txt
```

**About the DWH schema (`dwh`, `audit`, `marts`, `staging`)**: this
checkout **does not include the DDL to create it from scratch** — there is
no `sql/` folder and no `scripts/init_db.py`. The `pgdata_oxxo` volume is
declared `external: true` in `docker-compose.yaml` on purpose (so that
`docker-compose down -v` never deletes it), but that also means Compose
**does not create it**: it has to already exist as a Docker volume with the
schema and data loaded. In this development environment, `pgdata_oxxo`
already contained the full schema and 100,000 tickets from the June 29
full load (see `ESTADO_REAL.md §3.2, §3.7`). Reproducing this on a new
machine without that volume would require rebuilding the DDL by hand — it
is documented as a real limitation, not solved here.

### Generate data and run the pipeline

Two different generators, for two different purposes — don't confuse one
for the other (see `ESTADO_REAL.md §1`):

```bash
# A) Real full load (100,000 tickets) straight into Postgres — requires the
#    schema to already exist (see note above)
python data/synthetic/generate_data.py --tickets 100000

# B) A 600-ticket sample with real text (to test the DAG end to end without
#    touching the real Postgres). Runs on the host, not in the containers —
#    uses the seed corpus from seed_corpus_clientes.py /
#    seed_corpus_colaboradores.py via text_generator.py.
cd data/synthetic
python generate_ticket_samples.py --n 600
cd ../..
```

```bash
# Trigger the DAG (there is no standalone etl/pipeline.py — orchestration
# is Airflow, dags/cx_intelligence_pipeline.py)
docker exec airflow-docker-airflow-worker-1 airflow dags unpause cx_intelligence_pipeline
docker exec airflow-docker-airflow-worker-1 airflow dags trigger cx_intelligence_pipeline
# or from the UI: http://localhost:8080 → cx_intelligence_pipeline → Trigger

# ─── Real output of a run with the 600-ticket sample (staging/*.jsonl,
#     see ESTADO_REAL.md §2 for the run that produced these numbers) ───
# raw_external.jsonl          450
# raw_internal.jsonl          150
# validated_tickets.jsonl     600
# rejected_tickets.jsonl      0
# sla_calculated.jsonl        600
# reincidence_flagged.jsonl   600
# ai_classification.jsonl     600  (real classifier, calibrated)
# ai_sentiment.jsonl          600  (real sentiment, TF-IDF+LogReg)
# ai_sla_risk.jsonl           109  (only open/in_progress/pending tickets)
# dwh_snapshot.jsonl          600
# ──────────────────────────────────────────────────────────────────────
```

```bash
# (Optional) Retrain/recalibrate the Ticket Classifier
cd data/synthetic
python train_classifier.py
# Overwrites ai/classifier/models/ticket_classifier.joblib and metrics_fase_b.json
```

**Daily executive summary (Module 4)**: not implemented in this checkout —
see Module 4 above.

### Incremental execution

The DAG already runs on its own every hour during operating hours
(`0 6-23 * * *`, `dags/cx_intelligence_pipeline.py:56`) — there is no
separate `--incremental` mode and no standalone `etl/pipeline.py`. To
pause/resume that cron:

```bash
docker exec airflow-docker-airflow-worker-1 airflow dags pause cx_intelligence_pipeline
docker exec airflow-docker-airflow-worker-1 airflow dags unpause cx_intelligence_pipeline
```

---

## 📦 Full Tech Stack

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Language | Python | 3.11 | ETL, AI, scripts |
| Database | PostgreSQL | **16** | Main DWH |
| Orchestration | Apache Airflow | **3.2.2** | Pipeline scheduling |
| Data quality | Hand-written rules (no library) | — | The same rules Great Expectations would describe (not-null, range, uniqueness, duplicates) implemented directly in Python — **the `great_expectations` library is neither installed nor used** |
| Classical ML | Scikit-learn | **1.8** | Ticket classifier |
| Boosting | XGBoost | 2.0 (pinned `<3`, see note¹) | SLA predictor |
| Spanish NLP | TF-IDF + Logistic Regression | — | Substitute for `pysentimiento`/BERT (see Module 2) |
| Calibration | CalibratedClassifierCV (sklearn) | sigmoid/Platt | Real confidence for the Ticket Classifier (see Module 1) |
| LLM | Anthropic Claude API | claude-sonnet-4-6 | Planned for executive summaries — **not implemented in this checkout** (see Module 4) |
| Serialization | joblib | 1.3 | Model persistence |
| Visualization | Power BI Desktop | Latest | Planned for executive dashboards — **no `.pbix` files in this checkout** (see Project Structure) |
| Containers | Docker Compose | 3.9 | Reproducible environment |
| CI/CD | GitHub Actions | — | Workflow referenced, pending (no tests to run — there is no `tests/` folder) |
| Analysis | Jupyter | — | Planned for notebooks — **there is no `notebooks/` folder in this checkout** |

¹ `sla_breach_predictor.joblib` was serialized with XGBoost 2.x;
deserializing with 3.x fails (`XGBoostError: input stream corrupted`, a
format incompatibility between majors). Confirmed: works with 2.1.4, fails
with 3.3.0.

---

## 🗺️ Roadmap

```
Sprint 1 (Days 1-3)   ✅  PostgreSQL data model + synthetic data generator
Sprint 2 (Days 4-6)   ✅  ETL: extract + validate (own rules, not GE) + transform
Sprint 3 (Days 7-9)   ✅  Load to DWH, dimensions, working fact_tickets
Sprint 4 (Days 10-12) ✅  NLP classifier trained + Sentiment Analyzer
Sprint 5 (Days 13-15) ✅  SLA Predictor (XGBoost) + AI integration into the pipeline
Sprint 6 (Days 16-18) ✅  Power BI dashboard: CX Operations Board (5 pages)
Sprint 7 (Days 19-21) ✅  Power BI dashboard: Employee Service + AI Monitor
Sprint 8 (Days 22-24) ⚠️  Notebooks, final documentation, README (no test
                          suite — there is no tests/ folder in this repo)

── Future improvements (out of POC scope) ─────────────────────────────────────

v2.0  Upgrade the classifier to multilingual BERT (better accuracy on edge cases)
v2.0  Airflow DAG with retries and Slack/email alerts
v2.1  REST API (FastAPI) for real-time ticket classification
v2.1  Zendesk / Freshdesk integration via webhook
v3.0  BERTopic for automatic topic modeling of emerging trends
v3.0  Correlation analysis: customer tickets vs. store data (sales, inventory)
```

---

## 📁 Project Structure

> The tree below is the **real** content of this checkout (verified with
> `Get-ChildItem` on 2026-07-07, not an aspirational structure).
> Other sections of this README mention artifacts that **do not exist in
> this repo yet**: `.pbix` dashboards, notebooks, DDL in `sql/`,
> `ARCHITECTURE.md`/`DATA_MODEL.md`, `tests/`, and the CI workflow
> (see "Diagnostics and lessons from the process" and `ESTADO_REAL.md`).
> They are not listed here so as not to repeat the same inconsistency that
> was corrected in the rest of the document.

```
airflow-docker/
│
├── 📄 README.md                          ← This file
├── 📄 ESTADO_REAL.md                     ← Source of truth for the project's real state
│                                            (overrides this README wherever they disagree)
├── 📄 FASE_B_RESULTADOS.md               ← Ticket Classifier: per-category detail,
│                                            calibration, threshold sweep
├── 📄 FASE_C_RESULTADOS.md               ← Sentiment Analyzer: per-class detail +
│                                            migration snippet to real BERT (not executed)
├── 📄 FASE_D_RESULTADOS.md               ← SLA Predictor: SHAP per round, inference features
├── 📄 docker-compose.yaml                ← Airflow (scheduler/worker/apiserver/triggerer) +
│                                            metadata Postgres + postgres-oxxo (DWH) + Redis
├── 📄 Dockerfile
├── 📄 requirements-ai.txt
├── 📄 .env.example                       ← Copy to .env — nothing needs changing (see Quick Start)
├── 📄 .gitignore / .dockerignore
│
├── 📂 config/
│   └── airflow.cfg
│
├── 📂 dags/
│   └── cx_intelligence_pipeline.py       ← Airflow DAG (hourly, currently paused)
│
├── 📂 data/
│   ├── synthetic/
│   │   ├── generate_data.py              ← Synthetic full load (100k tickets + dims + audit.*)
│   │   ├── generate_ticket_samples.py    ← 600-ticket sample with real text (TEST- ids, no collision)
│   │   ├── seed_corpus_clientes.py       ← Seed corpus: 10 categories × 3 tones (182 templates)
│   │   ├── seed_corpus_colaboradores.py  ← Seed corpus: 10 categories × 3 tones (177 templates)
│   │   ├── text_generator.py             ← Generation engine: slots, synonyms, openings/closings
│   │   ├── train_classifier.py           ← Trains + calibrates the Ticket Classifier (holdout by template)
│   │   ├── train_sentiment.py            ← Trains the Sentiment Analyzer (same methodology)
│   │   └── train_sla_model.py            ← Trains the SLA Predictor (own causal dataset + A/B experiment)
│   ├── samples/
│   │   ├── external/                     ← facebook / instagram / whatsapp / email / chat_web (JSON)
│   │   └── internal/internal_tickets.csv
│   └── staging/                          ← Intermediate pipeline output (JSONL per stage)
│
├── 📂 etl/
│   ├── extractors/
│   │   ├── base_extractor.py
│   │   ├── json_channel_extractor.py
│   │   └── csv_internal_extractor.py
│   ├── transformers/
│   │   ├── sla_calculator.py
│   │   └── reincidence_detector.py
│   ├── loaders/
│   │   └── postgres_loader.py
│   ├── validation/
│   │   └── expectations_suite.py         ← Hand-written quality rules (does not use great_expectations)
│   └── common/
│       ├── catalog.py
│       ├── io.py
│       └── paths.py
│
├── 📂 ai/
│   ├── classifier/
│   │   ├── ticket_classifier.py          ← Inference wrapper (calibrated model)
│   │   ├── metrics_fase_b.json           ← Real metrics (+ .bak from the original 147-template corpus)
│   │   └── models/ticket_classifier.joblib
│   ├── sentiment/
│   │   ├── sentiment_analyzer.py         ← TF-IDF + LogReg (BERT substitute)
│   │   ├── metrics_fase_c.json           ← Real metrics (+ .bak from the original 147-template corpus)
│   │   └── models/sentiment_analyzer.joblib
│   └── sla_predictor/
│       ├── sla_model.py                  ← XGBoost (7 features, retrained 2026-07-07)
│       ├── metrics_fase_d.json           ← Real metrics (+ .bak from the pre-rebuild model)
│       └── models/sla_breach_predictor.joblib
│
└── 📂 monitoring/
    └── pipeline_monitor.py               ← Health check + run history
```

---

## 📄 License

MIT License — free for educational and portfolio use.

---

<div align="center">

**Built as a Proof of Concept for a Digital Transformation initiative in retail**

*This project uses entirely synthetic data generated for demonstration purposes.*
*It contains no real information from any company or organization.*

<br>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/cesar-rabago-perez)
[![GitHub](https://img.shields.io/badge/GitHub-See%20more%20projects-181717?style=for-the-badge&logo=github)](https://github.com/cesarrabago)

</div>
