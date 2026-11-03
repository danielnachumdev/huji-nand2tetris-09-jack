# nand-09

**Nand2Tetris Project 9 — a Jack tic-tac-toe game** for the Hack platform (keyboard + `Screen` graphics).

Play **X** vs **O** on an `N×N` board, enter moves as `row,column`, and see the grid drawn in the VM / hardware simulator.

## Why this repo?

Project 9 is the first time you write a full application in **Jack** (objects, OS APIs, no low-level HDL). This repo is that deliverable: a small multi-class game instead of a one-file demo.

- Configurable board size (prompted at start; values outside **4–9** fall back to **3×3**)
- Turn-based play with win / tie messaging and optional rematch (`y` / `n`)
- Custom drawing helpers (`Graphics`, `Renderer`) on top of the standard Jack OS

## Quick start

1. Install the [Nand2Tetris software suite](https://www.nand2tetris.org/software) (Jack compiler + VM emulator).
2. Point a local `LOCAL.py` (gitignored) at your Jack compiler binary — see [`AGENTS.md`](./AGENTS.md).
3. Compile the `.jack` sources (helper or official tools):

```bash
python compile.py
# or: JackCompiler .   # from the Nand2Tetris tools, on this directory
```

4. Load the generated `.vm` files in the **VM Emulator** (optional: `loaderVM.tst` runs many `vmstep`s).
5. Run `Main.main` and follow the on-screen prompts.

## What’s in the game

| Piece | Role |
| ----- | ---- |
| `Main` | Welcome, size prompt, rematch loop |
| `Game` / `Board` / `Player` | Turns, empty cells, win checks |
| `Renderer` / `Graphics` | Grid, X/O marks, win highlights |
| `WindowController` / `Utils` / `intArray2d` | Cursor/color helpers, parsing, 2D storage |

Agent and maintainer workflow (compile helper, ignore rules, layout): [`AGENTS.md`](./AGENTS.md).
