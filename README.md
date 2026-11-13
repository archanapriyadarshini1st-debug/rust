# Chess-rust-engine

UCI chess engine in Rust. Clone, build, run — the **S45 NNUE** is already in `nets/default.nnue` and is compiled into the binary.

| | |
|---|---|
| Protocol | UCI |
| Eval | NNUE 768→128×2→1 (S45) with HCE fallback |
| Net | 16M Lichess labels, shards 4+5 |
| vs HCE | 97.5% / 40 games (10+0.1) |
| vs Stockfish 19 `UCI_Elo 2900` | 62.5% / 24 games (10+0.1, Hash=64, 1 thread) |

## Build

Needs a recent Rust (1.70+ is enough).

```bash
git clone https://github.com/archanapriyadarshini1st-debug/rust.git
cd rust
cargo build --release
```

Faster on your CPU:

```bash
make native
```

Binary: `target/release/chess-rust-engine` (or `./chess-rust-engine` after `make native`).

## Run

The engine speaks UCI on stdin/stdout. Drop it into Cute Chess, Arena, Banksia, or any UCI GUI.

```bash
./target/release/chess-rust-engine
```

```
uci
isready
position startpos
go movetime 1000
```

Useful UCI options: `Hash` (MB), `UseNNUE` (default on). The net is embedded; you do not need extra files next to the binary.

Override the net if you want:

```bash
CRE_NNUE_FILE=/path/to/other.nnue ./target/release/chess-rust-engine
```

GPL-3.0-or-later. Original engine code; the architecture follows public chess-programming practice (not a Stockfish/Reckless fork).
