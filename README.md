# tiny-chess-01 entry

A chess engine in at most 4 KB of Python, built for make.fun's tiny-chess-01 bounty.

`main.py` is the packed entrypoint: a negamax alpha-beta engine with quiescence search,
check extensions, a transposition table, null-move pruning, MVV-LVA and killer move
ordering, repetition-aware scoring, and a material + piece-square-table evaluation with
a separate king endgame table. It searches a fixed node budget, so every replay is
deterministic, and it plays through the make.fun environment protocol
(`MAKEFUN_ENV_URL`).

The readable source the entrypoint was packed from ships with the entry's transcripts.

## Design notes

- The board is a 0x88 array and every score is kept incrementally in make/unmake,
  including the Zobrist hash, so the transposition table and the repetition sets
  (positions from earlier in the same game, and positions on the current search path)
  cost almost nothing to maintain.
- Positions the environment has already shown in the current game score as draws
  inside the search, which steers the engine away from repeating a worse position
  and toward repeating a better one.
- The evaluation separates the king's middlegame and endgame tables and switches on a
  simple material phase test, so the king centralises once the queens come off.
