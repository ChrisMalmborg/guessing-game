# Number Guessing Game

A classic number guessing game enhanced with AI-powered strategy analysis using the Anthropic Claude API.

<!-- Screenshot placeholder — replace with actual screenshot or GIF -->
<!-- ![Gameplay Screenshot](screenshot.png) -->

**[Live Demo](https://chrismalmborg.github.io/guessing-game/)**

---

## Features

- **Core Gameplay** — Guess a number between 1 and 100, receive higher/lower feedback, and beat your best score
- **High Score Tracking** — Personal best is persisted across sessions via `localStorage`
- **Sound Effects** — Distinct audio feedback for correct guesses, near misses, and wrong attempts
- **Confetti Celebration** — Victory animation triggers on a win
- **AI Strategy Analysis** — After each game, Claude reviews your guess history and explains whether your approach was optimal, and how a binary search strategy compares

---

## Tech Stack

| Layer    | Technology                          |
|----------|-------------------------------------|
| Frontend | HTML, CSS, JavaScript               |
| Backend  | Node.js, Express                    |
| AI       | Anthropic Claude API (`claude-sonnet-4-6`) |
| Hosting  | GitHub Pages (frontend), Railway (backend) |

---

## Architecture

```
Browser (GitHub Pages)
    │
    │  guess history + result
    ▼
Express API (Railway)          ← environment variable: ANTHROPIC_API_KEY
    │
    │  prompt
    ▼
Anthropic Claude API
    │
    │  strategy analysis text
    ▼
Browser — displays analysis in modal
```

- **Frontend** is a single `index.html` file served via GitHub Pages. No build step required.
- **Backend** is a lightweight Express server that proxies requests to the Claude API, keeping the API key server-side and handling CORS for the GitHub Pages origin.
- **AI layer** receives the player's full guess history and game outcome, then returns a plain-English analysis of their guessing strategy.

**Backend repo:** [ChrisMalmborg/guessing-game-backend](https://github.com/ChrisMalmborg/guessing-game-backend)

---

## What I Learned

- **Full-stack architecture** — Splitting a project across a static frontend and a separate API backend, and getting them to talk to each other across different hosting providers
- **API integration** — Authenticating with and prompting the Anthropic Claude API; structuring messages to get consistently useful responses
- **Debugging across environments** — Tracing CORS errors, mismatched property names, and modal z-index issues across local dev and production deployments
- **Deployment** — Publishing a static site to GitHub Pages and deploying a Node.js service to Railway with environment-variable configuration
