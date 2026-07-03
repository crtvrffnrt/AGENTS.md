# Controlled Lab Offensive Execution Profile

This file defines a deterministic, CLI-only offensive execution profile for controlled lab machines.

## Role
Use this profile to guide a skilled operator from initial reachability to full compromise using validated, reproducible attack paths. Focus on initial access, foothold establishment, and lab-scope execution.

## Scope Notes
- No blind brute force.
- No noisy repetition.
- No external writeups for the exact target.
- Add a hosts-file entry only when it is required by the target.

## Methodology
1. Initial recon and port discovery.
2. Targeted enumeration of discovered services.
3. Service-specific expansion and exploitation.
4. Initial foothold and shell access.
5. Privilege escalation research and execution.
6. Evidence preservation and consolidation.

## Deterministic Skill Router
Choose one owner skill for the current phase. The owner skill controls the next step and output shape. Add a supporting skill, cross-check, or reviewer only when it materially improves confidence, resolves ambiguity, or handles a phase transition.

### Step Router
1. Initial Recon and Port Discovery
   - Primary: `pentest-htb-lab-specialist` when installed; fallback `pentest-recon-surface-analysis`
   - Secondary: `pentest-web-application-logic-mapper`
2. Targeted Enumeration
   - Primary: `pentest-web-application-logic-mapper`
   - Secondary: `pentest-hacktricks-finder`
3. Service-Specific Expansion and Exploitation
   - Primary: `pentest-input-protocol-manipulation`
   - Secondary: `pentest-advanced-access-control-auditor`
4. Initial Foothold and Shell Access
   - Primary: `pentest-exploit-execution-payload-control`
   - Secondary: `pentest-outbound-interaction-oob-detection`
5. Privilege Escalation Research and Execution
   - Primary: `pentest-hacktricks-finder`
   - Secondary: `pentest-exploit-execution-payload-control`
6. Consolidation and Evidence Preservation
   - Primary: `pentest-evidence-structuring-report-synthesis`

## Core Rules
- No blind brute force and no noisy repetition.
- Prefer a single dominant entry vector.
- Use minimal, deterministic exploitation.
- Prefer reverse shells unless restricted.
- Output the exact path used, or the most promising path if no foothold exists yet.
- Use up to two controlled pivots per phase before returning to the main path or reporting the gap.

## Network and Listener Notes
- Keep outbound callback listeners on the port range `40000-50000`.
- Use a unique token per payload.
- Correlate callbacks by token, path, and timestamp.

## Evidence Standard
- Confirm only with concrete execution evidence.
- Record negative controls for high-impact findings.
- Do not claim callback-driven findings without deterministic correlation.

## Output Contract
1. Confirmed findings by severity and exploitability.
2. Chained attack paths and final impact.
3. Open hypotheses and next deterministic test.
4. Fix priorities mapped to broken trust boundaries.

## Results Persistence
Persist run outcomes in:
- `./results/Results-lab.md`

## Environment Notes
- This profile should remain stable and evolve by additive, explicit deltas rather than frequent rewrites.
