# Puzzle Game Solver

Browser tool for setting up a **stack-sort / water-sort** style tube puzzle and finding a solution step by step.

Open `stack_sort_board.html` in a browser (Chrome, Edge, etc.). No install or build step is required.

---

## 1. Start the game (choose tube count)

1. On the first screen, set **Number of tubes** (allowed range: **4–16**).
2. Click **Submit** to build the board.
3. Or click **Load from file** to restore a previously saved puzzle (JSON).

Each tube holds up to **4** color blocks. Empty tubes are allowed (useful as working space while sorting).

### Resetting the tube count

After you submit, the tube-count screen is hidden. **There is no in-app control to change the number of tubes.**

To pick a different tube count:

1. **Refresh the page** (F5 / Ctrl+R / Cmd+R).
2. Enter the new number of tubes.
3. Click **Submit** again.

Refreshing clears the current board and solution. Use **Save** first if you want to keep the **initial** puzzle (the same state **Start over** restores).

---

## 2. Fill the board (initialize colors)

After Submit you see the tubes and a **Colors** palette on the side.

1. **Drag** a color from the palette.
2. **Drop** it onto a block slot in a tube to set or replace that block.
3. Repeat until the board matches your puzzle (or leave unknowns as `?` — see below).

You can also leave some slots empty (no color) when that matches the real game.

### Unknown (`?`) blocks

The palette includes a **`?`** color for blocks you have not revealed yet (e.g. covered layers in the mobile game).

- Drop `?` onto a slot when the real color is still unknown.
- As you step through the solution, moves may **unveil** `?` blocks that need a real color before you can continue.

---

## 3. Solve

1. Click **Solve**.
2. Wait while the solver searches (status shows *Solving…* and depth).
3. When a solution is found, the panel shows the **total steps** and the current move.

If no solution is found, see **Dead ends** below.

---

## 4. Step through the solution

The board shows the state **before** the current move. Arrows mark the move:

- **↑ out** (red) — tube whose top block(s) leave
- **↓ in** (green) — tube that receives them

### How to go to the next / previous step

- **Next step:** click the tube marked **↑ out** (the blocks that are about to move), **or** press the keyboard **→** (Right Arrow) key.
- **Previous step:** press the keyboard **←** (Left Arrow) key.

Keep advancing until the panel shows **Done.**

### When a `?` block is unveiled

If a move reveals an unknown block:

1. Drag a real color from the palette onto that `?` block to replace it.
2. Press **Solve** again to continue from the updated board.

Guessing the wrong color for a `?` can lead to a **dead end** (see below).

### Dead ends

When the solver cannot finish from the **current** board, the UI explains which case you hit:

**Mid-path dead end** (you already stepped through some moves, then replaced a `?` and pressed Solve again):

- The current branch has no solution.
- Press **Start over** to go back to the **initial** board.
- Colors you set by drag & drop (including `?` replacements) are **kept** on that initial state.
- Choose different colors if needed, then press **Solve** and try another path.

**Dead end at the very beginning** (Solve fails on the starting board, before any successful mid-path continue):

- Either this puzzle has **no solution at all**, or the **initial setup is invalid** (wrong colors, wrong empties, etc.).
- Check the board against the real puzzle and fix it, then press **Solve** again.

---

## 5. Start over, Save, and Load

| Control | What it does |
|--------|----------------|
| **Start over** | Restores the board to the original layout. Move playback is cleared. Drag-and-drop edits (including `?` colors you filled in) stay on that original. |
| **Save** | Downloads a JSON file of the **initial state** — the same board you get when you click **Start over** (not the mid-solution step currently on screen). Includes tube count and any `?` colors you already replaced by drag & drop. |
| **Load** | Opens a saved JSON and rebuilds that initial board (also available on the first setup screen). |

**Start over** does **not** change the tube count. To change how many tubes you have, **refresh the page** and submit a new count (see above).

If you are mid-solution and click **Save**, the file still stores the Start-over board, so you can reload later and solve again from that baseline.

---

## Quick flow

```
Open HTML → choose tube count → Submit
        ↓
Drag palette colors onto tube blocks (use ? if unknown)
        ↓
Solve → click ↑ out tube or use ← / → to step
        ↓
If ? unveiled → drop a real color → Solve again
        ↓
Dead end mid-path? → Start over (kept ? colors) → try again
Dead end at start? → no solution or invalid setup — fix board
        ↓
Done.
        ↓
Need a different tube count? Refresh the page and start again.
```
