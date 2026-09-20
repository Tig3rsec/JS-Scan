<div align="center">

# JS Recon

### JavaScript intelligence for bug bounty hunters and security teams

Turn minified JavaScript into a prioritized attack-surface report in seconds — entirely in your browser.

**[Launch JS Recon](https://tig3rsec.github.io/js-recon/)** &nbsp;·&nbsp; **[Follow on GitHub](https://github.com/Tig3rsec)**

</div>

---

## Executive summary

Modern web applications ship large, minified JavaScript bundles that quietly expose internal APIs, cloud resources, credentials and hidden functionality. Finding them by hand is slow and inconsistent.

**JS Recon** automates that first pass. Load a script by pasting, uploading or fetching it from a URL, and it beautifies the code, extracts 21 categories of security-relevant data, and — optionally — hands the findings to an AI model that returns a ranked, color-coded triage report.

It is one HTML file. There is nothing to install, no server to run, and no data stored anywhere except your own browser.

## Why teams use it

| | |
|---|---|
| **Fast triage** | From raw bundle to structured findings in one click. |
| **Broad coverage** | 21 extraction categories across endpoints, secrets, cloud, auth and configuration. |
| **AI-assisted analysis** | Six purpose-built prompts turn raw findings into prioritized next steps. |
| **Private by design** | Runs locally. Data leaves your browser only when you fetch a URL or run AI analysis. |
| **Zero infrastructure** | A single static file that deploys anywhere in minutes. |

## Capabilities

### Extraction engine

| Domain | Coverage |
|---|---|
| **Hosts and URLs** | Domains and subdomains · internal IPs and ports · full URLs · dev, staging and test URLs · WebSocket endpoints · OAuth and auth URLs |
| **APIs and routes** | API endpoints · versioned APIs · GraphQL · admin and internal functions · hidden endpoints · upload and download endpoints |
| **Secrets and cloud** | Hardcoded secrets and tokens · AWS, Firebase and cloud references · third-party integrations · authorization headers · environment variables |
| **Logic and configuration** | Feature flags and roles · hidden and debug parameters · source maps and backups · CORS maps and errors |

### AI intelligence layer

Connect an [OpenRouter](https://openrouter.ai) API key once and choose from a live, multi-provider model catalogue (Google, Anthropic, OpenAI, DeepSeek, Meta, Mistral, Qwen and more). The model list is fetched live, so it never points at a retired model. A free-model router is the default, with optional automatic fallback if a model fails.

Built-in analyses: **Triage Secrets · Attack Surface · Cloud Exposure · Auth Analysis · API Mapping · Risk Report**, plus a free-form custom query.

Results render as an executive-style report with severity badges, a findings summary, and a fullscreen view. Export as Markdown or a standalone HTML file to share with your team.

### Resilient URL acquisition

JS Recon tries multiple routes in order and stops at the first that returns real content:

1. Direct request
2. Your private proxy *(optional, recommended)*
3. A configurable list of public CORS proxies

Firewall and challenge pages are detected and skipped. With a private proxy, requests can rotate through multiple browser agents to reduce false blocks.

## Quick start

1. Open JS Recon (hosted link above, or open `index.html` locally).
2. Load code: paste it, upload a file, or enter a URL and choose **Fetch URL**.
3. Select **Beautify** and review the extracted findings.
4. *(Optional)* Open **AI Analysis**, add your API key in **Settings**, and run a prompt.

## Private proxy (recommended)

Public proxies share IP addresses that many firewalls block. A free Cloudflare Worker gives you a dedicated route and enables browser-agent rotation.

1. Create a Worker in the [Cloudflare dashboard](https://dash.cloudflare.com) and paste the code from **Settings → URL fetching**.
2. Set your proxy in Settings to `https://YOUR-NAME.workers.dev/?url={url}&ua={ua}`.
3. Choose a browser agent, or leave it on **Auto-rotate**.

Keep the Worker address private.

## Security and privacy

- **Local by default.** Analysis runs in your browser. There is no JS Recon server.
- **What leaves the page:** the URL you choose to fetch (to the target or your proxy), and the extracted findings you choose to send for AI analysis (to OpenRouter and the selected model provider).
- **Stored on your device only:** your API key and settings, in browser storage.
- **AI data handling:** free models may log or train on prompts. Use a paid model for sensitive targets.

## Responsible use

Use JS Recon only on systems you own or are explicitly authorized to test, and follow each program's scope and disclosure rules.

## Troubleshooting

| Symptom | Resolution |
|---|---|
| All fetch routes show "unreachable" | The host blocks outbound requests, or a browser extension or network filter blocks the proxy domains. Some free hosts (including Neocities' free plan) block all outbound requests; use a host that allows them, or open `index.html` locally. Otherwise, disable the blocker. |
| All fetch routes show 403 | The target's firewall blocks browsers and shared proxies. Use your private proxy, or paste the file contents manually. |
| AI reports "no endpoints found" | The model was retired. Refresh the model list in Settings and choose another. |
| AI reports a privacy-settings block | Allow free endpoints at [openrouter.ai/settings/privacy](https://openrouter.ai/settings/privacy). |
| API key not remembered | Keys are stored per browser and per address. A new location, private window or cleared data requires re-entry. |

---

<div align="center">

**Created by [D4RK TIG3R](https://github.com/Tig3rsec)**

</div>
