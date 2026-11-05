# Bambinos.live — AI Program Manager (Marketing) Take-Home

**Repository:** `Bambinos_AI_Program_Manager_Marketing`  
**Assignment:** AI-enabled pipeline for finding parent-relevant short-form moments in live-class recordings  
**Current status:** Public GitHub repository and end-to-end tested n8n automation MVP uploaded; final review and Google Form submission remain pending.

## 1. Project objective

This project presents a repeatable, no-code / AI-assisted process for identifying authentic 10–20 second learning moments from long live-class recordings, evaluating their parent-facing value, screening for unsuitable content, verifying selected moments against the original recordings, and preparing editor-ready Ad Creative Briefs for human review.

The aim is to reduce manual review effort while preserving educational authenticity, child privacy, safeguarding and human approval.

## 2. What this repository contains

| Path | Purpose |
| :--- | :--- |
| `Bambinos_AI_Program_Manager_Case_Report.pdf` | Compulsory case report covering the problem, proposed process, sample results, metrics and rollout plan. |
| `prompts/01_content_mining_system_prompt.md` | The content-mining system prompt used for transcript analysis. |
| `results/Bambinos_AI_Content_Mining_Tracker.xlsx` | Candidate tracker, scores, compliance flags and review decisions. |
| `results/shortlisted_candidates.csv` | Structured records for ENG-001, GIT-001 and SCI-001. |
| `results/rejected_moments.md` | Five rejected moments and concise, privacy-conscious rejection reasons. |
| `results/ad_briefs/ENG-001.md` | English Ad Creative Brief. |
| `results/ad_briefs/GIT-001.md` | Gita / Little Yogi Ad Creative Brief. |
| `results/ad_briefs/SCI-001.md` | Science Ad Creative Brief. |
| `workflows_or_scripts/workflow_architecture.md` | End-to-end workflow design and human approval gates. |
| `workflows_or_scripts/sop.md` | Standard Operating Procedure for the content-mining process. |
| `workflows_or_scripts/scoring_rubric.md` | Six moment categories, ten-point scoring rubric and hard exclusions. |
| `workflows_or_scripts/tracker_formula.md` | Total-score formula and tracker data rules. |
| `workflows_or_scripts/n8n/` | **End-to-end tested n8n workflow MVP** (`Bambinos_Candidate_Intake_Review_Gate_v2.json`), setup guide, Google Sheets header template (`Automation_Intake_Headers.csv`), synthetic test suite (`TEST_CASES.md`), execution logs (`TEST_RESULTS.md`) and verification screenshots. |
| `docs/decision_log.md` | Candidate decisions, unresolved checks and evidence boundaries. |
| `docs/submission_checklist.md` | Final repository and submission checklist. |
| `.gitignore` | Excludes local recordings, raw transcripts and common local development files from Git workflows. |

## 3. Sample results

The tracker contains three moments retained for creative review:

| Candidate | Subject | Original time window | Duration | Score | Tracker decision |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `ENG-001` | English | 00:09:56.139—00:10:13.179 | 17.040 sec | 6/10 | Needs Review |
| `GIT-001` | Gita / Little Yogi | 00:47:01.679—00:47:15.340 | 13.661 sec | 7/10 | Needs Review |
| `SCI-001` | Science | 00:04:57.939—00:05:15.889 | 17.950 sec | 7/10 | Needs Review |

**Threshold qualification:** The system prompt states that a candidate needs at least 7/10 and must have no hard exclusion to qualify for shortlisting. ENG-001 has a score of 6/10. It is retained in the working creative-review set as a documented review-only exception; it is not a threshold-qualified candidate. GIT-001 and SCI-001 meet the numerical threshold, but both remain subject to all compliance and consent checks.

Five moments were rejected and retained as quality-control evidence:
* `MATH-REJ-001`
* `MATH-REJ-002`
* `MATH-REJ-003`
* `MATH-REJ-004`
* `SCI-REJ-001`

Their score fields are blank because hard exclusions override numerical scoring. See `results/rejected_moments.md`.

## 4. Workflow overview

1. Obtain the session reference, original recording and timestamped WebVTT transcript.
2. Analyse the transcript using the versioned system prompt.
3. Identify potential 10–20 second moments and log timestamps, dialogue, taxonomy, scores and compliance flags in the tracker (either directly or via the tested n8n Candidate Intake Form workflow).
4. Reject or escalate content that triggers a hard exclusion.
5. Have a human reviewer inspect each candidate in the original recording, including surrounding context, audio and visual evidence.
6. Confirm guardian marketing consent, privacy requirements and any necessary cultural or contextual review.
7. Prepare an Ad Creative Brief and hand off only candidates that have received all required approvals.
8. Have the editor produce a draft, followed by marketing and safeguarding quality checks before any advertising use.

The AI output is a candidate recommendation, not an approval decision. A transcript alone cannot establish visual quality, actual audio clarity, a child's comfort, consent or the full classroom context. Human review is mandatory.

## 5. Scoring and decision rules

The ten-point rubric uses:
* Parent learning value: 0–2
* Scroll-stopping hook: 0–2
* Child participation: 0–2
* Positive authentic emotion: 0–1
* Visual potential: 0–1
* Audio clarity: 0–1
* Sound-off readability: 0–1

Hard exclusions override scores. These include child or family identifying information, embarrassment or distress, teacher shaming or threatening behaviour, inappropriate interactions, unverified outcome claims, misleading edits, private information on shared screens, missing consent and material that cannot responsibly be cleared.

The tracker total uses:
```excel
=IF(COUNT(J2:P2)=7,SUM(J2:P2),"")
```
The formula calculates a total only when all seven score cells contain numeric values. Missing scores remain blank rather than being treated as zero.

## 6. Tools and implementation status

To maintain strict transparency between what has been built, tested and planned, this project is structured across three clearly separated layers:

### A. Completed Prompt-and-Tracker Prototype (Core Assignment Deliverables)
* **AI content analysis:** ChatGPT using the versioned system prompt (`prompts/01_content_mining_system_prompt.md`) across all four official subjects (English, Gita / Little Yogi, Maths and Science).
* **Tracking and scoring:** Google Sheets / Excel-compatible 22-column candidate tracker (`results/Bambinos_AI_Content_Mining_Tracker.xlsx`) with automated score-validation formula.
* **Audio-visual verification:** Manual review of the original class recordings for `ENG-001`, `GIT-001` and `SCI-001`, plus five documented hard-exclusion rejections (`results/rejected_moments.md`).
* **Documentation and handoff:** Three editor-ready Ad Creative Briefs (`results/ad_briefs/`), SOP, workflow architecture and the compulsory case report PDF (`Bambinos_AI_Program_Manager_Case_Report.pdf`).

### B. Tested n8n Automation MVP (`workflows_or_scripts/n8n/`)
* **Implemented and end-to-end tested workflow:** A local self-hosted n8n (`v2.46.6`) workflow running in Docker Desktop on Windows 11 (`Bambinos_Candidate_Intake_Review_Gate_v2.json`) connected to Google Sheets via OAuth2 API.
* **Three-node architecture:**
  1. **Candidate Intake Form (`formTrigger` v2.2):** Collects anonymised candidate metadata, timestamps, seven-component rubric scores, compliance flags and human review statuses with a mandatory operator attestation checkbox.
  2. **Validate Scores and Apply Review Gates (`code` v2):** Validates required fields, parses `HH:MM:SS.mmm` timestamps, enforces the 10–20 second duration window, verifies integer score ranges (0–10 total), enforces hard-exclusion overrides and assigns a cautious gate classification.
  3. **Append Review Record to Google Sheets (`googleSheets` v4.7):** Appends validated 28-column records to a dedicated `Automation Intake` tab in the Google Sheets tracker without overwriting the main `Candidate Tracker` tab.
* **Verified safeguarding and gate outcomes:** Tested end-to-end with synthetic, non-identifying records (`workflows_or_scripts/n8n/TEST_RESULTS.md`). Hard exclusions, failed privacy reviews or failed visual verification automatically classify the record as `Rejected`, withhold all numerical scores (leaving score cells blank) and redact the dialogue field to `[REDACTED — rejected record; do not reproduce]`. Pending consent or scores below `7/10` hold the record in `Needs Review`. When all intake checks pass, the maximum automated classification is `Eligible for Editor Review`—never automatic advertising approval.

### C. Future AI Integrations (Post-MVP Roadmap — Not Yet Deployed)
The following capabilities are designed for future rollout only after formal organisational approval, enterprise data-privacy sign-off and guardian-consent integration:
* **Automated AI transcript mining via authorised enterprise API:** Sending approved, pre-anonymised transcript chunks to an enterprise LLM API (with zero data-training retention) to output structured candidate JSON directly into n8n.
* **Automated Ad Creative Brief drafting:** Generating draft Markdown briefs for candidates that pass human visual verification and guardian consent checks.
* **Editor notifications and weekly analytics dashboards:** Automated Slack/email handoff alerts, false-positive rate tracking and weekly content-mining throughput reporting.

## 7. Privacy and responsible sharing

The original classroom recordings and complete raw WebVTT transcripts are intentionally not included in this public repository. They should remain in appropriately access-controlled storage. Do not commit raw recordings, complete transcripts, children's names, ages, contact details, school or family information, or screenshots that reveal identifying data.

All end-to-end tests of the n8n workflow (`workflows_or_scripts/n8n/`) were conducted exclusively using synthetic, non-identifying test records. Exported workflow JSON files have OAuth credentials and live spreadsheet IDs sanitised (`REPLACE_WITH_YOUR_GOOGLE_SPREADSHEET_ID`).

A `Verified - Pass` value in the tracker or an `Eligible for Editor Review` status in the n8n intake gate does not mean that a candidate is approved for advertising. All three real candidates (`ENG-001`, `GIT-001` and `SCI-001`) currently remain `Needs Review` and are **not cleared for advertising**.

## 8. Business impact and rollout assumptions

The case report models a planning volume of 500 live classes per week. Time, cost and capacity figures are scenario-based assumptions for evaluation and planning; they are not measured Bambinos operating data, verified savings or actual campaign results. Proposed KPIs and 30-60-90 day milestones are labelled as targets, not achieved outcomes.

## 9. Official assignment references

* [Official Bambinos.live hiring-assessment repository](https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments)
* [Official marketing assets and instructions](https://www.google.com/search?q=https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments/tree/main/AI-PM-Marketing)
* [Final assignment submission form](https://forms.gle/qu5gzySRHTSd5Uou9)

## 10. Repository and submission status

The assignment files and the verified n8n workflow extension have been prepared for this public GitHub repository. The final quality review and official Google Form submission are still pending. The assignment should only be described as submitted after the form has been completed successfully and submission has been confirmed.

Use `docs/submission_checklist.md` for the remaining final checks.
