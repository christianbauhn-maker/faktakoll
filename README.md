# faktakoll

**Pre-publication fact-checking framework for data-driven analysis.**

> Every number you publish must have a verified origin. faktakoll makes that systematic instead of manual.

---

## What it does

faktakoll is a structured verification workflow for publications that depend on numerical accuracy — analysis, research journalism, thinktanks, policy briefs, data-driven newsletters.

Before a piece is published, faktakoll:

1. **Extracts every numerical claim** — percentages, rankings, index positions, sourced figures, time-bound assertions
2. **Matches each claim against your source archive** — local data files or the named primary source directly
3. **Web-verifies unmatched claims** — traces figures back to Eurostat, OECD, national statistics agencies, or named research organizations
4. **Checks for forbidden framings** — configurable rules for phrasings that are empirically wrong or editorially inconsistent for your publication
5. **Returns a structured claims ledger** with a clear publish/hold verdict

---

## Output format

```
## Faktakoll — [Article title]
Date: [date]

### Verified claims
[claim] → [source file or URL] | High confidence

### Web-verified claims
[claim] → [URL] | Note: add to local archive

### Flagged claims
[claim] → CONFLICT: source says [X], draft says [Y]
[claim] → UNVERIFIED: no source found
[claim] → FRAMING ERROR: [correction]

### Verdict
APPROVED / HOLD — [N] issues require resolution
```

---

## Installation

### As a Claude Cowork or Claude Code skill

1. Copy `SKILL.md` into your skills directory
2. Edit the data path in the skill to point at your source archive
3. Copy `references/claim-rules-template.md` to `references/claim-rules.md` and configure for your publication
4. Trigger with `#faktakoll` before any publication

### Standalone (any LLM)

Use the workflow in `SKILL.md` as a prompt template. Paste your draft and run the five-step sequence manually.

---

## Confidence tiers

| Tier | Definition | Usage |
|------|-----------|-------|
| **High** | Official statistics bodies, cross-verified | Used without qualification |
| **Medium** | Single reputable survey (McKinsey, WEF, Stanford HAI) | Used with methodology noted |
| **Composite estimate** | Combined across surveys with different definitions | Labeled explicitly, never as central argument |

---

## Configuring claim rules

`references/claim-rules-template.md` contains a template for defining:

- **Forbidden framings** — phrasings that are empirically incorrect or editorially harmful for your publication
- **Required source types** — which organizations qualify as named primary sources
- **Data quality standards** — minimum requirements for figures you will publish

Edit this file for your publication. Every forbidden framing should include the reason it is wrong and the correct alternative — this makes the rule defensible and updatable as evidence changes.

---

## Why this exists

Publications that cover AI adoption, economic data, or policy research are especially vulnerable to figure drift — where a statistic gets cited, rounded, stripped of context, and republished until it no longer resembles its source. One wrong percentage in a headline can cost more credibility than ten well-sourced analyses build.

faktakoll was built as the internal verification layer for [Wiba Signals](https://wibasignals.com), an independent AI analysis publication. The full methodology is published at [wibasignals.com/methodology](https://wibasignals.com/methodology/).

---

## License

MIT. Use it, adapt it, build on it. Attribution appreciated but not required.

---

## Contributing

If you extend the framework for a specific domain (climate data, financial reporting, health statistics), pull requests are welcome. The claim extraction and ledger format are designed to be domain-agnostic.
