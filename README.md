# How to connect Strava to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Strava account.** Strava's official Claude connector is read-only and only for Strava subscribers, and Strava has no official ChatGPT app. Cotlet.dev connects your own signed-in Strava account to any AI agent, so you can ask in plain words and the AI lists your activities and updates their gear for you.

## What you can ask

> List all my rides from the last 7 days with distance, moving time and elevation gain.

> Set the gear on every run since October 1 to my Nike Pegasus 41.

> Change the bike on Saturday's 82 km ride to my Canyon Endurace.

> Show my 10 longest runs this month and which shoes I wore for each one.

> How many km are on my Hoka Clifton 9? List the runs logged with them since August.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Strava tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"strava":{"command":"uvx","args":["strava-cotlet-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t strava-mcp .
docker run -i --rm -e COTLET_API_KEY strava-mcp
```

Tools: `strava_guide`, `strava_status`, `strava_open`, `strava_read`, `strava_click`, `strava_type`, `strava_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install strava-cotlet-mcp        # or run it once: uvx strava-cotlet-mcp connect
strava-cotlet-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 strava_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 strava_agent.py status    # is Strava ready in your Cotlet.dev account
python3 strava_agent.py guide     # Strava screens and sign-in link
python3 strava_agent.py read      # open Strava, read the page, close the browser
python3 strava_agent.py tools     # list Cotlet.dev tools
python3 strava_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Strava users

**Does Strava have an API?**

Strava has an official API and, since 1 June 2026, an official MCP connector (checked 27 Oct 2026). The MCP is read-only, works with Claude only and needs a paid Strava subscription. Cotlet.dev works in your own signed-in Strava account, so your AI agent can list activities and update gear with no API key and no code.

**Is there an official Strava integration for ChatGPT?**

Strava has no official ChatGPT app. It lists Claude and Gemini as its supported assistants. Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Strava once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Strava API key.

**Is there a Strava connector for Claude?**

Yes. Strava has an official read-only Claude connector for subscribers. To also update activity gear, run the one-line `claude mcp add` command above in Claude Code. In the Claude app, add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Strava account through Cotlet.dev.

**Is there a Strava MCP server?**

Strava offers an official, Anthropic-verified connector for Claude with read-only access for subscribers. Cotlet.dev is a hosted MCP server that works in Strava for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier, including updating activity gear.

## Find it on

- [Strava on Cotlet.dev](https://cotlet.dev/integrations/strava-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=strava&utm_content=find)
- [PyPI package strava-cotlet-mcp](https://pypi.org/project/strava-cotlet-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-strava-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/strava-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=strava

Start free: https://cotlet.dev/signup?app=strava&utm_source=github&utm_medium=readme&utm_campaign=strava
