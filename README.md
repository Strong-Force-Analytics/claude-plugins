# claude-plugins

Strong Force Analytics' internal **Claude Code plugin marketplace**. One place to get the
Claude Code add-ons our team shares, installed with two commands.

## Plugins

| Plugin | What it does |
|--------|--------------|
| [architect-crew](https://github.com/Strong-Force-Analytics/architect-crew) | Opus session delegates reading, commands and edits to cheap Haiku/Sonnet subagents. Big budget saver. |

## Install a plugin

Requirements: Claude Code, and access to this repo plus the plugin's repo
(`gh auth login` if you haven't authenticated with GitHub).

```
/plugin marketplace add Strong-Force-Analytics/claude-plugins
/plugin install architect-crew@sfa-plugins
/reload-plugins
```

The marketplace is named `sfa-plugins`; that's the part after `@`. You only add the
marketplace once, then install any plugin from it.

Get the latest versions:

```
/plugin marketplace update
/reload-plugins
```

## Enable it for everyone on a project

To have teammates prompted to install automatically when they open a repo, commit this
to that repo's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "sfa-plugins": {
      "source": {
        "source": "github",
        "repo": "Strong-Force-Analytics/claude-plugins"
      }
    }
  },
  "enabledPlugins": {
    "architect-crew@sfa-plugins": true
  }
}
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "repository not found" / auth error | You need access to the repo and git credentials: run `gh auth login`, and ask an org admin to add you. |
| Plugin installed but not active | Run `/reload-plugins`, then start a new session. |
| Not seeing a new version | Run `/plugin marketplace update`. A plugin only updates when its `version` was bumped. |

## Adding or updating a plugin

See [CONTRIBUTING.md](CONTRIBUTING.md).
