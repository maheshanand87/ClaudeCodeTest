# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working in this repository.

## Repository purpose

A collection of browser-playable web games and projects. Each project is a self-contained HTML file with inline CSS and JS — no build step, no dependencies, no server required. Open any file directly in a browser.

## Git workflow

After every code change, commit and push to GitHub (https://github.com/maheshanand87/ClaudeCodeTest) before reporting the task as done:

```bash
git add <file>
git commit -m "Descriptive message"
git push
```

Use clean, descriptive commit messages that explain what changed and why. Do not batch multiple changes into one commit — commit and push each logical change as it is completed.

## Project conventions

- **One file per game/project** — all HTML, CSS, and JS lives in a single `.html` file.
- **No external dependencies** — no CDN links, no npm, no bundlers.
- **Dark theme palette** — background `#1a1a2e`, surface `#16213e`, accent red `#e94560`, accent teal `#a8dadc`.

## Architecture of `tictactoe.html`

The JS uses two separate board representations:
- `board[]` — the live game state, mutated by `applyMove()`
- The `minimax()` function receives a copy `b` and mutates it in-place during tree search, restoring values after each recursive call (no board cloning).

`checkWinner()` checks the live `board[]`; `checkBoardResult()` is the minimax-only variant that checks an arbitrary board array `b`. Both use the same `WINS` constant. Keeping these two functions separate avoids side effects during AI search.

The computer always plays as O. `applyMove()` triggers `computerMove()` via `setTimeout(..., 300)` after the human's move so the UI updates visibly before the AI responds.
