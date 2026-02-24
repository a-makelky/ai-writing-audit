# AI Writing Audit

A Claude skill that audits text for patterns commonly found in AI-generated writing, based on Wikipedia's "Signs of AI Writing" detection guide.

## What This Does

This skill systematically audits text for **linguistic and structural patterns** that frequently appear in LLM-generated content, including:

- Inflated language ("stands as," "serves as," "testament to")
- AI-lexicon overuse ("delve," "landscape," "multifaceted," "leverage")
- Formulaic structures (not-only-but, rule-of-three parallelism)
- Superficial qualifiers ("-ing" phrases tacked onto facts)
- Structural tells (em-dash overuse, title case headings, inline bolding)
- Communication artifacts (knowledge cutoff references, collaborative phrases)
- Citation problems (vague attribution, malformed references)

The skill provides:
1. **Detailed audit** with tagged patterns and severity markers
2. **Optional rewrite** that removes flagged patterns while preserving meaning
3. **Changelog** documenting each correction

## What This Does NOT Do

**This skill does not detect whether text was written by AI.**

Here's why:

- **Humans write this way too.** Many flagged patterns appear in human writing, especially in academic, marketing, or formal contexts.
- **AI can avoid these patterns.** Well-prompted LLMs can produce text without any of these tells.
- **Patterns ≠ Authorship.** Finding these patterns means the text has characteristics common in AI writing—nothing more.

**This is a style audit tool, not an authorship detection tool.**

Use it to improve writing quality by removing formulaic patterns, not to determine if something was AI-generated.

## Installation

1. Download `ai-writing-audit.skill` from the [releases page](https://github.com/a-makelky/ai-writing-audit/releases)
2. In Claude (claude.ai), go to your account settings
3. Upload the `.skill` file in the Skills section

## Usage

### Basic Audit

Simply provide text and ask Claude to audit it:

```
Audit this text for AI writing patterns:

[your text here]
```

Claude will provide a detailed audit with tagged patterns like:

```
## AUDIT

1. "stands as a testament" [INFLATED] [AI-LEX +H]
2. "delve into the intricacies" [AI-LEX +H]
3. "Not only does it provide clarity, but also" [NOT-ONLY-BUT]
...

— END AUDIT: 12 issues found —
```

### Audit + Rewrite

To get corrected text after the audit:

```
Audit this text and provide a corrected version:

[your text here]
```

You'll receive:
- Complete audit with tagged issues
- Corrected text with patterns removed
- Changelog of all changes made

## Pattern Categories

The skill checks for patterns across multiple categories:

**Content Tells**
- Inflated language and symbolism
- Promotional tone
- Superficial qualifiers
- Generic future outlook sections

**Language Tells**
- AI-lexicon overuse (40+ flagged terms)
- Formulaic structures
- Elegant variation
- Vague attribution

**Structural Tells**
- Formatting patterns (title case, inline bold)
- Em-dash overuse
- Markdown/formatting artifacts

**Communication Artifacts**
- Direct address to readers
- Collaborative phrases ("Let me know if...")
- Knowledge cutoff references
- Letter-style formatting

**Citation Issues**
- Source emphasis patterns
- Malformed references
- Citation artifacts (oaicite, etc.)

See `references/checklist.md` for the complete detection checklist.

## Examples

### Before Audit
```
The implementation of AI technologies stands as a testament to innovation. 
Delving into the intricate landscape of machine learning, we can see how 
these transformative tools are not only enhancing productivity, but also 
fostering unprecedented collaboration—ultimately reshaping the future of work.
```

### After Audit + Rewrite
```
AI technologies show significant innovation. Machine learning tools are 
increasing productivity and enabling new forms of collaboration, changing 
how people work.
```

**Flagged patterns removed:**
- "stands as a testament" → deleted puffery
- "Delving into" → removed AI-lex
- "intricate landscape" → simplified
- "not only...but also" → broke formula
- "transformative," "fostering," "unprecedented" → replaced inflated language
- Em-dash → restructured sentence
- "ultimately reshaping the future" → cut vague claim

## Limitations

1. **False positives happen.** Some flagged patterns are perfectly fine in context—use judgment.
2. **Not comprehensive.** Patterns evolve faster than any checklist can track.
3. **Context matters.** Academic writing, legal documents, and formal reports may legitimately use some of these patterns.
4. **Style preferences vary.** What's flagged as "AI writing" might be appropriate for your audience or domain.

**Always review audit results critically.** This tool suggests improvements; you decide what to keep.

## When to Use This Skill

✅ **Good use cases:**
- Editing marketing copy for authenticity
- Reviewing documentation for formulaic language
- Improving academic writing clarity
- Catching Wikipedia-style AI tells before publication
- Training yourself to recognize these patterns

❌ **Bad use cases:**
- "Proving" a student's essay was AI-generated
- Content moderation decisions
- Automated AI detection systems
- Making accusations about authorship

## Contributing

Found a pattern that should be added? Have suggestions for the checklist? Open an issue or submit a pull request.

## Credits

Detection patterns based on [Wikipedia's Signs of AI Writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide.

## License

MIT License - See LICENSE file for details.

---

**Remember:** This tool identifies patterns, not authors. Use it to improve writing, not to judge writers.
