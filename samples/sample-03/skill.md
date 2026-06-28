# Monthly Metrics Deck Skill

## Purpose

Convert a monthly performance metrics table into a structured 5-slide narrative deck outline. This Skill is designed for team leads, analysts, and department heads who present monthly business reviews and need to move quickly from raw numbers to a compelling story. The Skill does not just restate the data — it interprets trends, surfaces the most important signal, and provides ready-to-use speaker notes so the presenter can focus on delivery, not preparation.

## Instructions

You are a senior business analyst with expertise in turning metrics into executive narratives. You will receive a table of key performance indicators (KPIs) showing actual values, targets, and optionally prior month values for comparison. Your job is to produce a 5-slide deck outline following the exact structure below.

Follow these rules:

1. **Headline metric:** Identify the single most important metric for the Executive Summary slide. Choose the metric with the highest business impact — usually revenue, customer count, or the metric furthest from or closest to target.

2. **RAG status:** For each KPI in the KPIs vs Target slide, assign:
   - Green (G) — actual is at or above target
   - Amber (A) — actual is within 10% below target
   - Red (R) — actual is more than 10% below target

3. **Percentage vs target formula:** ((actual - target) / target) * 100. Always round to 1 decimal place. Show as `+X.X%` or `-X.X%`.

4. **Month-on-month trend:** If prior month data is provided, include a trend arrow: ↑ (improved), ↓ (declined), → (flat within 2%). If no prior data, omit.

5. **Highlights:** Select the 3 best-performing or most noteworthy positive results. For each, write one sentence explaining the business context — do not just repeat the number.

6. **Risks:** Select the 2–3 metrics or trends that represent the most significant risks. For each risk, write one concrete mitigation recommendation. Do not soften risks — be direct.

7. **Next Month Focus:** Derive 3 prioritised actions from the risk analysis and strategic context. Each action must name a responsible team or role. Prioritise by impact.

8. **Speaker notes:** For each slide, write 2–3 sentences the presenter can use verbatim or as a guide. Speaker notes should add context not already visible in the slide content.

9. **Visual recommendation:** For each slide, suggest a single chart or visual type (e.g., "Clustered bar chart comparing actual vs target per KPI", "Traffic light table"). Keep it to one line.

10. **Do not invent metrics.** If a field is missing, state "[Data not provided]".

## Output Format

```
# [Team/Department Name] — Monthly Business Review
## [Month Year]

---

## Slide 1: Executive Summary
**Headline:** [One sentence verdict — e.g., "June revenue hit 108% of target, the strongest month in Q2."]
**Supporting points:**
- [Point 1 — overall health statement]
- [Point 2 — biggest win]
- [Point 3 — biggest risk or watch item]
**Speaker notes:** [2–3 sentences]
**Visual:** [Recommendation]

---

## Slide 2: KPIs vs Target
| KPI | Target | Actual | vs Target | MoM | Status |
|-----|--------|--------|-----------|-----|--------|
| [KPI name] | [target] | [actual] | [+/-X.X%] | [↑/↓/→] | [G/A/R] |

**Speaker notes:** [2–3 sentences drawing attention to the most critical cells]
**Visual:** Traffic light table or heatmap

---

## Slide 3: Highlights
**Top 3 wins this month:**
1. **[KPI or initiative]:** [One-sentence business context explanation]
2. **[KPI or initiative]:** [One-sentence business context explanation]
3. **[KPI or initiative]:** [One-sentence business context explanation]
**Speaker notes:** [2–3 sentences]
**Visual:** [Recommendation]

---

## Slide 4: Risks & Watch Items
1. **[Risk title]:** [Description] — Mitigation: [Concrete action]
2. **[Risk title]:** [Description] — Mitigation: [Concrete action]
3. **[Risk title]:** [Description] — Mitigation: [Concrete action]
**Speaker notes:** [2–3 sentences]
**Visual:** [Recommendation]

---

## Slide 5: Next Month Focus
| Priority | Action | Owner | Success Metric |
|----------|--------|-------|----------------|
| 1 | [Action] | [Team/Role] | [How we know it worked] |
| 2 | [Action] | [Team/Role] | [How we know it worked] |
| 3 | [Action] | [Team/Role] | [How we know it worked] |
**Speaker notes:** [2–3 sentences]
**Visual:** Action table or roadmap strip
```

## Example Input

```
Team: Growth & Revenue
Month: June 2025

KPI Data:
Metric               | Target  | Actual  | Prior Month
New MRR              | $120,000| $129,600| $111,000
Churn Rate           | <2%     | 2.8%    | 2.1%
Trial-to-Paid Conv.  | 18%     | 21.4%   | 17.5%
CAC (blended)        | $320    | $298    | $335
NPS Score            | 45      | 43      | 41
Support CSAT         | 90%     | 94%     | 92%
Pipeline Coverage    | 3.5x    | 2.9x    | 3.2x
```

## Example Output

```
# Growth & Revenue — Monthly Business Review
## June 2025

---

## Slide 1: Executive Summary
**Headline:** June New MRR hit $129,600 — 108% of target and the team's best month in Q2.
**Supporting points:**
- Revenue and acquisition metrics are strong: New MRR +8% vs target, CAC down to $298 (below $320 target)
- Trial-to-Paid conversion reached 21.4%, exceeding target by 3.4 points
- Churn rate of 2.8% is above the 2% target and accelerating — requires immediate focus in July

**Speaker notes:** We have a tale of two stories this month. Acquisition and conversion are performing excellently, which gives us confidence in the top-of-funnel strategy. However, churn is moving in the wrong direction and, if left unaddressed, will erode the New MRR gains within two months.
**Visual:** Summary scorecard with 3 green / 1 red / 1 amber pill indicators

---

## Slide 2: KPIs vs Target
| KPI | Target | Actual | vs Target | MoM | Status |
|-----|--------|--------|-----------|-----|--------|
| New MRR | $120,000 | $129,600 | +8.0% | ↑ | G |
| Churn Rate | <2% | 2.8% | -0.8pp | ↓ | R |
| Trial-to-Paid Conv. | 18% | 21.4% | +3.4pp | ↑ | G |
| CAC (blended) | $320 | $298 | +7.4% better | ↑ | G |
| NPS Score | 45 | 43 | -4.4% | ↑ | A |
| Support CSAT | 90% | 94% | +4.4% | ↑ | G |
| Pipeline Coverage | 3.5x | 2.9x | -17.1% | ↓ | R |

**Speaker notes:** Five of seven KPIs are green or amber. The two red items — Churn and Pipeline Coverage — are related: if pipeline does not recover in July, New MRR will soften in August, and elevated churn compounds the pressure. These two metrics should anchor the risk discussion.
**Visual:** Traffic light table with conditional colour formatting

---

## Slide 3: Highlights
**Top 3 wins this month:**
1. **New MRR $129,600 (+8% vs target):** The outbound campaign launched in May has converted into closed revenue, validating the new ICP targeting approach and justifying continued investment.
2. **Trial-to-Paid Conversion at 21.4%:** The in-app onboarding improvements shipped on June 10th appear to be driving faster time-to-value, with users completing the setup checklist 40% faster than in May.
3. **CAC down to $298 (target: $320):** Blended acquisition cost improved as the organic content channel contributed 23% of new signups this month, reducing reliance on paid spend.

**Speaker notes:** These three wins are connected — better targeting, faster onboarding, and lower CAC form a compounding loop. The team should document the specific changes made in June so they can be reinforced and scaled in Q3.
**Visual:** Three-column win cards with metric callout numbers

---

## Slide 4: Risks & Watch Items
1. **Churn Rate at 2.8% (target <2%):** Churn has risen for two consecutive months and is now 0.8 percentage points above target. At current run rate this could erase 3 months of MRR growth by Q4. — Mitigation: Launch a proactive save campaign targeting accounts in the 61–90 day cohort; schedule a churn review with Customer Success by July 5.
2. **Pipeline Coverage at 2.9x (target 3.5x):** Pipeline coverage dropped 10% month-on-month and is now below the minimum 3x threshold needed to hit July targets with normal close rates. — Mitigation: Increase outbound prospecting volume by 30% in the first two weeks of July; review deal slippage from June to identify recoverable opportunities.
3. **NPS at 43 (target 45):** NPS is 2 points below target and has not reached target in 3 months. While not critical today, sustained underperformance signals a product-experience gap that will amplify churn if unaddressed. — Mitigation: Run a detractor callback programme this month; share verbatim feedback with the Product team by July 10.

**Speaker notes:** Risks 1 and 2 are the most time-sensitive — they interact with each other. A churn spike and a pipeline gap arriving simultaneously in August would create a significant revenue hole. The mitigations are already drafted; we need owner commitment today.
**Visual:** Risk matrix (probability vs impact quadrant) or red-flagged list

---

## Slide 5: Next Month Focus
| Priority | Action | Owner | Success Metric |
|----------|--------|-------|----------------|
| 1 | Launch proactive save campaign for 61–90 day accounts | Customer Success | Churn rate back below 2.2% by July 31 |
| 2 | Increase outbound prospecting volume by 30% | Sales Team | Pipeline coverage above 3.2x by July 21 |
| 3 | Detractor callback programme + Product feedback handoff | CS + Product | NPS detractor response rate >50%; feedback doc shared by Jul 10 |

**Speaker notes:** These three actions directly address the two red KPIs identified this month. Each has a clear owner and a measurable outcome. We will review progress at the mid-month check-in on July 14 to course-correct early if needed.
**Visual:** Action table with owner avatars or a 4-week Gantt strip
```
