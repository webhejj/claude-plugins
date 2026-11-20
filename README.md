# claude-plugins

A Claude Code marketplace named `webhejj`. It lists plugins and holds none of them: each plugin
lives in its own repository, and an entry here points at it.

| Plugin          | Repository                                                                     |
|-----------------|--------------------------------------------------------------------------------|
| `awt`           | [webhejj/agent-wiki-toolbox](https://github.com/webhejj/agent-wiki-toolbox)    |
| `atlas`         | [webhejj/atlas-plugin](https://github.com/webhejj/atlas-plugin)                |
| `duckdb-skills` | [gnagy/duckdb-skills](https://github.com/gnagy/duckdb-skills)                  |

## Install

Add the marketplace once, then install the plugins you want:

```bash
claude plugin marketplace add webhejj/claude-plugins
```

```bash
claude plugin install atlas@webhejj
```

`--scope project` writes the plugin into a repository's `.claude/settings.json` instead of your
user settings, so collaborators are offered it; each of them still installs it once.

Auto-update is off for third-party marketplaces. To take a newer version:

```bash
claude plugin marketplace update webhejj
```

```bash
claude plugin update atlas@webhejj
```

## Testing a change before it is pushed

Start a session with the working copy:

```bash
claude --plugin-dir path/to/atlas-plugin
```

A `--plugin-dir` plugin replaces an installed plugin of the same manifest name for that session
only, and writes nothing. `claude plugin list` still shows the installed one as enabled, so the only
sign of which copy is running is how the session was started.

## Adding a plugin

Add an entry to `.claude-plugin/marketplace.json` with a `github` source, then check it:

```bash
claude plugin validate .
```

A plugin whose `plugin.json` sets `version` is updated only when that string changes. Leave it out
and the commit is the version.
