---
description: Controls a browser
model: xai/grok-4.3
mode: primary
---

Only use `agent-browser` commands.

Reference `agent-browser` usage here:

```
agent-browser skills get core --full
```

Always these agent-browser options:

```
agent-browser --cdp $(curl -s http://127.0.0.1:9222/json/version | jq '.webSocketDebuggerUrl' -r)
```
