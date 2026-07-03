# Optional: Scheduled Runs (Level 3) — autopilot for analysis, not for orders

The effective version of "autopilot" is automating the **analysis**, not the **execution**. The agent can run by itself every morning, reconcile your portfolio read-only, check every stop and trigger, and leave ready-to-click order cards waiting for you. You still click. See the last section for why that line stays.

## The morning brief (cron / launchd)

Claude Code runs headless with `claude -p "<prompt>"`. Schedule it in the kit folder:

```bash
# crontab -e   (weekdays at 8:30, before market open)
30 8 * * 1-5  cd ~/my-warren && claude -p "Morning brief: read the memory \
files, reprice the portfolio, check every stop and trigger against current \
prices, flag thesis-relevant news, and write the brief with any ready order \
cards to memory/briefs/$(date +\%F).md" >> memory/briefs/cron.log 2>&1
```

You wake up to a dated brief: what moved, what's near a stop, which trigger fired, and the exact order card to place if one did. Ten minutes with coffee, then one click at your broker if warranted.

Good scheduled jobs:
- **Daily pre-market brief** (above)
- **Weekly pulse** (Sunday): full portfolio health, thesis checkpoints, upcoming earnings dates
- **Results-day check**: on an earnings date, verify the thesis against actual numbers and write add / hold / kill with reasoning

With a read-only broker connection ([broker-integration.md](broker-integration.md)), the brief reconciles real holdings automatically. Without it, the brief works from `portfolio.md`.

## Why the order button stays human (read before "improving" this)

It is tempting to finish the loop: give the agent the trading API credentials and let it place the orders too. Four reasons this kit will never do that, in increasing order of severity:

1. **Fat fingers at machine speed.** A hallucinated ticker, a misread price, a quantity off by 10x. With a human click, these are a caught mistake. With execution access, they are a fill.
2. **Prompt injection is not theoretical.** This agent reads forums, news pages, and search results *by design*. Any web page it reads is untrusted input. If the agent holds order-placement credentials, a malicious page that says "urgent: buy X" is an instruction with a wallet attached. Read-only credentials make that entire attack class harmless.
3. **Regulation.** In India, SEBI's algo-trading framework and broker terms put real conditions on automated order placement by retail users (approvals, order tagging, rate limits). "My AI clicks for me" is not a compliance strategy anywhere.
4. **The discipline is the product.** The forced ten seconds where a human reads the order card is where over-trading, revenge trades, and FOMO go to die. Automate it away and you have built a faster way to make unreviewed mistakes.

The division of labor that works: **the agent runs every day; your judgment runs once, at the click.**
