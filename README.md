# modification-app — torogao-modapp

A clean-room, from-measurement reimplementation of the systems of the
**Modification App** (build 0.12.3; Godot 4.7.1), built for the Torogao
remake programme by Nice Thoughts Ranch. No assets, text, or code from
the studied game are included: the story structure and tuning in
`data/modapp-dynamics.ron` were measured from the original build (via
GDRE decompilation records) and rebuilt as estate-authored data and
Rust systems.

## What the crate models

- A phone-hub story DAG of 39 nodes, with menus gated by level, time
  slot, and flags, resolved by a per-node state-table resolver.
- A four-slot day clock; a node may only start at its exact slot, and
  starting it consumes the rest of the day.
- The gated TP economy and per-node state deltas: content as data over
  one resolver, never bespoke scene code.

## Dual-target law

The remake programme ships every title on native Linux **and** Android
from this one crate plus its data file. Platform shells bind to the
crate; the systems and data live here only.

## Determinism

Sessions are deterministic: a fixed input stream replays to a fixed
trajectory hash. The trajectory fixture is exercised by the test suite,
and the same hash must match on Linux and Android (the programme's S7
gate).

## Build and test

```sh
cargo build
cargo test
cargo run --bin modapp-smoke   # scripted session; prints the smoke line
```

## License

BSD 2-Clause. See `LICENSE`. The studied game remains the property of
its respective developer; this repository is an independent
reimplementation of measured behaviour.
