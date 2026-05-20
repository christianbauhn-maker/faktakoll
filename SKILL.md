---
name: faktakoll
description: >
  Mandatory pre-publication fact-check for data-driven analysis. Trigger IMMEDIATELY when the user writes "#faktakoll", "faktagranska", "kolla siffror", "verifiera data", "pre-pub check", or "publicera" in combination with a draft text. Also trigger whenever an article, post, daily entry, or report is about to be published or pushed live — even if the user doesn't explicitly ask for a check. This skill protects publication credibility by verifying every numerical claim against source data and checking for forbidden framings. One unverified number can destroy months of trust-building.
---

# faktakoll — Pre-Publication Verification

Every numerical claim in a published piece must have a verified origin. This skill makes that systematic.

**Run before every publication. No exceptions.**

---

## What this skill checks

### 1. Numerical claim verification (primary)
Every number, percentage, ranking, and named figure in the text must be matched to a source:
1. Local source archive (strongest — you own the data)
2. Source attribution already in the text (acceptable if verifiable)
3. Web search against the named source (fallback)

### 2. Framing compliance (secondary)
Check against `references/claim-rules.md` (or `references/claim-rules-template.md` if not yet configured). Flag any forbidden phrasing as a framing error — these are corrections, not suggestions.

---

## Execution workflow

### Step 1 — Extract all claims
Scan the full text. List every verifiable assertion:
- Any specific number or percentage
- Any ranking or index position
- Any named source cited
- Any comparative claim
- Any time-bound claim

If it sounds like a fact, it is a claim.

### Step 2 — Match against local data
Search the configured source archive. Note file path and location for every match.

- Match found: mark **VERIFIED**
- No match: proceed to Step 3

### Step 3 — Web verification
For unmatched claims, search for the exact figure at the named source. Exact match required — not approximate, not rounded.

- Exact match found online: mark **WEB-VERIFIED** (acceptable, add to archive later)
- Source gives different figure: mark **CONFLICT**
- No source found: mark **UNVERIFIED** — cannot publish

### Step 4 — Framing check
Read `references/claim-rules.md`. Flag every forbidden phrase as a **FRAMING ERROR** with the correct alternative.

### Step 5 — Output ledger and verdict

If any items remain flagged: **HOLD — cannot publish.** List what must be fixed.
If only web-verified items: **APPROVED** with a note to archive sources.
If all verified: **APPROVED.**

After verdict, offer to apply inline corrections for all flagged items.

---

## Output format

```
## Faktakoll — [Title or type]
Date: [today]

### Verified
[claim] → [source] | [note]

### Web-verified
[claim] → [URL] | Note: add to local archive

### Flagged
[claim] → [CONFLICT / UNVERIFIED / FRAMING ERROR]
[what source actually says, if applicable]
Suggested correction: [corrected phrasing]

### Verdict
[APPROVED / HOLD] — [summary]
Open issues: [N]
```

---

## Inline corrections

After the ledger, ask: "Apply corrections directly?" If yes, make minimal edits to resolve each flagged item. Do not rewrite — only fix what the ledger identified.

---

## Configuration

Copy `references/claim-rules-template.md` to `references/claim-rules.md` and edit for your publication. At minimum, define:
- Which source organizations qualify as named primary sources
- Any forbidden framings specific to your editorial standards
- Your local data archive path

---

## On confidence

The standard here is not "close enough" — it is exact. If you cannot verify a number with confidence, flag it. A web-verified note is honest. A silent approval on an unverified claim is a liability.
