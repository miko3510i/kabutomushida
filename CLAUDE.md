# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Kabutomushi-da (カブトムシ打)** is a browser-based typing game where players type programming terms or UNIX commands as beetles (kabutomushi) carry them across the screen. The entire application is self-contained in a single `index.html` file with inline CSS and JavaScript.

## Development Commands

```bash
# Run locally - no build required
# Option 1: Direct browser
open index.html

# Option 2: Python server (for browser security features)
python3 -m http.server 8000
# Then visit: http://localhost:8000/index.html

# Interactive testing with Playwright
npx playwright open index.html      # Manual testing
npx playwright codegen index.html    # Generate test scripts
```

## Architecture & Core Concepts

### Game State Management
The game uses a simple state machine with these core variables:
- `timeLeft`: 60-second countdown timer
- `activeBeetles`: Map tracking beetles on screen (only one active at a time)
- `currentBeetleId`: Enforces single-beetle constraint for focused gameplay
- Two game modes: `programming` (42 terms) and `unix` (45 commands)

### Key Architectural Patterns

1. **Single-File Architecture**: All HTML, CSS, and JavaScript live in `index.html` for zero-dependency deployment
2. **Event-Driven Design**: Game loop via `setInterval`, beetle lifecycle via `setTimeout`, CSS animations for movement
3. **Word Pool System**: Each mode has words[] array and meanings{} object mapping terms to Japanese explanations
4. **Visual Positioning**: Beetles follow `--beetle-track-center` CSS variable (currently 0.465) for vertical alignment with background trunk

### Critical Functions & Flow

```javascript
// Core game loop
startGame() → spawnBeetle() → handleTyping() → updateScore()/handleMiss()
                    ↓
            removeBeetle() → checkGameEnd()
```

### File Organization
- `index.html`: Complete application (UI, styles, game logic)
- `assets/`: 7 beetle sprites (kabutomushi.png + 6 variants)
- `haikei/`: Background images (tree trunk with lane overlay)
- `images/`: Screenshots and visual references
- `AGENTS.md`: Development guidelines

### Recent Changes Context
- Positioning system refactored from `--beetle-groundline` to `--beetle-track-center`
- Added mode selector for switching between programming terms and UNIX commands
- Beetles now center vertically using `centerY - beetleHeight / 2` calculation
- Background uses `plant_eda1_lane.png` for visual beetle pathway

## Testing & Quality

**Manual Testing Checklist:**
1. Both game modes spawn correct word pools
2. Beetle alignment with tree trunk visual
3. Score calculation includes combo bonuses
4. Miss counter stops game at 5
5. Timer countdown and game over states
6. Mobile responsive layout

**Before Publishing:**
- Test in both modes
- Verify beetle path alignment
- Capture screenshot for `images/` if UI changes
- Maintain 2-space indentation
- Keep CSS properties descriptive (`--beetle-track-center`)

## Commit Style

Follow existing pattern: `verb: description`
- `feat:` new features
- `style:` visual changes  
- `fix:` bug fixes

Example: `style: raise beetle flight path`