# Playwright WSL Root Environment Guide

## Overview

This system is configured to run Playwright CLI inside WSL as root with GUI support via WSLg. 
Chrome/Chromium sandboxing is disabled through a wrapper to allow execution under root.

---

## Environment

- User: root
- OS: WSL (Kali/Debian-based)
- Node: v24.14.1
- npm: 11.11.0
- Playwright: 1.59.1
- Display: WSLg (Wayland/X11 bridge)
- Browser backend: Chromium via Chrome wrapper

---

## Critical Configuration

Chrome is wrapped to bypass sandbox restrictions:

```bash
/opt/google/chrome/chrome
```

Wrapper content:

```bash
#!/usr/bin/env bash
exec /opt/google/chrome/chrome.real --no-sandbox "$@"
```

Do NOT remove this wrapper.

---

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

Click / Fill:

```bash
playwright-cli click "Submit"
playwright-cli fill "input[name=q]" "test"
```

Keyboard:

```bash
playwright-cli press Enter
```

---

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

---

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

---

## Session Management

```bash
playwright-cli list
playwright-cli close
playwright-cli close-all
playwright-cli kill-all
```

---

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

---

## JavaScript Execution

```bash
playwright-cli eval "document.title"
playwright-cli eval "document.cookie"
playwright-cli eval "localStorage"
```

---

## Tabs

```bash
playwright-cli tab-new https://example.com
playwright-cli tab-list
playwright-cli tab-select 0
playwright-cli tab-close 0
```

---

## Artifacts

- Snapshots: `.playwright-cli/*.yml`
- Console logs: `.playwright-cli/*.log`
- Profiles: `/tmp/playwright_*`
- Cache: `~/.cache/ms-playwright`

---

## Validation

```bash
playwright-cli open https://example.com --browser chrome --headed --json
```

Expected: JSON with session + snapshot path.

---

## Troubleshooting

If sandbox error appears:

```bash
Running as root without --no-sandbox is not supported
```

Recreate wrapper:

```bash
playwright-cli kill-all || true

mv /opt/google/chrome/chrome /opt/google/chrome/chrome.real 2>/dev/null || true

cat > /opt/google/chrome/chrome << 'EOF'
#!/usr/bin/env bash
exec /opt/google/chrome/chrome.real --no-sandbox "$@"
EOF

chmod +x /opt/google/chrome/chrome
```

---

## Security Note

Browser runs WITHOUT sandbox.

Implications:
- No isolation
- Do not use for personal browsing
- Use ephemeral sessions
- Clear state after use

```bash
playwright-cli delete-data
```

---

## Agent Rules

Agents must:

1. Always use `--headed` for visible debugging
2. Call `snapshot` before interaction
3. Use semantic selectors
4. Inspect `console` and `network`
5. Avoid reinstalling Playwright
6. Preserve Chrome wrapper
7. Kill stale sessions before retry
8. Treat browser as non-isolated
9. Prefer Chromium via wrapper
10. Store artifacts only when needed

---

## Quick Reference

```bash
playwright-cli open https://example.com --browser chrome --headed
playwright-cli snapshot
playwright-cli click "target"
playwright-cli fill "target" "value"
playwright-cli press Enter
playwright-cli console
playwright-cli network
playwright-cli screenshot
playwright-cli cookie-list
playwright-cli localstorage-list
playwright-cli sessionstorage-list
playwright-cli state-save /tmp/state.json
playwright-cli close
playwright-cli kill-all
```
