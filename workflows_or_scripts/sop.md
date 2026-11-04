# Standard Operating Procedure (SOP)

## Purpose

Find authentic 10–20 second learning moments in long live-class recordings and prepare safe, editor-ready briefs without treating AI output as publication approval.

## Procedure

1. **Intake:** Record the session ID, subject, recording reference and transcript version. Keep original source timestamps intact.
2. **Transcript analysis:** Run the supplied WebVTT through `prompts/01_content_mining_system_prompt.md`. Ask for candidate moments and a separate rejection report. Do not force a minimum number of clips.
3. **Candidate logging:** Add each candidate to the tracker with start/end times, duration, hook, moment bucket, verbatim dialogue, score components, geography hypothesis, compliance flags and editor notes.
4. **Hard-exclusion review:** Reject or escalate child/family PII, distress, embarrassment, shaming, insulting or threatening language, private screen content, unsupported claims, misleading edits or missing consent. Hard exclusions override scores.
5. **Score:** Score only evidence that can be supported. Transcript-only analysis cannot confirm visual quality, real audio clarity or sound-off readability. Keep those fields pending until the recording is reviewed.
6. **A/V verification:** A human watches the exact candidate window plus surrounding context. Check whether the child is visible, whether the relevant activity is happening, whether speech is intelligible and whether captions match the recording. Record the verification outcome.
7. **Consent and privacy gate:** Confirm documented guardian marketing consent and required internal approvals. Redact identifying details. For culturally/religiously contextual material, obtain appropriate context review. A visual pass alone is not clearance.
8. **Decision:** Use `Rejected` for hard exclusions, `Needs Review` where any approval or evidence is outstanding, and only the authorised cleared status when all required checks are documented. Never mark an item approved based solely on its numerical score.
9. **Editor handoff:** Only hand off cleared candidates with the exact time window, source dialogue, proposed hook, caption direction, editing notes and compliance conditions.
10. **Final QA:** Review the edited creative against the source recording and approval record before any campaign upload.
11. **Feedback loop:** Log editor rejection / false-positive reason, corrections, time spent and eventual usable-clip outcome. Update the prompt and SOP through version control.

## Roles

| Role | Responsibility |
|---|---|
| AI / workflow operator | Run prompt, capture outputs, preserve source references |
| Marketing reviewer | Validate parent-facing value, hook and taxonomy |
| Human video reviewer | Confirm A/V context and usable footage |
| Safeguarding / authorised approver | Consent, privacy and sensitive-context clearance |
| Video editor | Produce the draft from an approved brief |
| Marketing lead | Final creative and campaign approval |

## Exception handling

- If transcript and audio differ, audio must be checked and the discrepancy documented.
- If a word remains unclear, do not guess; omit or visibly mark it as unclear.
- If consent status is unknown, keep `Needs Review` and do not publish.
- If a class yields no safe clips, return zero rather than lowering the quality bar.
