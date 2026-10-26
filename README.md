# SSH Authentication Investigation — Rocky Linux and Kali

## Overview

This project documents a controlled SSH authentication investigation
using two virtual machines in VMware.

I generated six failed password attempts against a dedicated Rocky Linux
test account, followed by one successful login. I then reviewed the
server-side journal, exported the relevant evidence, and reconstructed
the authentication timeline.

This was an authorized lab simulation, not a real compromise.

## Environment

| Component | Role | Details |
|---|---|---|
| Rocky Linux | Monitored SSH server | Rocky Linux 10.2 |
| Kali Linux | Test activity source | SSH client |
| VMware | Virtualization platform | Two virtual machines |
| Target address | Rocky Linux | 192.168.137.133 |
| Source address | Kali Linux | 192.168.137.134 |
| Test account | Dedicated account | soclab |
| Evidence source | Server-side logs | systemd journal, sshd service |

## Investigation Question

What authentication activity occurred against the soclab account,
where did it originate, and did a successful login follow the failures?

## Method

1. Verified Rocky's network address and SSH service status.
2. Confirmed that the soclab test account existed.
3. Inspected the existing account-lockout configuration.
4. Tested SSH connectivity before starting the simulation.
5. Recorded a fresh simulation start time.
6. Generated six separate SSH connections with one incorrect password each.
7. Connected again using the correct password.
8. Reviewed and exported the SSH service journal.
9. Recorded a SHA-256 checksum for the exported evidence.

The preliminary connectivity test was excluded from the simulation's
evidence window.

## Timeline

Date: October 25, 2026.
Timezone: CDT, UTC-05:00.

All events below concern account soclab and source address 192.168.137.134.

| Time | Event | Source port | Process ID |
|---|---|---|---|
| 22:17:58 | Failed password | 42928 | 5055 |
| 22:18:57 | Failed password | 44782 | 5058 |
| 22:19:06 | Failed password | 53914 | 5061 |
| 22:19:17 | Failed password | 35516 | 5065 |
| 22:19:25 | Failed password | 50632 | 5068 |
| 22:19:38 | Failed password | 59798 | 5072 |
| 22:20:11 | Accepted password and session opened | 34032 | 5075 |

## Findings

- Six explicit "Failed password" events preceded one "Accepted password" event.
- All seven authentication outcomes involved the same account and source IP.
- Different source ports and process IDs were consistent with the separate
  SSH connections generated during the exercise.
- The accepted password occurred 33 seconds after the final failure.
- The first failed password and accepted password were 2 minutes,
  13 seconds apart.
- A session-opened event followed the accepted password.
- Related PAM failure messages were not counted as additional password attempts.

## Assessment and Limitations

The evidence establishes repeated rejected passwords followed by a
successful password authentication and session opening.

In a real investigation, this sequence would warrant further review.
It does not, by itself, establish malicious intent, password cracking,
credential theft, or unauthorized access.

For this exercise, I know the activity was generated manually from my
own Kali VM. Six attempts against one account are not sufficient to
claim password spraying, and no automated brute-force tool was used.

The reviewed authentication evidence does not establish which commands
were executed after login.

## Evidence

- evidence/simulation-start.txt — recorded exercise start time
- evidence/ssh-simulation.log — 20-line SSH journal export
- evidence/SHA256SUMS — checksum of the exported log

The journal export covers October 25, 2026, from 22:17:00 through
22:22:00 in the server's local timezone.

The checksum provides a reference for detecting later changes to the
export. It does not independently authenticate the source logs.

## Skills Demonstrated

- Linux SSH service inspection
- Authentication-log analysis
- Correlation by account, source IP, source port, and process ID
- Timestamp and timezone interpretation
- Evidence export and checksum verification
- Investigation reporting with explicit limitations
EOF
