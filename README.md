# RemixViral plugins for Claude Code

A Claude Code plugin marketplace with one plugin, [`remixviral`](plugins/remixviral/README.md): read the ranked Shorts RemixViral cut from your long videos, and make faceless Shorts from a topic, with the cost shown and your yes required before anything spends credits.

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
