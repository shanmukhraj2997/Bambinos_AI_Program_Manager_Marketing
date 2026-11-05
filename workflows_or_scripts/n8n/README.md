# n8n MVP — Candidate Intake and Human Review Gate

## Purpose

This MVP automates the **post-analysis intake and review-gate stage** of the Bambinos content-mining process. The existing `prompts/01_content_mining_system_prompt.md` remains the prompt used to analyse transcript excerpts. A human operator enters the resulting anonymised candidate record into an n8n Form. n8n validates timestamps and rubric scores, calculates duration and total score, applies explicit review and safeguarding gates, and appends the structured record to a dedicated `Automation Intake` tab in Google Sheets.

This is intentionally scoped as a human-in-the-loop intake and governance automation rather than an autonomous AI transcript-mining system. It does not call an external LLM on raw classroom transcripts, inspect video/audio autonomously, verify guardian consent without human confirmation, or approve advertising. Those activities remain human-controlled.

## Workflow File

- `Bambinos_Candidate_Intake_Review_Gate_v2.json` (and `Bambinos_Candidate_Intake_Review_Gate.json`)

### Nodes

1. **Candidate Intake Form (`n8n-nodes-base.formTrigger`, v2.2)** — Captures anonymised candidate metadata, timestamps, 7-component rubric scores, and human compliance/review statuses.
2. **Validate Scores and Apply Review Gates (`n8n-nodes-base.code`, v2)** — Validates required fields, parses `HH:MM:SS.mmm` timestamps, enforces the 10–20 second clip duration rule, validates integer rubric scores (total 0–10), enforces hard-exclusion overrides and dialogue redaction, and assigns a cautious gate classification.
3. **Append Review Record to Google Sheets (`n8n-nodes-base.googleSheets`, v4.7)** — Appends the validated 28-column record to the `Automation Intake` worksheet tab in Google Sheets without overwriting the primary `Candidate Tracker` tab.

## Decision Logic

- **`Rejected`**: Assigned automatically whenever `Hard Exclusion Identified? = Yes`, `Privacy Review = Failed`, or `Visual Verification = Verified – Fail`. Numerical scores are withheld (left blank) and `Verbatim Dialogue` is replaced with `[REDACTED — rejected record; do not reproduce]` before writing to Google Sheets.
- **`Needs Review`**: Assigned when visual verification, guardian marketing consent, privacy review, or cultural/context review is pending/unverified, or when the total rubric score is below the `7/10` threshold.
- **`Eligible for Editor Review`**: Assigned only when all configured intake checks pass and total score is `>= 7/10`. This is **not** final advertising approval; authorised human sign-off and final creative QA remain mandatory.

## Verified Environment & End-to-End Execution

- **Runtime**: Self-hosted n8n (`v2.46.6`) running in Docker Desktop on Windows 11 (`docker.n8n.io/n8nio/n8n`, persistent volume `n8n_data`, timezone `Asia/Kolkata`).
- **Integration**: Connected via Google Sheets OAuth2 API and Google Drive API to the `Automation Intake` tab of `Bambinos_AI_Content_Mining_Tracker`.
- **End-to-End Verification**: Tested end-to-end with synthetic, non-identifying candidate submissions covering valid control (`Eligible for Editor Review`), pending guardian consent (`Needs Review`), below-threshold score (`Needs Review`), and hard exclusion (`Rejected` with automatic dialogue redaction and blank score fields). See `TEST_CASES.md` and `TEST_RESULTS.md` for full execution records.

## Setup & Reproduction Steps

1. Import `Bambinos_Candidate_Intake_Review_Gate_v2.json` into n8n via **Workflow menu (`...`) → Import from File...**.
2. In your Google Sheets tracker, create a separate worksheet tab named `Automation Intake` and paste the 28 headers from `Automation_Intake_Headers.csv` into Row 1 (`A1:AB1`).
3. Open the **Append Review Record to Google Sheets** node in n8n:
   - Connect your **Google Sheets OAuth2 API** credential (with Google Sheets API and Google Drive API enabled in Google Cloud Console).
   - Set **Document (`By ID`)** to your Google Spreadsheet ID.
   - Set **Sheet (`From list` or `By Name`)** to `Automation Intake`.
   - Keep **Mapping Column Mode** set to `Map Automatically`.
4. Save the workflow (`Ctrl + S`) and click **Execute** to open the `Candidate Intake Form` test URL and submit synthetic or anonymised records.

## Privacy and Safe Use

- Never submit raw classroom recordings, full raw transcripts, children's names, ages, contact details, school/family details, or other identifying information.
- Guardian marketing consent must be independently verified and documented by the authorised Bambinos team.
- Exported workflow JSON files in this repository have credential bindings and live spreadsheet IDs sanitised (`REPLACE_WITH_YOUR_GOOGLE_SPREADSHEET_ID`) so no OAuth tokens or private credentials are exposed in version control.
