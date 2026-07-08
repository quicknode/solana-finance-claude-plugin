# Looping on Solana — 3-minute video script

Target length: ~3 minutes at a natural speaking pace (~500 words).
Example trade: USDC in, leveraged NVDAx (tokenized Nvidia) out.

---

**[0:00 — The pitch]**

Say you've got a thousand USDC and you think Nvidia is going up. You could buy NVDAx — tokenized Nvidia stock on Solana — and get one-to-one exposure. Looping turns that same thousand dollars into two or three thousand dollars of Nvidia, onchain, no brokerage account, no margin desk. Here's how: buy NVDAx with your USDC, deposit it into a lending market as collateral, borrow USDC against it, buy more NVDAx, deposit that too, and repeat. Your dollars become the debt. The stock becomes the collateral. Each loop, the position grows.

**[0:40 — LTV: the number that runs everything]**

The whole strategy is governed by loan-to-value: how much you can borrow against your collateral. Tokenized stocks get conservative LTVs — call it 50%. So deposit $1,000 of NVDAx, borrow $500. Redeposit, borrow $250. Then $125. Every loop shrinks — it's a geometric series, and it converges: max exposure is one divided by one minus the LTV. At 50%, that's 2x, ever. You can't loop past it, and in practice you stop short, because max LTV sits right next to liquidation LTV.

**[1:20 — Actual exposure versus perceived exposure]**

This is where people get hurt. You put in $1,000, so it feels like a $1,000 bet. After looping you're actually holding $1,900 of Nvidia against a $900 loan. Now a 10% drop in Nvidia isn't a $100 loss — it's $190, nineteen percent of your money. And you don't get to ride it out: if the collateral falls far enough, the protocol liquidates you automatically and the loss is locked in. One more wrinkle with tokenized stocks: Nvidia trades six and a half hours a day in New York. NVDAx trades around the clock. Earnings drop after close on a Friday and your position reprices all weekend while the real market is shut.

**[1:55 — Automated looping]**

You don't loop by hand anymore. Platforms like Kamino run this as a one-click product — a flash loan opens the whole position at your target leverage in a single transaction, and one click unwinds it. Same leverage, easier button. And you can run it in reverse: deposit USDC, borrow the stock, sell it — congratulations, you've built a leveraged short.

**[2:15 — The real risks]**

Here's the part the APY screenshots skip. This position has negative carry: you're paying interest on the USDC loan every single day, and the stock pays you nothing onchain — time works against you, so it's a trade, not an investment. Borrow rates are variable and can spike. If the market turns and everyone unwinds at once, thin tokenized-stock liquidity means slippage on the way out. Liquidation penalties apply to the whole borrowed stack, not your deposit. And you're stacking smart contract risk and oracle risk on top of plain old Nvidia risk. The other flavor of looping — staked SOL against SOL — flips the carry positive and gets paid to wait, but that's a different video.

**[2:45 — Close]**

So: know your real exposure, not your deposit. Watch the interest clock. And keep your health factor far from the line — because onchain, nobody calls you before they liquidate you.

---

*Notes for the presenter: the 50% LTV → 2x cap is illustrative — check the live xStocks market parameters (Kamino, etc.) before recording. The $1,000 → $500 → $250 → $125 series is worth showing on screen during the LTV section. The "$1,900 of Nvidia against a $900 loan" figures assume ~3–4 loops at 50% LTV, stopped short of the cap.*
