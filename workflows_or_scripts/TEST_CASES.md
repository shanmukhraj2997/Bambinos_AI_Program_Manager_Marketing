# Synthetic Test Cases — n8n Candidate Intake & Review Gate MVP

All end-to-end tests use synthetic, non-identifying candidate text. No real child dialogue or personal data was submitted.

| Test ID | Candidate ID | Subject | Timestamp Range | Duration | Rubric Scores (PV/H/P/E/V/A/M) | Total Score | Visual Verification | Guardian Consent | Privacy Review | Context Review | Hard Exclusion | Expected Decision & Gate Behaviour |
|---|---|---|---|---:|---|---:|---|---|---|---|---|---|
| **Test 1 (Valid Control)** | `SYNTH-ENG-001` | English | `00:10:00.000` – `00:10:15.000` | `15s` | `2, 2, 2, 1, 1, 1, 0` | `9/10` | `Verified – Pass` | `Confirmed` | `Passed` | `Not Required` | `No` | **`Eligible for Editor Review`** (not final advertising approval) |
| **Test 2 (Consent Pending)** | `SYNTH-GIT-002` | Gita / Little Yogi | `00:12:00.000` – `00:12:14.000` | `14s` | `2, 2, 2, 1, 1, 1, 0` | `9/10` | `Verified – Pass` | **`Pending`** | `Passed` | `Completed` | `No` | **`Needs Review`** (blocked from editor queue despite 9/10 score) |
| **Test 3 (Score < 7/10)** | `SYNTH-SCI-003` | Science | `00:18:10.000` – `00:18:22.000` | `12s` | `1, 1, 1, 1, 1, 1, 0` | **`6/10`** | `Verified – Pass` | `Confirmed` | `Passed` | `Not Required` | `No` | **`Needs Review`** (flagged as below 7/10 threshold) |
| **Test 4 (Hard Exclusion)** | `SYNTH-MATH-REJ-001` | Maths | `00:25:00.000` – `00:25:15.000` | `15s` | `2, 2, 2, 1, 1, 1, 0` (input) | Blank in output | `Verified – Fail` | `Confirmed` | `Failed` | `Not Required` | **`Yes`** | **`Rejected`**; dialogue replaced with `[REDACTED — rejected record; do not reproduce]` and all 8 numeric score columns left blank |
| **Test 5 (Guardrail Check)** | Unchecked attestation | English | `00:10:00.000` – `00:10:15.000` | `15s` | `2, 2, 2, 1, 1, 1, 0` | Halted | `Verified – Pass` | `Confirmed` | `Passed` | `Not Required` | `No` | Execution stopped at `Validate Scores and Apply Review Gates` with error: `Submission stopped: confirm that the data is synthetic or anonymised and approved for this workflow.` |
