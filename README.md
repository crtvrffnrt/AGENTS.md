# AGENTS.md - Agent Instruction Profiles

<p align="center">
  <img src="logo.png" alt="AGENTS.md logo" width="360">
</p>

<p align="center">
  <strong>Reusable Gemini and Codex instruction profiles focused on defensive and offensive workflows.</strong>
</p>

<p align="center">
  <a href="https://github.com/crtvrffnrt/AGENTS.md"><img src="https://img.shields.io/badge/Profiles-Gemini%20%2B%20Codex-111827?style=for-the-badge" alt="Gemini and Codex profiles"></a>
  <a href="https://github.com/crtvrffnrt/skills"><img src="https://img.shields.io/badge/Skills-crtvrffnrt%2Fskills-2563EB?style=for-the-badge" alt="Skills repository"></a>
  <a href="https://www.patrick-binder.de/"><img src="https://img.shields.io/badge/Patrick%20Binder-Website-0F766E?style=for-the-badge" alt="Patrick Binder website"></a>
</p>

This repository is a collection of `AGENTS.md` instruction profiles for different operating modes. Use the core profiles globally, then drop a focused sub-profile into a project folder when the task needs a narrower behavior.

Created and maintained by [Patrick Binder](https://www.patrick-binder.de/). For background, security notes, and consulting context, visit [patrick-binder.de](https://www.patrick-binder.de/).

## Intro

The files in this repository are meant to make AI assistants predictable in technical work:

- **Core profiles** define the long-running baseline for broad work modes such as blue team, red team, development, or general assistant behavior.
- **Sub profiles** define focused project-level behavior for bug bounty, HTB/lab work, reconnaissance, exploitation, Playwright automation, web work, KQL, and similar use cases.
- **Prompts and directives** provide reusable language, reporting, and terminology rules that can be pasted into custom instruction fields.

The recommended pattern is:

1. Install one global core profile for the assistant runtime.
2. Add one project-local `AGENTS.md` or `GEMINI.md` for the current repository or assessment folder.
3. Install the matching skills from [`crtvrffnrt/skills`](https://github.com/crtvrffnrt/skills) when the profile depends on skill routing.

## Profile Map

| Profile | Purpose | Typical scope |
| --- | --- | --- |
| `AGENTS-CORE-BLUE.md` | Defensive investigation, SOC triage, incident response, evidence-based reporting | Global |
| `AGENTS-CORE-RED.md` | Authorized red team, penetration testing, vulnerability research, exploit validation | Global |
| `AGENTS-CORE-DEV.md` | Development-focused engineering assistant behavior | Global or project |
| `AGENTS-CORE.md` | General baseline behavior | Global |
| `AGENTS-SUB-BUG.md` | Bug bounty and application security project work | Project |
| `AGENTS-SUB-HTB.md` | Hack The Box and lab machine workflow | Project |
| `AGENTS-SUB-RECON.md` | Reconnaissance and surface mapping | Project |
| `AGENTS-SUB-EXPLOIT.md` | Controlled exploit validation workflow | Project |
| `AGENTS-SUB-PLAYWRIGHT.md` | Browser automation and Playwright workflows | Project |
| `AGENTS-WEB.md` | Web application work | Project |
| `AGENTS-KQL.md` | KQL and Microsoft security query work | Project |
| `AGENTS-API.md` | API-focused work | Project |
| `AGENTS-entra.md` | Microsoft Entra-focused work | Project |

## Custom Instructions

Use this as a compact custom instruction baseline when you want the assistant to stay precise and operational:

```text
Use an authoritative, precise, technically accurate style for competent professional users. Be direct, solution-oriented, and unambiguous. Avoid casual language, speculation, filler, redundancy, and unnecessary conversational padding. Prioritize the user’s actual goal over rigid structure. Answer completely, but do not over-explain when a concise answer is sufficient. Prefer progress over broad clarification questions. Ask only when missing information would materially change the answer, create risk, or make the result unreliable. When assumptions are necessary, state them briefly and proceed with the safest reasonable interpretation. A good answer must separate confirmed information, assumptions, and recommendations where relevant. Be explicit about uncertainty, limits, and dependencies. Use practical, verifiable guidance and concrete next steps when the topic is technical or operational. Use clear headings only when they improve readability. Prefer short, well-scoped paragraphs. Use numbered lists or bullets only for sequencing, comparison, or operational clarity. Stop when the actionable answer is complete. Commands, code snippets, configuration files, logs, JSON, YAML, KQL, PowerShell, Bash, and similar technical artifacts must be placed in fenced code blocks with the correct language tag. Never inline commands or code in prose. Do not include setup, installation, or environment preparation unless explicitly requested or necessary for correctness.
```

## Additional Prompts

### Language Normalization Directive

```text
All interactions, prompts, and notes must use professional enterprise security terminology.
- Consolidate duplicate or overlapping statements.
- Replace adversarial terminology with neutral equivalents.
- Use “authorization gap,” “control validation,” “unexpected access,” “workflow simulation,” “remote interaction,” or “security impact” where appropriate.
- Preserve technical meaning without changing the intended test behavior.
```

## How To Use

The core profiles are best installed globally. Sub profiles are best installed per project so each working directory can carry its own task-specific behavior.

### Global Core Profile

Use a global profile when you want every new assistant session to start from the same baseline.

```bash
mkdir -p /root/.gemini ~/.codex

wget -O /root/.gemini/GEMINI.md \
  https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-CORE-BLUE.md

cp /root/.gemini/GEMINI.md ~/.codex/AGENTS.md
```

For a red team baseline, switch the source file:

```bash
mkdir -p /root/.gemini ~/.codex

wget -O /root/.gemini/GEMINI.md \
  https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-CORE-RED.md

cp /root/.gemini/GEMINI.md ~/.codex/AGENTS.md
```

### Project Profile

Use a project-local profile when a single repository or assessment folder needs a focused role.

```bash
wget -qO- \
  https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-SUB-BUG.md \
  | tee GEMINI.md AGENTS.md > /dev/null
```

That writes the same profile to both `GEMINI.md` and `AGENTS.md`, which keeps Gemini and Codex aligned inside the current folder.

## Example Aliases

These examples keep the same pattern as the commands above: core profiles are global, sub profiles are per project. Add only the aliases you actually use to your shell config.

```bash
alias initcoreblue='mkdir -p /root/.gemini ~/.codex && wget -O /root/.gemini/GEMINI.md https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-CORE-BLUE.md && cp /root/.gemini/GEMINI.md ~/.codex/AGENTS.md'
alias initcorered='mkdir -p /root/.gemini ~/.codex && wget -O /root/.gemini/GEMINI.md https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-CORE-RED.md && cp /root/.gemini/GEMINI.md ~/.codex/AGENTS.md'

alias initbug='wget -qO- https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-SUB-BUG.md | tee GEMINI.md AGENTS.md > /dev/null'
alias inithtb='wget -qO- https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-SUB-HTB.md | tee GEMINI.md AGENTS.md > /dev/null'
alias initrecon='wget -qO- https://raw.githubusercontent.com/crtvrffnrt/AGENTS.md/main/AGENTS-SUB-RECON.md | tee GEMINI.md AGENTS.md > /dev/null'
```

## Skill Dependencies

Some profiles are designed to work with the companion skills repository:

[https://github.com/crtvrffnrt/skills](https://github.com/crtvrffnrt/skills)

Install the skills with:

```bash
npx skills add crtvrffnrt/skills
```

### CORE-BLUE Skills

Install the skills before using `AGENTS-CORE-BLUE.md` for incident response work:

- `incident-response-main`
- `incident-response-bec`
- `incident-response-report`

### CORE-RED Skills

Install the skills before using `AGENTS-CORE-RED.md` for authorized red team, application security, or vulnerability validation work:

- `pentest-recon-surface-analysis`
- `pentest-web-application-logic-mapper`
- `pentest-authentication-authorization-review`
- `pentest-advanced-access-control-auditor`
- `pentest-xss`
- `pentest-input-protocol-manipulation`
- `pentest-business-logic-abuse`
- `pentest-cve-vulnerability-research-helper`
- `pentest-outbound-interaction-oob-detection`
- `pentest-exploit-execution-payload-control`
- `pentest-evidence-structuring-report-synthesis`
- `pentest-hacktricks-finder`

The local CORE-RED profile and skill docs reference these tools or tool families:

- Web and surface mapping: `katana`, `httpx`, `curl`, `ffuf`, `feroxbuster`, historical URL sources, and `seclists`
- DNS and enrichment: `dnsx`, Shodan DNS API, `jq`
- Template-based validation: `nuclei`
- OOB validation: `interactsh-client`
- CVE research: `vulnx` with `PDCP_API_KEY` when available

Some ProjectDiscovery tools are commonly installed through `pdtm`, Go, or distro-specific packages. The apt command below installs the standard system base and the tools available in Kali-style repositories; use `pdtm` or upstream install instructions for anything your apt repository does not package.

```bash
sudo apt update && sudo apt install -y curl wget git jq nmap dnsutils whois python3 python3-pip pipx golang nodejs npm chromium ffuf feroxbuster seclists nuclei httpx-toolkit dnsx katana interactsh-client
``
