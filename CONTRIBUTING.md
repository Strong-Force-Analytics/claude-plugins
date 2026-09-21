# Contributing

This repo is only a **catalog**: `.claude-plugin/marketplace.json`. Each plugin lives in
its own repo and is listed here.

## Add a plugin

1. Build the plugin in its own repo (`.claude-plugin/plugin.json` at the root, plus
   `agents/`, `skills/`, `hooks/` as needed). Test it with
   `claude --plugin-dir ./my-plugin` and `claude plugin validate ./my-plugin`.
2. Add an entry to `plugins` in `.claude-plugin/marketplace.json`:

   ```json
   {
     "name": "my-plugin",
     "source": {
       "source": "url",
       "url": "https://github.com/Strong-Force-Analytics/my-plugin.git"
     },
     "description": "One sentence on what it does."
   }
   ```

   Use the full HTTPS `url` form, not the `github` shorthand. The shorthand tries SSH
   first, which fails for anyone without SSH set up for GitHub (we hit this in testing).
   HTTPS uses the same credentials as `gh auth login`.

3. Add a row to the table in `README.md`.
4. Run `claude plugin validate .` in this repo. It must pass.
5. Open a pull request. CI runs the same validation.

## Release a new version of a plugin

That happens in the plugin's own repo, not here:

1. Change the plugin, bump `version` in its `.claude-plugin/plugin.json`, and add a
   `CHANGELOG.md` entry.
2. Merge to `main`.
3. Teammates run `/plugin marketplace update` to receive it. If the version isn't
   bumped, they won't get the change.

No change is needed in this repo, because the entry tracks the plugin repo's default
branch. To pin a plugin to a fixed release, add `"ref": "v1.2.0"` (a tag) to its
`source`.

## Rules

- The marketplace `name` (`sfa-plugins`) must not be changed casually, since every
  install command and team `settings.json` refers to it. Names that look like official
  Anthropic marketplaces are rejected by `claude plugin validate`.
- Keep plugin repos private unless everyone involved agreed to open-source them.
- Don't put secrets in a plugin. Anyone who can install it can read it.
