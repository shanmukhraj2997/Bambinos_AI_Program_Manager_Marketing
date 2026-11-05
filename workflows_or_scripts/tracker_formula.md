# Tracker Formula and Data Rules

## Total Score

The tracker uses the following formula in the Total Score column (Q):

```excel
=IF(COUNT(J2:P2)=7,SUM(J2:P2),"")
```

It calculates a total only when all seven score cells (J:P) contain numbers. Missing scores are left blank rather than treated as zero. Fill the formula down for subsequent rows.

## Rejected records

The five hard-rejected candidates have blank score components and blank total scores. Do not populate numeric scores for hard-rejected records.

## Repository copy correction

The original uploaded workbook had an incorrect label in cell A1: it displayed the English hook instead of `Session ID`. The repository copy `results/candidate_tracker.xlsx` corrects only that header label. The original uploaded workbook was not modified.
