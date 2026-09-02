<div align="center">

<img src="https://api.iconify.design/lucide/shield-check.svg?color=%232563eb&width=72" width="72" height="72" alt="" />

# AtherDLP

**See what your app is sending — before it leaves.**

Data loss prevention for outbound HTTP, built for developers.
Three lines in your app, one command for the dashboard.

[![PyPI — server](https://img.shields.io/pypi/v/atherdlp-server?label=atherdlp-server&color=2563eb)](https://pypi.org/project/atherdlp-server/)
[![PyPI — sdk](https://img.shields.io/pypi/v/atherdlp?label=atherdlp&color=2563eb)](https://pypi.org/project/atherdlp/)
[![Python](https://img.shields.io/pypi/pyversions/atherdlp-server?color=2563eb)](https://pypi.org/project/atherdlp-server/)
[![License](https://img.shields.io/badge/license-Apache--2.0-2563eb)](https://github.com/AetherDLP/AtherDLP-backend/blob/main/LICENSE)

[**Documentation**](https://aetherdlp.github.io/docs/#/) · [**Getting Started**](https://aetherdlp.github.io/docs/#/GETTING_STARTED) · [**Use Cases**](https://aetherdlp.github.io/docs/#/USE_CASES)

</div>

---

## The problem

Your app calls OpenAI. Someone pastes a customer record into a prompt. It leaves
your infrastructure and you never find out.

The same story runs for every outbound call your service makes — a support
ticket forwarded to a vendor API, a CSV posted to an analytics endpoint, an
error report carrying a session token. Traditional DLP watches the network
perimeter. It cannot see inside your process, and by the time it could, the
request is already gone.

AtherDLP watches from **inside the application**, at the `httpx` layer, so it
sees the payload as your code constructed it.

## Try it in 60 seconds

```bash
pip install atherdlp-server
atherdlp up
```

That starts the dashboard at <http://localhost:8473> with demo data already in
it — SQLite, no Postgres, no Redis, no Docker, no Node toolchain.

Then point your application at it:

```bash
pip install atherdlp
```

```python
import atherdlp

atherdlp.configure(endpoint="http://127.0.0.1:8473/events/http")
atherdlp.install()

# your app's httpx calls happen here — nothing else changes

atherdlp.uninstall()
```

Every outbound request now appears in the dashboard, classified, matched against
detectors, and resolved to a decision.

## What you get

| | |
|---|---|
| **Destination awareness** | Calls to OpenAI, Anthropic, Gemini, Mistral and Cohere are tagged as LLM egress; Stripe as PCI. You see *where* data went, not just that it went. |
| **Content detection** | Credit card numbers, emails and API keys are matched inside JSON bodies **and inside uploaded files** — PDFs and text extracted, images via optional OCR. |
| **Policy decisions** | Every event resolves to `allow`, `alert`, or `block`. |
| **End-to-end tracing** | One `trace_id` links the outbound call, the extracted content, and the alert it raised. Follow a single leaked field from origin to alarm. |
| **Fail-open by design** | The SDK never breaks your app. Delivery is non-blocking; if the collector is down, your request still goes out. |

## Use cases

- **Catch prompts carrying customer data** before they reach an LLM vendor.
- **Audit which third parties your service actually talks to** — usually more than anyone remembers.
- **Prove what a file upload contained** when a customer asks what you sent.
- **Give security a decision log** without routing production traffic through a proxy.

Full walkthroughs with runnable code: [**Use Cases →**](https://aetherdlp.github.io/docs/#/USE_CASES)

## Repositories

| Repo | What it is |
|---|---|
| [**AtherDLP-backend**](https://github.com/AetherDLP/AtherDLP-backend) | The server: policy engine, REST API, and dashboard. Published as [`atherdlp-server`](https://pypi.org/project/atherdlp-server/). |
| [**AtherDLP-sdk**](https://github.com/AetherDLP/AtherDLP-sdk) | The Python `httpx` interceptor. Published as [`atherdlp`](https://pypi.org/project/atherdlp/). |
| [**AtherDLP-frontend**](https://github.com/AetherDLP/AtherDLP-frontend) | React dashboard. Compiled into the server package — you never build it. |
| [**AtherDLP-infra**](https://github.com/AetherDLP/AtherDLP-infra) | Docker Compose for Postgres/Redis deployments. |
| [**docs**](https://github.com/AetherDLP/docs) | The documentation site. |

## Status

Early alpha, and honest about it: **the server has no authentication yet.** It
binds to loopback by default, which keeps it private to your machine. Do not
expose it on a public interface — the read APIs return captured payload samples,
which are by definition the most sensitive data the tool handles.

<div align="center">

**[Get started →](https://aetherdlp.github.io/docs/#/GETTING_STARTED)**

Apache-2.0

</div>
