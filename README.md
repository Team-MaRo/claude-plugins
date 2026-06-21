# Team-MaRo Claude Code Plugins

A Claude Code plugin marketplace. Each plugin lives in its own folder under [`plugins/`](plugins/); add the marketplace once, then install whichever plugins you want.

[![License](https://img.shields.io/github/license/Team-MaRo/claude-plugins)](LICENSE.txt)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.0-4baaaa)][code-of-conduct]


## Add the marketplace

```sh
claude plugin marketplace add Team-MaRo/claude-plugins
```

Then install a plugin (see the table below) and enable it via `/plugin`.

## Available plugins

| Plugin | Install | Description |
|---|---|---|
| **cc-statusline** | `claude plugin install cc-statusline@team-maro` | Wires up the [cc-statusline](https://github.com/Team-MaRo/cc-statusline) MCP server — read-only access to live context usage, rate-limit snapshots, and session cost/token summaries. Requires the `cc-statusline` binary on `PATH`. |

### cc-statusline

The plugin contributes one stdio MCP server (`cc-statusline`) defined in [`plugins/cc-statusline/.mcp.json`](plugins/cc-statusline/.mcp.json):

```json
{ "mcpServers": { "cc-statusline": { "command": "cc-statusline", "args": ["mcp"] } } }
```

Install the binary first (`brew install Team-MaRo/tap/cc-statusline`, `cargo install --git …`, Nix, or a release binary). Tools exposed: `context_usage`, `rate_limits`, `session_summary` (data from `$XDG_CACHE_HOME/cc-statusline/sessions.json`).

## Adding a new plugin

1. Create `plugins/<name>/` with a `.claude-plugin/plugin.json` and its components (`skills/`, `commands/`, `.mcp.json`, `hooks/`, …).
2. Add an entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) with `"source": "./plugins/<name>"`.
3. Register it in `.github/release-please-config.json` (`packages["plugins/<name>"]`) and `.github/release-please-manifest.json`.

## Contributing

Conventional Commits; automated releases via release-please (per-plugin tags like `cc-statusline-0.1.0`). See [CONTRIBUTING.md][contributing].

## Contributing

Please read [CONTRIBUTING.md][contributing] for details on our code of conduct and the process for submitting pull requests.

This project uses [Conventional Commits](https://www.conventionalcommits.org/).

## Versioning

We use [SemVer](http://semver.org/) for versioning. For available versions, see the [tags on this repository][gh-tags].

## Authors

### Special thanks for all the people who had helped this project so far

- **Manuele** - [D3strukt0r](https://github.com/D3strukt0r)

See also the full list of [contributors][gh-contributors] who participated in this project.

### I would like to join this list. How can I help the project?

We're currently looking for contributions for the following:

- [ ] Bug fixes
- [ ] Translations
- [ ] etc...

For more information, please refer to our [CONTRIBUTING.md][contributing] guide.

## License

This project is licensed under the MIT License - see the [LICENSE.txt](LICENSE.txt) file for details.

## Acknowledgments

This project currently uses no third-party libraries or copied code.

[gh-tags]: https://github.com/Team-MaRo/claude-plugins/tags
[gh-contributors]: https://github.com/Team-MaRo/claude-plugins/contributors
[contributing]: https://github.com/Team-MaRo/.github/blob/master/CONTRIBUTING.md
[code-of-conduct]: https://github.com/Team-MaRo/.github/blob/master/CODE_OF_CONDUCT.md
