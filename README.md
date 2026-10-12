# FanZero Publish for Codex and Claude Code

Publish an indie game on [FanZero](https://fanzero.app), find an audience for its launch, and work with content creators through revenue-share pacts.

This repository contains a publishing **skill**, marketplace catalogs and optional manual connection recipes. The plugin does not automatically connect to a server, execute code, create accounts, upload games or grant an agent permission to offer revenue. It includes no application source or studio credentials.

Current uploads accept an offline HTML build or playable slice, with bundled assets and an `index.html` entry, up to 8 MB. Native games need a compatible export or slice; a store link can accompany it. A human curator reviews each new game.

## Install in Codex

On a Codex CLI with plugin marketplace support:

```bash
codex plugin marketplace add marcos-recolons/fanzero-agents
codex plugin add fanzero@fanzero-agents
```

Restart the client or begin a new session, then ask:

> Use FanZero Publish to check this game and prepare a listing and revenue-share offer for my approval.

In the desktop app, add the marketplace, restart the app and select **FanZero Publish** from **FanZero Agents** in the Plugins Directory. This repository marketplace is separate from the official public directory; listing there requires review.

The portable manifest is `plugins/fanzero/plugin.json`; skills use the Agent Skills layout. For an older client without plugins, copy only `plugins/fanzero/skills/fanzero-publish/` to the skill directory supported by that client.

To install just the skill using the [skills CLI](https://skills.sh/docs/cli):

```bash
npx skills add marcos-recolons/fanzero-agents --skill fanzero-publish
```


## Install in Claude Code

```bash
claude plugin marketplace add marcos-recolons/fanzero-agents
claude plugin install fanzero@fanzero-agents
```

Begin a new session and invoke:

```text
/fanzero:fanzero-publish
```

Or ask Claude to assess your game for FanZero. The Claude-compatible manifest is `plugins/fanzero/.claude-plugin/plugin.json`, and it loads the same skill.

## Optional manual MCP connection

Install the skill without MCP for planning and build guidance. When you want the publishing tools, add an anonymous connection yourself:

```bash
# Codex
codex mcp add fanzero --url https://fanzero.app/mcp

# Claude Code
claude mcp add --transport http fanzero https://fanzero.app/mcp
```

`connections/codex.toml` and `connections/claude-code.json` show equivalent settings. They are outside the plugin and are not loaded during installation. Merge settings only when you decide to connect; avoid replacing an existing configuration file.

Five tools work without a key: `read_listing_guidelines`, `check_build`, `whoami`, `create_studio` and `browse_games`. The first, second, third and fifth are read-only; **`create_studio` creates an account and must be authorized**. Studio tools require your studio's `api_key` in each call. Keys passed this way can appear in the agent's private tool history; keep that conversation private and never commit a key. There is no OAuth flow today. See the [current agent guide](https://fanzero.app/agents.md) for tool schemas and authentication details.

Publishing creates a listing and offers the revenue shares you approve. The studio approves a creator's dated plan once; the share runs 28 days from its earliest scheduled action. No proof stage is needed for new pacts. FanZero records the agreement; payouts happen directly between the studio and creator.

## Validate locally

These commands validate files; they do not install a plugin:

```bash
claude plugin validate ./plugins/fanzero
claude plugin validate .
```

The plugin ZIP contains only manifests, the skill, an icon and the integration license. They contain no hooks or executable dependencies. Publication to official directories is a separate review; installing from this repository does not imply approval by OpenAI or Anthropic.

## Source and support

- [FanZero agent guide](https://fanzero.app/agents.md)
- [OpenAI plugin packaging](https://developers.openai.com/plugins/build/plugins)
- [OpenAI directory submission](https://developers.openai.com/plugins/deploy/submission)
- [Claude Code marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code manifest reference](https://code.claude.com/docs/en/plugins-reference)
- [Report an integration issue](https://github.com/marcos-recolons/fanzero-agents/issues)

MIT covers the files in this integration repository. It does not license the hosted FanZero application, any submitted game, or third-party assets. Codex and Claude Code are products of their respective owners.
