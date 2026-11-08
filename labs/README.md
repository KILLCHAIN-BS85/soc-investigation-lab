# Lab Index and Naming Convention

## Naming convention

Use a permanent repository-wide ID, LAB-NNN, and folder format `lab-NNN-short-topic`. Use lowercase, hyphen-separated topic names. Allocate the next unused number; never reuse IDs or renumber existing labs. Keep dates and certification versions inside each write-up rather than in permanent IDs.

## Lab index

| ID | Activity | Location | Status |
| --- | --- | --- | --- |
| LAB-001 | SSH authentication investigation | [Existing walkthrough](../README.md) | Existing lab; files remain in their original locations |
| LAB-002 | HTTP exposure assessment and remediation | [Activity write-up](lab-002-http-exposure/README.md) | Pending execution evidence |

Next available ID: LAB-003.

## Future lab structure

```text
labs/
  lab-NNN-short-topic/
    README.md
    screenshots/
    evidence/
```

Create artifact directories only when files are ready. Each activity write-up should include purpose, scope, environment, actions, actual observations, remediation, validation, limitations, and lessons learned. Knowledge-check worksheets are not part of this repository structure.

Use Planned, In progress, Completed, or Archived as appropriate. Separate expected behavior from observed results. Mark a lab Completed only when execution and validation are supported by evidence. Caption screenshots with what they demonstrate; do not treat screenshots alone as proof of a broader security assessment. Review artifacts for credentials, personal information, and unrelated traffic before publishing.
