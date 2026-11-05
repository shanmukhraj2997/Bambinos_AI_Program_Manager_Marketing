# End-to-End Execution Results — n8n Candidate Intake & Review Gate MVP

## Test Environment

- **n8n Version**: `2.46.6 (Self Hosted)` via Docker Desktop (`docker.n8n.io/n8nio/n8n`) on Windows 11 (`Asia/Kolkata`)
- **Destination**: Google Sheets (`Bambinos_AI_Content_Mining_Tracker` → `Automation Intake` worksheet tab via OAuth2 API)
- **Date Verified**: 2026-11-05

## End-to-End Execution Summary

| Sheet Row | Session ID | Candidate ID | Subject | Computed Duration | Output Scores (`J`–`P`) | Total Score (`Q`) | Final Decision (`U`) | Dialogue Output (`I`) | Observed Outcome |
|---:|---|---|---|---:|---|---|---|---|---|
| **Row 2** | `SYNTH-SESSION-001` | `SYNTH-ENG-001` | English | `15` | `2, 2, 2, 1, 1, 1, 0` | `9` | `Eligible for Editor Review` | `[Teacher]: What sound blends these two letters? [Student A]: Oh! It makes the 'sh' sound!` | **Passed** — Appended cleanly; capped at `Eligible for Editor Review` |
| **Row 3** | `SYNTH-SESSION-002` | `SYNTH-GIT-002` | Gita / Little Yogi | `14` | `2, 2, 2, 1, 1, 1, 0` | `9` | `Needs Review` | `[Teacher]: What do we do when we feel nervous? [Student B]: Take three deep breaths first.` | **Passed** — Pending guardian consent held record in `Needs Review` |
| **Row 4** | `SYNTH-SESSION-003` | `SYNTH-SCI-003` | Science | `12` | `1, 1, 1, 1, 1, 1, 0` | `6` | `Needs Review` | `[Teacher]: Move the torch closer. [Student C]: The shadow got bigger!` | **Passed** — Score `6/10` held record in `Needs Review` |
| **Row 5** | `SYNTH-SESSION-004` | `SYNTH-MATH-REJ-001` | Maths | `15` | *(Blank)* | *(Blank)* | `Rejected` | `[REDACTED — rejected record; do not reproduce]` | **Passed** — Hard exclusion overrode 9/10 input score, blanked score cells, and redacted dialogue |

## Key Engineering Note Discovered During Live n8n Testing

During end-to-end testing in **n8n v2.46.6**, we identified that `n8n-nodes-base.formTrigger` (`typeVersion: 2.2`) keys its output payload by the human-readable `fieldLabel` (e.g. `"Session ID"`) and emits single-checkbox fields without option values as a non-empty array (`[null]`) when checked. The `Validate Scores and Apply Review Gates` Code node was updated to support both `fieldName` and `fieldLabel` keys and to accurately evaluate the v2.46.6 checkbox payload.
