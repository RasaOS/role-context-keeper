# role-context-keeper

**Version:** 0.1.3 · `rasa.module.role.context-keeper` · public

The **Context Keeper** role (`context-keeper`) as a RasaOS role module. Keeps a repo's CLAUDE.md and session-start files correct and compact. Checks every claim against the source, trims without losing rules, stamps what it verified, and opens a PR.

| File | What it is |
|---|---|
| `role.json` | The role's fields (id, name, summary, version, consumers, knowledge, takes, kinds, grants). galt publishes them to `/tenant_config/roles/context-keeper`. |
| `prompt.md` | The role's prompt, byte for byte the body of `roles/context-keeper.md` in vsi-tenant. |
| `.claude-plugin/plugin.json` | The plugin manifest, which makes the repo loadable into a session with `--plugin-dir`. |
| `rasa.json` | The Element manifest: `kind: module`, with the role's id and version under `rasa`. |
| `bin/check-role` | The release gate. |

Role version **1**, from `roles/context-keeper.md` at vsi-tenant `fd0c872`.

**Work.** It takes `refresh` through `galt work`, per the tenant's `roles/WORK.md`.

## Loading it

- **As an agent's brain:** `galt agent new <name> --brain RasaOS/role-context-keeper@v0.1.3`. galt reads `role.json` and `prompt.md`. There is no role assignment this way, so no grants.
- **As the source of the published role:** the tenant's `roles/context-keeper.md` becomes the one line `element: RasaOS/role-context-keeper@v0.1.3`. After a person runs Publish roles, every agent with role `context-keeper` loads this Element. galt's scheduler supports this; it advertises `role_elements` (galt ADR 0064).
- **Public:** any computer can fetch it. No vault token is needed.

## Changing the role

Until the tenant's `roles/context-keeper.md` points here, that file is what Publish roles reads, and this repo is a snapshot of it. vsi-tenant's `/role` skill (`bin/role-element`) keeps them together; see `CLAUDE.md`.
