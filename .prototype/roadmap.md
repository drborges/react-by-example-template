# React By Example: Tic Tac Toe Game

<p align="center">
  <a href="https://egbnq.csb.app">
    <img width="420" alt="tic tac toe demo" src="https://user-images.githubusercontent.com/508128/105741872-91cec380-5f19-11eb-9c2d-b0c8bf980935.gif" />
  </a>
</p>

## Hello World

- [ ] Basic React App (no component at this point)
  - [ ] Note on `import React from "react"`?
- [ ] Can be styled with CSS just like a HTML tag
- [ ] Can also be styled programmatically via the `style` prop
- [ ] Our first Component: `<Text value="Hello World" />`
  - [ ] Conditional rendering: `variant` prop
  - [ ] Let's move this into its own file so we don't clutter too much our `index.jsx` file
- [ ] Can have children elements: The `<Card />` component
  - [ ] Let's make this a little more interesting: The `zoomed` prop
- [ ] Event handling: The `<Button />` component
  - [ ] Add some style so it looks a little nicer...
  - [ ] Passing down extra props into the native button. Example: `onClick` and `aria-label` props.

## Thinking in React

1. Break down your UI/mockup into smaller building blocks that can be implemented as React components;
1. Compose them together to build the final prototype matching the mockup;
1. Add application logic (usually, bettere placed in the root component).

<p align="center">
  <img width="420" alt="tic-tac-toe-components" src="https://user-images.githubusercontent.com/508128/105741941-a4e19380-5f19-11eb-98d6-813e36845b58.png">
</p>

## JSX Structure

The pseudo code below gives an idea of how we can structure our app in terms of the component abstractions we just went over.

```jsx
1: <Game>:
  2: <Card>
    3: <Text variant="title" value="Tic Tac Toe" />
    3: <Text value="Currently Playing: circle (6s)" />

    4: <Board>
      5: <Cell />
      5: <Cell />
      5: <Cell />

      5: <Cell />
      5: <Cell />
      5: <Cell />

      5: <Cell />
      5: <Cell />
      5: <Cell />
    </Board>

    3: <Text value="Winner: N/A. Moves Left: 4" />
    6: <Button>Reset Game</Butotn>
  </Card>
```

## Getting Thing Done

### The Board Component

What do we know about this component?

- [ ] It needs to render the board
- [ ] It will take cell elements as its children elements

### The Cell Component

What do we know about this component?

- [ ] Should be clickable
- [ ] Should support keyboard navigation
- [ ] Can be empty
- [ ] Can be taken by a player, either a “circle” or a “cross”
- [ ] Is highlighted in bold red when the cell belongs to a winning move
- [ ] Should be disabled when:
  1. [ ] taken;
  2. [ ] highlighted (belongs to a winning move);
  3. [ ] the game is over.
- [ ] Should allow for a callback to be passed in so it is executed when the cell is clicked, informing the position of the cell within the board.

### The Game Component

What do we know about this component?

- [ ] It’s the root of our application
- [ ] Will be responsible for encapsulating the state and application logic of our app and pass data down to other components via their props
- [ ] But for now… it will simply encapsulate all our game structure

### The Text Component

- [x] Should support two styles:
  - [x] One to be used for the “Tic Tac Toe” title
  - [x] Another for the rest of the text used in the App

### The Card Component

- [x] It will define the boundaries of our app, e.g. container holding the app title, match info, game board, game statistics, etc...

### The Button Component

- [x] Should decorate the native button element with our custom style
- [x] Should still provide all the built-in capabilities of a button. Example: `onClick` and `aria-label` props.

## State and Application Logic

So far, our app does not do much, it's pretty much static. In order to make it more interactive, we need to track and manage the game state based on the user interactions.

Let's see how we can implemeent application logic and abstracted it away into reusable building blocks by implementing a simple `Counter` app.

### Managing the Board State

```js
// prettier-ignore
const { rows, take, reset } = useBoard([
  [null, null, null],
  [null, null, null],
  [null, null, null],
])
```

We'll be implementing a new custom hook `useBoard` that will allow us to:

- [ ] Dynamically initialize the board using a data structure (rather than hardcoding cells like we've been doing);
- [ ] Update the board state as users make moves.
- [ ] Reset the board when the `Reset Game` button is clicked

### Managing the Game Rules

```js
// prettier-ignore
const {
  currentPlayer,
  nextPlayer,
  winner,
  isGameOver,
  movesLeft,
} = useJudge(boardState)
```

The `useJudge` custom hook should provide an abstraction of a game judge, encapsulating logic to implement the game rules. Its API should allow us to:

- [ ] Access the current player (either "circle" or "cross");
- [ ] Switch turns as players make moves;
- [ ] Compute a winner if one exists;
- [ ] Check if the game is over;
- [ ] Check how many moves are left.

### Implementing the Timer

```js
// prettier-ignore
const { count, reset, stop } = useTimer()
```

The `useTimer` custom hook will be responsible for managing the game timer, and will allow us to:

- [ ] Access the current timer state
- [ ] Reset the timer when the game is reset
- [ ] Stop the timer when the game is over

## Optimizations

- [ ] Avoid prop drilling with the context API
- [ ] Skipping expensive operations in `useJudge` hook
- [ ] Skipping unnecessary side-effects in the `useTimer` hook
- [ ] Skipping unnecessary renderings with `React.memo`
- [ ] CSS Modules to avoid CSS leaking
