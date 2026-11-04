# Personify plugin

Make AI UGC reels for your brand without leaving your AI assistant. [Personify](https://personify.gg) turns a brand brief into vertical creator-style videos with AI presenters, in 100 formats measured from proven viral reels. This plugin gives Claude, Codex, ChatGPT or Cursor eleven skills on top of the Personify MCP server: browse the formats, write hooks and scripts that fit them, plan a batch of drafts, follow progress, and quote a render before a single credit is spent.

![Personify](assets/personify.png)

## Install

**Claude Code**

```bash
claude plugin marketplace add personify-gg/personify-plugin
claude plugin install personify@personify
```

Then start Claude Code, run `/mcp`, choose `plugin:personify:personify` and select **Authenticate**. Personify opens in your browser: sign in, check that the brand you want is the one selected, and select **Authorize access**.

**claude.ai and Cowork**

Open **Customize > Plugins**, add the marketplace `personify-gg/personify-plugin`, install Personify, and connect it on its **Connectors** tab.

**Codex, ChatGPT and Cursor**

The same folder is an [Agent Plugin](https://agent-plugins.org/specification) (`plugin.json`, `mcp.json`, `skills/`). Add it from the app's plugin settings, then sign in to Personify when asked.

You need a Personify account with a brand. Sign up at [personify.gg](https://personify.gg).

## Skills

| Skill | What it does | Personify tools it calls |
| --- | --- | --- |
| `/personify:connect` | Sign in, show the connected brand and what the connection can do | `get_brand` |
| `/personify:formats [filter]` | Browse the 100 reel formats and pick three that fit the brand | `get_brand`, `list_formats` |
| `/personify:hooks [format]` | Ten opening hooks across five angles, inside the format's limits | `get_brand`, `list_formats`, `list_videos` |
| `/personify:script [format]` | Write a script that fits a format and save it as a draft, or edit a draft | `get_brand`, `list_formats`, `create_draft`, `get_video`, `edit_draft` |
| `/personify:remake [format or reel]` | Make the brand's version of a viral format, or a fresh take on one of its own reels | `get_brand`, `list_formats`, `list_assets`, `get_video`, `create_draft` |
| `/personify:plan [count, goal]` | Plan up to ten reels across formats, then save the approved ones as drafts | `get_brand`, `list_formats`, `list_videos`, `list_assets`, `create_draft` |
| `/personify:status [id]` | Drafts, renders in progress, finished and failed reels, and the next step for each | `list_videos`, `get_video` |
| `/personify:review <id>` | The link where the owner checks a draft and confirms its render in Personify | `prepare_generation_approval` |
| `/personify:render <id>` | Quote a render, ask you to confirm the price, then start it; without the render permission, the owner's review link | `get_video`, `quote_video`, `render_video`, `prepare_generation_approval` |
| `/personify:download <id>` | The mp4 of a finished reel the owner approved | `get_video_download`, `list_assets` |
| `/personify:assets [kind]` | The brand's finished reels, clips, photos and approved references | `list_assets`, `list_approved_assets` |

In Claude the skills run as `/personify:<skill>`; every assistant also uses them on its own when your request matches, for example "give me five reel ideas for this week".

## Spending is opt-in

Saving a draft never generates or charges anything. The standard connection this plugin makes cannot spend credits at all: it reads your brand and saves drafts, and the owner confirms each render inside Personify from a review link.

The assistant can start a render only if the owner approved Personify's separate render permission on the consent screen. Even then, `/personify:render` gets a quote first, shows you the price and starts the render only after you answer yes to that price in the conversation. Personify itself refuses a render without a fresh quote, the draft's exact version and `confirm: true`. `/personify:render` explains how an owner adds the render permission.

## What the plugin sends and fetches

- The plugin declares one remote MCP server, `https://personify.gg/api/mcp`, run by Personify. It has no local code, hooks or scripts.
- The assistant sends Personify the titles, scripts and captions you approve when it saves or edits a draft, and the ids of the videos it reads, quotes or renders.
- The assistant receives your brand profile, your drafts and videos, your media library with links that expire, the Format Book, and quotes.
- Sign-in uses OAuth 2.1 with PKCE in your browser; the assistant never sees your Personify password. One connection covers one brand, every call is logged in your Personify account, and you can revoke access any time under Settings > AI connections.
- `/personify:download` can offer to save a finished reel with `curl` from the link Personify returns, and `/personify:render` mentions the Personify CLI (`npx personify-cli@0.1.0`) as an option; neither runs unless you agree.

What Personify stores and how it uses data: [privacy policy](https://personify.gg/privacy) and [terms](https://personify.gg/terms).

## What it cannot do

Create or switch brands, upload footage or photos, publish or schedule posts, change billing, run research or strategy, or approve a final review. Those stay in the Personify app.

## Support

Email [info@personify.gg](mailto:info@personify.gg). Documentation: [personify.gg/docs/agents](https://personify.gg/docs/agents) and [personify.gg/docs/mcp](https://personify.gg/docs/mcp).

## License

MIT
