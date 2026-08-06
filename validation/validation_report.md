# Validation report

Release: **1.0.0**  
Validation date: **2026-08-06**

## Outcome

**PASS** - 33 checks passed, 1 warning(s), and 0 failure(s).

## Passed checks

- All required repository files are present.
- Publication copy is byte-identical to its archived source: documentation/annotation_guideline.docx
- Publication copy is byte-identical to its archived source: documentation/annotation_guideline.pdf
- Publication copy is byte-identical to its archived source: documentation/pura_final_report.docx
- Publication copy is byte-identical to its archived source: data/source/refined_terminology_usage.xlsx
- Publication copy is byte-identical to its archived source: data/release/community_terminology_dataset.json
- JSON release is a metadata object containing a records array.
- JSON contains 181 records.
- JSON domain counts are cybersecurity=74 and gaming=107.
- All required JSON fields are present and non-empty.
- Every JSON record has exactly the documented seven fields.
- JSON record IDs are unique.
- JSON IDs are complete and ordered by domain.
- Observed labels exactly match the 15-label controlled vocabulary.
- All source URLs use HTTP or HTTPS syntax.
- Workbook contains the expected sheets in the expected order.
- Cybersecurity has the expected five headers.
- Gaming has the expected five headers.
- Workbook domain counts are cybersecurity=74 and gaming=107.
- Workbook and JSON agree exactly across all 181 records.
- No exact duplicate terms were found.
- Embedded total statistic matches recomputation.
- Embedded domain statistics match recomputation.
- Embedded construction statistics match recomputation.
- documentation/annotation_guideline.pdf has 2 pages.
- documentation/annotation_guideline.pdf has no text-empty pages.
- documentation/pura_final_report.pdf has 3 pages.
- documentation/pura_final_report.pdf has no text-empty pages.
- assets/domain_distribution.png has publication-readable dimensions (1600x900).
- assets/linguistic_construction_distribution.png has publication-readable dimensions (1900x1350).
- README prose length is within target (1533 words).
- README contains all required sections.
- All recorded SHA-256 checksums match.

## Warnings

- One source URL is shared by two distinct records (MFA fatigue and MFA bombing); this is documented and retained.

## Failures

- None.

## Scope and interpretation

This validation checks structure, counts, controlled labels, required fields, cross-format equality, file identity, PDF page/text presence, image dimensions, and recorded checksums. It validates URL syntax but deliberately does not require live URL retrieval: community pages can be edited, deleted, blocked, or rate-limited. It also does not treat automated checks as a substitute for additional expert annotation or inter-annotator agreement measurement.
