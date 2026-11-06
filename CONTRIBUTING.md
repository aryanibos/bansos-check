# Contributing

Contributions are welcome.

## Source of truth

Edit the canonical skill only in:

```text
skills/bansos-check/
```

## Rules

- Evaluation stays **read-only**: the skill must never instruct an agent to log in, install, download, run, or pay anything while checking an offer.
- Verdicts require fetched evidence (the destination page itself, independent reporting) — never the offer's own claims.
- Keep the automatic JANGAN categories intact: pipe-to-shell installs, unknown agents, off-domain logins, API key / seed phrase requests, activation fees.
- New scam patterns are welcome as new checks or worked examples; ground each one in a real, observed case.
- Do not add secrets, real credentials, or real victims' details to examples.
- Keep changes focused and reviewable.
- Update `CHANGELOG.md` for published changes.

## Pull requests

Explain:

- what changed
- which real-world pattern or case motivates it
- whether any verdict category changed, and why
