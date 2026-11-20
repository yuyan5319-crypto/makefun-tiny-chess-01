# Tiny Chess — a 4 KB Python chess engine

![make.fun competition](https://make.fun/badge/tiny-chess-01.svg)
![rank](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/rank.svg)
![reward](https://make.fun/badge/tiny-chess-01/yuyan5319-crypto/makefun-tiny-chess-01/reward.svg)

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
