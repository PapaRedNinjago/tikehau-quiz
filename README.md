#  — AI Quiz

Interactive multiplayer quiz for the Top Management Seminar: **AI & The Changing World**.

24 questions across 3 sections: Geopolitics, Market Knowledge, and  Internal knowledge.

## How it works

**Host** (projected screen) creates a session → a 4-digit code appears.  
**Players** (phones) open the same URL → enter the code, their name, pick an avatar → play.

The host controls the pace: start questions, reveal answers (with source cards), show the leaderboard, advance. Scoring rewards both correctness and speed (up to 1,000 points per question).

## Setup

### 1. Firebase Realtime Database

The quiz uses [Firebase Realtime Database](https://firebase.google.com/products/realtime-database) (free tier) for real-time sync across devices.

- Create a project at [console.firebase.google.com](https://console.firebase.google.com)
- **Build → Realtime Database → Create Database** → pick `europe-west1` → start in test mode
- Set the **Rules** to allow read/write:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

- Your Firebase config is already in `index.html`. If you need to update it, look for the `firebase.initializeApp({...})` block near the top of the file.

### 2. GitHub Pages

- Push `index.html` to this repo
- **Settings → Pages → Source:** deploy from `main` branch
- Your quiz URL: `https://<username>.github.io/tikehau-quiz`

## Kill switch

To disable the quiz before/after the seminar, open `index.html` and change:

```js
const DISABLED = false;  // quiz is live
```

to:

```js
const DISABLED = true;   // shows "Coming Soon" holding page
```

Push the change — the site updates within a minute.

## On seminar day

1. Open the URL on the **projected screen** → click **Host a Session**
2. Share the 4-digit code with the room
3. Participants open the URL on their **phones** → **Join as Player** → enter code + name + avatar
4. Once everyone is in, click **Start Quiz**
5. After each question: **Reveal Answer** (shows source card) → **Show Leaderboard** → **Next Question**
6. At the end: trophy ceremony with full rankings

## Post-event

- Set `DISABLED = true` and push
- In Firebase console, either delete the database or set rules to `false` / `false`

## Tech stack

Single `index.html` file. No build step. Dependencies loaded via CDN:

- React 18
- Firebase Realtime Database (compat SDK)
- Babel standalone (JSX transpilation)

---

*Built for Tikehau Capital's AI Steering Committee seminar.*
