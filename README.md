# RemixViral plugins for Claude Code

RemixViral is an AI clip maker built for AI agents to operate over MCP: you upload a long video you own, your agent reads the ranked, captioned 9:16 Shorts cut from it (with the reason each was picked) and can start faceless Shorts, and you tag the work, review and approve.

## At a glance

| | |
|---|---|
| Who it is for | AI agents and assistants that operate it, and the people who supervise them: podcast, webinar and event teams, agencies, in-house video teams, creators, small businesses |
| Does not do | No link import (upload your own video only), no timeline editor, no team seats, no free plan, no translation of other people's videos, no guarantee of views |
| Price | From the Starter plan; no free plan. Current plans and what a clip project costs: https://remixviral.ai/pricing.md |
| Human oversight | The owner approves access on an OAuth consent screen, sees and revokes keys under Dashboard, API keys, and, for an API key they create themselves, can limit its scopes. Spending is capped by the prepaid credit balance. There is no per-action approval queue; confirmation depends on your MCP client |
| MCP server | `https://remixviral.ai/api/mcp` (Streamable HTTP), registry name `ai.remixviral/clipper` |
| Docs | https://remixviral.ai/en/mcp (agent quickstart, human oversight), https://remixviral.ai/mcp.md, https://remixviral.ai/llms.txt |
| Official listing | Published in the Official MCP Registry as `ai.remixviral/clipper`; details at https://remixviral.ai/en/mcp |

## Example prompts (you tag the work, you review the result)

- "Assign to RemixViral: go through my latest clip job and pick the three best clips. Show me the start and end times, the score and why each was picked, so I can approve them."
- "Use RemixViral to list my videos that are still rendering and the finished ones with links, so I can review what is ready."
- "Assign to RemixViral: a 30-second faceless Short about three tips for choosing a wedding photographer. Check my balance and tell me the cost first, and only create it after I say yes."

More on https://remixviral.ai/en/mcp#prompts.

A Claude Code plugin marketplace with one plugin, `remixviral`: the MCP server, two skills and three commands.

## Install

```text
/plugin marketplace add airdropfi/remixviral-claude-plugin
/plugin install remixviral@remixviral-plugins
```

You need a RemixViral account (https://remixviral.ai) and Claude Code. Reading clips, videos and your balance is free; `create_video` spends credits and the plugin asks before it. From a shell: `claude plugin marketplace add airdropfi/remixviral-claude-plugin` then `claude plugin install remixviral@remixviral-plugins`.

Then `/reload-plugins`, open `/mcp`, choose `remixviral` and Authenticate (OAuth sign-in in your browser; no key to paste). Details and usage are in [plugins/remixviral/README.md](plugins/remixviral/README.md).

## Layout

```text
.claude-plugin/marketplace.json     marketplace "remixviral-plugins", lists the plugin
plugins/remixviral/
  .claude-plugin/plugin.json        manifest (name, version, listing URLs, icon)
  .mcp.json                         remote MCP server https://remixviral.ai/api/mcp (OAuth)
  skills/                           review-my-clips, make-a-faceless-short
  commands/                         /remixviral:clips, :videos, :credits
  README.md, LICENSE, assets/icon.png
scripts/validate.mjs                schema checks, no dependencies
LICENSE                             MIT
```

## Validate

```bash
node scripts/validate.mjs            # documented-schema checks, exit 1 on errors
node scripts/validate.mjs --strict   # warnings fail too
node scripts/validate.mjs --cli      # also runs `claude plugin validate --strict` when the claude CLI is installed
```

## Keeping it honest

- The skills name tools from the RemixViral MCP server's tool list.
- Prices and balances are never written in the skills. They come from tool output only.
- No earnings or performance claims.

## License

MIT, see [LICENSE](LICENSE).
