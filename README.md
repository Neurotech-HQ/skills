# Neurotech Skills

Agent skills published by [Neurotech](https://github.com/Neurotech-HQ) for the [skills.sh](https://skills.sh) ecosystem.

These skills give AI coding agents — Claude Code, Cursor, Codex, Gemini CLI, and any other agent compatible with the [skills CLI](https://github.com/vercel-labs/skills) — the procedural knowledge to work correctly with Neurotech's tools, APIs, and conventions. Drop one into your agent and it gains expert-level knowledge of the covered topic without you having to re-explain it on every prompt.

This repository follows the **multi-skill pattern**: each skill lives in its own top-level folder and can be installed independently with the `--skill` flag.

## Available skills

### snippe-integration

Build integrations with [Snippe](https://snippe.sh) — a payment processing API for Tanzania covering mobile money, cards, QR codes, hosted checkout sessions, and disbursements. The skill gives your agent the protocol-level knowledge to write correct Snippe API calls, verify webhook signatures securely, and dodge the easy-to-miss gotchas (idempotency key length, TZS-only amounts, the `data.amount` object shape in webhooks).

**Install:**

```bash
npx skills add Neurotech-HQ/skills --skill snippe-integration
```

**What's covered:**

- **Authentication** — bearer tokens, scopes, key management
- **Payments** — mobile money (M-Pesa, Airtel Money, Mixx by Yas, Halotel), card, dynamic QR
- **Sessions** — hosted checkout pages, payment profiles, shareable payment links
- **Disbursements** — mobile money and bank payouts across 40+ Tanzanian banks
- **Webhooks** — HMAC-SHA256 signature verification with working examples in Node.js, Python, PHP, and Go
- **Error handling** — status codes, validation rules, recovery patterns, and the `PAY_001` idempotency-key gotcha

**Triggers automatically when** the user mentions Snippe, Tanzania payments, mobile money integrations, TZS currency, disbursements to Tanzanian wallets/banks, or webhook verification for their payment provider — even if they don't say "Snippe" by name.

## Installing skills from this repo

All skills in this repository are installed via the `npx skills` CLI:

```bash
npx skills add Neurotech-HQ/skills --skill <skill-name>
```

The `--skill` flag is required because this is a multi-skill repo — without it, the CLI wouldn't know which top-level folder to install.

### Example: install into Claude Code

```bash
npx skills add Neurotech-HQ/skills --skill snippe-integration
```

The CLI auto-detects your agent and places the skill in the correct directory (e.g. `.claude/skills/` for Claude Code, `.cursor/skills/` for Cursor). See the [skills CLI docs](https://github.com/vercel-labs/skills) for options like global installs, project-scoped installs, and updating.

### Updating

```bash
npx skills update snippe-integration
```

This pulls the latest version from the repo.

## Structure

```
skills/
├── README.md                 (this file)
├── LICENSE                   (MIT)
├── snippe-integration/       (one skill per top-level folder)
│   ├── SKILL.md              (metadata + main instructions)
│   └── references/           (progressive-disclosure reference docs)
└── <future skills here>
```

Each skill is self-contained — its `SKILL.md` holds the metadata (`name`, `description`) and the core instructions the agent loads whenever the skill triggers, and the optional `references/` subfolder holds deeper documentation that the agent pulls in only when the task requires it. This keeps the agent's context small for simple questions and expands it only when the work needs the detail.

## Contributing

Found a bug, gap, or confusing section in one of the skills? Open an issue or a pull request on [this repo](https://github.com/Neurotech-HQ/skills). For new skills, follow the existing folder layout (`<skill-name>/SKILL.md` plus an optional `references/` directory) and make sure the `name` field in the frontmatter matches the folder name — the skills CLI enforces this.

## License

[MIT](./LICENSE) © Neurotech
