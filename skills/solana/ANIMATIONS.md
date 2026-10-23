# Animated Account Diagram Guidelines

**These build on [DIAGRAMS.md](DIAGRAMS.md)** and apply whenever account diagrams are animated for a screen: a talk, a docs site, a video. An animation is the printed figures stepped through: each key press plays the next thing the program does, as accounts are created, fields change and tokens travel along their arrows. DIAGRAMS.md still governs what a box, a dot, a seed list or an arrow looks like; this file adds what changes when the figure moves and the reader is an audience.

Write the animation as code, not as a video: a scene file that places the accounts and lists the steps as data (create this account, set this field, transfer this amount), and an engine that draws the scene and animates each step. Each step's end state is computed by replaying its actions without motion, so going back, jumping, or cutting an animation short lands on the same picture the forward animation ends on. A video, when one is wanted, is a recording of the page.

## The animation matches its source

- **Every person, asset, event, order of events and number is the source's.** An animation of a book chapter or a docs page shows that chapter's story. Never invent a scenario, swap one person for another, add an event the source doesn't describe, or show a number it doesn't state. One talk liquidated a different borrower in a different market from the chapter it animated; every number checked out, and none of them could be found in the book.
- **A balance may follow from the source's numbers by plain arithmetic.** Mark it in a comment in the scene file. A number the source leaves out stays out: describe it in words, or leave the field undrawn.
- **A minor branch may be left out for time, never replaced.**
- **Steps follow the handler's real order, not the prose's.** If the handler writes the account's state and runs its custody check before either transfer, the animation does too. Read the handler, not only the chapter.

## Before any Solana, say what people want

An audience may not have read the chapters before this one. Open on the people and the product, not the chain:

1. What each person wants, one large panel each: the buyer wants the asset below the market price, the writer wants to be paid for waiting.
2. How the product gives both of them that.
3. The product's own terms, defined where the next slide needs them (see below).
4. "Now let's build it on Solana", and then the diagram.

## Open the diagram slowly

- **The first step is the empty network.** "This is Solana Devnet", with the curve and nothing else, and one idea a line beneath it: it is a global computer; financial products are programs that run on it; all data is stored in accounts; each account has an address; some addresses are public keys, others are made from seeds chosen by programmers.
- **Then one account at a time.** The first person's wallet, then the mints when a token is first needed, then that person's token accounts, then what they want, then "Programs are accounts too", which leads into the first handler.
- **A person appears in the step where they first do something**, with the accounts that step uses, not in a crowd at the start. Their role joins their name when they take it on: "Alice" becomes "Alice (writer)" in the step where she writes.
- **A term is defined where the animation first needs it**: not before, where it means nothing yet, and not after, where it was already used unexplained. A call is defined just before someone writes one; "covered" in the step where the collateral lands in the vault; "in the money" in the step where the holder exercises.

## The screen has no print limits

- **Draw on a 16:9 canvas.** The extra width puts every public-key account beneath the one curve; there is no continued curve.
- **The curve runs to both edges of the frame**, continuing along its own tangent past the canvas, so the frame never shows its end.
- **One series bar sits on top of every slide**, the diagrams included, and nothing in the diagram covers its rule.
- **Accounts may be filled cards on a dark ground**, one fill per account kind, so the kind reads from the colour as well as the icon. A faded account is a dark slab. The one accent stays the step's action.

## Each step says what it does

- **A step has a title with one highlighted keyword**: `Maria runs [collect_fees()]`, `Bob pays Alice the [premium]`. The step number sits in a corner as `// STEP n`.
- **Its caption is at most four lines**, and may keep line breaks for a list of short facts.
- **The running handler sits on a full-width accent band with a ▶ marker, in bold.** Set it in a face that has a real bold weight: a monospace face without one gets a made-up bold from the browser, which is too faint to find from the back of a room. Only the running handler is bold; handler names elsewhere are set like the words around them. When a handler calls another program, that program's handler lights too.
- **Every account a step touches is drawn in full** before the step plays on it: an arrow never lands on a faded slab, and a field never changes inside one.

## Motion means value moved

- **A transfer draws its arrow, then a coin rides it** while the source balance counts down and the destination counts up. Tokens move along transfer arrows, never along the curve.
- **One arrow on screen at a time** when a handler makes several transfers: each replaces the last, so the audience follows the current one.
- **A changed value stays marked.** It counts from its old value to its new one, then settles bold on the accent band until the next step starts, so the new number is easy to find once it stops moving.
- **A new account grows in with a `NEW` badge that stays for the whole step.** A closed account is marked `CLOSED` and fades out, taking the step's arrows with it.
- **A step no program takes**, a price moving or time passing, lights no handler.

## Other possible endings

- **An alternative ending branches off the main story and returns to it.** The cancelled offer starts from the open offer; the expired option starts from the purchase, not from the exercise before it. The jump between them fades out and back in, so it never reads as the program doing something.
- **Open such a step plainly**: "It's possible that nobody takes the offer", "It's possible NVDAx stays at $165". Not "Another future", and not "Future B".

## Slides between the steps

- **One icon means one idea throughout a talk.** Reuse it where the idea comes back, and never give it to anything else.
- **Animate a change that is the point of the slide.** When a price rallies and a fund's weights drift, the bar grows; when the losing side of a bet pays the winners, the loser's bar drains into theirs. Open on the state before, hold it long enough to read, then move.
- **A part too thin to hold its words is drawn at its true width**, with its label outside the bar and an arrow to it.

## Check it

- **Render every step's end state and look at it.** Text overflowing a box, an arrow crossing an account, a faded account receiving tokens, a caption past four lines: none of these shows up in the scene file.
- **Record the whole thing once**, holding each step as a presenter would, and watch it.
