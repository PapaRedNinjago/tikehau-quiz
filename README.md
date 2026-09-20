# Quiz

Interactive multiplayer quiz for seminars and events.

20 questions across 2 sections: Geopolitics (7) and Market Knowledge (13). Add your own questions via the admin panel (`/?admin`) — including an "Internal" category for anything specific to your organization.

Each question is either a scored **Quiz** question or an opinion-gathering **Poll** — see [Polls](#polls) below.

## Three modes via URL

| URL | Mode | Who uses it |
|---|---|---|
| `/` | **Player** | Participants on their phones — join with session code, name, avatar |
| `/?host` | **Host** | Presenter on projected screen — start session or review questions |
| `/?review` | **Review** | Prep mode — browse all questions with answer reveal |

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

## Polls

A question can be marked **Poll** instead of **Quiz** in the admin panel (`/?admin` → Edit Questions → open a question → Type toggle). Polls are for gathering opinion rather than testing knowledge:

- Every option is valid — there's no correct answer, no score, and no leaderboard impact.
- Players still pick one of 4 options and submit, exactly like a quiz question.
- The host's "Reveal" step becomes **Show Results**: a live bar chart of how the room voted (count + %), with the leading option highlighted in orange instead of green. Players see the same results on their own screen.
- Since nothing changes on the leaderboard, the host flow skips straight to the next question instead of showing a leaderboard screen.
- An optional "takeaway" line (the same field used for a quiz's short explanation) can be shown after the results close.
- The Excel template/upload has a `Type` column (`Quiz` / `Poll`) — leave `Correct (A-D)` blank for poll rows.

## Review mode

Open `/?review` to preview all questions. Each question shows:

- **Left:** question text, 4 colored answer options, themed illustration
- **Right:** locked panel → click "Show Answer" (or press spacebar) to reveal the correct answer, explanation, and full source citation. For a poll question, this instead shows "Show Notes" and a reminder that there's no correct answer, plus the optional takeaway text.

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

5. In `index.html`, find the `firebase.initializeApp({...})` block near the top of the script and replace the placeholder values with your project's config (**Project Settings → General → Your apps → SDK setup and configuration**).

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

## Brand

- Navy: `#1B1464`
- Orange: `#FF6633`
- Background: `#FAF6F1` (warm beige)
- Organic shapes: `#E8DFD3` (cream)
- Font: Franklin Gothic Medium / Libre Franklin
- Player answer colors: Red ▲ / Blue ◆ / Yellow ● / Green ■
