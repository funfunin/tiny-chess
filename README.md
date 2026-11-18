# tiny-chess-01

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/funfunin/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/funfunin/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in at most 4,096 bytes of Python. Entry for
[make.fun bounty tiny-chess-01](https://make.fun/bounty/tiny-chess-01):
the strongest engine in 4 KiB, judged by playing the house gauntlet
(alpha-beta depth-2/3/4 and node-limited 100k–2M engines).

## Engine

`main.py` is the whole program (packed with `makefun compress` from the
readable `src.py` beside it): a 0x88 board, alpha-beta with iterative
deepening, quiescence over captures, promotions and check replies, a
transposition table, killer moves, MVV-LVA capture ordering, formula
piece-square tables with phase-interpolated king safety, bishop-pair
bonus, and repetition / fifty-move awareness. It searches to a fixed
node budget (60,000 nodes per move, never a clock), so replayed trials
play the same moves. It plays every game through the env API
(`POST /game`, `/move`, `/resign`) and exits when the trial is over.

## Practice result

Practice trial-0 (6 games vs depth-2 to nodes-500k): **4 wins, 0 draws,
2 losses** — about **1,450 Elo** on the gauntlet anchors, above the
1,154 practice floor and the sunfish baseline (~1,365). Wins against
depth-2, depth-3, depth-4 and nodes-100k; losses to nodes-250k and
nodes-500k.

## Files

- `main.py` — packed entrypoint (≤ 4,096 bytes)
- `src.py` — readable source that `makefun compress` packs
- `LICENSE` — MIT
