# Object Bingo

A small browser game for practicing how to read JavaScript objects. Every square on a 4×4 bingo board is a JavaScript expression. A value is called, and you click the square whose expression returns it. Complete a row, column, or diagonal to win.

Live version: https://ttijs.github.io/data-objects-game/index.html

## Running it

The whole project is one file, `index.html`. Open it in a browser. There is no build step and no dependencies. The page loads two fonts from Google Fonts and falls back to system fonts if they are unavailable.

## Levels

| Level | Object | What it practices |
| --- | --- | --- |
| Examples | `pet` | A study page: 5 expressions with their results and a short explanation each. No game. |
| Level 1 | `game` | Dot and bracket notation, array indexes, nested objects, `.length`, simple math, `toUpperCase()` |
| Level 2 | `cafe` | `Object.keys`, `Object.values`, `join`, `includes`, `hasOwnProperty`, nested lookups |

The levels do not use `map` or `filter`.

## How to play

1. Pick a level. The object is shown on the left (or on top on small screens).
2. Read the called value in the ball. Strings keep their quotes, so `"7"` is not `7`.
3. Click the square whose expression returns that value.
4. A wrong pick counts as a miss, and the message tells you what that expression actually returns.
5. Get four in a row, column, or diagonal to win. **Play again** reshuffles the board and the call order.

## Hints

Hints are off by default. Add `?show_hint=1` to the page URL to turn on the Hint button and counter. A hint outlines the correct square with a dashed border, and each call counts as one hint no matter how often you click.

To change the default in the code, edit this line near the top of the script:

```js
let SHOW_HINT = false;
```

Some hosts embed pages in a frame and may not pass the query string through. If `?show_hint=1` has no effect, set the variable to `true` instead.

## Adding or editing a level

Levels live in the `LEVELS` array in the script. Each level looks like this:

```js
{
  label: "Level 3: library",   // text on the level button
  name: "library",             // variable name shown in the code panel
  data: { /* the object */ },
  cells: [
    ['library.books[0].title', g => g.books[0].title],
    // ...
  ]
}
```

Each cell is `[source text, function, optional note]`. The function receives the `data` object, so write it against `g` (for example `g => g.books[0].title`). The source text is what players see, so keep it in sync with the function.

Rules for a playable level:

- It needs **exactly 16 cells** for the 4×4 board.
- Every cell must return a **different value**. The game finds the matching square by identity, so two squares with the same value make a call ambiguous.
- Values can be strings, numbers, booleans, or arrays.

For an examples-style study page, add `examples: true` to the level. It can have any number of cells, and the optional third item in each cell is the explanation shown under it.

## Customizing the look

Colors are CSS variables on `:root` at the top of the file, with a dark-mode set under `prefers-color-scheme`. The ball size is set in `.ball`, and square text wrapping in `.cell`.
