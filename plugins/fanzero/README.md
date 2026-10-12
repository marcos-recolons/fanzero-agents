# FanZero Publish

Find a place to distribute your indie game and connect with content creators who can bring an audience to its launch. This plugin gives Codex and Claude Code a publishing skill for preparing a compatible build, a reviewed listing and revenue-share offers on [FanZero](https://fanzero.app).

Invoke `fanzero-publish` in Codex or `/fanzero:fanzero-publish` in Claude Code. Start with an assessment or draft; submitting a game needs a clear publishing request and approval of its revenue-share terms. Current uploads require an offline HTML build or playable slice, bundled assets, an `index.html` entry and at most 8 MB. An arbitrary native executable is not an upload format.

The plugin contains instructions and an icon. It has no hooks, executable dependencies, automatic MCP connection or embedded credentials. Installing it does not create a studio, publish a game or approve a creator. For optional manual connection instructions, see the [integration repository](https://github.com/marcos-recolons/fanzero-agents) and [current agent guide](https://fanzero.app/agents.md).

## Data when using FanZero

The skill has no storage or telemetry of its own. If you choose a manual MCP or HTTPS connection, your agent sends data to `https://fanzero.app`: studio details and any contact you provide, build files, listing content, pact terms and creator action schedules. Studio calls also send your API key for authentication. FanZero stores accounts, submitted builds and listings, and pact records. `check_build` processes the supplied build without saving it as a draft or submission. Account, publication and pact records currently have no automatic deletion or configured retention deadline; they may remain stored for more than 30 days.

New pacts start their 28-day revenue share at the first proposed action date, with one studio approval and no proof stage. FanZero records the agreement; the studio and creator settle payments directly. See `LICENSE` for the MIT license covering this plugin, and [integration issues](https://github.com/marcos-recolons/fanzero-agents/issues) for support.
