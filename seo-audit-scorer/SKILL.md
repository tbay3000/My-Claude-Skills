---
name: seo-audit-scorer
description: >
  Score a client's completed quarterly SEO audit checklist against the fixed
  5-category/100-point rubric (Website Foundation, GBP Optimization, Local SEO
  & Map Pack, Off-Page Authority, Brand Visibility) and produce full quarterly
  reporting: scored breakdown with reasoning, Quarterly Highlights (Ranking
  Summary + What Got Better), Key Focus Areas This Quarter, Client Action
  Items, Performance Metrics at a Glance, Suggested Talking Points, and
  ClickUp cards (Title + Why We're Doing This). Use whenever the user pastes a
  completed audit checklist (Y/N or short-answer questions like "Is Business
  Name correct?", "Website Speed within Range?"), shares rank-tracker data
  (e.g. Local Dominator), or asks to "score this audit," "score the
  campaign," write "quarterly notes/highlights," or build ClickUp cards from
  audit findings — even without the word "audit." Does NOT do its own
  research — all data comes from the user. If Claude should autonomously
  research a client itself, use quarterly-seo-audit instead.
---

# SEO Audit Scorer

Scores a completed quarterly audit checklist against the fixed rubric and turns it into client-ready reporting plus internal ClickUp cards. No autonomous research — the user supplies everything.

---

## Step 1: Collect Inputs

Ask for (or extract from what's already been pasted):

1. **This quarter's completed checklist** — the Y/N / short-answer audit responses.
2. **Previous quarter's checklist + scores**, if this isn't the client's first audit. Needed for the quarter-over-quarter comparison that drives Highlights.
3. **Ranking data**, if available (e.g. Local Dominator). Note the convention: **lower position number = better ranking.** Never invert this.

Do not go fetch or verify any of this yourself — treat everything the user provides as ground truth.

**If this is the client's first-ever audit (no prior quarter to compare):** don't assume how to handle it — ask the user how they want to handle scoring/highlights for a baseline audit before proceeding.

**Checklist completeness check:** Read `references/audit-checklist.md` — it has the fixed 46-item checklist across GBP, Website, Citations/Brand Entity, GSC/Indexing, and Ahrefs/Heatmap. Compare what the user pasted against this list. If items are missing, note the gap briefly (e.g. "I don't see answers for GSC indexing questions — I'll flag those as data gaps") and proceed with what's available. Don't block waiting for 100% completeness.

---

## Step 2: Score Each Category

Read `references/scoring-rubric.md` for the full band definitions before scoring. Five categories, 0–20 each, 100 total.

For each category:
- Map the relevant checklist answers to the rubric bands (the checklist file notes which checklist section feeds which category — some checklist sections feed more than one category, e.g. Ahrefs/Heatmap data informs both Off-Page Authority and Local SEO).
- Land on a score and **write 2-4 sentences of reasoning** citing the specific checklist findings that justify it (e.g. "Title tags are now optimized and local schema is fixed — real progress. Still no blog and no location pages, which caps the score here.").
- If comparing to a previous quarter, note the point change and what specifically drove it.

Sum for the total score, then apply the health status band from the rubric (🔥 Critical / 🔴 Red / 🟡 Yellow / 🟢 Green).

**Output this as a table:**

| Category | Last Quarter | This Quarter | Change |
|---|---|---|---|
| Website Foundation & On-Page SEO | XX | XX | +/-X |
| GBP Optimization | XX | XX | +/-X |
| Local SEO & Map Pack | XX | XX | +/-X |
| Off-Page Authority | XX | XX | +/-X |
| Brand Visibility & Indexation | XX | XX | +/-X |
| **Total** | **XX** 🔴 | **XX** 🟡 | **+/-X** |

Followed by the reasoning for each category.

For a baseline (first-ever) audit, drop the Last Quarter / Change columns and just show the current score.

---

## Step 3: Quarterly Highlights

Two parts, in this order:

**Ranking Summary** — compare this quarter's ranking data (e.g. Local Dominator) against last quarter's, keyword by keyword. Remember: **lower position number = better ranking.**

Group keywords into three buckets and format like this:

```
Rankings Summary ([Start Month] → [End Month] [Year]):

🔺 Strong Improvements
- [Keyword]: [old] → [new] ✅ [short qualifier, e.g. "significant gain" / "major improvement"]

✅ Stable / Slight Gains
- [Keyword]: [old] → [new] ([short qualifier, e.g. "essentially flat, still strong" / "marginal improvement"])

🔻 Concerning Drops
- [Keyword]: [old] → [new] ⚠️ [short qualifier, e.g. "major drop" / "significant loss"]
```

**Bucket thresholds** (rule of thumb, not rigid — use judgment for borderline cases):
- **Strong Improvements**: position improved by roughly 0.5+ points.
- **Stable / Slight Gains**: position improved by less than ~0.3 points — essentially holding.
- **Concerning Drops**: any decline, regardless of size. Scale the qualifier phrase and the ⚠️ to the magnitude — a 1.5+ point drop is "major drop" / "significant loss"; a decline of 0.1-0.2 is "slight drop" / "marginal decline" / "worth monitoring." If a keyword declined but is still sitting in a strong position overall, note that context (e.g. "declining from a strong position") rather than just flagging the raw movement.

Every keyword in the data goes into exactly one bucket — don't omit any, even small or flat movements. Close with a one-line overall read after the three buckets (e.g. "7 of 18 keywords showed strong gains, but water-damage terms specifically are trending the wrong way — worth a closer look").

**What Got Better** — compare this quarter's checklist to last quarter's item by item and list what measurably improved: a checklist item that flipped from a problem to fixed, a score that went up and why, positive trend data. This is a genuine diff, not a restatement of the scores. Only positives go here — do not list what's still broken in this section; that content moves to Key Focus Areas (Step 4) instead. If technical fixes improved but rankings haven't moved yet, it's fine to note that distinction briefly here (infrastructure wins vs. visibility wins), but the deeper "here's what's still not working" framing belongs in Step 4.

---

## Step 4: 🎯 Key Focus Areas This Quarter

This section now carries the weight of both "what's still broken" and "what we're prioritizing" — draft the full list of things the campaign should work on next quarter, pulled from anything that stayed broken, got worse, or is highest-leverage. Call out recurrence explicitly where relevant (e.g. "flagged last quarter too, still not actioned") — that context is what makes a focus area feel urgent rather than generic.

**Before finalizing, show the user the full draft list and ask which items should be excluded as internal/agency-side blockers** (e.g. things that require access the agency doesn't have, work that's in progress but not yet client-relevant, internal process items). Do this every time — don't assume based on past answers, since scope changes quarter to quarter. Only the confirmed, client-relevant subset goes into the final client-facing report.

Write each focus area as: a short bolded title, then 1-3 sentences explaining what it is and why it matters — client-facing language, no jargon.

---

## Step 5: Client Action Items

Separate from Key Focus Areas — this section is specifically things the **client** needs to do (grant tool access, approve something, provide content/photos/info, respond to something). If nothing requires client action this quarter, say so plainly rather than manufacturing a task.

---

## Step 6: Performance Metrics at a Glance

A short scannable summary block, e.g.:

```
SEO Score:         XX/100 (status)
vs. Last Quarter:  +X / -X / first audit
GBP Reviews:       [count] · [rating]
Map Pack Movement: [summary from ranking data, if provided]
Referring Domains: [trend]
```

Only include lines where data was actually provided — don't fabricate metrics that weren't in the input.

---

## Step 7: Suggested Talking Points

3-5 bullet points an account manager could use on a client call — enough context to speak to each naturally, tying back to the scores, highlights, and focus areas above. Not a repeat of prior sections verbatim — frame them as talking points ("lead with X because Y").

---

## Step 8: ClickUp Cards

For each Key Focus Area (and any other discrete action item that surfaced), produce a card:

```
Title: [Client Name] — [Short, specific title]
Why we're doing this: [2-4 sentences, plain language, written so anyone on the team — not just SEO specialists — understands the issue and its impact without prior context.]
```

Keep titles specific enough to be actionable on their own (e.g. "RestoPros of the Upstate — URL Migration Audit", not "Fix Links"). One card per distinct initiative — don't split a single initiative into multiple cards, and don't bundle unrelated issues into one card.

---

## Output Order

Produce outputs in this order every time: Scoring table + reasoning → Quarterly Highlights (Ranking Summary → What Got Better) → 🎯 Key Focus Areas This Quarter (after scope confirmation) → Client Action Items → Performance Metrics at a Glance → Suggested Talking Points → ClickUp Cards.

Write all client-facing sections (Quarterly Highlights, Key Focus Areas, Client Action Items, Performance Metrics, Talking Points) in plain, warm, professional language — this should be usable directly in a client-facing ClickUp doc or call without further editing. ClickUp cards can be more internal/direct since they're for the team, not the client.
