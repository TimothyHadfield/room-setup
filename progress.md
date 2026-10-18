# Room Planner — progress

## START HERE
Last updated 2026-10-16. Read order: this file, then `CLAUDE.md` (file map, how to run, traps).

## Goal right now
None active. The app is finished and published; work only on what Tim asks.

## Status
| Area | State |
|---|---|
| App (`index.html`) | Working on laptop. Live at https://timothyhadfield.github.io/room-setup/ |
| Phone (390px) | Loads with no errors or page overflow, but the canvas is only about 93px wide (layout is laptop-first) |
| Tests | None (single-file app). Verified with phone-view `--eval` |
| 2026-10-17 site icon | `icon.svg` (tab) + `apple-touch-icon.png` 180px (iPhone home screen): white floor plan (walls, door swing, bed) on the accent blue |

## Authorized next steps
None.

## Standing instructions
- From the README: "best on a laptop (drag with a mouse, keyboard shortcuts)".

## Traps
- See `CLAUDE.md` Traps.

## Decisions
- 2026-10-16 sweep: Layout Check now flags furniture inside a door swing or closet front (it said "All clear" before, contradicting the README). Arrow keys no longer move a locked item. Ctrl/Cmd+R no longer rotates the selected item before reloading. Under 700px the header and status bar scroll sideways instead of cutting off Save/Load/Clear. Added aria-labels, meta description and an empty favicon (stops a 404). Desktop pixels unchanged (pixel diff vs live).

- 2026-10-17: all 9 browser alert/confirm/prompt dialogs replaced by one in-app dialog (`appAlert/appConfirm/appPrompt`, styled from the Help modal); same Cancel/OK meaning; a capture-phase key guard stops app shortcuts while it is open. Desktop pixels unchanged when closed (pixel diff).

## NOT verified
- Real iPhone touch: dragging, double-tap to add a corner (`dblclick` on touch), the inline number editor with the iOS keyboard.
- PNG export and Load File on iOS Safari.

## Rejected / parked
- Parked for Tim: a real phone layout (stack the sidebar under the canvas, or similar). It changes layout, so it's his call.
- Parked for Tim: should "Lock position" also block rotation? The canvas ↻ handle is hidden for locked items, but the R key and the panel rotate buttons still rotate them.
