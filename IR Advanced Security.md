<div align="center">

# IT Helpdesk Portfolio
### Advanced Security Incident Response — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Advanced%20Security%20Incident%20Response-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-5-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Sentinel%20%7C%20Forensics%20%7C%20IR-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases five representative engagements spanning the most common **Advanced Security Incident Response** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0467588`](#inc0467588--single-alert-unravels-into-a-multi-week-advanced-persistent-threat-requiring-full-kill-chain-reconstruction) | Single alert unravels into a multi-week advanced persistent threat requiring full kill-chain reconstruction | P1 | 4d 10h |
| 2 | [`INC0467931`](#inc0467931--active-ransomware-outbreak-requires-isolation-forensics-and-recovery-architecture-decisions-in-real-time) | Active ransomware outbreak requires isolation, forensics, and recovery architecture decisions in real time | P1 | 1d 14h |
| 3 | [`INC0468274`](#inc0468274--zero-day-disclosed-with-active-exploitation-and-no-vendor-patch-requires-emergency-compensating-control) | Zero-day disclosed with active exploitation and no vendor patch requires emergency compensating control | P1 | 6h 40m |
| 4 | [`INC0468619`](#inc0468619--trusted-vendor-software-update-confirmed-compromised-at-the-source-requiring-independent-internal-investigation) | Trusted vendor software update confirmed compromised at the source, requiring independent internal investigation | P1 | 2d 8h |
| 5 | [`INC0468955`](#inc0468955--insider-threat-investigation-requiring-coordination-with-hr-and-legal-and-formal-chain-of-custody) | Insider threat investigation requiring coordination with HR and Legal and formal chain of custody | P1 | 5d 2h |

---

<br>

## `INC0467588` — Single alert unravels into a multi-week advanced persistent threat requiring full kill-chain reconstruction

<table>
<tr><td><b>Environment</b></td><td>Enterprise multi-host environment, Microsoft Sentinel / Defender for Endpoint</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Security Incident Response > APT Investigation</td></tr>
<tr><td><b>Time to Resolve</b></td><td>4d 10h</td></tr>
</table>

**Reported Symptom**
A single detection — unusual outbound traffic from one server — was the visible tip of a presence that had been active in the environment for considerably longer than the alert itself suggested, requiring a full reconstruction of initial access, persistence, and lateral movement.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated the single alert as a starting thread, not a contained incident. Opened a full investigation predicated on the assumption that a single detected connection from a patient adversary likely represented a small visible fraction of a larger presence.
2. Established a forensically sound timeline from the first confirmed host. Captured memory and disk images from the initially alerting host following proper forensic acquisition procedures before any further action that could alter system state.
3. Reconstructed the initial access vector. Worked backward through process execution history, email logs, and the malicious document itself to identify the exact phishing email and vulnerability exploited.
4. Mapped persistence and lateral movement across every touched system. Identified the disguised scheduled task mechanism and traced authentication logs and endpoint telemetry to identify every additional host the harvested credentials had been used against.
5. Assessed what the adversary had actually accessed. Reviewed file access, data staging, and outbound transfer activity on each compromised host to determine specific impact and distinguish lateral-movement hosts from the likely actual objective.
6. Eradicated simultaneously and validated with active hunting. Removed every identified persistence mechanism and credential exposure across all compromised hosts at once, then conducted a dedicated threat-hunting sweep using the adversary's known TTPs to confirm no additional compromise existed.

</details>

**Root Cause**
The adversary gained initial access through a spear-phishing email exploiting an unpatched document-handling application, established persistence via a scheduled task disguised as system maintenance, harvested credentials from memory, and moved laterally to two additional systems over several weeks while operating below the pace that would trigger standard volumetric detections.

**Resolution**
Reviewed file access, data staging, and outbound transfer activity on each compromised host to determine specific impact and distinguish lateral-movement hosts from the likely actual objective. Removed every identified persistence mechanism and credential exposure across all compromised hosts at once, then conducted a dedicated threat-hunting sweep using the adversary's known TTPs to confirm no additional compromise existed.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0467931` — Active ransomware outbreak requires isolation, forensics, and recovery architecture decisions in real time

<table>
<tr><td><b>Environment</b></td><td>Multi-system production environment, active outbreak condition</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Security Incident Response > Ransomware Outbreak</td></tr>
<tr><td><b>Time to Resolve</b></td><td>1d 14h</td></tr>
</table>

**Reported Symptom**
Ransomware began encrypting files across multiple systems in a short window, still actively spreading at the moment of identification. Every decision in the opening minutes carried consequences for the entire recovery, including the tradeoff between isolation speed and forensic evidence preservation.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Made the isolation-versus-evidence tradeoff deliberately. Isolated affected systems at the network layer first rather than powering them off, cutting off spread while preserving volatile memory evidence needed to understand the ransomware's behavior.
2. Established incident command immediately. Assumed technical incident command, set a decision cadence for the fast-moving early hours, and established clear communication with executive leadership.
3. Captured forensic evidence before any recovery action. Acquired memory and disk images from a representative sample of affected systems across the observed spread pattern before any remediation touched them.
4. Identified the actual entry point and spread mechanism. Traced authentication logs from the remote access portal to the credential-stuffing pattern and confirmed the payload's rapid internal spread was enabled by the segment's broad trust.
5. Made an evidence-based recovery decision rather than paying the ransom. Confirmed backup integrity and recency, verified a viable uncompromised recovery path existed, and built the recovery plan around restoration.
6. Rebuilt the compromised access path before returning to full operation. Enforced MFA on the remote access portal without exception, revoked and reissued affected credentials, and implemented network segmentation between the previously overly trusted systems.

</details>

**Root Cause**
The ransomware entered through a compromised remote access credential obtained via credential stuffing against an externally facing portal lacking MFA, then deployed broadly across reachable systems on a network segment with unusually broad internal trust and minimal segmentation.

**Resolution**
Confirmed backup integrity and recency, verified a viable uncompromised recovery path existed, and built the recovery plan around restoration. Enforced MFA on the remote access portal without exception, revoked and reissued affected credentials, and implemented network segmentation between the previously overly trusted systems.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0468274` — Zero-day disclosed with active exploitation and no vendor patch requires emergency compensating control

<table>
<tr><td><b>Environment</b></td><td>Widely deployed enterprise application, actively exploited in the wild</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Security Incident Response > Zero-Day Response</td></tr>
<tr><td><b>Time to Resolve</b></td><td>6h 40m</td></tr>
</table>

**Reported Symptom**
Public disclosure of a zero-day vulnerability in a widely deployed application arrived with active exploitation already observed and no vendor patch available, requiring a real defensive answer within hours rather than a plan contingent on the vendor's timeline.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Assessed actual exposure before designing any control. Inventoried every instance of the affected application, confirmed which were reachable from untrusted networks, and prioritized those first.
2. Studied the published exploitation technique in detail. Reviewed available threat intelligence and proof-of-concept details to understand the precise malicious input pattern the attack depended on.
3. Designed a compensating control targeted at the technique, not the feature. Built and deployed a WAF rule and IPS signature matching the identified malicious input pattern, blocking the exploitation technique while leaving legitimate functionality intact.
4. Validated the control for both effectiveness and false positives. Tested the rule against a safe reproduction of the exploitation technique and against representative normal traffic to confirm no legitimate use was blocked.
5. Layered detection behind the control. Deployed a SIEM detection rule to alert on any traffic matching the exploitation pattern that reached the application despite the perimeter control.
6. Maintained the posture until the vendor patch was validated. Kept the compensating controls active and monitored throughout the disclosure window, applying the official patch through change management once available and validating it before removing the temporary controls.

</details>

**Root Cause**
The vulnerability existed in a core function that could not simply be disabled without breaking legitimate business use, and the exploitation technique depended on a specific, identifiable pattern of malicious input reaching that function.

**Resolution**
Deployed a SIEM detection rule to alert on any traffic matching the exploitation pattern that reached the application despite the perimeter control. Kept the compensating controls active and monitored throughout the disclosure window, applying the official patch through change management once available and validating it before removing the temporary controls.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0468619` — Trusted vendor software update confirmed compromised at the source, requiring independent internal investigation

<table>
<tr><td><b>Environment</b></td><td>Third-party software dependency, enterprise-wide deployment</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Security Incident Response > Supply-Chain Compromise</td></tr>
<tr><td><b>Time to Resolve</b></td><td>2d 8h</td></tr>
</table>

**Reported Symptom**
A routine software update delivered through a trusted vendor's normal, digitally signed update mechanism was later confirmed by the vendor and independent researchers to have been compromised at the source, embedding a malicious payload in an update customers had installed through completely normal channels.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated vendor notification as the start of an investigation, not the end. Began an independent internal investigation into every system running the affected software rather than relying solely on the vendor's own impact assessment.
2. Inventoried every affected instance and version. Compiled a complete inventory of systems running the software and cross-referenced installed versions against the vendor's disclosed compromised version list.
3. Hunted for the specific malicious behavior disclosed. Used published indicators of compromise to actively hunt for evidence the payload had actually executed, rather than assuming installation alone equated to compromise.
4. Assessed for second-stage compromise on confirmed-executed systems. Conducted deeper forensic review for credential harvesting, lateral movement, or data staging on any system where the payload was confirmed to have run.
5. Isolated and remediated confirmed-affected systems with full rigor. Applied the same evidence-preserving isolation and remediation process used for any confirmed compromise, regardless of the vendor-sourced origin.
6. Reassessed supply-chain risk governance as a direct outcome. Implemented additional verification steps for critical vendor updates before broad deployment and built a rapid-response inventory capability for future disclosures.

</details>

**Root Cause**
The compromise originated entirely in the vendor's own build and distribution pipeline, meaning standard defenses — signature verification, official channel-only updates — had functioned as designed and still failed, since the malicious code was signed with the vendor's own legitimate, compromised-at-source signing certificate.

**Resolution**
Applied the same evidence-preserving isolation and remediation process used for any confirmed compromise, regardless of the vendor-sourced origin. Implemented additional verification steps for critical vendor updates before broad deployment and built a rapid-response inventory capability for future disclosures.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0468955` — Insider threat investigation requiring coordination with HR and Legal and formal chain of custody

<table>
<tr><td><b>Environment</b></td><td>Cross-functional investigation (IT, HR, Legal), single named employee</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Security Incident Response > Insider Threat Investigation</td></tr>
<tr><td><b>Time to Resolve</b></td><td>5d 2h</td></tr>
</table>

**Reported Symptom**
A manager's tip, corroborated by a DLP alert, raised a credible concern that an employee with legitimate access to sensitive data might be preparing to take it upon an anticipated departure. Every technical step carried legal and human consequences from the outset.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Engaged HR and Legal before any investigative action. Looped in HR and Legal immediately to establish proper scope, ensure compliance with employment law, and agree on decision authority before any technical step was taken.
2. Established formal chain of custody from the first evidence collected. Documented every piece of evidence — access logs, DLP alerts, file access records — with a formal chain of custody from the moment of collection.
3. Conducted a scoped, proportionate technical review. Limited the review to the data access and transfer activity relevant to the concern, in direct coordination with Legal's guidance on appropriate scope.
4. Corroborated the DLP alert with independent evidence. Cross-referenced the original alert against independent authentication logs, file access records, and endpoint activity to build a factual, evidence-based picture.
5. Preserved evidence in a forensically sound, tamper-evident manner. Captured forensic images of assigned devices following proper legal procedure once HR and Legal authorized that step.
6. Supported the joint decision with a complete, factual record. Presented the complete, chain-of-custody-documented findings to HR and Legal without personal recommendation on employment consequences, keeping the technical and personnel decisions clearly separated.

</details>

**Root Cause**
The employee had, over several weeks, methodically accessed company data outside the normal scope of their role and transferred a subset to personal cloud storage and an external device, using access that was technically authorized at every step — a matter of judgment and apparent intent rather than any control failure.

**Resolution**
Captured forensic images of assigned devices following proper legal procedure once HR and Legal authorized that step. Presented the complete, chain-of-custody-documented findings to HR and Legal without personal recommendation on employment consequences, keeping the technical and personnel decisions clearly separated.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 5 |
| **Critical (P1) Incidents** | 5 |
| **Average Time to Resolve** | ~2d 18h |
| **Systems Touched** | Forensic Memory & Disk Imaging · Microsoft Sentinel & Defender for Endpoint · MITRE ATT&CK Framework Mapping · Endpoint & Authentication Log Timeline Reconstruction · Post-Incident Threat Hunting · Network-Layer Isolation · Incident Command Structure · Backup Integrity Assessment & Recovery Planning |

## Skills Demonstrated

`APT / Kill-Chain Reconstruction` · `Ransomware Outbreak Response` · `Zero-Day Compensating Controls` · `Supply-Chain Compromise Investigation` · `Insider Threat Investigation` · `Forensic Chain of Custody`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across advanced security incident response — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>