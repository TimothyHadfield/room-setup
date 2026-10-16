# Room Planner (repo: room-setup)

A to-scale bedroom layout planner Tim built for himself: draw the room (rectangle, L-shape, custom
corners), drag furniture around, and a "Layout Check" flags overlaps, items through walls, and
blocked clearance zones (desk chair, drawers, door swing, closet front). No accounts, no backend.

- **Live:** https://timothyhadfield.github.io/room-setup/ (GitHub Pages, deploys from `main`, root folder)
- **README** says "best on a laptop (drag with a mouse, keyboard shortcuts)". It is a showcase README for the public repo.
- Handoff state: `progress.md` (read START HERE first).

## File map
- `index.html`: the whole app. One file, inline CSS + vanilla JS + `<canvas>`, no libraries, no build step.
  - `PRESETS` (top of script): furniture sizes in inches and default clearances `cl:{front,back,left,right}`.
    `fixture:true` = Door / Closet / Window (sit on a wall; skip wall/overlap checks).
  - Geometry → `itemStatus()` (layout check) → units (`fmtLen`, `toField`/`fromField`) → view/render →
    inline dimension editor → pointer/keyboard → undo/save → setups → sidebar panels → boot (`init()`).
- `README.md`, `docs/screenshots/*.png`: the public showcase (screenshots are referenced by the README).

## Data
- Everything lives in the browser's `localStorage`, key `roomPlannerSetups` = `{activeId, setups:[{id,name,data,updatedAt}]}`,
  where `data` is a JSON snapshot `{room:{poly,locked}, items, settings, unit}`. All lengths are stored in **inches**.
- Older single-layout key `roomPlanner` is migrated once on first load. `normalizeState()` repairs old or hand-edited saves.
- Save File / Load File = the same snapshot JSON; Load adds it as a new setup.

## Run and test locally
- `python -m http.server 8112` in the repo folder, then open http://localhost:8112/.
- There is **no test suite**. Verify with `node ~/.claude/tools/phone-view.mjs http://localhost:8112/ --desktop --eval "..."`:
  the app's functions are globals, so e.g. `addPreset(findPreset('Twin Bed'))`, then set `state.items[n].x/y`,
  `refreshPanels()`, and read `document.getElementById('issuesBody').innerText`.
- Default room: 156" x 132", Door at (78,132) rotated 180 (swing into the room), Closet at (106,0).

## Traps
- Rotation is in 90° steps only; `footprint()` swaps w/h for 90/270. "Front" is +y at rot 0.
- Door clearance is drawn as an arc but checked as its bounding square, so the far corner of the square counts as blocked.
- Fixtures sit half outside the room on purpose; never add a "sticks out past a wall" check for them.
- At phone width the 300px sidebar leaves the canvas about 93px wide. The header and status bar scroll sideways
  under 700px (added 2026-10-16) so nothing is cut off; a real phone layout is Tim's decision (see progress.md).
- Wall-length locks: `state.room.locked[i]` is wall i→i+1. Adding/deleting a corner resets all locks.
- No accounts, so no `claude-test` login is needed.

## Standing instructions
- Tim owns looks, wording, layout and names. Desktop pixels must stay identical unless he asks
  (the 2026-10-16 sweep checked this with a pixel diff against the live site).
