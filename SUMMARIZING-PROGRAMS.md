# Summarizing Solana Programs

Rules for explaining a Solana program clearly and truthfully — in a README, a
walkthrough, a video script, or an answer.

**These build on [SKILL.md](SKILL.md), which already governs the shared rules** and
apply whenever you explain a program, not just when you write one:

- *Fight for Truth* — grep before naming any identifier; describe what **is**, not
  what was.
- *Terminology* — Solana, not Ethereum ("programs" not "smart contracts",
  "transaction fees" not "gas").
- *Writing About Financial Software* — one name per role; describe custody
  precisely instead of saying "non-custodial"/"trustless"; name the actual
  instruction handlers in lifecycle prose.

This file adds only the explanation-specific guidance not covered there.

## Explain through people and motivations

- **Cast the walkthrough with named people, each with a concrete motive.** A
  protocol becomes legible when you follow real actors doing real things.
- **Naming convention.** End *users* take names from the start of the alphabet —
  **Alice, Bob, Carol, Dave** — and are ordinary users, never Solana developers.
  *Admins / operators* take a name from later in the alphabet — **Maria**, or
  another late letter.
- **Every actor needs a motivation — including the operator.** If a participant
  has no reason to take part, the explanation (and probably the program) is
  incomplete. A canonical lending cast:
  - **Alice** wants to earn yield on her USDC.
  - **Bob** wants to stay long NVIDIA, so he borrows USDC against his NVDAx
    instead of selling it.
  - **Carol** wants to short SpaceX, so she borrows SPCXx and sells it.
  - **Dave** liquidates unhealthy positions for the discount.
  - **Maria** runs the market and earns the interest spread (the reserve factor).
- **Show opposing cases when the program is symmetric** (a long that wins and a
  short that gets liquidated teaches more than one happy path).

## Use real, recognizable assets

- **Only reference tokens that actually exist** — verify before naming one.
- **Prefer well-known real-world assets** the audience already understands, and
  gloss each on first use: **USDC** (US dollars), **NVDAx** (NVIDIA stock),
  **SPCXx** (SpaceX stock).
- **No memecoins**, and **avoid SOL** wherever possible — its price is
  meaningless to most people, whereas a dollar or a familiar stock is not.
- **Numbers are real and current, or clearly hypothetical.** Cite a price you
  state (real token, today's value, with a source); label any invented or future
  figure as illustrative. Keep token math concrete with base units and a worked
  example ("100 SPCXx at \$170 = \$17,000 collateral; 75% LTV ⇒ borrow up to
  \$12,750").

## Get the mechanism and incentives right

- **Explain incentives correctly, and correct plausible-but-wrong mental
  models.** Example: liquidation is not a "crank fee" — the liquidator is a
  principal who repays debt from their own pocket and takes the borrower's
  collateral at a discount; the program can't sell collateral itself, so it pays
  outsiders to show up.
- **Contrast onchain vs offchain on what actually differs:** collateral instead
  of credit, rules-as-deployed-bytecode, algorithmic (utilization-based) rates,
  permissionless liquidation, oracle dependence, and the finality of bugs.
- **Get the account hierarchy right** — say what owns what (market → reserves →
  vault + share mint; obligations; per-obligation collateral vaults) rather than
  hand-waving "the program stores it."

## Name peers, kept current

Reference real comparable programs (e.g. **Kamino Lend**, **MarginFi**, **Save**)
and use **current** names (Save, not Solend). Don't cite dead, hacked, or
irrelevant projects, and don't reach to other ecosystems for the comparison.

## Push back on an incomplete program — don't disclaim it

- **If a program isn't production-ready, fix it, don't paper over it.** When a
  feature is missing or a participant has no incentive to take part (e.g. the
  market operator earns nothing), say so and offer to add it — a disclaimer is
  not a substitute for a working design.
- **Deliberate test-only scaffolding is different** and should simply be labelled
  as such — e.g. a mock price account standing in for a real Switchboard/Pyth
  feed in tests. Distinguish "missing functionality" (fix it) from "test
  stand-in" (document it).

## Shape

Lead with the outcome, then support it. Respect a length or time budget, cut
anything that doesn't earn its place, and match the depth to the audience.
