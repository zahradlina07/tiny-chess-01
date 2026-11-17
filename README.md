# tiny-chess-01 entry

A chess engine in under 4 KB of Python, entered in make.fun's `tiny-chess-01`
competition.

`main.py` is a fork of sunfish's 4 KB entry (`nnue_4k/pst_entry.py` at commit
e396948acbd80cdcbad3dccfb07e878fba9df8f4 of github.com/thomasahle/sunfish, by
Thomas Ahle and contributors, GPL-3.0-only).

Changes from upstream:

- The UCI loop and its clock are replaced with a driver for this competition's
  env (`POST /game`, `POST /move`).
- The search is capped by a fixed node budget per move instead of a wall
  clock, so every move is a pure function of the position and the history, as
  the competition's replay rule requires.
- The position is rebuilt by replaying the env's `moves` list from the start
  position rather than parsing a FEN string, which is both smaller and free of
  the board-orientation pitfalls of a from-scratch FEN parser.
- The piece-square tables are rounded to a multiple of 4 to fit the 4096-byte
  cap.
- Dead code, the unused net payload and redundant helpers are removed.

Search, evaluation and move generation are sunfish's.
