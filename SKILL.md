---
name: ai-writing-audit
description: Audit and identify patterns that signal AI-generated writing. Use when reviewing any written content (articles, documentation, marketing copy, social posts, academic writing) to detect LLM-generated text. Triggers include requests to "check if this is AI-written," "audit for AI patterns," "identify AI tells," "detect LLM writing," or any analysis of text authenticity.
---

# AI Writing Pattern Detector

Identify patterns that signal AI-generated text based on systematic detection methods. Provides detailed audit with tagged patterns and optional rewrite suggestions.

## Two-Phase Workflow

Complete AUDIT fully before starting REWRITE (if requested). Do not skip phases.

### Phase 1: Audit

1. Read draft once, slowly
2. Work through checklist in `references/checklist.md` in exact order
3. For each offense:
   - Quote shortest offending snippet (≤12 words)
   - Append all applicable `[TAGS]`
   - One numbered line per offense; stack tags if multiple tells in one sentence
4. After last offense: `— END AUDIT: [n] issues found —`
5. If zero issues: `— AUDIT COMPLETE: 0 issues —` and skip Phase 2

**Severity suffixes** (append when applicable):
- `+H` = high severity (strong tell or compounded patterns)
- `+S` = structural (affects document structure, not just wording)

### Phase 2: Rewrite (Optional)

Only proceed with rewrite if user explicitly requests it.

**Core rewrite principles:**

1. Output complete corrected text with all flagged issues fixed
2. Preserve everything not flagged—no new edits
3. Do not add new content, claims, or citations
4. Maintain original meaning and factual content
5. Replace AI patterns with natural, conversational language

**Fix principles by tag type:**

| Tags | Action |
|------|--------|
| `[INFLATED]` `[SYMBOLISM]` `[PROMO]` | Delete puffery or replace with specific fact. No fact? Cut entirely. |
| `[SUPERFICIAL-ING]` | Remove -ing phrase or convert to separate sentence with substance |
| `[AI-LEX]` | Replace with plainer, more natural word |
| `[NOT-ONLY-BUT]` `[RULE-OF-3]` | Break parallelism; vary structure; state directly |
| `[ELEGANT-VAR]` | Pick one term consistently, or use pronouns |
| `[VAGUE-ATTR]` `[WEASEL]` | Name source specifically, add quantifier, or delete claim |
| `[CHALLENGES-FUTURE]` | Restructure or cut; be honest about difficulty |
| `[EM-DASH]` | Replace with comma, colon, or parentheses |
| `[INLINE-BOLD]` `[INLINE-LIST]` `[TITLE-CASE]` | Remove excess formatting; sentence case for headings |
| `[DIRECT-ADDRESS]` `[COLLAB]` `[LETTER-FORMAT]` `[REFUSAL]` `[KNOWLEDGE-CUTOFF]` | Delete entirely |
| `[OAICITE]` `[MARKDOWN]` `[PLACEHOLDER]` `[REF-BUG]` | Remove artifacts; fix or flag citations for human review |

## Output Format

```
## AUDIT

1. "quoted snippet" [TAG] [TAG +H]
2. "quoted snippet" [TAG]
...

— END AUDIT: [n] issues found —

## CORRECTED TEXT
(Only if rewrite requested)

[Full corrected text]

## CHANGELOG
(Only if rewrite provided)

• Location: brief description of change
• Location: brief description of change
...
```

CHANGELOG: one terse line per fix, referencing original snippet or location.

## References

- `references/checklist.md` — Complete AI detection tags and patterns
