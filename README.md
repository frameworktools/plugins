# Framework plugins

Plugins that connect Claude and ChatGPT to [Framework Cloud](https://framework.pub).
Once connected, the agent can read your projects, published artifacts, and
reports, publish files, design blueprints, and write reports from your results.

## Install

**Claude** (chat, Cowork, or Claude Code): open Customize, then Plugins. Select
Add, then Add marketplace, and enter `frameworktools/plugins`. Under Discover,
choose Framework Cloud and select Add. In Claude Code, run:

```
claude plugin marketplace add frameworktools/plugins
claude plugin install framework-cloud@framework
```

**ChatGPT and Codex**: in Codex, run:

```
codex plugin marketplace add frameworktools/plugins
```

Then open the Plugins directory, choose the Framework source, and install
Framework Cloud.

The first time the agent uses Framework Cloud, it opens framework.pub in your
browser. Sign in, choose what the agent may do, and select Connect. The
[guide to AI apps](https://framework.pub/docs/ai-apps) explains each access
level.

## What's inside

`plugins/framework-cloud` connects to the Framework Cloud MCP server at
`https://framework.pub/mcp`. It holds a Claude manifest
(`.claude-plugin/plugin.json` and `.mcp.json`) and a portable manifest for
ChatGPT and Codex (`plugin.json` and `mcp.json`). The marketplace files are
`.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`.

On a self-hosted Framework Cloud server, add the server's own `/mcp` address
as a connector instead.
