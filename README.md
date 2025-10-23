# Tenzies (React + Vite)

Roll the dice until **all ten** show the **same value**. Click a die to **hold** its value between rolls. When every die is held and matches, you win 🎉 and the **Roll** button becomes **New Game**.

![Screenshot](./screenshot.png)

---

## Features

- 🎲 Ten-die board with selective re‑rolls (only unheld dice change).
- 📌 Hold/Unhold a die by clicking (toggles `isHeld`).
- 🏁 Win detection: _all dice held_ **and** _all values equal_.
- 🎉 Victory confetti sized to the viewport (`react-confetti` + `react-use`).
- ♿️ Accessibility:
  - Dice are `<button>` elements with `aria-pressed` and descriptive `aria-label`s.
  - A screen‑reader‑only live region announces the win.
  - Focus automatically moves to **New Game** after victory.
- 🔑 Stable React keys via `nanoid`.
- ⚡️ Built with Vite for fast dev and production builds.

---

## Tech Stack

- **React 19**, **Vite 7**
- **nanoid** – unique IDs for dice
- **react-confetti** – win animation
- **react-use** – `useWindowSize` hook
- Plain **CSS** for styling

---

## Getting Started

> Requires **Node 18+** (or any actively supported LTS) and npm/pnpm/yarn.

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Create production build
npm run build

# Preview the production build locally
npm run preview
```

Vite will print a local URL for development (e.g., `http://localhost:5173`).

---

## How to Play

1. Click **Roll** – all unheld dice will (re)roll to values 1–6.
2. Click any die to **hold** its current value (click again to unhold).
3. Repeat until **all ten dice are held** and **show the same value**.
4. When you win:
   - Confetti appears
   - Screen readers hear: “Congratulations! You won!”
   - The action button label becomes **New Game** (and receives focus).

---

## Code Tour

- **`src/App.jsx`**
  - Initializes `dice` with a _lazy_ function `generateAllNewDice()`.
  - `rollDice()` maps over dice; rerolls only those with `isHeld === false`.
  - `hold(id)` toggles `isHeld` for a specific die.
  - `gameWon` is true when **every** die is held **and** **all values match**.
  - Uses `react-use`’s `useWindowSize()` to size `react-confetti`.
  - Moves focus to the main action button when the game is won (for a11y).
- **`src/Die.jsx`**
  - Renders one die as a `<button>` with a green background when held.
  - Sets `aria-pressed` and a helpful `aria-label` (value + held/not held).
- **`src/index.css`**
  - Layout (centered card), grid for dice (5×2), typography, buttons, SR‑only utility.
- **Dependencies** are declared in `package.json`; Vite config is in `vite.config.js`.

---

## Project Structure (key files)

```
tenzies
├─ public/
├─ src/
│  ├─ assets/
│  ├─ App.jsx
│  ├─ Die.jsx
│  ├─ index.css
│  ├─ main.jsx
├─ index.html
├─ package.json
├─ vite.config.js
└─ README.md
```

---

## Design Notes

- **State shape**: each die is `{ id, value, isHeld }`.
- **Randomization**: values are `Math.ceil(Math.random() * 6)`.
- **Keys**: `nanoid()` prevents key collisions across re‑renders.
- **A11y**: live region + focus management improves screen‑reader UX.

---

## Ideas for Extensions

- Track **roll count**, **timer**, and **best score** (persist with `localStorage`).
- Render **pips** on dice faces instead of numbers.
- **Keyboard support** (e.g., arrow navigation + Space to hold).
- **Difficulty modes** (more dice, target patterns, time attack).
- Add **tests** (e.g., React Testing Library) for game logic.

---

## Scripts

- `npm run dev` – start dev server
- `npm run build` – production build
- `npm run preview` – preview build locally
- `npm run lint` – run ESLint

---

## License

Add your preferred license (e.g., MIT) or keep the repository private.
