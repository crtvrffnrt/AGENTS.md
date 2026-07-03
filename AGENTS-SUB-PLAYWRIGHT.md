# Playwright Browser Environment Guide

## Overview
Use this profile for browser automation and visual or DOM validation with Playwright-compatible tooling. Prefer the runtime's available Playwright tool first; use the local CLI notes below only when they match the current machine.

## Local Environment Notes
- Some workstations run Playwright CLI inside WSL with GUI support via WSLg.
- Some root-based WSL environments require Chromium sandboxing to be disabled through a wrapper.
- Treat `/opt/chrome`, `/tmp/playwright_*`, and `.playwright-cli/` as local conventions, not portable requirements.
- Check tool availability before relying on `playwright-cli`.

## Conditional Wrapper Configuration
Create a wrapper that passes `--no-sandbox` only when the current environment requires it.

Wrapper path:
```bash
/opt/chrome/chrome
```

Wrapper content:
```bash
#!/usr/bin/env bash
exec /opt/chrome/chrome.real --no-sandbox "$@"
```

Do not change an existing wrapper unless the current Playwright run is blocked by a sandbox error.

## Core Commands
Open browser:
```bash
playwright-cli open https://example.com --browser chrome --headed
```

Navigate:
```bash
playwright-cli goto https://target
```

Snapshot DOM:
```bash
playwright-cli snapshot
```

Click and fill:
```bash
playwright-cli click "Submit"
playwright-cli fill "input[name=q]" "test"
```

Keyboard:
```bash
playwright-cli press Enter
```

## Debugging
Console logs:
```bash
playwright-cli console
```

Network:
```bash
playwright-cli network
```

Screenshot:
```bash
playwright-cli screenshot
```

PDF:
```bash
playwright-cli pdf
```

## Storage Inspection
```bash
playwright-cli cookie-list
playwright-cli localstorage-list
playwright-cli sessionstorage-list
```

Persist session:
```bash
playwright-cli state-save /tmp/state.json
playwright-cli state-load /tmp/state.json
```

## Session Management
```bash
playwright-cli list
playwright-cli close
playwright-cli close-all
playwright-cli kill-all
```

## Network Testing
Offline mode:
```bash
playwright-cli network-state-set offline
```

Restore:
```bash
playwright-cli network-state-set online
```

Mock routes:
```bash
playwright-cli route "**/api/**"
```

## JavaScript Execution
```bash
playwright-cli eval "document.title"
playwright-cli eval "document.cookie"
playwright-cli eval "localStorage"
```

## Tabs
```bash
playwright-cli tab-new https://example.com
playwright-cli tab-list
playwright-cli tab-select 0
playwright-cli tab-close 0
```

## Artifacts
- Snapshots: `.playwright-cli/*.yml`
- Console logs: `.playwright-cli/*.log`
- Profiles: `/tmp/playwright_*`
- Cache: `~/.cache/ms-playwright`

## Validation
```bash
playwright-cli open https://example.com --browser chrome --headed --json
```

Expected: JSON with session and snapshot path.

## Troubleshooting
If a sandbox error appears, recreate the wrapper:
```bash
playwright-cli kill-all || true

mv /opt/chrome/chrome /opt/chrome/chrome.real 2>/dev/null || true

cat > /opt/chrome/chrome << 'EOF'
#!/usr/bin/env bash
exec /opt/chrome/chrome.real --no-sandbox "$@"
EOF

chmod +x /opt/chrome/chrome
```

## Security Note
- Keep the wrapper limited to the current machine and workflow.
- Do not submit credentials, modify production data, or interact outside the authorized target during browser automation.
- If the expected Playwright tool is missing, report the gap and use screenshots, static HTML, curl, or other available evidence where safe.
