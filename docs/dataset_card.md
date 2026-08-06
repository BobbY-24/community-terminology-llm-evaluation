# Dataset card

## Dataset summary

The **Community-Specific Gaming and Cybersecurity Terminology** dataset supports research on community-grounded semantic understanding: whether a reader or language model can interpret an expression according to its conventional meaning in a specific community. The release focuses on English-language terminology from gaming and cybersecurity contexts.

The unit of analysis is one term or multiword expression paired with a primary linguistic-construction label, a community/subcommunity description, an authentic usage example, and a traceable source URL. The release is intended as a curated research foundation for lexical-semantic evaluation, context ablation, retrieval, and benchmark prototyping. It is not presented as a completed gold-standard benchmark of model comprehension.

## Dataset composition

### Records by domain

| Domain | Records |
|---|---:|
| Cybersecurity | 74 |
| Gaming | 107 |
| **Total** | **181** |

### Records by linguistic construction

| Construction | Records |
|---|---:|
| Metaphor | 74 |
| Compound | 29 |
| Initialism | 19 |
| Affixation | 12 |
| Blending | 11 |
| Multiword Expression | 8 |
| Acronym | 6 |
| Semantic Shift | 5 |
| Abbreviation | 4 |
| Clipping | 4 |
| Borrowing | 3 |
| Functional Shift | 3 |
| Code Word | 1 |
| Community-specific Jargon | 1 |
| Meme Expression | 1 |

The distribution is strongly imbalanced: metaphors alone account for 74 records, while three categories have one record each. Analyses by construction should report sample sizes and avoid treating category-level estimates as equally stable.

### Source-family distribution

The workbook's `Source Audit` sheet assigns each retained row to a source family. These are collection strata, not estimates of platform prevalence or community size.

| Cybersecurity source family | Records | Gaming source family | Records |
|---|---:|---|---:|
| Industry Research | 15 | Reddit | 20 |
| Reddit | 15 | Official Game Forums | 19 |
| Technical Q&A | 13 | Steam Community | 19 |
| CTF/Exploit Writeups | 12 | Arqade | 16 |
| Institutional Reports | 11 | Speedrun.com Forums | 14 |
| Hack The Box Forums | 4 | Game Wikis/Guides | 13 |
| GitHub Issues/Discussions | 3 | GitHub Issues/Discussions | 5 |
| Hacker News | 1 | Hacker News | 1 |
| **Total** | **74** | **Total** | **107** |

### Completeness and duplicates

All seven required JSON record fields have zero missing values. IDs are unique and form complete ordered sequences from `cybersecurity_001` to `cybersecurity_074` and from `gaming_001` to `gaming_107`.

- Exact duplicate term groups: **0**.
- Case-insensitive duplicate term groups: **0**.
- Duplicate source-URL groups: **1**, covering **2** records.
- Shared URL: `cybersecurity_012` (`MFA fatigue`) and `cybersecurity_066` (`MFA bombing`).

The shared URL is retained because the two rows represent distinct terms supported by the same source page. No data correction was required: the workbook and JSON agree exactly across all 181 records, including the shared link.

## Schema

| Field | Type | Description |
|---|---|---|
| `id` | string | Stable release identifier composed of domain and a zero-padded sequence number. |
| `domain` | string | `cybersecurity` or `gaming`. |
| `term` | string | Narrowest complete target expression, preserving capitalization, punctuation, numerals, and spelling. |
| `linguistic_construction` | string | Primary descriptive label from the 15-value controlled vocabulary. |
| `community_subcommunity` | string | Broad community followed by a narrower practice, game, mechanic, or technical context. |
| `real_usage_example` | string | Authentic usage evidence copied from the associated source; not a gold definition. |
| `source_url` | string | Direct HTTP(S) page or thread URL associated with the example. |

Cybersecurity example:

```json
{
  "id": "cybersecurity_001",
  "domain": "cybersecurity",
  "term": "Pass the hash",
  "linguistic_construction": "Multiword Expression",
  "community_subcommunity": "Red Team / Windows Credential Abuse",
  "real_usage_example": "It is my understanding that pass the hash works by stealing hashes from LSASS of users that have logged on to the system.",
  "source_url": "https://www.reddit.com/r/AskNetsec/comments/c323rh/pass_the_hash_questions/"
}
```

Gaming example:

```json
{
  "id": "gaming_001",
  "domain": "gaming",
  "term": "freeze the wave",
  "linguistic_construction": "Metaphor",
  "community_subcommunity": "League of Legends / Top-Lane Wave Management",
  "real_usage_example": "Everyone always says \"freeze the wave\" over and over again but even in all the wave management videos I've watched no one actually tells you HOW to freeze the wave.",
  "source_url": "https://www.reddit.com/r/summonerschool/comments/dpklzk/how_do_you_freeze_a_wave/"
}
```

## Collection process

Source discovery began with relevant gaming and cybersecurity communities, including discussion forums, technical question-and-answer sites, community boards, wikis, documentation, and public threads. Candidate identification was conducted by reading discussions and marking expressions that appeared opaque, conventionalized, shifted, abbreviated, coded, or dependent on insider knowledge. The full usage sentence was preserved as soon as a candidate was identified.

Verification used surrounding discussion and community-sensitive search. Translation checks were used when relevant to borrowed, non-English, or code-mixed material. An LLM interpretation check was used diagnostically to expose ambiguity or likely failure, not as authoritative evidence. Candidates were kept, excluded, or marked for review based on authentic community support and the stability of the context-specific sense.

The linked source is evidence of usage, not evidence that the expression originated on that page. Search-result counts, when collected during the broader workflow, are unstable retrieval metadata and are not included as popularity estimates in this release.

## Annotation process

For each retained expression, the annotator selected the narrowest complete span, assigned one primary linguistic-construction label, standardized the community/subcommunity description, copied a natural usage example, and saved a direct source URL. Authentic community evidence was prioritized over surface intuition.

The construction label is descriptive rather than evaluative. It indicates how a form is built or conventionalized; it does not itself specify whether a reader or model should find the term easy, medium, or hard. When two construction labels were plausible, the guideline called for choosing the best primary label and flagging the item for review. The current release does not include a separate review flag or comprehension-difficulty field.

No inter-annotator reliability measurement is reported in the supplied files. Additional expert review and agreement measurement would be appropriate before treating the release as a fully validated gold benchmark.

## Intended uses

Appropriate research uses include:

- lexical-semantic evaluation;
- controlled context ablations;
- cloze tasks;
- definition generation;
- contrastive or multiple-choice meaning selection;
- retrieval studies;
- uncertainty calibration;
- paraphrase evaluation;
- qualitative error analysis; and
- benchmark prototyping.

Researchers should preserve record identifiers, document any filtering or relabeling, control for construction and domain imbalance, and avoid train/test leakage through shared pages or closely related communities.

## Out-of-scope uses

This version should not be treated as:

- an exhaustive dictionary of gaming or cybersecurity language;
- a frequency lexicon;
- a representative sample of all gamers or cybersecurity practitioners;
- proof that a term originated in the linked source;
- a measure of term popularity;
- a complete, validated gold benchmark of model comprehension; or
- evidence that any model has already been evaluated on all records.

## Limitations

The domain and construction distributions are uneven. Platform selection favors accessible English-language sources, and source genres range from informal conversations to industry research and institutional reports. Source pages may be edited, deleted, moved, blocked, or otherwise become difficult to retrieve. Meanings can change across communities and over time, while a single primary label may simplify ambiguous formations.

Some authentic usage examples may directly or indirectly reveal a definition, reducing their value for controlled comprehension testing. Additional screening is needed for definition leakage, near-duplicate concepts, and context sufficiency. Source quotations are evidence of authentic use, but authentic usage and redistribution rights are distinct; downstream users should review platform terms and applicable law. More human validation, documented adjudication, and inter-annotator reliability measurement are recommended before benchmark-scale claims.
