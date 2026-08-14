# AI Input Governance Framework

**Purpose:** Most AI quality problems trace back to inputs, not the model: stale data, unverified claims, and no accountable owner. This framework defines a set of gates that inputs must clear before they are used to produce AI-assisted work, so review time goes down instead of up.

## The Core Problem

AI output looks polished regardless of input quality. A sloppy draft used to look sloppy. A sloppy AI draft often doesn't, which means bad inputs now produce more review burden, not less, because errors are harder to spot. These gates exist to catch problems at the input stage, before they are laundered into confident-sounding output.

## The Gates

### Gate 1: Source of Truth

Every input must trace back to an approved, identifiable source (a system of record, a named document, a live data feed), not "I remember this" or an unsourced assumption.

- **Pass condition:** Source is named and locatable.
- **Fail condition:** Source is "general knowledge," a prior AI output, or unattributed.

### Gate 2: Freshness

Every input carries a last-verified date, and that date is within the staleness threshold for its category.

Suggested default thresholds (adjust per org):

| Category | Threshold |
| :-- | :-- |
| Pricing, inventory, headcount, org structure | 30 days |
| Market / competitive data | 90 days |
| Policy, legal, compliance language | 6 months or on-change |
| Foundational / reference material (brand guidelines, historical data) | 12 months |

- **Fail condition:** No date attached, or date exceeds threshold with no re-verification.

### Gate 3: Attribution at the Claim Level

Specific factual claims (numbers, quotes, named entities, dates) are traceable to a specific source, not just the document as a whole.

- **Pass condition:** A reader can find where each material claim came from.
- **Fail condition:** Claims are asserted without a traceable origin, even if the surrounding document is well-sourced.

### Gate 4: Named Owner

Every input package has one accountable human name attached. Not a team, not "marketing," a person.

This is the single highest-leverage gate: "the AI wrote it" stops being a valid defense once a name is required.

- **Fail condition:** No individual owner, or owner listed is not the person who actually assembled the input.

### Gate 5: Confidence Tiering

Inputs are tagged by stakes:

- **Low-stakes** (internal draft, brainstorm): light review, gates 1-4 optional.
- **Medium-stakes** (external-facing, non-binding): all gates required, single reviewer.
- **High-stakes** (legal, financial, public commitment, customer-facing numbers): all gates required, plus independent second-party fact-check before use.

- **Fail condition:** High-stakes input processed with low-stakes rigor.

### Gate 6: Change Detection

If the underlying source updates after the input was captured, there is a mechanism to flag that the AI-assisted output built on it may now be stale.

This does not need to be automated at first. Even a manual "recheck before quarterly reuse" rule closes most of the gap.

- **Fail condition:** Input is reused indefinitely with no re-verification trigger.

## Applying the Gates

| Stakes level | Gate 1 (Source) | Gate 2 (Freshness) | Gate 3 (Attribution) | Gate 4 (Owner) | Gate 5 (Tiering) | Gate 6 (Change detection) |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| Low | Recommended | Recommended | Optional | Required | n/a | Optional |
| Medium | Required | Required | Required | Required | Required | Recommended |
| High | Required | Required | Required | Required + 2nd reviewer | Required | Required |

## Rollout Notes

- Start with Gate 4 (named owner) alone if you can only introduce one thing. It changes behavior fastest and costs the least to implement.
- Frame this as an efficiency initiative, not a quality-control initiative, in cultures where "AI-first" is the stated direction: rework and review cycles are the actual cost being cut, not adoption being slowed.
- Measure review-time-per-deliverable before and after. That number is the argument, not a policy document.

## Prototype

A companion interactive tool (`index.html` in this repo) implements Gates 1-4 as an automated first-pass check: paste a piece of input content, and it evaluates sourcing, freshness signals, claim-level attribution, and named ownership, returning a pass / needs review / fail per gate with specific issues flagged.

Gates 5 and 6 are process controls, not text-inspectable properties, so the tool does not attempt them. Note also that the tool's freshness gate checks whether a verification date is present and plausible; it does not enforce the category thresholds above, which require knowing the input's category.
