# Tiny Chess: a compact alpha-beta engine in 4 KB of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A from-scratch chess engine that plays the make.fun tiny-chess-01 gauntlet
through the env at MAKEFUN_ENV_URL. The readable source is packed into
main.py with makefun compress; main.py alone is the engine.

How it plays: negamax alpha-beta search with iterative deepening under a
fixed node budget (never a clock, so replays match), a transposition
table, quiescence search over captures, promotions and check evasions,
check extensions, and MVV-LVA plus killer-move ordering. Evaluation is
material plus piece-square tables with a tapered king table, the bishop
pair and doubled-pawn penalties, on a 0x88 board with Zobrist hashing
and repetition detection inside the search.
