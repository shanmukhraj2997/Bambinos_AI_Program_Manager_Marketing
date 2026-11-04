# Decision Log and Evidence Boundaries

## Current candidate outcomes

| Candidate | Score | Visual verification | Tracker decision |
|---|---:|---|---|
| ENG-001 | 6/10 | Verified – Pass | Needs Review |
| GIT-001 | 7/10 | Verified – Pass | Needs Review |
| SCI-001 | 7/10 | Verified – Pass | Needs Review |

## Rejected records

MATH-REJ-001 through MATH-REJ-004 and SCI-REJ-001 are rejected. Their score fields remain blank. Rejection reasons are summarised in `results/rejected_moments.md`.

## Important qualifications

- `Verified – Pass` records the user's stated manual video-verification result; it is not advertising approval.
- All three selected candidates remain `Needs Review`. Guardian marketing consent and other required reviews remain outstanding in the tracker.
- GIT-001 requires cultural/religious context review. SCI-001 includes unclear transcript wording and needs careful audio verification for captions.
- ENG-001 scores 6/10, below the system prompt's 7/10 threshold. It is included as a review-only exception in the working shortlist.
- Geography labels are marketing hypotheses only; they are not evidence of a child's location, nationality or identity.
- Economic scenarios and targets in the case report are planning assumptions / proposed targets, not measured results.
- The workflow is a no-code / AI-assisted prototype and documented process. No production application, API integration or automatic end-to-end deployment is claimed.

## Source files

- `prompts/01_content_mining_system_prompt.md`: exact prompt file supplied for the assignment.
- `results/candidate_tracker.xlsx`: populated tracker export, with the A1 header corrected in this repository copy.
- `Bambinos_AI_Program_Manager_Case_Report.pdf`: compulsory case report.
- Candidate facts and statuses are transcribed from the supplied tracker and the candidate handover.
