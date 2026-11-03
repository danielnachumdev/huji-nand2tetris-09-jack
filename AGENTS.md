# nand-09 – Agent Context

Implementation guide for coding agents changing **nand-09**. Product pitch and player-facing run steps: [`README.md`](README.md).

---

## Orientation

| Question | Answer |
| -------- | ------ |
| What is this? | Nand2Tetris **Project 9** Jack app: graphical tic-tac-toe |
| Source of truth | `*.jack` classes in the repo root (not a Python package) |
| Python role | Optional compile helper only (`compile.py`) |
| Toolchain | Official Nand2Tetris **JackCompiler** + **VM Emulator** |
| Tests | No automated suite; validate by compiling + running in the VM Emulator |
| Secrets / local paths | Never commit `LOCAL.py`, compiler paths, or machine-specific configs |

```text
.
├── Main.jack              # Entry: prompts, rematch loop
├── Game.jack              # Turn loop, win / tie
├── Board.jack             # N×N board over intArray2d
├── Player.jack            # X/O, coordinate input `row,column`
├── Renderer.jack          # Draw board + marks
├── Graphics.jack          # Lines, X, O, clear helpers
├── WindowController.jack  # Cursor / Screen color state
├── Utils.jack             # String → int digit helper
├── intArray2d.jack        # Row/col Array wrapper
├── compile.py             # Deletes *.vm then runs LOCAL.COMPILER
├── loaderVM.tst           # VM Emulator load + many vmstep
├── LOCAL.py               # gitignored — COMPILER path for compile.py
├── README.md              # Marketing / how to play
└── AGENTS.md              # This file
```

Open Dependabot / shared-actions adoption may land separately (do not invent CI commands that are not on `main`).

---

## Develop

### Compile

`compile.py` expects a sibling **`LOCAL.py`** (listed in `.gitignore`) that exports `COMPILER` as the Jack compiler invocation used by `danielutils.cm`:

```python
# LOCAL.py — local only, never commit
COMPILER = "path/to/JackCompiler"  # or the command your machine uses
```

Then:

```bash
python compile.py
```

That deletes existing `*.vm` in `.` and runs `COMPILER`. Official alternative: run the course **JackCompiler** on this directory. Generated `*.vm` are gitignored.

Dependencies of the helper: `danielutils` (and whatever `LOCAL.COMPILER` needs). There is no `pyproject.toml` / lockfile in this repo.

### Run / smoke

1. Open the Nand2Tetris **VM Emulator**.
2. Load this directory’s `.vm` output (or use `loaderVM.tst`).
3. Execute `Main.main`. Confirm size prompt, moves as `row,column`, win/tie text, rematch `y`/`n`.

Do **not** invent HDL, assembler, or OS changes — Project 9 is Jack application code only.

---

## Code notes

- Board size: `Main` asks for `X`; if `X < 4` or `X > 9`, size becomes **3**.
- `Game.new(..., winStreak)` is called with `3`; keep win-check behavior consistent with existing `Game` methods when editing.
- Players: `X = 1`, `O = -1`; empty cells are `0`.
- Prefer small Jack classes with clear ownership (`dispose` where memory is allocated).
- Do not commit `*.vm`, `LOCAL.py`, `.vscode/` junk, or course PDFs (see `.gitignore`).

---

## PRs

If this repo uses semver labels (when CI/semver workflows are present), attach **exactly one** of: `noBump` | `bumpPatch` | `bumpMinor` | `bumpMajor`. Docs-only changes → **`noBump`**.
