# Onboarding Interview — First Session Script

*(Agent: run this when `memory/financial-profile.md` is missing or still a template. Interview conversationally — one section at a time, not all 20 questions in one wall of text. Write files as you go, not at the end.)*

## Goal
In ~15 minutes, build the user's complete financial picture in `memory/` so every future session starts fully informed.

## Step 0 — Set expectations
Tell the user:
- "I'll ask about income, expenses, savings, investments and goals. Everything stays in local files on your machine (`memory/` is gitignored)."
- "Rough numbers are fine — we refine over time."
- "You can drop bank statements or holdings exports (CSV/PDF) into `inbox/` and I'll parse them instead of asking."

## Step 1 — Cash flow
Ask:
1. Monthly income (all sources — salary, freelance, rent, etc.)
2. Monthly expenses (rent, family support, EMIs, lifestyle — rough split)
3. → Compute and confirm **monthly savings capacity**. This number drives everything.

## Step 2 — Balance sheet
4. Bank balances (per account, rough is fine)
5. Emergency fund status (target = 6 months of expenses; flag the gap if short)
6. Existing investments: stocks, mutual funds, FDs, EPF/PPF, crypto, gold, real estate
   - If they have holdings: ask them to paste the list OR drop a broker export in `inbox/` → parse it into `memory/portfolio.md` with quantities and average prices.
7. Debts: loans, credit cards, rates. (High-interest debt gets flagged — paying off 36% credit-card debt beats any stock pick.)

## Step 3 — Goals
8. What are they building toward? (house, car, FIRE, education, wedding, a number)
9. For each goal: target amount, deadline, priority.
10. → Write `memory/goals.md` with a funding plan skeleton.

## Step 4 — Risk profile & hard limits
11. Experience level (first-timer / some MFs / active stock investor)
12. How would they feel about a holding falling 30%? (calibrate honestly)
13. Set THEIR hard limits (suggest defaults, let them adjust):
    - Max single order without re-confirmation: (default: 5% of portfolio)
    - Max % of net worth in direct stocks: (default: beginners 20-30%, experienced 50%)
    - F&O / leverage: (default: OFF)
14. Tax situation basics (regime, bracket) — affects harvesting and instrument choice.

## Step 5 — Write everything
Create from templates in `templates/`:
- `memory/financial-profile.md` — income, expenses, savings capacity, balances, debts, risk limits
- `memory/portfolio.md` — current holdings with entry data (or "none yet")
- `memory/goals.md` — goals with amounts, deadlines, funding plans
- `MEMORY.md` — one-line index entries pointing at each
- `memory/YYYY-MM-DD.md` — first daily log: "Onboarded. Key numbers: ..."

## Step 6 — First recommendations (end with action)
Based on what you learned, close the session with a prioritized starter plan. Typical order:
1. **Kill high-interest debt** (if any) — guaranteed return, do first
2. **Emergency fund to 6 months** (liquid fund / sweep FD) — before any market money
3. **Start SIPs** sized to savings capacity (broad index core; keep it simple at first)
4. **Direct stocks only after 1-3 above**, starting small, using `docs/screening-criteria.md`
5. Schedule rhythm: suggest a weekly check-in and a monthly full review

Then give the numbered next-actions menu as always.

## Parsing inbox/ files
When the user drops files in `inbox/`:
- **Bank statement (CSV/PDF):** extract 3-6 month average of income credits and expense debits → refine the cash-flow numbers in the profile. Categorize the top recurring expenses.
- **Broker/MF holdings export:** parse into `memory/portfolio.md` (symbol, qty, avg price, current value if present).
- Never copy raw statements into memory files — extract the numbers, note the source and date, and suggest the user delete the raw file after parsing.
