# Tiny Chess: a compact alpha-beta engine in 4 KB of Python

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
