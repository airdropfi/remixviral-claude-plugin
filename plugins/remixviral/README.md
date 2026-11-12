# RemixViral for Claude Code

Read the ranked, captioned Shorts [RemixViral](https://remixviral.ai) cut from your long videos, and make faceless Shorts from a topic, without leaving Claude Code. The plugin connects Claude to the RemixViral MCP server and adds two skills and three commands. Nothing that costs credits runs until you have seen the cost and said yes.

## What it contains

| Component | Name | What it does |
|---|---|---|
| MCP server | `remixviral` (`https://remixviral.ai/api/mcp`) | The RemixViral tools. Sign-in is OAuth; there is no key to paste. |
| Skill | `review-my-clips` | Ranked clips of a clip job with times, reasons and scores. Read-only. |
| Skill | `make-a-faceless-short` | Faceless Short from a topic: balance and cost first, create after your yes. |
| Command | `/remixviral:clips` | Ranked clips of a clip job. Read-only. |
| Command | `/remixviral:videos` | Your latest videos with status and links. Read-only. |
| Command | `/remixviral:credits` | Your credit balance. Read-only. |

## Tools

| Tool | What it does | Charges credits |
|---|---|---|
| `list_clip_jobs` | The clip jobs of your account, newest first. | No |
| `get_clip_job` | One job: status, then the ranked clips with start/end seconds, the reason each was picked, a score and a render status. Optional full transcript. | No |
| `create_video` | Starts a faceless Short from a topic (30, 60 or 90 s). Returns an id; the render runs asynchronously. | **Yes** |
| `get_video` | Status and, when done, the video link. | No |
| `list_videos` | Your videos, newest first, optional status filter. | No |
| `list_niches` | Valid niches, art styles, qualities and durations for `create_video`. | No |
| `get_credit_balance` | Credit balance, monthly allocation and plan. | No |

## Install

You need a RemixViral account (https://remixviral.ai) and Claude Code. Clip jobs are started in the app by uploading a long video you own at https://remixviral.ai/dashboard/clips; faceless videos are charged in credits.

```text
/plugin marketplace add airdropfi/remixviral-claude-plugin
/plugin install remixviral@remixviral-plugins
```

From a shell: `claude plugin marketplace add airdropfi/remixviral-claude-plugin` and `claude plugin install remixviral@remixviral-plugins`.

Then run `/reload-plugins`, open `/mcp`, choose `remixviral` and select Authenticate. A browser window opens: sign in to RemixViral and click Allow. Try `/remixviral:credits`.

To try it from a local checkout without a marketplace: `claude --plugin-dir ./plugins/remixviral`.

### API key instead of OAuth

Prefer a key? Create one at https://remixviral.ai/developers; the tools need the `video:read` scope (`create_video` also needs `video:create`, `get_credit_balance` needs `credits:read`), and a key without a needed scope is refused with a 403. To use it, add the server yourself instead of the plugin's OAuth one:

```bash
claude mcp add --transport http remixviral https://remixviral.ai/api/mcp --header "Authorization: Bearer YOUR_API_KEY"
```

## Use

- "Show the best clips RemixViral found in my latest upload" starts `review-my-clips`.
- "Make a 30-second faceless Short about why octopuses have three hearts" starts `make-a-faceless-short` and stops for your yes.
- You can also run a command directly, for example `/remixviral:videos 5`.

## What it will and will not do

- Reading clip jobs, clips, transcripts, videos, niches and your balance is free and changes nothing.
- `create_video` is the one tool that spends credits. Those credits are real and a started render cannot be undone. The agent is told to check your balance, state the cost and wait for your explicit yes first.
- Starting a clip job is done in the RemixViral app by uploading a video you own; no tool takes a link.
- Nothing here posts, schedules, buys credits or changes your plan.
- Faceless videos use AI-generated images and voice. Switch on the platform's AI-content label when you post.
- No result is promised: nobody can tell you how a clip or video will perform.

## Data and privacy

The MCP server receives what the tools need: the ids, topics and settings you ask your agent to send, and the clip, video and credit data on your RemixViral account. This repository stores nothing and runs no code on your machine; it is a server address, Markdown instructions and a logo. See the [privacy policy](https://remixviral.ai/en/privacy) and [terms](https://remixviral.ai/en/terms). Keys and sign-in tokens are revocable in your RemixViral dashboard under API keys.

## Support

https://remixviral.ai/en/support or support@remixviral.ai. Documentation: https://remixviral.ai/en/developers.

## License

MIT for the files in this repository (see `LICENSE`). The RemixViral service is governed by its terms.
