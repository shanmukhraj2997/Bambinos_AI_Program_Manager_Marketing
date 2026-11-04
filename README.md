# Bambinos.live — AI Program Manager (Marketing) Take-Home

**Repository:** [Bambinos_AI_Program_Manager_Marketing](https://github.com/shanmukhraj2997/Bambinos_AI_Program_Manager_Marketing)  
**Assignment:** AI-enabled pipeline for finding parent-relevant short-form moments in live-class recordings  
**Current status:** Public GitHub repository uploaded; final review and Google Form submission remain pending.

## 1. Project objective

This project presents a repeatable, no-code / AI-assisted process for identifying authentic 10–20 second learning moments from long live-class recordings, evaluating their parent-facing value, screening for unsuitable content, verifying selected moments against the original recordings, and preparing editor-ready Ad Creative Briefs for human review.

The aim is to reduce manual review effort while preserving educational authenticity, child privacy, safeguarding and human approval.

## 2. What this repository contains

| Path | Purpose |
|---|---|
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
| `docs/decision_log.md` | Candidate decisions, unresolved checks and evidence boundaries. |
| `docs/submission_checklist.md` | Final repository and submission checklist. |
| `.gitignore` | Excludes local recordings, raw transcripts and common local development files from Git workflows. |

## 3. Sample results

The tracker contains three moments retained for creative review:

| Candidate | Subject | Original time window | Duration | Score | Tracker decision |
|---|---|---|---:|---:|---|
| ENG-001 | English | 00:09:56.139–00:10:13.179 | 17.040 sec | 6/10 | Needs Review |
| GIT-001 | Gita / Little Yogi | 00:47:01.679–00:47:15.340 | 13.661 sec | 7/10 | Needs Review |
| SCI-001 | Science | 00:04:57.939–00:05:15.889 | 17.950 sec | 7/10 | Needs Review |

**Threshold qualification:** The system prompt states that a candidate needs at least 7/10 and must have no hard exclusion to qualify for shortlisting. ENG-001 has a score of 6/10. It is retained in the working creative-review set as a documented review-only exception; it is not a threshold-qualified candidate. GIT-001 and SCI-001 meet the numerical threshold, but both remain subject to all compliance and consent checks.

Five moments were rejected and retained as quality-control evidence:

- `MATH-REJ-001`
- `MATH-REJ-002`
- `MATH-REJ-003`
- `MATH-REJ-004`
- `SCI-REJ-001`

Their score fields are blank because hard exclusions override numerical scoring. See [`results/rejected_moments.md`](results/rejected_moments.md).

## 4. Workflow overview

1. Obtain the session reference, original recording and timestamped WebVTT transcript.
2. Analyse the transcript using the versioned system prompt.
3. Identify potential 10–20 second moments and log timestamps, dialogue, taxonomy, scores and compliance flags in the tracker.
4. Reject or escalate content that triggers a hard exclusion.
5. Have a human reviewer inspect each candidate in the original recording, including surrounding context, audio and visual evidence.
6. Confirm guardian marketing consent, privacy requirements and any necessary cultural or contextual review.
7. Prepare an Ad Creative Brief and hand off only candidates that have received all required approvals.
8. Have the editor produce a draft, followed by marketing and safeguarding quality checks before any advertising use.

The AI output is a candidate recommendation, not an approval decision. A transcript alone cannot establish visual quality, actual audio clarity, a child's comfort, consent or the full classroom context. Human review is mandatory.

## 5. Scoring and decision rules

The ten-point rubric uses:

- Parent learning value: 0–2
- Scroll-stopping hook: 0–2
- Child participation: 0–2
- Positive authentic emotion: 0–1
- Visual potential: 0–1
- Audio clarity: 0–1
- Sound-off readability: 0–1

Hard exclusions override scores. These include child or family identifying information, embarrassment or distress, teacher shaming or threatening behaviour, inappropriate interactions, unverified outcome claims, misleading edits, private information on shared screens, missing consent and material that cannot responsibly be cleared.

The tracker total uses:

```excel
=IF(COUNT(J2:P2)=7,SUM(J2:P2),"")
```

The formula calculates a total only when all seven score cells contain numeric values. Missing scores remain blank rather than being treated as zero.

## 6. Tools and implementation status

The current deliverable is a working prompt-and-tracker prototype supported by a documented manual review process:

- **AI content analysis:** ChatGPT using the supplied system prompt.
- **Tracking and scoring:** Google Sheets / Excel-compatible candidate tracker.
- **Audio-visual verification:** Manual review of the original recordings.
- **Documentation and handoff:** Markdown files and the case report PDF.

This repository does **not** contain a deployed application, production API integration, or fully automated end-to-end pipeline. No n8n, Make, Zapier or other production automation has been built or deployed as part of the current prototype. The `workflows_or_scripts/` directory documents the designed process, SOP, rubric and formulas. An automation export may be added there if a workflow is implemented and tested in a later iteration.

## 7. Privacy and responsible sharing

The original classroom recordings and complete raw WebVTT transcripts are intentionally not included in this public repository. They should remain in appropriately access-controlled storage. Do not commit raw recordings, complete transcripts, children's names, ages, contact details, school or family information, or screenshots that reveal identifying data.

The candidate samples and rejected-moment summaries are limited to the material needed to explain the process. Before any public or marketing use, confirm that repository sharing is permitted and that all required guardian marketing consent, privacy, safeguarding and contextual approvals have been documented.

A `Verified – Pass` value in the tracker records the stated video-verification outcome; it does not mean that a candidate is approved for advertising. All three candidates currently remain `Needs Review` and are **not cleared for advertising**.

## 8. Business impact and rollout assumptions

The case report models a planning volume of 500 live classes per week. Time, cost and capacity figures are scenario-based assumptions for evaluation and planning; they are not measured Bambinos operating data, verified savings or actual campaign results. Proposed KPIs and 30-60-90 day milestones are labelled as targets, not achieved outcomes.

## 9. Official assignment references

- [Official Bambinos.live hiring-assessment repository](https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments)
- [Official marketing assets and instructions](https://github.com/bambinoslive/AI-PM-hiring-take-home-assignments/tree/main/marketing)
- [Final assignment submission form](https://forms.gle/qu5gzySRHTSd5Uou9)

## 10. Repository and submission status

The assignment files have been uploaded to this public GitHub repository. The final quality review and official Google Form submission are still pending. The assignment should only be described as submitted after the form has been completed successfully and submission has been confirmed.

Use [`docs/submission_checklist.md`](docs/submission_checklist.md) for the remaining final checks.
