# Bambinos.live — AI Program Manager (Marketing) Take-Home

This repository contains the working no-code / AI-assisted prototype, candidate evidence, creative briefs, workflow documentation and compulsory case report prepared for the Bambinos.live AI Program Manager (Marketing) take-home assignment.

## Objective

Identify authentic 10–20 second classroom moments from long live-class recordings, evaluate their parent-facing value, screen for unsafe or unsuitable material, verify promising moments against the original recording, and prepare editor-ready briefs for human review.

## What is included

| Path | Purpose |
|---|---|
| `Bambinos_AI_Program_Manager_Case_Report.pdf` | Compulsory final case report |
| `prompts/01_content_mining_system_prompt.md` | Exact system prompt used for transcript content mining |
| `results/candidate_tracker.xlsx` | Populated tracker and scoring worksheet |
| `results/shortlisted_candidates.csv` | Structured output for the three shortlisted candidates |
| `results/rejected_moments.md` | Five hard-rejected moments and concise reasons |
| `results/ad_briefs/` | Individual Ad Creative Briefs for ENG-001, GIT-001 and SCI-001 |
| `workflows_or_scripts/workflow_architecture.md` | End-to-end workflow and human approval gates |
| `workflows_or_scripts/sop.md` | Operating procedure for the marketing workflow |
| `workflows_or_scripts/scoring_rubric.md` | Six moment buckets, 10-point rubric and hard exclusions |
| `workflows_or_scripts/tracker_formula.md` | Total-score formula and tracker data rules |
| `docs/decision_log.md` | Current decisions, unresolved checks and evidence boundaries |
| `SUBMISSION_CHECKLIST.md` | Pre-submission checks |

## Current sample results

| Candidate | Subject | Window | Score | Tracker decision |
|---|---|---|---:|---|
| ENG-001 | English | 00:09:56.139–00:10:13.179 | 6/10 | Needs Review |
| GIT-001 | Gita / Little Yogi | 00:47:01.679–00:47:15.340 | 7/10 | Needs Review |
| SCI-001 | Science | 00:04:57.939–00:05:15.889 | 7/10 | Needs Review |

Five other moments are recorded as rejected: MATH-REJ-001, MATH-REJ-002, MATH-REJ-003, MATH-REJ-004 and SCI-REJ-001. Their score fields are blank because hard exclusions override numerical scoring. See `results/rejected_moments.md`.

**Important:** ENG-001 scores 6/10, below the system prompt's 7/10 shortlist threshold. It is retained as a review-only exception in the working creative set; it is not a threshold-qualified candidate. All three candidates remain `Needs Review`, not approved for advertising.

## Workflow at a glance

1. Obtain the recording reference and timestamped WebVTT transcript.
2. Run transcript analysis using the versioned system prompt.
3. Log proposed moments, verbatim dialogue, taxonomy, scores and flags in the tracker.
4. Reject or escalate hard-exclusion content.
5. Manually verify the exact video/audio window and surrounding context.
6. Confirm guardian marketing consent, privacy and any sensitive cultural/contextual review.
7. Hand only cleared moments to an editor; complete marketing and safeguarding QA before publication.

The AI output is a candidate recommendation, not an approval decision. Transcripts alone cannot confirm visual quality, actual audio clarity, child comfort, consent or full context. Human review is mandatory.

## Tools and implementation status

- AI content analysis: ChatGPT using the supplied system prompt.
- Tracking and scoring: Google Sheets / Excel-compatible tracker.
- Verification: manual review of the original class recordings.
- Documentation and handoff: Markdown files and PDF.

This is a working prompt-and-tracker prototype and documented operating process. It is **not** a deployed application, production API integration, or fully automated pipeline. No production automation has been claimed.

## Data protection note

This repository intentionally does not include original class recordings or complete raw transcripts. Candidate dialogue is limited to the selected, anonymised candidate windows needed to demonstrate the sample outputs. Rejected private or identifying information is not reproduced. Check all permissions and safeguarding requirements before sharing the repository publicly.

## Tracker note

The original uploaded workbook had an incorrect heading in cell A1. The repository copy corrects A1 to `Session ID`; the original uploaded file was left unchanged. The score formula is `=IF(COUNT(J2:P2)=7,SUM(J2:P2),"")`.

## Economic assumptions and targets

The case report includes scenario-based unit-economics calculations for a planning volume of 500 classes per week. These are illustrative assumptions, not measured Bambinos operating data or verified cost savings. Proposed KPIs and rollout targets are labelled as targets rather than actual results.

## Official references

- Assignment repository: https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments
- Marketing assets folder: https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments/tree/main/marketing
- Final submission form: https://forms.gle/qu5gzySRHTSd5Uou9

## Repository status

Prepared as a GitHub-ready handover package. The package has not yet been pushed to a personal GitHub repository. See `SUBMISSION_CHECKLIST.md` for the remaining upload and final-submission steps.
