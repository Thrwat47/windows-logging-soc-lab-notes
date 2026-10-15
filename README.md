

# Windows Logging for SOC — TryHackMe

**Completed:** 09/28/2026

## Overview

Hands-on notes from the TryHackMe Windows Logging for SOC room.

## Objectives

- Understand Windows Security logs and Sysmon.
- Review process, file, registry, network, and DNS events.
- Practice tracing suspicious activity across related events.

## Tools and Data

- Windows Event Viewer
- Sysmon
- `Practice-Sysmon.evtx` (provided by the lab)

## Investigation Workflow

1. Review Sysmon process creation events (Event ID 1).
2. Note suspicious process IDs, image paths, command lines, and parent processes.
3. Correlate related events using the Process ID and timestamps.
4. Review file and registry events for persistence clues.
5. Review network connections and DNS queries.
6. Record evidence and summarize the timeline.

## Key Event IDs Reviewed
- **4624** — Successful Login 
- **4625**  — Failed Login 
- **4720**  — A user account created
- **4722**   — A user account enabled
- **4738**  — A user account changed
- **4725**  — A user account disabled
- **4726**  — A user account deleted
- **4723**  — A user changed his password
- **4724**  — A user's password  reset
- **4732**  — A user was added to a security group
- **4733**  — A user was removed from a security group
- **4688**  — Log an event every time a new process is launched, including its command line and process details
- **1** — Process creation
- **3** — Network connection
- **11** — File creation
- **12–14** — Registry changes
- **15** — File stream hash
- **22** — DNS query

## Findings

- **Suspicious file:** C:\Users\sarah.miller\Downloads\ckjg.exe
- **C2 IP and port:** 193[.]46[.]217[.]4:7777
- **Related domain:** hkfasfsafg[.]click
- **Evidence:** 
- **Process event:** Sysmon Event ID 1 showed `(ckjg.exe) running from `C:\Users\sarah.miller\Downloads\ckjg.exe`.
- **Persistence evidence:** A related file or registry event showed `[C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url]`.
- **Network evidence:** A related network event showed a connection to `193[.]46[.]217[.]4:7777`.
- **Persistence evidence:** Sysmon Event ID 11 recorded `DeleteApp.url` in the user's Startup folder.
- **DNS evidence:** Sysmon Event ID 22 recorded the query for `hkfasfsafg.click`.
- **Correlation:** I linked the events by Process ID and timestamp.
## What I Learned


I learned how to investigate Windows activity by correlating Sysmon events across processes, files, registry changes, network connections, and DNS queries. This helped me trace malware persistence and identify its command-and-control activity.
## Screenshots


<img width="1895" height="951" alt="Screenshot 2026-10-15 060734" src="https://github.com/user-attachments/assets/4d82aa8c-2562-4bbc-ad86-4b87cb91b64b" />


