# Linux Privilege Escalation Workflow Diagram

```mermaid
flowchart TD

A[Start Lab] --> B[Environment Validation]

B -->|Linux Confirmed| C[Phase 1: System Context]
B -->|Not Linux| Z[Stop Execution]

C --> D[Phase 2: Privilege Audit]

D -->|Full Sudo Access| R[Escalate to Root]
D -->|Limited Access| E[Phase 3: SUID Check]

E --> F[Phase 4: Cron Review]
F --> G[Phase 5: Writable Files]
G --> H[Phase 6: Capabilities]
H --> I[Phase 7: Kernel Mapping]

I -->|Exploit Found| R
I -->|No Exploit| X[Generate Failure Report]

R --> S[Generate Escalation Summary]
S --> END[Stop]