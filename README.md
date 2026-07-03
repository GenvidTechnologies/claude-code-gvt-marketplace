# claude-code-gvt-marketplace

Genvid's [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) (catalog name `gvt-plugins`).

This repo holds **only the catalog** (`.claude-plugin/marketplace.json`). Each plugin lives in its own repository and is referenced from the catalog by a pinned release tag.

## Plugins

| Plugin | Repo | Install |
|--------|------|---------|
| `gvt-dev` | [`claude-code-plugin-gvt-dev`](https://github.com/GenvidTechnologies/claude-code-plugin-gvt-dev) | `gvt-dev@gvt-plugins` |
| `gvt-construct3` | [`claude-code-plugin-gvt-construct3`](https://github.com/GenvidTechnologies/claude-code-plugin-gvt-construct3) | `gvt-construct3@gvt-plugins` |

## Install

```text
/plugin marketplace add https://github.com/GenvidTechnologies/claude-code-gvt-marketplace.git
/plugin install gvt-dev@gvt-plugins
```

## How plugins are referenced

Each entry in `marketplace.json` sources the plugin from its own repo, pinned to a specific release tag via the `ref` field. Pinning means consumers get a reproducible install and updates are deliberate. A plugin whose shipped artifact lives in a subfolder of its repo uses a `git-subdir` source with a `path`; a plugin at its repo root uses a `url` source.

### Releasing a plugin update

1. Push the change to the plugin repo's default branch.
2. Tag the release `vX.Y.Z` and push the tag.
3. Update that plugin's `ref` in `.claude-plugin/marketplace.json` here and push.
4. Consumers run `/plugin update <plugin>@gvt-plugins`.

## Adding a new plugin

Add an entry to the `plugins` array in `.claude-plugin/marketplace.json` with the plugin's `name`, a source pointing at its repo (a `url` source for a root plugin, or a `git-subdir` source with a `path` for a subfolder plugin), a pinned `ref` tag, and a `description`. Validate with `claude plugin validate .`.
