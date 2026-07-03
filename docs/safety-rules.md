# Safety Rules — Non-Negotiable

These exist because every one of them was learned the expensive way by someone.

## 1. The agent never executes trades
The agent produces **order cards**:
```
BUY  <SYMBOL> (<exchange>) — <qty> shares
LIMIT ₹<price>  ·  ~₹<total>
Stop-loss: <level> (set as GTT/stop order same day)
Reason: <one line from the thesis>
```
You place the order at your broker yourself. This human click is the final safety gate against hallucinated tickers, fat-finger sizes, and bad days. **Do not automate it away.**

## 2. Every position has a stop-loss — defined the same day as the buy
A stop is the pre-agreed "the thesis is broken" line, decided when you're calm. No position is exempt. Log it with the buy.

## 3. LIMIT orders for exits
Market-selling into a falling, illiquid small-cap donates your money to the spread.

## 4. Hard money boundaries
- **Emergency fund (6 months expenses) is untouchable.** Not for dips, not for "sure things."
- Money reserved for a dated goal (fees, wedding, house down-payment <3 years away) never goes into equities.
- Max single order and max direct-equity % come from your `memory/financial-profile.md` limits — the agent must respect them and you shouldn't override them casually.

## 5. No leverage, no F&O, by default
Derivatives and margin turn survivable mistakes into terminal ones. If you're experienced and insist, enable it explicitly in your profile with a ring-fenced capital cap and a hard daily-loss circuit breaker enforced in code — not on the honor system. This rule exists because automated strategies without circuit breakers reliably find their worst day.

## 6. Everything gets logged
Every order card, fill, dividend, and decision goes in `memory/YYYY-MM-DD.md` — before and after execution. If you can't reconstruct why you bought something six months later, you're gambling, not investing.

## 7. Verify before trusting
- Double-check the exact trading symbol before every order (similar names are a classic error).
- The agent's web data can be stale or wrong — cross-check price/fundamentals at your broker or Screener before clicking.
- "A famous investor bought it" is not a reason. Verify the date; check who sold.

## 8. Position sizing assumes you're sometimes wrong
Size every position so a 50% fall is a bad month, not a changed life. The screen reduces mistakes; nothing eliminates them — the −20% position in the original Warren's book passed every gate too.

## 9. The agent must remain able to say NO
If you find yourself prompting the agent to "find me something to buy this week," you've broken the system. The most valuable output is a well-reasoned "nothing passes; here's what I'm waiting for."
