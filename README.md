# ♞ Chess Arena

A cinematic chess website: an animated intro sequence, a hero with parallax and floating embers,
an engine opponent with three levels, local duels, and dashboards that record every game you finish.

## What's inside

**Website**
- Opening title sequence (plays once per browser session; click to skip)
- Hero with parallax background, light rays, fog, golden embers and a floating queen
- "Story in Three Acts" section with live mini-boards, feature cards, a quote band,
  animated numbers and a "Hall of Legends" timeline (from chaturanga to today)
- Sign-in / register built into the landing page, plus **Play as guest**

**Game**
- Versus the engine: Squire (easy), Knight (medium), Grandmaster (hard); it runs in a Web Worker so the UI never freezes
- Local two-player mode
- Click-to-move or drag-and-drop, sliding piece animation, last-move / check / legal-move highlights
- Evaluation bar, captured pieces with material count, hints, undo, resign, board flip
- Synthesized sound effects (mute button in the top-right)
- Cinematic game-over screen; finished games are saved automatically when signed in

**Dashboards**
- Player: quick-play cards, games played, wins vs engine, win rate, streak, rank, match history
- Admin: player count, games recorded, last 24h activity, searchable player list

## Setup

```bash
# 1. Backend (project root)
npm install
cp .env.example .env        # then put a long random JWT_SECRET (32+ chars) in .env
npm run create-admin        # optional: create the single admin account
npm run dev                 # API on http://localhost:5000

# 2. Frontend (new terminal)
cd client
npm install
npm run dev                 # site on http://localhost:5173
```

The existing `chess_arena.db` keeps working. A new `games` table is created automatically on start.

### Production

```bash
cd client && npm run build && cd ..
npm start                   # Express serves client/dist and the API on one port
```

## New API endpoints

| Method | Path               | Auth   | Purpose                          |
|--------|--------------------|--------|----------------------------------|
| POST   | `/api/games`       | player | Save a finished game             |
| GET    | `/api/games/me`    | player | Your last 25 games + totals      |
| GET    | `/api/admin/stats` | admin  | Player / game counts             |
| GET    | `/api/admin/users` | admin  | Account list with game stats     |

`CLIENT_ORIGIN` in `.env` controls CORS (comma-separated list, default `http://localhost:5173`).
