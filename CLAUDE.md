# Israel Handgun License — AI-Assisted Application

This Claude Code workspace guides you through applying for an Israeli handgun license (רישיון לנשיאת אקדח) via the gov.il portal.

## Quick Start

Tell Claude:
> "Help me apply for a gun license"

Claude will check your eligibility, collect your information, navigate the gov.il portal, and submit your application.

## Skills Available

| Skill | Purpose |
|-------|---------|
| `gun-license` | Main orchestrator — start here |
| `eligibility` | Determine which eligibility category applies to you |
| `collect-info` | Step-by-step interview to gather all required data |
| `login` | Authenticate on gov.il |
| `apply` | Fill and submit the application form |
| `status-check` | Check application status |

## Data

Your data is stored locally in `./data/<id>/applicant.md`. It is gitignored and never leaves your machine.

## Licensing Portal

The Israel Police Firearms Licensing Division (ענף רישוי נשק) handles all civilian licenses via:
- Online: `https://www.gov.il/he/service/firearms_license`
- In-person: district firearms licensing offices (לשכות רישוי נשק)

## Phases

| Phase | Description |
|-------|-------------|
| 1 | Eligibility check |
| 2 | Data collection |
| 3 | Login to gov.il |
| 4 | Submit application |
| 5 | Medical exam (in-person, cannot be automated) |
| 6 | Status tracking |

## Note

Claude automates the administrative submission only. The medical examination, background check, and final decision are performed by authorized personnel and cannot be automated.
