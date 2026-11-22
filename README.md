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

## Design notes

The search budget is a fixed 30,000 nodes per move, never a wall-clock
deadline. The finals replay every game move for move, so a clock-based
engine could return a different move on a faster or slower machine and
fail the replay; a node cap makes the chosen move a pure function of
the position. Iterative deepening still applies — it simply stops when
the node budget is spent, and the best move from the last completed
depth is the one that gets played.

The transposition table is keyed on the Zobrist hash and stores depth,
bound type and the best move found. Mate scores are stored relative to
the root and re-based by ply on the way in and out, so a mate found
deep in one branch is still quoted correctly when the same position is
reached again by a different route. Positions where the side to move
is in check get a one-ply extension: those are exactly the nodes where
a shallow search most often misevaluates, and extending only there
buys depth where it matters instead of spending nodes everywhere.

Quiescence search is deliberately narrow: it follows captures and
promotions, and when the side to move is in check it follows every
legal evasion, so a leaf is never scored in the middle of a forced
sequence. It does not chase checks or quiet positional moves — under a
fixed node budget those nodes earn more inside the main search. Move
ordering carries most of the efficiency: transposition move first,
then captures by MVV-LVA with promotions scored in the same tier,
killers, and a history table for the quiet moves.

Local results back these choices. Against the kit's practice gauntlet
on this machine, trial-0 scored Elo 1364 and trial-1 — different
openings, colours swapped — scored about 1450. The competition floor
is 1154, so the margin is roughly 200 to 300 Elo. That headroom is the
point of the node budget: grading hardware may run faster or slower,
but the moves themselves stay identical, so the score should hold.
