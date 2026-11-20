# Tiny Chess — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine that fits in 4,096 bytes of Python and plays its games
through the make.fun trial env. It is built around one rule: never crash,
never play an illegal move. Every move is chosen by a negamax search with
alpha-beta pruning, a transposition table, quiescence over captures and
checks, MVV-LVA and killer move ordering, and material plus piece-square
evaluation with an endgame king table. The search runs to a fixed node
budget — never a clock — so a replayed trial plays the identical moves.
Candidate moves are always intersected with the env's own legal move
list, and any internal failure falls back to a legal move, so a game is
never lost to a broken engine.
