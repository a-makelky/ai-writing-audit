---
name: ai-writing-audit
description: Audit and correct text to remove signs of AI-generated writing. Use when reviewing any written content (marketing copy, articles, documentation, social posts) to identify and remove patterns that signal LLM generation. Triggers include requests to "make this sound less AI," "humanize this," "remove AI tells," "audit for AI patterns," "make this sound more natural," or any review of drafted content before publication.
---

# AI Writing Audit & Correction

Identify and remove patterns that signal AI-generated text, based on Wikipedia's "Signs of AI Writing" detection guide.

When the /audit command is entered into a chat, run the two-phase workflow below.

## Two-Phase Workflow

Complete AUDIT fully before starting REWRITE. Do not skip phases.

### Phase 1: Audit

1. Read draft once, slowly.
2. Work through checklist in `references/checklist.md` in exact order.
3. For each offense:
   - Quote shortest offending snippet (≤12 words)
   - Append all applicable `[TAGS]`
   - One numbered line per offense; stack tags if multiple tells in one sentence
4. After last offense: `— END AUDIT: [n] issues found —`
5. If zero issues: `— AUDIT COMPLETE: 0 issues —` and skip Phase 2.

**Severity suffixes** (append when applicable):
- `+H` = high severity (strong tell or compounded patterns)
- `+S` = structural (affects document structure, not just wording)

### Phase 2: Rewrite

**Core rewrite principles:**

1. Output complete corrected text with all flagged issues fixed.
2. Preserve everything not flagged—no new edits.
3. For each fix, prioritize:
   - Specificity over generality
   - Concrete details over abstract claims
   - Plain statement over rhetorical flourish
   - Varied sentence structure over formulaic patterns
4. Do not add new content, claims, or citations.
5. Maintain original meaning, tone intent, and factual content.

**Fix principles by tag type:**

| Tags | Action |
|------|--------|
| `[INFLATED]` `[SYMBOLISM]` `[PROMO]` | Delete puffery or replace with specific factual claim. No fact? Cut entirely. |
| `[SUPERFICIAL-ING]` | Remove -ing phrase or convert to separate sentence with substance. |
| `[AI-LEX]` | Replace with plainer synonym or restructure sentence to eliminate the word. |
| `[NOT-ONLY-BUT]` `[RULE-OF-3]` | Break parallelism; vary structure; state directly. |
| `[STACCATO]` | Reconstruct into connected, conversational phrasing that matches the source material's natural rhythm. Combine fragments into a single flowing sentence. |
| `[ELEGANT-VAR]` | Pick one term consistently, or use pronouns. |
| `[VAGUE-ATTR]` `[WEASEL]` | Name source specifically, add quantifier, or delete claim. |
| `[CHALLENGES-FUTURE]` | Restructure or cut; do not preserve the formula. |
| `[EM-DASH]` | Remove entirely. Restructure the sentence to eliminate the need for any dash. Split into two sentences, use a comma, use a colon, or rewrite. Never preserve an em dash or en dash in the corrected text. |
| `[INLINE-BOLD]` `[INLINE-LIST]` `[TITLE-CASE]` | Remove excess formatting; sentence case for headings. |
| `[DIRECT-ADDRESS]` `[COLLAB]` `[LETTER-FORMAT]` `[REFUSAL]` `[KNOWLEDGE-CUTOFF]` | Delete entirely. |
| `[OAICITE]` `[MARKDOWN]` `[PLACEHOLDER]` `[REF-BUG]` | Remove artifacts; fix or flag citations for human review. |

## Output Format

```
## AUDIT

1. "quoted snippet" [TAG] [TAG +H]
2. "quoted snippet" [TAG]
...

— END AUDIT: [n] issues found —

## CORRECTED TEXT

[Full corrected text]

## CHANGELOG

- Line/section: brief description of change
- Line/section: brief description of change
...
```

CHANGELOG: one terse line per fix, referencing original snippet or location.

## References

- `references/checklist.md` — AI detection tags and patterns
