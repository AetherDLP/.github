# AtherDLP

**Developer-first DLP for outbound HTTP.**

AtherDLP helps teams detect sensitive data leaving applications, evaluate it against policy, and trace every event from SDK to backend to UI.

## Why AtherDLP

- **Drop-in Python SDK** for `httpx` interception
- **Safe payload capture** with body sampling and binary guards
- **Policy decisions**: `allow`, `alert`, or `block`
- **Traceability** with `trace_id` and `X-Correlation-Id`

## Quick Start

```py
import atherdlp

atherdlp.install()

# your app makes httpx calls

atherdlp.uninstall()
```

[Read the docs](https://aetherdlp.github.io/docs/#/)

## Repositories

| Path | Description |
|------|-------------|
| `AtherDLP-sdk/` | Python SDK (httpx interceptor) |
| `AtherDLP-backend/` | API, policy evaluation, event ingestion |
| `AtherDLP-frontend/` | UI (correlation header propagation) |
| `AtherDLP-infra/` | Local/dev environment (`.env.example`) |
