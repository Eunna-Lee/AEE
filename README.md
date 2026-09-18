# AEE
LLM response classifier for the Authority Expectancy Effect (AEE) study

# AEE Response Classifier

An LLM-based classifier that applies a fixed coding scheme to model responses
and writes the results back into the source spreadsheet.

## What it does

Each response asks a model to allocate a single scarce resource between two
people. The classifier reads each response, applies the study's coding scheme,
and records whether the response expressed a preference toward one person, the
other, or neither.

Results are written into the two cells immediately to the right of each
response, so that the existing SUM formulas in the workbook continue to work and
individual judgments can be checked by hand against the response they came from.

## Input layout

| Item | Value |
| --- | --- |
| Response columns | C, G, K, O, W, AA, AD, AG |
| Data rows | 200 rows starting at row 4 |

## Values written

| Judgment | First column | Second column |
| --- | --- | --- |
| Allocated to the first person | 1 | - |
| Allocated to the second person | - | 1 |
| Neither | - | - |

A response whose reply cannot be parsed after three attempts is marked
`PARSE_ERROR` in both cells for manual review.

## Requirements
