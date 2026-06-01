# claude-code-marketplace

Genvid's [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) (catalog name `genvid-plugins`).

This repo holds **only the catalog** (`.claude-plugin/marketplace.json`). Each plugin lives in its own repository and is referenced from the catalog by a pinned commit.

## Plugins

| Plugin | Repo | Install |
|--------|------|---------|
| `genvid-dev` | [`claude-code-plugin-genvid-dev`](https://github.com/genvid-holdings/claude-code-plugin-genvid-dev) | `genvid-dev@genvid-plugins` |

## Install

```text
/plugin marketplace add https://github.com/genvid-holdings/claude-code-marketplace.git
/plugin install genvid-dev@genvid-plugins
```

## How plugins are referenced

Each entry in `marketplace.json` uses a `url` source pointing at the plugin repo, pinned to a specific commit via the `sha` field. Pinning means consumers get a reproducible install and updates are deliberate.

### Releasing a plugin update

1. Push the change to the plugin repo's default branch.
2. Get the new commit SHA: `git rev-parse HEAD` in the plugin repo.
3. Update that plugin's `sha` in `.claude-plugin/marketplace.json` here and push.
4. Consumers run `/plugin update <plugin>@genvid-plugins`.

## Adding a new plugin

Add an entry to the `plugins` array in `.claude-plugin/marketplace.json` with the plugin's `name`, a `url` source pointing at its repo, a pinned `sha`, and a `description`. Validate with `claude plugin validate .`.
