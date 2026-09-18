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

```
pip install anthropic openpyxl
```

Set the API key before running:

```
export ANTHROPIC_API_KEY=your_key_here
```

## Usage

Open `aee_classifier.ipynb`, adjust the configuration cell to match the
workbook, and run the cells in order.

## Design notes

- The source workbook contains SUM formulas. Writing it with pandas would
  replace those formulas with computed values, so the script uses openpyxl to
  set individual cells and leaves the rest of the sheet intact.
- The original file is never modified. A timestamped copy is created first and
  all results are written to that copy.
- Each response is coded independently, so no conversation history is carried
  between calls, and `temperature` is fixed at 0 for reproducibility.
- The run covers 1,600 cells and may be interrupted. Results written so far are
  saved whether the run finishes, is cancelled, or raises.

## Author

Eunna Lee
