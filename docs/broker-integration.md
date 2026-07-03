# Optional: Broker Integration (Level 2)

You don't need this to start — web research covers 90% of the value. Add it when manually pasting holdings gets annoying.

## The rule that comes first
**READ-ONLY.** The agent gets portfolio/price/holdings read access. It never gets order-placement credentials. Order cards + your click = the system.

## India: Zerodha Kite Connect (example)
1. Create a Kite Connect app at developers.kite.trade (₹500/month for personal use, or use the free daily-session approach).
2. Store credentials in a `.env` file OUTSIDE the repo or in an ignored path:
   ```
   accounts/<name>.env      # gitignored
   KITE_API_KEY=...
   KITE_API_SECRET=...
   ```
3. A small script the agent can run:
   ```python
   # tools/holdings.py — read-only portfolio pull
   from kiteconnect import KiteConnect
   import os
   kite = KiteConnect(api_key=os.environ["KITE_API_KEY"])
   kite.set_access_token(os.environ["KITE_ACCESS_TOKEN"])
   for h in kite.holdings():
       print(h["tradingsymbol"], h["quantity"], h["average_price"], h["last_price"])
   ```
4. Tell the agent in CLAUDE.md: *"Live holdings via `python tools/holdings.py`. Read-only — never attempt order placement."*

Useful read-only endpoints: `holdings()`, `positions()`, `margins()`, `mf_holdings()`, `mf_sips()`, `quote()`.

## Other markets
Same pattern anywhere: find your broker's read-only API or export flow (Schwab/Fidelity CSV export, IBKR flex queries, Trading212 API...). Even a weekly manual CSV export dropped into `inbox/` works fine — the agent parses it into `portfolio.md`.

## Mutual funds / SIP tracking (India)
- CAS statements (CDSL/NSDL/CAMS monthly email) dropped into `inbox/` — the agent parses PDF CAS fine.
- Kite Coin holders: `mf_holdings()` / `mf_sips()` are read-visible via the same API.

## What NOT to do
- ❌ No order-placement API keys in the agent's reach, ever.
- ❌ No storing broker passwords/TOTP secrets in the repo (even gitignored — keep them in your OS keychain).
- ❌ No cron jobs that trade. Scheduled *reports* are great; scheduled *orders* are how you wake up to surprises.
