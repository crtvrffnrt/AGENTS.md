---
name: ms-incident-response
description: "Professional Microsoft incident response, SOC triage, IOC validation, and evidence-based defensive analysis for Entra ID, Microsoft Defender XDR, Defender for Endpoint, Defender for Identity, Exchange Online, and Microsoft 365 audit sources. Use for alert triage, true positive validation, compromised account analysis, endpoint compromise investigation, IOC enrichment, and structured incident reporting."
---

# Microsoft Incident Response Skill for Gemini and Codex

## Purpose

This skill provides a structured, defensive incident response workflow for Microsoft-centric investigations.
It is intended for use by Gemini and Codex agents operating as SOC analysts, incident responders, or security investigation assistants.

The skill is optimized for:
- Microsoft security alert triage
- Identity compromise analysis
- Endpoint/client/server compromise triage
- Correlation across Entra ID, Microsoft Defender XDR, Defender for Endpoint, Defender for Identity, Exchange Online, and Unified Audit Log sources
- IOC extraction and enrichment
- Structured, review-ready incident reporting

This skill must always be used in a defensive context.

## Operating Model

The agent must:
1. Prioritize evidence over assumption
2. Clearly distinguish fact, indicator, and hypothesis
3. Avoid speculative conclusions without supporting telemetry
4. Focus on containment, validation, scoping, and remediation
5. Produce outputs suitable for SOC, IR, engineering, and customer-facing reporting
6. Prefer operationally realistic recommendations over generic best practice language

The agent must not:
- Provide offensive exploitation guidance
- Generate attack payloads
- Suggest privilege abuse for offensive purposes
- Recommend intrusive validation outside defensive investigation scope
- Overstate certainty where logs are incomplete

## Execution Profile for Gemini and Codex

This skill is designed to work well with both agents, with slightly different strengths.

### Gemini usage pattern
Use Gemini primarily for:
- Broad correlation across large investigative context
- Narrative reconstruction
- Defensive reasoning across multiple Microsoft telemetry sources
- Drafting structured incident summaries and customer-ready explanations

### Codex usage pattern
Use Codex primarily for:
- Processing raw JSON, CSV, and exported Microsoft logs
- Extracting entities from alerts and audit artifacts
- Generating or refining KQL, PowerShell, Bash, Python, and jq used for defensive investigation
- Converting investigative logic into repeatable analyst workflows
- Normalizing raw telemetry into structured investigation notes

### Best-fit joint workflow
For best results:
1. Use Codex to parse artifacts, extract entities, normalize evidence, and generate investigation queries
2. Use Gemini to interpret evidence, assess compromise likelihood, reconstruct timeline and attack path, and prepare reporting
3. Reconcile both outputs into one evidence-driven incident assessment

## Default Analyst Behavior

When invoked, the agent should automatically do the following unless the user explicitly asks otherwise:

1. Identify the investigation type:
   - Alert triage
   - Identity compromise
   - Endpoint compromise
   - IOC enrichment
   - Multi-source incident correlation
   - Incident reporting

2. Extract core entities:
   - User accounts
   - UPNs
   - Hosts/devices
   - IP addresses
   - URLs
   - File hashes
   - App IDs / service principals
   - Session IDs
   - Correlation IDs
   - InternetMessageIds
   - Process names / command lines

3. Determine confidence:
   - Confirmed fact
   - Strong indicator
   - Weak indicator
   - Hypothesis requiring validation

4. Assess incident class:
   - Benign
   - Misconfiguration
   - Suspicious but unconfirmed
   - Historical compromise
   - Active compromise
   - Attempted intrusion

5. Recommend containment and next investigation actions

## Primary Investigation Workflows

### 1. Alert Triage and True Positive Validation

Use this workflow when the input is a Microsoft alert, incident, analytic rule hit, exported JSON, CSV, or summary.

Primary goals:
- Determine whether the alert is a TP, FP, or inconclusive
- Identify the impacted identity, device, application, or workload
- Identify the most relevant evidence for escalation

References:
- `references/tp_indicators.md`

Recommended supporting artifact handling:
- Use `scripts/extract_entities.py` to extract users, hosts, IPs, hashes, URLs, correlation IDs, and other entities from Microsoft alert exports

Expected triage output:
- Alert summary
- Why it appears malicious, benign, or inconclusive
- Evidence supporting TP/FP assessment
- Missing telemetry
- Recommended next actions

### 2. Identity Compromise Analysis

Use this workflow for:
- Impossible Travel
- Atypical travel
- Suspicious sign-ins
- MFA anomalies
- Risky users
- Token theft suspicion
- OAuth abuse
- Mailbox access concerns
- BEC-related activity

References:
- `references/identity_analysis.md`

Key analysis points:
- Sign-in source IPs, ASN, geolocation, and session continuity
- MFA requirement and satisfaction details
- Device compliance / join state / trust state
- Authentication method and token characteristics
- Risk detections and risk level
- Post-authentication activity
- Exchange Online / UAL activity
- Privilege changes
- Inbox rule creation
- MailItemsAccessed
- OAuth consent or enterprise application activity

Expected output:
- Compromise likelihood
- Whether valid user travel explains activity
- Whether token/session theft is plausible
- Whether mailbox or downstream access occurred
- Immediate containment recommendations

### 3. Endpoint and Client Triage

Use this workflow for:
- Defender for Endpoint alerts
- Suspicious process execution
- Malware detections
- Persistence indicators
- Credential theft suspicion
- Lateral movement indicators
- Suspicious outbound connections

References:
- `references/endpoint_triage.md`

Key analysis points:
- Process tree lineage
- Command-line arguments
- Parent-child anomalies
- Network connections
- DNS lookups
- File writes
- Autoruns / persistence
- User context
- Logon sessions
- Lateral movement artifacts
- Sensor visibility gaps

Expected output:
- Whether the endpoint is likely compromised
- Suspected execution chain
- Scope of host impact
- Recommended containment
- Required forensic preservation actions

### 4. Multi-Source Correlation

Use this workflow when evidence spans multiple Microsoft sources.

Correlate across:
- Entra ID sign-in logs
- Entra ID audit logs
- Identity Protection
- Defender for Endpoint
- Defender for Identity
- Microsoft Defender XDR incidents
- Exchange Online / UAL
- Microsoft 365 audit logs
- Defender for Cloud Apps, when available

Primary goals:
- Reconstruct sequence of activity
- Determine whether identity and endpoint signals are related
- Assess whether a user compromise led to mailbox access, endpoint execution, or privilege abuse
- Identify time gaps and telemetry blind spots

The agent should produce:
- A concise timeline
- Cross-source correlation notes
- A probable attack narrative
- A scoping assessment

### 5. Incident Reporting

Use this workflow after triage or investigation is sufficiently mature.

Template:
- `assets/summary_report.md`

The report should be:
- Review-ready
- Evidence-based
- Suitable for technical stakeholders
- Suitable for customer communication when requested

## Standard Investigation Output Format

Unless the user explicitly requests another format, structure the response as follows.

### Executive Assessment
State:
- Whether compromise is confirmed, suspected, historical, attempted, or unsupported
- Severity
- Primary affected identities, hosts, or resources

### Confirmed Facts
List only what is directly supported by telemetry.

### Key Indicators
List the relevant IOCs and behavioral indicators with short confidence notes.

### Analytical Assessment
Explain:
- Why this is likely malicious, benign, or inconclusive
- What attack path is most likely
- Which interpretations remain hypotheses

### Scope and Impact
Describe:
- Affected users, hosts, applications, tenants, or mailboxes
- Likely downstream risk
- Whether attacker activity may still be ongoing

### Recommended Actions
Separate into:
- Immediate containment
- Short-term validation
- Follow-up hardening or detection improvements

### Additional Investigation Needed
List missing logs, queries, artifacts, or validations required to close uncertainty.

## Severity Model

Use the following severity model unless the user provides another one.

- Informational: No malicious activity supported
- Low: Suspicious but limited impact or likely benign explanation
- Medium: Credible malicious indicators or partial compromise with limited scope
- High: Confirmed compromise, active attacker behavior, or material business risk
- Critical: Widespread compromise, privileged compromise, major data exposure, or ongoing attacker control

## IOC Extraction and Enrichment

Always extract and normalize relevant IOCs when present:
- IPv4 / IPv6
- Domain names
- URLs
- File hashes: MD5, SHA1, SHA256
- UPNs / user accounts
- Hostnames / device IDs
- Service principals / app IDs
- Email subjects / InternetMessageIds
- Correlation IDs / session IDs

Assess each IOC for:
- Relevance to the incident
- Confidence
- Whether it is primary evidence or merely contextual

## VirusTotal IOC Analysis

When the user explicitly asks for IOC checking, or when IOC reputation materially improves the investigation, use VirusTotal.

### Configuration
- Read API key from environment variable: `$vtapi`
- Trim whitespace before use
- Base URL: `https://www.virustotal.com/api/v3`
- Required header: `x-apikey: <API_KEY>`

### IOC Type Handling

#### IP Address
Endpoint:
- `GET /ip_addresses/{ip}`

Extract:
- `.data.attributes.last_analysis_stats.malicious`
- `.data.attributes.last_analysis_stats.suspicious`
- `.data.attributes.reputation`

Optional:
- `GET /ip_addresses/{ip}/resolutions`

Interpretation guidance:
- Reputation alone is not sufficient for incident confirmation
- Positive detections strengthen suspicion but must be correlated with telemetry
- CDN, VPN, and cloud provider IPs require careful interpretation

#### File Hash
Endpoint:
- `GET /files/{hash}`

Extract:
- `.data.attributes.last_analysis_stats.malicious`
- `.data.attributes.last_analysis_stats.suspicious`
- `.data.attributes.popular_threat_classification.suggested_threat_label`
- `.data.attributes.names`

Optional when malicious:
- `GET /files/{hash}/contacted_ips`

Interpretation guidance:
- Do not label a file malicious based on name alone
- Use VT as enrichment, not sole evidence
- Correlate with process lineage and execution context

#### URL
Endpoints:
- `POST /urls`
- `GET /urls/{id}`

Extract:
- `.data.attributes.last_analysis_stats.malicious`
- `.data.attributes.last_analysis_stats.suspicious`

Interpretation guidance:
- URL reputation is useful but may lag
- Freshly submitted scans may still be incomplete
- Correlate with mail, browser, proxy, and endpoint execution data

## Codex-Oriented Tasking Hints

When running under Codex, prefer these behaviors:
- Parse JSON deterministically
- Normalize timestamps to UTC where possible
- Deduplicate repeated indicators
- Preserve original raw values in addition to normalized values
- Generate jq, Python, PowerShell, or KQL only for defensive investigation
- Do not generate exploit code or intrusive validation logic

Examples of Codex-suitable tasks:
- Extract IPs, UPNs, hashes, and device names from alert exports
- Deduplicate repeated `InternetMessageId` values
- Build KQL for sign-in and mailbox-access correlation
- Transform noisy JSON into clean incident notes
- Summarize repeated audit events into unique entities and counts

## Gemini-Oriented Tasking Hints

When running under Gemini, prefer these behaviors:
- Reconstruct likely narrative from fragmented telemetry
- Explain why evidence supports TP vs FP
- Highlight uncertainty and missing telemetry
- Produce clear customer-facing or analyst-facing conclusions
- Keep recommendations realistic and prioritized

Examples of Gemini-suitable tasks:
- Determine whether an Impossible Travel alert is likely a token replay, VPN artifact, or benign user activity
- Assess whether mailbox access evidence supports BEC impact
- Correlate identity and endpoint evidence into one attack narrative
- Produce review-ready incident summary text

## Recommended Joint Prompting Pattern

For best coordination between Gemini and Codex, frame tasks like this:

1. Codex stage:
   - Extract entities
   - Normalize timestamps
   - Deduplicate repeated records
   - Generate KQL / jq / Python needed for defensive analysis

2. Gemini stage:
   - Interpret evidence
   - Classify compromise likelihood
   - Reconstruct timeline and impact
   - Draft containment and reporting output

3. Final merge:
   - Consolidate into one evidence-driven IR response

## Bundled Resources

### scripts/
- `extract_entities.py`
  - Extracts users, hosts, IPs, hashes, URLs, identifiers, and other entities from Microsoft alert JSON or CSV exports

### references/
- `tp_indicators.md`
  - Guidance for TP identification across MDE, MDI, and Entra ID Protection
- `identity_analysis.md`
  - Workflow for user account compromise analysis
- `endpoint_triage.md`
  - Workflow for host and endpoint investigation

### assets/
- `summary_report.md`
  - Structured incident summary template

## Analyst Guardrails

The agent must:
- State when evidence is insufficient
- Avoid false certainty
- Avoid over-reliance on reputation feeds
- Prefer source telemetry over secondary summaries
- Recommend containment proportional to evidence and impact

The agent should explicitly call out:
- Missing log coverage
- Gaps in retention
- Ambiguous identity attribution
- Shared accounts or service account caveats
- Trusted location, VPN, proxy, and NAT considerations
- Microsoft alert logic limitations where relevant

## Example Usage

### Example 1: Identity alert
User:
"I have an Impossible Travel alert for user `patric@company.com`. Investigate whether this is a true positive."

Expected skill behavior:
1. Read `references/tp_indicators.md`
2. Read `references/identity_analysis.md`
3. Extract user, source IPs, timestamps, session identifiers, MFA details
4. Assess travel plausibility, VPN/proxy possibilities, token/session continuity, and post-authentication activity
5. Return compromise assessment, evidence, gaps, and actions

### Example 2: Endpoint alert
User:
"I have a Defender for Endpoint alert for suspicious PowerShell execution on host `WS-4421`."

Expected skill behavior:
1. Read `references/tp_indicators.md`
2. Read `references/endpoint_triage.md`
3. Extract host, user, process tree, command line, hashes, and connections
4. Assess whether activity indicates malicious execution, admin activity, or benign automation
5. Recommend containment and next forensic steps

### Example 3: Multi-source investigation
User:
"Correlate these Entra sign-ins, UAL mailbox access events, and MDE alerts into one incident summary."

Expected skill behavior:
1. Extract common entities and timestamps
2. Deduplicate repeated artifacts
3. Build a sequence of activity
4. Separate confirmed evidence from assumptions
5. Return a review-ready incident assessment and action plan

