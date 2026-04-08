# AGENTS.md

A curated collection of reusable agent instruction files for offensive security, defensive security, API assessment, OSINT, web testing, cloud investigations, exploit development, and task-specific operator workflows.

These files are intended to be dropped into an AI-assisted workflow as high-signal operating profiles. Each file defines a concrete role, execution model, scope, routing logic, and output expectations for a specific type of work.

## What This Repository Contains

This repository currently contains agent profiles such as:

- `GEMINI-CORE.md`: general-purpose offensive security core profile.
- `GEMINI-CORE-RED.md`: red-team and penetration-testing core profile.
- `GEMINI-CORE-BLUE.md`: blue-team, incident response, and defensive investigation profile.
- `GEMINI-API.md`: offensive API security assessment profile.
- `GEMINI-WEB.md`: web application penetration testing profile.
- `GEMINI-SUB-RECON.md`: passive reconnaissance and OSINT specialist.
- `GEMINI-SUB-HTB.md`: Hack The Box execution profile.
- `GEMINI-SUB-EXPLOIT.md`: exploit development and controlled impact proof profile.
- `GEMINI-SUB-BUG.md`: bug bounty workflow profile.
- `GEMINI-entra.md`: Entra ID and entitlement-management analysis profile.
- `GEMINI-Aisupercycle.md`: AI market and infrastructure intelligence profile.

The intent is not to provide generic prompting text. The intent is to provide repeatable agent operating instructions that shape behavior in a predictable way for specific tasks.

## What These Agents Do

These agents act as operational instruction sets for AI tools. Depending on the selected file, they can:

- constrain the model to a defined mission and scope.
- enforce a specific investigation or exploitation workflow.
- define guardrails and allowed execution style.
- route work toward specialized skills or task categories.
- standardize terminology, evidence handling, and final output.
- reduce prompt drift during long-running technical work.

In practice, this means you select the profile that matches the task and give it to your AI tooling as the active instruction layer.

## How To Use The Agents

### 1. Pick the correct profile
Choose the file that matches the work you want to perform.

Examples:

- Use `GEMINI-CORE-RED.md` for authorized offensive assessments.
- Use `GEMINI-CORE-BLUE.md` for SOC triage, IR, and defensive analysis.
- Use `GEMINI-API.md` for API-centric testing.
- Use `GEMINI-WEB.md` for web application testing.
- Use `GEMINI-SUB-RECON.md` when you want passive-only reconnaissance.
- Use `GEMINI-SUB-EXPLOIT.md` when you need exploit implementation rather than high-level analysis.

### 2. Load the file as the active instruction set
There are several ways to do this depending on the tooling:

- paste the file contents into the system or instruction prompt.
- reference the file from a local workflow that injects instructions automatically.
- copy or adapt the selected file into a repository-local `AGENTS.md` file.

### 3. Add task-specific context
The agent file defines the operating model, but you still need to provide the actual task context, for example:

- target or application scope.
- explicit safety constraints.
- credentials, cookies, request samples, or telemetry.
- the output format you want.

### 4. Run the task under that profile
Once the instruction file is active, use the model normally. The selected profile should influence how the tool reasons, what it prioritizes, and how it structures output.

## Using These Agents With Codex

These profiles can be used with tools such as Codex.

A practical approach is to place the content of the selected profile into a file named `AGENTS.md` at the root of the repository or working directory where you want Codex to operate. Codex reads repository-level instruction files and uses them as part of its operating context.

That means you can take a profile from this repository, for example `GEMINI-WEB.md` or `GEMINI-CORE-BLUE.md`, copy the relevant content into `AGENTS.md`, and then run Codex in that directory. The instructions in `AGENTS.md` become the local behavior contract for the session.

Typical Codex workflow:

1. Choose the agent profile that matches the task.
2. Copy that profile into `AGENTS.md` in the target repository.
3. Add any local project-specific instructions that should also apply.
4. Start Codex in that directory.
5. Give Codex the concrete task, scope, and artifacts.

This pattern is useful when you want Codex to consistently behave as a red-team operator, a blue-team analyst, an API tester, a web tester, or another specialist defined in this repository.

## Example Usage Pattern

### Example: Web application assessment with Codex

1. Open `GEMINI-WEB.md`.
2. Copy its contents into `AGENTS.md` in your target project directory.
3. Add any local target notes such as URLs, exclusions, or auth material.
4. Launch Codex from that directory.
5. Provide the concrete assessment objective.

### Example: Incident response workflow with Codex

1. Open `GEMINI-CORE-BLUE.md`.
2. Write or merge its contents into `AGENTS.md` in the investigation workspace.
3. Add local constraints such as the tenant, timeframe, or available telemetry.
4. Launch Codex and assign the IR task.

## Recommended Operating Model

For best results:

- use one primary profile per task or phase.
- switch profiles when the mission changes materially.
- keep the profile stable during a single workstream to reduce behavioral drift.
- add local facts separately rather than modifying the core role definition every time.
- preserve the original files in this repository as reusable templates.

## Why `AGENTS.md` Matters

`AGENTS.md` provides a simple, repository-local way to express how an AI coding or analysis assistant should behave inside that workspace. Instead of re-explaining the same operating model on every run, you define it once in `AGENTS.md` and let the tool inherit it automatically.

This repository is therefore both:

- a library of specialist agent profiles.
- a source of reusable content that can be written into `AGENTS.md` for tools such as Codex.

## Intended Audience

This repository is built for practitioners who want deterministic, role-specific AI behavior rather than generic assistant responses, including:

- penetration testers
- red-team operators
- incident responders
- SOC analysts
- cloud security engineers
- API security testers
- security researchers

## Notes

These files should be adapted to your environment, authorization model, and operational constraints. They are strongest when used as a controlled starting point and then refined for the exact engagement or workflow.
