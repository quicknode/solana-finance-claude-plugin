# Looping on Solana — 3-minute video script

Target length: ~3 minutes at a natural speaking pace (~480 words).

---

**[0:00 — What looping is, and why people do it]**

Looping is DeFi's version of a leveraged carry trade. On Solana it usually looks like this: deposit a yield-bearing asset — say JitoSOL — into a lending market like Kamino or marginfi, borrow SOL against it, swap that SOL back into JitoSOL, deposit again, and repeat. Every loop, you're stacking more of the staking yield on the same starting capital. As long as the yield you earn is higher than the rate you pay to borrow, the spread is pure profit — multiplied by your leverage. That spread is the entire trade. People loop to turn a 7% staking yield into 15 or 20%, or to farm points and emissions with size they don't actually have.

**[0:40 — LTV: the number that runs everything]**

The whole strategy is governed by loan-to-value, or LTV: how much you can borrow against your collateral. If JitoSOL has an 80% max LTV, depositing 10 SOL worth lets you borrow 8. And here's the key mechanic: each loop shrinks. Deposit 10, borrow 8. Deposit that 8, borrow 6.4. Then 5.12, and so on. It's a geometric series, and it converges: at 80% LTV your maximum possible exposure is 1 divided by 1 minus 0.8 — five times your starting capital. You can never loop past that ceiling, and in practice you stop well short of it, because max LTV sits right next to liquidation LTV.

**[1:20 — Actual exposure versus perceived exposure]**

This is where people get hurt. Your wallet shows 10 SOL. Your actual exposure after three loops might be 25. If you're looping an LST against SOL, your *price* exposure is mostly to the peg between them, not to SOL itself — which feels safe. But your *liquidation* exposure is to everything: the LST trading below fair value during a panic, borrow rates spiking when utilization jumps, or an oracle printing a bad price. A 3% depeg at 4x leverage is a 12% hit to your equity, and it can push you straight into liquidation.

**[1:50 — Automated looping]**

You don't have to loop by hand anymore. Kamino Multiply, marginfi's looper, and products like Loopscale use flash loans to open the entire leveraged position in a single transaction — one click, max efficiency, and one click to unwind. Convenient, but the leverage is identical. The button being easy doesn't make the position safe.

**[2:15 — The real risks]**

Be honest about what can go wrong. Borrow rates are variable — a rate spike can flip your carry negative overnight, so a profitable loop becomes a position that bleeds. High utilization can trap you: if all the SOL is borrowed, you can't unwind. Liquidations on leverage are expensive — you pay the penalty on your whole borrowed stack, not your deposit. Add smart contract risk, oracle risk, and yields propped up by temporary points programs.

**[2:45 — Close]**

So: know your real exposure, not your deposit. Watch the spread, not the APY. And keep your health factor far from the line — because on-chain, nobody calls you before they liquidate you.

---

*Notes for the presenter: numbers (80% LTV → 5x max leverage) are illustrative; check live parameters on the protocol before publishing. Consider showing the geometric series 10 → 8 → 6.4 → 5.12 on screen during the LTV section.*
