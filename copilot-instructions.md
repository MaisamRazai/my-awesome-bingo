# Copilot Instructions  Soc Ops

AI-guided development for the Social Bingo game. These instructions help Copilot understand the codebase, architecture, and design guidelines.

## Development Checklist

Before committing, verify:
- [ ] Lint passes: 
pm run lint
- [ ] Tests pass: 
pm run test
- [ ] Build succeeds: 
pm run build

## Project Overview

**Soc Ops** is a social icebreaker bingo game for in-person mixers. Players find people matching question prompts and mark their 55 bingo card to get 5 in a row (horizontal, vertical, or diagonal).

**Tech Stack:**
- React 19 with TypeScript
- Vite 7 for bundling
- Tailwind CSS 4 (latest)
- Vitest for testing

## Architecture

### Game Logic (src/utils/bingoLogic.ts)
Core algorithms for:
- **generateBoard()**: Creates randomized 55 grid with 24 unique questions + 1 free space (center)
- **toggleSquare()**: Marks/unmarks squares (free space always stays marked)
- **checkBingo()**: Detects winning patterns (rows, columns, diagonals)
- **getWinningSquareIds()**: Returns winning line's square IDs for highlighting

### Game State (src/hooks/useBingoGame.ts)
Custom hook managing:
- GameState: 'start' | 'playing' | 'bingo'
- Board array of BingoSquareData
- localStorage persistence

### Components
- **StartScreen**: Welcome screen with start button
- **GameScreen**: Main game UI with board and instructions
- **BingoBoard**: 55 grid layout
- **BingoSquare**: Individual clickable square
- **BingoModal**: Victory celebration overlay

### Types (src/types/index.ts)
`	ypescript
BingoSquareData { id, text, isMarked, isFreeSpace }
BingoLine { type, index, squares }
GameState: 'start' | 'playing' | 'bingo'
`

### Questions (src/data/questions.ts)
24 social prompts for discovering common traits (e.g., "bikes to work", "speaks 2+ languages", "can juggle").

## Design Guidelines

### Tailwind CSS 4
- Use latest utilities from Tailwind v4
- Leverage CSS variables for consistent theming
- Grid-based layout (55 squares)
- Responsive design for mobile and desktop

### Frontend Style
- Clear, engaging UI that encourages social interaction
- Accessible buttons and touch targets (44px minimum)
- Visual feedback on square selection
- Celebratory modal for wins

## Common Tasks

### Adding Questions
Edit src/data/questions.ts  Add to questions array (keep it social and discovery-oriented).

### Modifying Game Rules
Update logic in src/utils/bingoLogic.ts  Add corresponding tests in ingoLogic.test.ts.

### Styling Changes
Use Tailwind classes in component files. Follow mobile-first responsive design.

### State Management
Changes to game flow go in src/hooks/useBingoGame.ts. Persist to localStorage for resume functionality.

## Testing

Run 
pm run test to execute Vitest suite (currently 21 passing tests covering bingoLogic).

When adding features:
1. Write tests first (TDD preferred)
2. Implement logic
3. Test in dev server (
pm run dev)

## Deployment

Push to main branch  GitHub Actions auto-deploys to GitHub Pages.

Build output goes to dist/ directory.

