# Looping on Solana — 3-minute video script

Target length: ~3 minutes at a natural speaking pace (~550 words).
Example trade: USDC in, leveraged NVDAx (tokenized Nvidia) out.
Running example position: $1,900 NVDAx collateral against a $900 USDC loan (~1.9x).

---

**[0:00 — The pitch]**

Say you've got a thousand USDC and you think Nvidia is going up. You could buy NVDAx — tokenized Nvidia stock on Solana — and get one-to-one exposure. Looping turns that same thousand dollars into nearly two thousand dollars of Nvidia, onchain, no brokerage account, no margin desk. Here's how: buy NVDAx with your USDC, deposit it into a lending market as collateral, borrow USDC against it, buy more NVDAx, deposit that too, and repeat. Your dollars become the debt. The stock becomes the collateral. Each loop, the position grows.

**[0:40 — LTV: the number that runs everything]**

The whole strategy is governed by loan-to-value: how much you can borrow against your collateral. Tokenized stocks get conservative LTVs — call it 50%. So deposit $1,000 of NVDAx, borrow $500. Redeposit, borrow $250. Then $125. Every loop shrinks — it's a geometric series, and it converges: max exposure is one divided by one minus the LTV. At 50%, that's 2x, ever. And in practice you stop short — around $1,900 against a $900 loan — because just past max LTV sits the liquidation LTV, call it 65%: the line where the protocol starts selling your collateral.

**[1:20 — Actual exposure versus perceived exposure]**

This is where people get hurt. You put in $1,000, so it feels like a $1,000 bet. You're actually holding $1,900 of Nvidia against a $900 loan. A 10% drop in Nvidia isn't a $100 loss — it's $190, nineteen percent of your money.

And here's the mechanic to burn into your brain: your debt is fixed in dollars, but your collateral is Nvidia. So when Nvidia falls, your LTV *rises* — and it rises faster the further the price drops. You start at 47%. Nvidia falls 10%: you're at 53. Another 10%: 59. At minus 27%, you hit the 65% liquidation line and the protocol sells you out, penalty included. Notice the first leg down cost you five points of buffer and the second cost nearly seven — falling prices eat your margin at an accelerating rate. One more wrinkle with tokenized stocks: Nvidia trades six and a half hours a day in New York, but NVDAx trades around the clock. Earnings drop after close on a Friday and your LTV climbs all weekend while the real market is shut.

**[1:55 — Automated looping]**

You don't loop by hand anymore. Platforms like Kamino run this as a one-click product, using a flash loan as scaffolding: flash-borrow $900, buy the whole $1,900 of NVDAx at once, deposit it, take out a normal $900 loan against it, and repay the flash loan with that — all in one transaction. The flash loan dies at the end of the transaction; the position it built lives on: your collateral, plus an ordinary loan. Same leverage as looping by hand, one click. And you can run it in reverse: deposit USDC, borrow the stock, sell it — congratulations, you've built a leveraged short.

**[2:15 — The real risks]**

Here's the part the APY screenshots skip. This position has negative carry: you're paying interest on the USDC loan every single day, and the stock pays you nothing onchain. And that interest doesn't just eat your profits — it's added to your debt, so your LTV creeps toward the liquidation line even if the price never moves. Borrow rates are variable and can spike. Tokenized-stock liquidity is thin, so unwinding in a panic means slippage. Liquidation penalties apply to the whole borrowed stack, not your deposit. And you're stacking smart contract risk and oracle risk on top of plain old Nvidia risk. The other flavor of looping — staked SOL against SOL — flips the carry positive, but that's a different video.

**[2:45 — Close]**

So: know your real exposure, not your deposit. Watch your LTV — price drops push it up, and interest pushes it up even when nothing happens. And keep far from the line, because onchain, nobody calls you before they liquidate you.

---

*Notes for the presenter:*

- *All numbers are illustrative — check live xStocks market parameters (Kamino etc.) before recording. 50% max LTV / 65% liquidation LTV are placeholders.*
- *On-screen graphic for the LTV section: the shrinking series $1,000 → $500 → $250 → $125.*
- *On-screen graphic for the exposure section — the accelerating LTV ladder ($1,900 collateral, $900 debt):*

| Nvidia move | Collateral | LTV |
|---|---|---|
| — | $1,900 | 47% |
| −10% | $1,710 | 53% |
| −20% | $1,520 | 59% |
| −27% | $1,387 | 65% → liquidated |
