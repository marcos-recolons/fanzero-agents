# FanZero for Codex and Claude Code

Publish an indie game on [FanZero](https://fanzero.app), find an audience for its launch, and work with influencers through revenue-share pacts.

This repository contains a publishing **skill**, marketplace catalogs and optional manual connection recipes. The plugin does not automatically connect to a server, execute code, create accounts, upload games or grant an agent permission to offer revenue. It includes no application source or studio credentials.

There are two packages:

- **FanZero Discover & Plan** (`fanzero-discover`) assesses whether FanZero fits a game and drafts an influencer launch plan from the context you provide. All its instructions are included in the package. It makes no network requests, runs no code and sends no data to FanZero. See its [README](plugins/fanzero-discover/README.md) and [privacy policy](plugins/fanzero-discover/PRIVACY.md).
- **FanZero Publish** (`fanzero`) guides complete listing preparation and one-operation publication through a manual connection to the hosted FanZero service. Its optional transmissions and storage are described in the [plugin README](plugins/fanzero/README.md#data-when-using-fanzero).

The installation commands below install FanZero Publish. To choose Discover & Plan, use `fanzero-discover@fanzero-agents` instead of `fanzero@fanzero-agents`; its Claude Code skill is `/fanzero-discover:fanzero-discover`. Official directory publication is a separate review.

Publish a listing with images or videos, a description, platform links, each platform's prices and currencies or a clear monetization model. The original link is the default when a game is easy to play online. The original game stays unchanged; publishing approval never authorizes an offline adaptation. A hosted preview qualifies only when representative of the original, played successfully in FanZero's sandbox, and preferable to the original link for a concrete reason. Agent uploads require truthful `preview_review` attesting to those facts. Unknown or false criteria mean publish media and original platform links without an upload. A qualifying upload needs offline HTML, bundled assets, an `index.html` entry and at most 8 MB and 1000 files. A listing needs no game port, playable slice or repository change. A human curator reviews each new game.

## Install in Codex

On a Codex CLI with plugin marketplace support:

```bash
codex plugin marketplace add marcos-recolons/fanzero-agents
codex plugin add fanzero@fanzero-agents
```

Restart the client or begin a new session, then ask:

> Use FanZero Publish to prepare a complete game listing and revenue-share offer for my approval.

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

Install the skill without MCP for planning and listing guidance. When you want the publishing tools, add an anonymous connection yourself:

```bash
# Codex
codex mcp add fanzero --url https://fanzero.app/mcp

# Claude Code
claude mcp add --transport http fanzero https://fanzero.app/mcp
```

`connections/codex.toml` and `connections/claude-code.json` show equivalent settings. They are outside the plugin and are not loaded during installation. Merge settings only when you decide to connect; avoid replacing an existing configuration file.

Read-only tools such as `read_listing_guidelines`, `check_build`, `whoami` and `browse_games` work without a key. **`create_studio` creates an account and must be authorized**. For a complete publication, `publish_game` accepts an existing studio key or approved `studio: { name, contact }` and creates the studio and listing together. It requires `human_approved: true` reflecting real approval and a stable `idempotency_key`; reuse the same key and identical payload when retrying. Keep any returned API key privately, because anonymous replays return a receipt without recovered credentials. Existing-studio calls require the key. Keys passed this way can appear in the agent's private tool history; keep that conversation private and never commit a key. There is no OAuth flow today. See the [current agent guide](https://fanzero.app/agents.md) for tool schemas and authentication details.

Publishing creates a listing and offers the revenue shares you approve. The studio approves an influencer's dated plan once; the share runs 28 days from its earliest scheduled action. No proof stage is needed for new pacts. After the window, the studio settles it: each platform's net revenue from that platform's own report, sent with your approval, which the influencer accepts or disputes. FanZero records the agreement and the settlement; the studio pays the influencer directly.

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
