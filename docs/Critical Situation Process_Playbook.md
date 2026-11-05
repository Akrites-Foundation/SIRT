This playbook proposes an outlined standard **Akrites Critical Situation (Crit-Sit)** incident response process designed for Akrites.

## **Akrites SIRT Crit-Sit Response Playbook**

### **Incident Severity & Escalation Matrix**

| Severity Level | Trigger Criteria | TLP Handling | Response SLA | Read-In & Escalation |
| :---- | :---- | :---- | :---- | :---- |
| **Crit-Sit (P1)** | Active exploitation, critical supply chain zero-day, unpatched high-impact library with no active maintainer ("Maintainer of Last Resort"), or high risk of embargo breach. | **TLP:RED** | **Immediate (\< 15 mins)** | Executive SIRT Lead, Primary Upstream Maintainers, CISA/SIRT Liaison |
| **Major (P2)** | High/Critical CVSS vulnerability in widely used dependency, no known active exploitation, standard CVD timeline feasible. | **TLP:AMBER** | **\< 1 hour** | Assigned SIRT Case Lead, Core Project Maintainers |
| **Minor (P3/P4)** | Low/Medium severity bug, low exploitability index, routine security patch. | **TLP:CLEAR / AMBER** | **Standard (1–3 Business Days)** | Standard Triage Team, Upstream Maintainer |

1. **Discovery:**   
   1. **Declaration, Deduplication & Read-In Control:**T-0 to T-15 Minutes.  
      1. **Intake & Dedupe:** Intake finding (from member, scanner, or external finder). Merge duplicate reports into a single canonical SIRT Case ID.  
      2. **Declare Crit-Sit:** SIRT Lead designates the case as a **TLP:RED Crit-Sit**.  
      3. **Enforce Read-In Protocol:**  
         1. Access to the case channel, bridge, and private advisory workspace is strictly locked to **invite-only**.  
         2. Every participant must complete a **Read-In Acknowledgement** (logging identity, role justification, and explicit agreement to non-disclosure / embargo compliance).  
      4. **Mobilize Core Roles:**  
         1. **Incident Commander (IC):** SIRT Case Lead overseeing operational flow.  
         2. **Remediation Lead:** Technical lead / maintainer drafting the fix.  
         3. **Read-In Officer / Scribe:** Tracks access logs, Read-In agreements, case timeline, and TLP state.  
         4. **Comms Lead:** Manages secure CVD channel updates with finders, upstream maintainers, and pre-notification partners.  
2. **Triage, Isolation & CVD Window Establishment:**T-15 to T-120 Minutes.  
   1. **Assess Impact & Score:** Evaluate CVSS v3/v4, EPSS score, and ecosystem dependency reach.  
   2. **Isolate Code Environment:** Work strictly within private GitHub Security Advisories (GHSA) or encrypted offline mirrors. **Zero public commits** or visible pull requests during this phase.  
   3. **Establish CVD Embargo:** Coordinate with the finder and upstream project maintainers to fix the CVD disclosure target date (e.g., expedited 7–14 day window for Crit-Sit vs. standard 90 days).  
   4. **Determine Maintainer Track:** If the upstream package is unmaintained, trigger Akrites "Maintainer of Last Resort" protocol to assume remediation authority.  
3. **Siloed Patch Development & Selective Read-In:**Active Remediation.  
   1. **Upstream-First Remediation:** Technical team develops and tests the patch, keeping fixes non-fragmented (no proprietary forks; fix flows directly to upstream original home).  
   2. **Selective Read-In Expansion:** If external SME or upstream project maintainers are needed, the Read-In Officer executes formal Read-In onboarding prior to granting workspace access.  
   3. **Pre-Notification (Trusted Partners):** Distribute pre-patch advisory material under **TLP:RED embargo** to critical infrastructure and pre-notification members via secure PGP channels.  
4. **Synchronized Release, CVE/VEX & Public CVD:**Disclosure Window.  
   1. **Validate Patch:** Run automated build matrices and regression tests.  
   2. **Publish Upstream:** Push the patch directly to the original upstream repository namespace at the designated embargo lift time.  
   3. **Issue Identifiers & Advisories:** Simultaneously publish CVE details, VEX (Vulnerability Exploitability eXchange) status, and formal security advisories.  
   4. **Read-Out / De-escalation:** Formally execute the **Read-Out Protocol**—notifying all read-in participants that the embargo has expired and transitioning case material from TLP:RED to TLP:CLEAR.  
5. **SIRT Post-Mortem & Ecosystem Review:**Within 24 \- 72 Hours.  
   1. **PIR & Disclosure Audit:** Convene post-incident review to verify that embargo boundaries held and no pre-patch leaks occurred.  
   2. **Downstream Monitoring:** Track ecosystem patch adoption and assist downstream distributions with integration.  
   3. **Process Refinement:** Update automated triage/deduplication heuristics to improve future AI-accelerated findings handling.

### 

### 

### **Akrites Internal Communication Templates**

#### **Executive Read-In & Status Template (TLP:RED)**

**\[TLP:RED \- STRICT EMBARGO\] CRIT-SIT DECLARATION: Case \#\[SIRT-ID\]**  
**Incident Lead:** \[Name\]  
**Read-In Workspace:** \[Private Link \- Invite Only\]  
**Affected Component / Upstream Library:** \[Package Name & Version Range\]

**1\. Summary of Severity & Ecosystem Risk:**  
\[CVSS Score / Exploitation Status / Scope of Impact across critical infrastructure\]  
**2\. Current Remediation Status:**  
\[Private patch status / Test results / Upstream Maintainer engagement\]  
**3\. CVD Timeline & Embargo Target:**  
Target Embargo Lift: \[Date/Time UTC\]

Next Internal Status Update: \[Time UTC\]

#### **Read-In Acknowledgment Protocol Log**

Plaintext

```

[READ-IN RECORD]
Case ID: SIRT-2026-XXXX
Participant Name: [Full Name]
Organization / Role: [Entity / Upstream Maintainer / Engineer]
Justification for Access: [e.g., Core Maintainer / Patch Reviewer]
Read-In Timestamp: 2026-09-22T11:36:20Z
Read-In Officer Signature: [SIRT Lead ID]
TLP Binding: TLP:RED (Strict embargo until coordinated public disclosure)

```

