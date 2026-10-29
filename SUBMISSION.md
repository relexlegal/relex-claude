# Submission — Anthropic Claude Directory (re-review)

> Prepared 2026-10-28; updated the same day for MCP server version 1.1.0
> (branch `docs/read-api-1.1.0`). Nothing has been submitted. The backend with
> neutral server instructions, data-only responses and the `read_api` tool is
> on `master` (5a5d7b9) and deployed as revision `relex-backend-00192`.

Hosted server: `https://relex.legal/api/mcp` (streamable HTTP, OAuth 2.1 with
PKCE and dynamic client registration). Thirteen tools: `list_matters`,
`read_matter_context`, `diagnose_matter_sources`, `read_matter_source`,
`save_matter_work_product`, `correct_matter_ontology`, `conclude_matter_session`,
`find_legal_professionals`, `read_legal_professional`,
`prepare_professional_request`, `search`, `read_api`, `execute`.

Server version 1.1.0. `read_api` reads one GET endpoint (read-only; parameters
`path` and optional `query`). `execute` creates, updates or deletes through one
endpoint (POST/PUT/PATCH/DELETE); DELETE and other irreversible routes are not
applied by the tool and return a Relex deep link where the user confirms the
change.

## Done in this branch
- [x] Plugin 0.2.16 (`plugin/.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`): description says "legal practice management" and names the thirteen tools.
- [x] Skills carry the workflow guidance the server no longer sends (`skills/relex/SKILL.md` "Connector workflow"; `skills/relex-steering/SKILL.md` documents the data-only `steering` fields).
- [x] Skills reference only endpoints that exist in the published OpenAPI spec (audit: 0 unknown references).
- [x] README, SECURITY, docs: thirteen tools; reading default corrected (Relex Private Model on Relex servers by default).
- [x] Listing copy and reply draft: `backend/docs/directory-listing-anthropic.md` and `backend/docs/anthropic-reply-draft.md` (backend `master`).

## User must do
- [ ] Check the live server: `initialize` reports `serverInfo.version` 1.1.0 and `tools/list` returns the thirteen tools with the annotations in `backend/docs/directory-listing-anthropic.md`.
- [x] Listing copy: models verified from `terraform/envs/prod.tfvars`; lawyer review described as optional (validatedGenerations, mark-delivered). Only Vertex AI naming is still `[CONFIRM WITH GEORGE]` (`backend/docs/directory-listing-anthropic.md`).
- [x] Guest AI notice: merged in frontend PR #13 (aed2580 / 4a6095e; invite page + guest intake panel, 21 locales). Confirm it is visible on relex.legal before replying to Anthropic.
- [ ] Publish the privacy-policy update after legal sign-off: draft on frontend branch `legal/privacy-ai-agents` (32a08fe), mirrored in `backend/docs/privacy-policy-ai-draft.md`.
- [ ] Update the directory form: one-liner, plugin commands/skills, thirteen tools, case-agent disclosure; untick or keep "server contains no instructions aimed at the assistant" (true for server 1.1.0).
- [ ] Send the reply (`backend/docs/anthropic-reply-draft.md`) and request re-review.

## Install (verify after push)
```
/plugin marketplace add relexlegal/relex-claude
/plugin install relex-legal@relex
claude mcp add --transport http relex https://relex.legal/api/mcp
```
