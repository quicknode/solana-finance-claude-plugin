# Quasar Guidelines (Quasar Programs)

Quasar is a zero-copy, zero-allocation Solana framework with Anchor-like ergonomics. Programs use the `quasar-lang`, `quasar-spl`, and `quasar-metadata` crates and are `no_std`. Read this alongside the general rules in [SKILL.md](SKILL.md). Most of the Anchor rules in [RUST.md](RUST.md) — checked arithmetic, onchain financial math, PDA bumps, no magic numbers — still apply. This file covers what is different in Quasar, especially its type system.

## Quasar has a `Vec` — do not claim otherwise

Quasar's prelude re-exports bounded, zero-copy collection types from the `zeropod` crate:

```rust
// quasar_lang::prelude (via quasar_lang::pod → zeropod::pod)
pub use crate::pod::{PodString as String, PodVec as Vec};
```

So in a Quasar program, `String` and `Vec` already mean Quasar's bounded types:

- **`Vec<T, const N: usize, const PFX: usize = 2>`** (`PodVec`) — a fixed-capacity vector. `N` is the capacity (maximum element count). The element `T` must be a fixed-size zero-copy type (`ZcElem`) — e.g. `u8`, `[u8; K]`, or one of the alignment-1 `PodU*` scalar wrappers below. The third generic is the length-prefix width in bytes, defaulting to `2` (a `u16` prefix).
- **`String<const N: usize, const PFX: usize = 1>`** (`PodString`) — a fixed-capacity UTF-8 string. `N` is the capacity in bytes. The second generic is the length-prefix width, defaulting to `1` (a `u8` prefix, so stored lengths up to 255). For longer strings, set it explicitly, e.g. `String<1024, 2>` for a `u16` prefix.

The capacity is **mandatory**: bare `String` / `Vec` (without `<N>`) are not accepted. Always supply `<N>`.

This is Quasar's equivalent of Anchor's `#[max_len(N)]` — the capacity lives in the type, not in an attribute. Where Anchor writes:

```rust
#[max_len(50)]
pub name: String,
```

Quasar writes:

```rust
pub name: String<50>,
```

## Constraints on dynamic fields

- **Fixed-size fields must precede dynamic ones.** In an account struct, put every fixed-size field (`u8`, `u64`, `Address`, `[u8; K]`, …) first, then the `String<N>` / `Vec<T, N>` fields.
- **No *nested* dynamic types.** A `Vec` of a dynamic element (e.g. `Vec<String<50>, N>`) is not supported — the element must be a fixed-size POD. This is the real limitation: "Quasar has no Vec" is wrong; "Quasar has no Vec of a *dynamic* element" is correct. (It is why a port of an Anchor account with `hobbies: Vec<String>` has to drop or restructure that field.)

## Other prelude types

- **`Address`** — Quasar's public-key type. Use `Address` (not `Pubkey`) in account fields and in `#[seeds(...)]`, e.g. `#[seeds(b"favorites", user: Address)]`.
- **Alignment-1 POD scalars**, re-exported from `zeropod::pod`: `PodBool`, `PodU16`/`PodU32`/`PodU64`/`PodU128`, `PodI16`/`PodI32`/`PodI64`/`PodI128`, and `PodOption`. Use these when a field (or a `Vec` element) needs guaranteed 1-byte alignment in a zero-copy layout. Native `u8`/`u64`/etc. are fine as plain account fields and as instruction-handler arguments.

## Macros and entrypoints (vs Anchor)

- `#[program]` module, `declare_id!(...)`, and `#[instruction(discriminator = N)]` on each handler.
- Account structs use `#[account(discriminator = N, set_inner)]` and `#[seeds(b"prefix", field: Address)]`.
- The instruction context type is **`Ctx<T>`**, not Anchor's `Context<T>`. Handlers return `Result<(), ProgramError>`.
- Programs are `no_std`: begin `lib.rs` with `#![cfg_attr(not(test), no_std)]`.
- CPI uses `quasar_lang::cpi::{InstructionAccount, InstructionView, Seed, Signer, CpiCall, CpiDynamic}` and `quasar_lang::remaining::RemainingAccounts`. Sysvars come from `quasar_lang::sysvars::Sysvar`.
- SPL Token / Token Extensions and Metaplex metadata helpers live in `quasar_spl` and `quasar_metadata`.

## Fight for Truth about Quasar

Per the truthfulness rules in SKILL.md: do not write "Quasar has no `Vec`" or "Quasar has no dynamic types". It has bounded `Vec<T, N>` and `String<N>`; the genuine limitations are (1) no nested dynamic types and (2) fixed-size fields must come before dynamic ones. Before writing any claim about Quasar's type system, grep the `quasar_lang` prelude or an existing Quasar example to confirm it.
