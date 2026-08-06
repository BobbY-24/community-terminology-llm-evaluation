# Annotation schema

## Record fields

| Field | Allowed value or format | Annotation rule |
|---|---|---|
| `id` | `cybersecurity_NNN` or `gaming_NNN` | Assigned in the JSON release; unique and stable within version 1.0.0. |
| `domain` | `cybersecurity`, `gaming` | Choose from the source community rather than the surface form alone. |
| `term` | Non-empty string | Copy the narrowest complete community-specific expression exactly. |
| `linguistic_construction` | One controlled label below | Select the primary surface-formation or conventionalization label. |
| `community_subcommunity` | Non-empty string, normally `Broad / Narrow` | Infer from the source and thread topic; record broad context first. |
| `real_usage_example` | Non-empty authentic quotation | Preserve natural wording and enough local context; use ellipses for omissions. Do not rewrite it as a definition. |
| `source_url` | Direct HTTP(S) URL | Link to the page or thread containing the usage, not a search-results page. |

## Controlled linguistic-construction vocabulary

All examples below occur in the released dataset and are evidence of usage, not gold definitions.

| Label | Identification rule | Dataset example |
|---|---|---|
| Abbreviation | A compressed written form using letters, numerals, or symbols rather than a full phrase. | `ret2libc` |
| Acronym | Initial letters pronounced or used as a single lexical item. | `TOCTOU` |
| Affixation | A base gains a prefix or suffix that creates the community form. | `twinking` |
| Blending | Parts of two or more words are fused into one form. | `Fashionframe` |
| Borrowing | A form is imported from another language or established cultural register. | `kaizo ironmon` |
| Clipping | A longer word or phrase is shortened while retaining the community meaning. | `uptime strat` |
| Code Word | An ordinary-looking expression conventionally masks or indirectly names a specialized practice. | `evil maid` |
| Community-specific Jargon | A conventional community label not adequately described by another formation process. | `Any%` |
| Compound | Two or more complete lexical units combine into one specialized term. | `MFA fatigue` |
| Functional Shift | An existing form changes grammatical function in community use. | `one tapped` |
| Initialism | Initial letters are normally read letter by letter. | `MITM` |
| Meme Expression | A phrase is conventionalized through recurring online humor or meme circulation. | `boomer shooter` |
| Metaphor | A familiar expression is transferred figuratively to a specialized community concept. | `golden ticket` |
| Multiword Expression | A fixed phrase functions as one conventionalized community unit. | `wall-to-wall pull` |
| Semantic Shift | An existing word keeps its form but acquires a distinct community-specific sense. | `blueberries` |

## Decision rules

### Term span

Select the smallest span that remains a complete community expression. For example, retain `pass the hash`, not only `hash`. Preserve distinctive capitalization and symbols in forms such as `LoLBins`, `ret2libc`, and `Any%`.

### Context and evidence

Interpret and annotate the term in its cited usage. A familiar surface word can have a specialized sense: `stat stick` in Warframe is not annotated according to an ordinary sense of *stick*. Community evidence outranks intuition.

The usage example should be a complete natural sentence with enough local context to support later analysis, but it should not directly state a dictionary-style definition. AI-generated text and paraphrases are not valid authentic examples. Open the source page and retain a direct URL where possible.

### Ambiguous constructions

Some forms plausibly involve more than one process. The schema permits one primary construction label. Choose the label that best explains the recorded form in context and flag genuinely balanced cases for human review in working data. Do not create a new category ad hoc, and do not change the controlled spelling or capitalization of a label.

Useful distinctions include:

- **Acronym vs. initialism:** select according to conventional pronunciation or lexical use, not capitalization alone.
- **Compound vs. multiword expression:** use *Compound* when complete lexical units form the specialized term; use *Multiword Expression* when the fixed phrase functions as a conventional unit and the formation is not better captured by another label.
- **Metaphor vs. semantic shift:** use *Metaphor* when figurative transfer is central; use *Semantic Shift* when an existing form has acquired a distinct community sense without a clearer competing process.
- **Blending vs. compound:** use *Blending* when source forms are truncated or fused, as with `Fashionframe`; use *Compound* when complete units combine.
- **Community-specific Jargon:** reserve this category for stable conventional labels not adequately captured by the more specific formation categories.

### Verification evidence

The underlying guideline recommends retaining the search query, displayed result-count text, retrieval date, translation check, LLM check, and Keep/Exclude/Review decision in working records. These working fields are not part of the seven-field public JSON release. Search counts may change and should never be interpreted as popularity. Translation and LLM interpretations are diagnostic records rather than gold sources.

## Construction is not comprehension difficulty

The linguistic-construction label describes form. It does not specify whether a term is easy or hard for a person or model to understand. The final report discusses a separate conceptual distinction in which easy expressions may be inferred from context, medium expressions may require a targeted lookup, and hard expressions may require broader community research or competing-sense comparison. That difficulty scale is not included as a released field and should not be reconstructed from construction labels alone.

Future evaluation should measure comprehension difficulty empirically under controlled context conditions rather than assume, for example, that every initialism is harder than every metaphor.
