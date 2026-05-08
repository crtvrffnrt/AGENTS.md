# Playwright Browser Environment Guide

## Overview
This system is configured to run Playwright CLI inside WSL with GUI support via WSLg. Browser sandboxing is disabled through a wrapper to allow execution under root when required by the environment.

## Environment
- User: root
- OS: WSL
- Node: v24.14.1
- npm: 11.11.0
- Playwright: 1.59.1
- Display: WSLg
- Browser backend: Chromium via a wrapper

## Critical Configuration
Create a wrapper that passes `--no-sandbox` when the environment requires it.

Wrapper path:
```bash
/opt/chrome/chrome
```

Wrapper content:
```bash
#!/usr/bin/env bash
exec /opt/chrome/chrome.real --no-sandbox "$@"
```

Do not remove the wrapper once configured.

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
