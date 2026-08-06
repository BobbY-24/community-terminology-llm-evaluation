# Proposed future experiments

This document describes a recommended next stage. No scores, model rankings, or completed large-scale evaluations are claimed in release 1.0.0.

## Research objective

Future experiments can test how progressively richer evidence changes a model's interpretation of community-specific terminology. The primary outcome should be community-grounded semantic understanding rather than surface fluency. Designs should separate recognition, meaning selection, context use, retrieval, uncertainty, and self-correction.

## Controlled context conditions

### 1. Term only

Provide only the target expression. This condition measures prior familiarity and the model's ability to recognize ambiguity. It should reward calibrated uncertainty when multiple community senses are plausible.

### 2. Term plus sentence

Provide the authentic usage example. Compare performance with the term-only condition to estimate sentence-level context improvement. Screen examples for direct-definition leakage before evaluation.

### 3. Term plus paragraph

Provide a surrounding paragraph or a carefully preserved local context window from the source. This condition can test whether discourse context resolves meaning beyond the selected sentence. Collection must respect quotation rights and minimize personal information.

### 4. Term plus community metadata

Add the domain and community/subcommunity field. The contrast with sentence-only conditions can show whether explicit social or technical metadata provides useful grounding or creates shortcuts.

### 5. Term plus external retrieval

Allow search or controlled retrieval. Record the generated query, retrieved pages, selected evidence, final answer, citations, uncertainty, and revisions. Retrieval should be evaluated independently from answer quality so that failures can be localized.

## Candidate tasks

- **Definition generation:** produce a concise community-sensitive interpretation while marking uncertainty.
- **Multiple-choice meaning selection:** choose among plausible general, neighboring-community, and correct senses.
- **Cloze completion:** predict a missing term or contextually compatible expression.
- **Contrastive usage discrimination:** decide which of two passages uses the expression in the target sense.
- **Paraphrase generation:** rewrite the sentence so the specialized meaning is clear without adding unsupported detail.
- **Uncertainty reporting:** state confidence, ambiguity, and whether more context or search is needed.
- **Token probability:** compare the probability assigned to the target or a meaning-revealing continuation.
- **Perplexity:** measure differences across authentic, perturbed, and meaning-incompatible contexts.
- **Retrieval query generation:** formulate a community-sensitive search query.
- **Evidence selection:** select passages that directly support the proposed interpretation.
- **Self-correction:** revise an initial answer after receiving context or retrieval evidence.

## Recommended metrics

Metrics should be selected by task and labeled as recommendations:

| Task family | Recommended metrics |
|---|---|
| Constrained meaning selection | Accuracy; exact match where the target is unambiguous. |
| Open-ended definitions and paraphrases | Semantic similarity; rubric-based human scoring; pairwise preference. |
| Uncertainty | Calibration error; Brier score; selective accuracy or risk-coverage. |
| Token-level modeling | Token-probability differences; perplexity differences. |
| Context ablation | Absolute and relative context improvement from a preregistered baseline. |
| Retrieval | Retrieval precision; evidence recall where annotations support it; query success. |
| Evidence-grounded answers | Evidence attribution, citation correctness, and unsupported-claim rate. |
| Qualitative analysis | Error-type frequency with double-coded samples and adjudication. |

Exact match should be used only when spelling variants and legitimate paraphrases are controlled. Semantic metrics should be supplemented with human rubrics because fluent but wrong definitions may appear lexically similar to correct ones.

## Leakage-aware split strategy

A random row split is not sufficient. Recommended splitting should group records before assigning train, development, and test partitions:

1. **Normalize terms** for case, punctuation, spacing, and simple inflection to identify near duplicates.
2. **Group source pages** by canonicalized URL so that two terms from the same thread remain in one partition. This is necessary for the shared `MFA fatigue` / `MFA bombing` source.
3. **Cluster close concepts** such as variants, expansions, abbreviations, and terms that reveal each other's meaning.
4. **Cluster related communities** when their terminology and source ecology overlap strongly, such as multiple forums for the same game or closely connected cybersecurity practices.
5. **Stratify at the group level** to preserve broad domain and construction coverage without breaking leakage groups.
6. **Reserve a temporal or community-held-out challenge set** if dates and coverage support it.
7. **Freeze the split manifest** with record IDs, group identifiers, and a documented random seed.

A reasonable first benchmark could use grouped 70/15/15 train/development/test proportions, followed by a stricter community-held-out analysis. Small construction categories should be reported descriptively rather than forced into unstable per-category scores.

## Agentic retrieval and self-correction analysis

For retrieval-enabled models, trace each stage separately:

1. Did the model recognize uncertainty?
2. Did it formulate a query containing the right community cues?
3. Did retrieval return relevant evidence?
4. Did the model select evidence that actually supports the meaning?
5. Did it revise an incorrect initial interpretation?
6. Did the final answer attribute evidence and retain calibrated uncertainty?

This decomposition distinguishes semantic failure from query, retrieval, evidence-selection, and revision failures. It also supports counterfactual interventions: for example, provide gold evidence after a failed search to test whether reasoning or retrieval is the limiting component.

## Reporting recommendations

Report model and prompt versions, inference settings, access dates, context condition, item counts, excluded cases, split-group logic, and uncertainty handling. Present aggregate results alongside domain, construction, community, and source-genre analyses, with confidence intervals where sample sizes permit. Never fabricate missing scores or treat the current descriptive dataset statistics as evaluation outcomes.
