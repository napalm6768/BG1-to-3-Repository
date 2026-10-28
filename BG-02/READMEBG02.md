# BG-02: Battleship (Complete Gameplay)

A two-player Battleship game that runs in one browser window. Two people share one computer and take turns.

**Play it:** https://YOUR-USERNAME.github.io/YOUR-REPO/battleship.html
(Replace this link with your GitHub Pages link, or download `battleship.html` and open it in a browser.)

## Goal

Sink all 5 of your opponent's ships before they sink yours.

## How to play

1. **Place your fleet.** Each player secretly places 5 ships on a 10×10 grid: Carrier (5), Battleship (4), Cruiser (3), Submarine (3) and Destroyer (2). Ships go across or down and cannot overlap or go off the board.
2. **Take turns firing.** Click one square in Enemy waters. You get one shot per turn, even after a hit.
3. **Read the result.** A red dot is a hit and a white dot is a miss. A ship is sunk when every one of its squares has been hit.
4. **Pass the device.** After you fire, the turn passes by itself after 3 seconds, or click **Pass now**. A cover screen hides the boards until the next player clicks "I'm ready".
5. **Win.** The first player to sink all 5 enemy ships wins.

## Controls

| Control | What it does |
| --- | --- |
| Click a square (setup) | Place the next ship |
| R key or Direction button | Rotate the ship (across / down) |
| Randomize | Place the whole fleet automatically |
| Undo last ship | Remove the most recent ship |
| Click a square (battle) | Fire at that square |
| Pass now | Skip the 3-second wait and pass the turn |
| Restart (click twice) | Reset everything and start over |
| ? button | Show the rules at any time |

## Bad actions the game blocks

| Bad action | What happens |
| --- | --- |
| Wrong turn: clicking a second square after you already fired | Red message: your turn is over |
| Wrong turn: ending your turn without firing | Red message: fire a shot first |
| Illegal move: placing a ship that overlaps or goes off the board | Red message: illegal placement |
| Illegal move: clicking your own fleet board during battle | Red message: fire at Enemy waters instead |
| Repeated click: firing at a square you already fired at | Red message: you already fired there |
| Repeated click: double-clicking through the cover screen | "I'm ready" stays disabled for about 0.7 seconds |

## Six checks

| # | Check | How I tested it | Expected result | Result |
| --- | --- | --- | --- | --- |
| 1 | Legal move | Fire at a new square | Red or white dot and a result message | |
| 2 | Wrong turn | Fire, then click another square. Also click End turn before firing | Red warning, no second shot, no skipped turn | |
| 3 | Illegal move | Place an overlapping ship in setup | Red "Illegal placement" message | |
| 4 | Repeated click | Click the same square twice. Double-click End turn | "Already fired" message. Cover screen is not skipped | |
| 5 | Ending | Sink all 5 ships | Winner screen with Play again | |
| 6 | Restart | Click Restart twice in the middle of a game | Empty boards, Player 1, back to ship placement | |

## Problem I fixed

**Problem:** Double-clicking End turn could send the second click to the "I'm ready" button on the cover screen, so the handoff screen was skipped and the next player saw the board right away.
**Fix:** The "I'm ready" button is now disabled for about 0.7 seconds when the cover screen appears.
**Retest:** Double-clicking End turn now leaves the cover screen up until the button turns on.

## One move, from click to screen

1. **Click:** The click handler on the Enemy waters board reads which square was clicked.
2. **Rule check:** It checks whether that square was already fired at, and whether this player has already taken a shot this turn. If either is true, it shows a warning and stops.
3. **Stored data:** Otherwise it calls `fire(i)`, which checks whether an enemy ship is on that square and saves `'h'` (hit) or `'m'` (miss) in the current player's `shots` data.
4. **Screen:** `render()` redraws both boards from the saved data, shows the result message, and starts the 3-second countdown.

## Files

- `battleship.html`: the whole game (HTML, CSS and JavaScript in one file)
- `README.md`: this document
