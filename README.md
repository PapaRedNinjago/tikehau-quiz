# AI Quiz

Interactive multiplayer quiz for seminars: **AI & The Changing World.**

24 questions across 3 sections: Geopolitics (8), Market Knowledge (10), and Internal (6).

## Three modes via URL

| URL | Mode | Who uses it |
|---|---|---|
| `/` | **Player** | Participants on their phones — join with session code, name, avatar |
| `/?host` | **Host** | Presenter on projected screen — start session or review questions |
| `/?review` | **Review** | Prep mode — browse all 24 questions with answer reveal |

## How it works

1. Host opens `?host` on the projected screen → **Start a Session** → a 4-digit code appears
2. Participants open the base URL on their phones → enter the code, their name, pick an avatar
3. Host starts the quiz — questions appear on both screens
4. **Players** see Kahoot-style colored shape buttons (▲ ◆ ● ■) and tap to answer
5. **Host** sees the question, answer options, a live answer counter, and a themed illustration
6. Host clicks **Reveal Answer** → correct answer highlights with slide-in panel showing explanation and full source citation
7. Host clicks **Show Leaderboard** → animated podium for top 3 (with crown) + cascade for remaining players
8. After the last question → final results with trophy ceremony

## Scoring

Up to 1,000 points per correct answer, weighted by speed. Wrong or unanswered = 0.

## Review mode

Open `/?review` to preview all 24 questions. Each question shows:

- **Left:** question text, 4 colored answer options, themed illustration
- **Right:** locked panel → click "Show Answer" (or press spacebar) to reveal the correct answer, explanation, and full source citation

Navigate with Prev/Next buttons or ← → arrow keys.

## Setup

### Firebase Realtime Database (one-time, 5 minutes)

The quiz uses Firebase Realtime Database (free tier) for real-time sync across devices.

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Open the project (or create one)
3. **Build → Realtime Database** → ensure it exists in `europe-west1`
4. **Rules** tab — set to:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

The Firebase config is already embedded in `index.html`.

### GitHub Pages

1. Push `index.html` and `README.md` to this repo
2. **Settings → Pages → Source:** deploy from `main` branch, `/ (root)`
3. The quiz is live at the GitHub Pages URL

## Kill switch

To disable the quiz before or after the event, edit `index.html` and change:

```js
const DISABLED = false;  // quiz is live
```

to:

```js
const DISABLED = true;   // shows "Coming Soon" holding page
```

Commit and push — the site updates within a minute.

## Post-event

1. Set `DISABLED = true` and push
2. In Firebase console: delete the database data or set rules to `false` / `false`

## Tech stack

Single `index.html` file — no build step, no dependencies to install.

- React 18 (CDN)
- Firebase Realtime Database compat SDK (CDN)
- Babel standalone for JSX (CDN)
- Libre Franklin font (Google Fonts)
- Logo embedded as base64

## Brand

- Navy: `#1B1464`
- Orange: `#FF6633`
- Background: `#FAF6F1` (warm beige)
- Organic shapes: `#E8DFD3` (cream)
- Font: Franklin Gothic Medium / Libre Franklin
- Player answer colors: Red ▲ / Blue ◆ / Yellow ● / Green ■
