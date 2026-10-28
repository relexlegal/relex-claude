# Submission — Anthropic Claude Directory (re-review)

> Prepared 2026-10-28 on branch `directory-review-2026-10`. Nothing has been
> submitted, pushed or deployed. Before any submission: deploy the backend branch
> `directory-review-2026-10` (neutral server instructions, data-only responses),
> then merge and push this repo.

Hosted server: `https://relex.legal/api/mcp` (streamable HTTP, OAuth 2.1 with
PKCE and dynamic client registration). Twelve tools: `list_matters`,
`read_matter_context`, `diagnose_matter_sources`, `read_matter_source`,
`save_matter_work_product`, `correct_matter_ontology`, `conclude_matter_session`,
`find_legal_professionals`, `read_legal_professional`,
`prepare_professional_request`, `search`, `execute`.

## Done in this branch
- [x] Plugin 0.2.14 (`plugin/.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`): description says "legal practice management" and names the twelve tools.
- [x] Skills carry the workflow guidance the server no longer sends (`skills/relex/SKILL.md` "Connector workflow"; `skills/relex-steering/SKILL.md` documents the data-only `steering` fields).
- [x] Skills reference only endpoints that exist in the published OpenAPI spec (audit: 0 unknown references).
- [x] README, SECURITY, docs: twelve tools; reading default corrected (Relex Private Model on Relex servers by default).
- [x] Listing copy and reply draft: `backend/docs/directory-listing-anthropic.md` and `backend/docs/anthropic-reply-draft.md` (backend branch `directory-review-2026-10`).

## User must do
- [ ] Review and deploy the backend branch (`backend/terraform/deploy.sh prod`), then check `initialize` returns the new instructions.
- [ ] Merge and push this branch to `main` on github.com/relexlegal/relex-claude.
- [ ] Resolve every `[CONFIRM WITH GEORGE]` in the listing copy (models, guest AI disclosure, lawyer review) and update the privacy policy (draft: `backend/docs/privacy-policy-ai-draft.md`).
- [ ] Update the directory form: one-liner, plugin commands/skills, twelve tools, case-agent disclosure; untick or keep "server contains no instructions aimed at the assistant" (true after deploy).
- [ ] Send the reply (`backend/docs/anthropic-reply-draft.md`) and request re-review.

## Install (verify after push)
```
/plugin marketplace add relexlegal/relex-claude
/plugin install relex-legal@relex
claude mcp add --transport http relex https://relex.legal/api/mcp
```
