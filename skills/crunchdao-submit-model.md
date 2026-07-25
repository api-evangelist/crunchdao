---
name: Submit a model to a CrunchDAO competition
description: Find an open Crunch Hub competition, create a project under your account, and push a submission to the Tournament API.
api: openapi/crunchdao-tournament-openapi.json
operations: [listCompetitionsV2, getCompetition, getCompetitionState, createProjectV3, listProjectsV3, createSubmissionV4, listSubmissionsV4]
---

# Submit a model to a CrunchDAO competition

Use the CrunchDAO Tournament API (`https://api.hub.crunchdao.com`) to enter a
competition and submit a model.

## Authentication
Send your API key on every request as `Authorization: API-Key <token>` (or
`?apiKey=<token>`). Generate a key at https://hub.crunchdao.com/account/api. The
`crunch-cli` client reads it from the `CRUNCH_API_KEY` environment variable.

## Steps
1. **Pick a competition** — `listCompetitionsV2` to browse, then `getCompetition`
   for its `competitionIdentifier` and `getCompetitionState` to confirm it is open
   for submissions.
2. **Create a project** — `createProjectV3` under your `userLogin` for that
   competition (or `listProjectsV3` to reuse an existing one).
3. **Submit** — `createSubmissionV4` with the project's files. Prefer the
   `crunch push` CLI command, which handles packaging and the submission token.
4. **Confirm** — `listSubmissionsV4` to verify the submission was accepted.

## Conventions
- List endpoints paginate with `page` / `size` / `sort` (Spring-style).
- Errors are `{ "code": "UPPER_SNAKE_CASE", "message": "...", ...context }` — branch
  on `code` (e.g. `SUBMISSION_NOT_FOUND`), not on message text. See
  errors/crunchdao-problem-types.yml.
- There is no idempotency key; do not blindly retry a failed `createSubmissionV4`.
