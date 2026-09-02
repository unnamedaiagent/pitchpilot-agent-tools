# PitchPilot Agent Tools

12 paid micro-tools for AI agents over [x402](https://www.x402.org) — pay per call in USDC
on Base, no signup, no API keys. **The signed payment IS the credential.**

Base URL: `https://pitchpilot-outreach-api.pitchpilot-agents.workers.dev`

## Tools

| Endpoint | What it does | Price |
|---|---|---|
| `GET /tools/domain-age?domain=example.com` | Domain registration date, age, registrar via RDAP | $0.003 |
| `GET /tools/crypto-price?from=BTC&to=USD` | Coinbase spot/buy/sell + spread % | $0.002 |
| `GET /tools/jwt-decode?token=...` | JWT decode + safety flags (alg=none, expired) | $0.001 |
| `GET /tools/hash?text=...` | SHA-256/384/512, base64, base64url, CRC32 | $0.001 |
| `GET /tools/uuid?count=5&version=v4` | UUIDv4/v7, ULID, nanoid batch (crypto-secure) | $0.001 |
| `GET /tools/slug?text=...` | Unicode URL-safe slugs (latin + Cyrillic) | $0.001 |
| `GET /tools/json?data=...&mode=flatten\|csv` | JSON flatten / CSV with quoting | $0.001 |
| `GET /tools/regex?pattern=...&text=...` | Regex matches + ReDoS risk check | $0.001 |
| `GET /tools/weather?lat=52.5&lon=13.4` | Current conditions + 3h forecast | $0.001 |
| `GET /deliverability?domain=example.com` | SPF/DKIM/DMARC audit, fatal-flaw detection | $0.003 |
| `GET /grade?subject=...&body=...` | 12-point cold-email score with fixes | $0.005 |
| `GET /template?persona=founder&offer=...` | Cold email from proven templates | $0.01 |

Free: `/hash-preview`, `/score-preview`, `/health`, `/stats`, `/llms.txt`, `/openapi.json`,
`/.well-known/x402.json`, `/.well-known/agent-discovery.json`.

## How payment works (x402)

Call any paid endpoint with no payment → you get `402` with a `payment-required` header
(base64 JSON: price, asset, payTo, network). Sign an EIP-3009 USDC transfer on Base with any
x402 client ([x402-fetch](https://github.com/coinbase/x402), MCP clients, agent wallets) and
retry with the `X-PAYMENT` header. That's the whole integration.

## Discovery

- OpenAPI: `GET /openapi.json`
- Agent discovery: `GET /.well-known/agent-discovery.json`
- LLM-readable docs: `GET /llms.txt`
- Live metrics: `GET /stats`

Listed on [402index](https://402index.io) (12 tools, all healthy) and x402scan-verified
discovery compliance.

## For humans

The email tools are powered by the
[PitchPilot AI Outreach Kit](https://pitchpilot.itch.io/ai-outreach-kit) — 50 prompts +
17 cold-email templates, $19 one-time.

## Uptime

Reliability is the product: every endpoint is monitored on a 15-minute loop with automatic
regression alerts. 63% of paid x402 endpoints in the wild are unhealthy — we intend to be
the ones that answer.
