# Warren Starter Kit 🏦

**Turn Claude Code into your personal finance agent in 20 minutes.**

This is a template repository for building your own AI finance agent — one that interviews you about your finances, remembers everything between sessions, screens stocks with hard quality gates, plans deployments with stop-losses, and logs every decision to files you can audit.

It's the exact system described in the blog post *"I Built an AI Stock Analyst Called Warren"* — generalized so anyone can start from zero.

> ⚠️ **What this is not:** investment advice, a get-rich scheme, or an auto-trader. The agent researches and plans; **you** decide and click. It never executes trades. See [DISCLAIMER.md](DISCLAIMER.md).

---

## Quick Start (20 minutes)

### 1. Get the kit
```bash
git clone https://github.com/<you>/warren-starter-kit my-warren
cd my-warren
```

### 2. Install Claude Code
```bash
npm install -g @anthropic-ai/claude-code
```
(Needs a Claude subscription or API key — see [claude.com/claude-code](https://claude.com/claude-code).)

### 3. Start the agent
```bash
claude
```
Then just type:
```
start my onboarding
```

The agent reads [ONBOARDING.md](ONBOARDING.md) and interviews you step by step:
- income, expenses, savings capacity
- bank balances and emergency fund
- existing investments (paste your holdings, or drop a CSV in `inbox/`)
- goals with amounts and deadlines
- risk appetite and hard safety rules

It writes everything into `memory/` files. From then on, **every session starts with the agent already knowing your finances.**

### 4. Your first real session
Try any of these:
```
give me a full financial health check
screen [stock you're curious about] against the quality gates
I can invest ₹25,000/month — build me a starting plan
```

---

## How it works

```
my-warren/
├── CLAUDE.md          ← the agent's persona, rules & safety rails (read every session)
├── ONBOARDING.md      ← first-run interview script
├── MEMORY.md          ← index of what the agent knows (auto-maintained)
├── memory/            ← YOUR data — gitignored, never leaves your machine
│   ├── financial-profile.md
│   ├── portfolio.md
│   ├── goals.md
│   └── YYYY-MM-DD.md  ← daily decision logs
├── inbox/             ← drop bank statements / holdings CSVs here — gitignored
├── templates/         ← blank templates the agent fills
├── prompts/PROMPTS.md ← copy-paste prompt library
└── docs/
    ├── screening-criteria.md   ← the 10-point stock quality gate
    ├── safety-rules.md         ← non-negotiable guardrails
    └── broker-integration.md   ← optional: read-only broker API setup
```

**The three ideas that make it work:**

1. **Files are the memory.** The agent forgets everything between sessions; markdown files don't. Every session starts by reading `MEMORY.md` + `memory/portfolio.md`, and every session writes at least one update back.
2. **Hard gates beat vibes.** Stocks are screened against explicit criteria ([docs/screening-criteria.md](docs/screening-criteria.md)) — including the cash-conversion gate that kills most "high growth" traps. The agent's most common (and most valuable) answer is *"no, and here's why."*
3. **The human clicks.** The agent produces order cards (symbol, qty, limit price, stop-loss). You place them at your broker. That separation is a feature, not a limitation.

---

## The operating cycle

| Cadence | What happens |
|---|---|
| Any session | Agent reads memory → acts → writes memory |
| Weekly | Portfolio pulse: prices, stops, thesis health |
| Earnings season | Verify every holding's thesis against actual results |
| Every ~2 months | Full cycle: fresh screen → verify survivors → staggered deployment plan → review |

## FAQ

**Is my financial data safe?** It lives in local markdown files in `memory/` and `inbox/`, both gitignored. Nothing is uploaded anywhere except to the model while you chat (same as anything you type into Claude). Don't commit these folders if you fork publicly.

**Do I need a broker API?** No. Level 0 (nothing connected) gives you 90% of the value via web research. See [docs/broker-integration.md](docs/broker-integration.md) if you want live portfolio reads later.

**Does this work outside India?** Yes — the process is universal. Templates use ₹ and Indian examples (Screener.in, ValuePickr); swap for your market's equivalents.

**Can it trade for me?** No, and don't change that. Read [docs/safety-rules.md](docs/safety-rules.md) before you're tempted.

## Contributing
PRs welcome: better templates, prompts for new use cases (tax planning, debt payoff, FIRE math), localization for other markets.

## License
MIT — see [LICENSE](LICENSE). Use it, fork it, build on it.
