---
name: Export a CrunchDAO competition leaderboard
description: Read the leaderboard standings and prediction history for a Crunch Hub competition via the Tournament API.
api: openapi/crunchdao-tournament-openapi.json
operations: [getCompetition, listRounds, listLeaderboards, getLeaderboardPositions, listPredictions]
---

# Export a CrunchDAO competition leaderboard

Read-only reporting over a competition's standings on the Tournament API
(`https://api.hub.crunchdao.com`).

## Authentication
`Authorization: API-Key <token>` (or `?apiKey=<token>`). Read endpoints still
require a valid key.

## Steps
1. **Resolve the competition** — `getCompetition` with the `competitionIdentifier`
   (e.g. `structural-break`).
2. **Enumerate rounds** — `listRounds` to get each `roundIdentifier`.
3. **List leaderboards** — `listLeaderboards` for the competition to get each
   `leaderboardDefinitionIdentifier`.
4. **Read positions** — `getLeaderboardPositions` per leaderboard definition to pull
   the ranked standings.
5. **(Optional) predictions** — `listPredictions` for a given project to inspect its
   prediction history.

## Conventions
- Paginate with `page` / `size` / `sort`.
- Some v1/v2/v3 leaderboard operations are deprecated in favor of the v4 endpoints —
  prefer `listLeaderboards` (v4). See lifecycle/crunchdao-lifecycle.yml.
- Error envelope: `{ code, message, ...context }` — see errors/crunchdao-problem-types.yml.
