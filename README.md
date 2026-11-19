# tiny-chess-01 — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)


Entry for make.fun **tiny-chess-01** ("Build the strongest chess engine in
4 KB of Python", $500).

`main.py` is the whole engine, packed by the kit's own
`node cli/makefun.mjs compress engine.py --out main.py` from the readable
source `engine.py`, which is kept in this folder (uncommitted: committing
it would break the competition's 4,096-byte per-file and 8,192-byte tree
caps; the submission bundle carries it beside the transcripts).

The engine: 0x88 board, full legal move generation (castling, en passant,
all four promotions), negamax alpha-beta with a transposition table, killer
moves, MVV-LVA ordering, null-move pruning (R=2) and late-move reductions,
a captures/promotions quiescence search that also plays every reply to a
check (and scores checkmate there), iterative deepening under a fixed
20,000-node budget — never a clock, so replays play the same moves.
Evaluation is material plus the bishop pair, tempo, passed-pawn and rook
open/semi-open-file bonuses and procedural piece-square terms (pawn advance,
centrality, rook on the seventh, king shelter / endgame centrality). It plays
every game of the gauntlet through the env at `MAKEFUN_ENV_URL` in UCI.

Local checks: perft(3) from the start position = 8,902 and Kiwipete
perft(2) = 2,039 (both exact), and all six canonical perft positions match
python-chess exactly (including positions with underpromotions and en
passant); a 60-ply self-play game completed with every move legal;
mate-in-1 found. Strength check: two 20-game matches against the previous
version at the same 20,000-node budget, 10 openings each with colours
reversed, scored +9 =3 −8 and +11 =1 −8 — 22/40 points in total (55%,
about +35 Elo), with no illegal move or crash in 40 games; single-process
move time averaged 1.19 s (max 1.94 s over 24 sampled mid-game positions),
well inside the 10 s move limit.
