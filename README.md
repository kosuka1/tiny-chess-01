# tiny-chess-01 entry

A chess engine in at most 4 KB of Python, built for make.fun's tiny-chess-01 bounty.

`main.py` is the packed entrypoint: a negamax alpha-beta engine with quiescence search,
check extensions, a transposition table, null-move pruning, MVV-LVA and killer move
ordering, repetition-aware scoring, and a material + piece-square-table evaluation with
a separate king endgame table. It searches a fixed node budget, so every replay is
deterministic, and it plays through the make.fun environment protocol
(`MAKEFUN_ENV_URL`).

The readable source the entrypoint was packed from ships with the entry's transcripts.
