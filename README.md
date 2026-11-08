# How to connect Contractor+ to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Contractor+ account.** Contractor+'s own integration catalog lists no official ChatGPT app or Claude connector. Cotlet.dev connects your own signed-in Contractor+ account to any AI agent, so you can ask in plain words and the AI creates estimates, schedules jobs and sends invoices for you.

## What you can ask

> Create an estimate for Mark Davis: replace 120 sq ft of bathroom tile at $14 per sq ft labor plus $850 in materials, and email it to him.

> Turn the approved estimate for the Rivera kitchen remodel into a job and schedule it for Monday at 8 am with Luis's crew.

> Invoice Sarah Chen $2,400 for the deck repair we finished yesterday, due in 15 days.

> Which estimates I sent in the last 30 days are still not approved? List them with the client and amount.

> Show me all unpaid invoices older than 14 days and the total still owed.

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

This repo is a real MCP server. It speaks MCP over stdio, lists its Contractor+ tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"contractor-plus":{"command":"uvx","args":["contractor-plus-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t contractor-plus-mcp .
docker run -i --rm -e COTLET_API_KEY contractor-plus-mcp
```

Tools: `contractor_plus_guide`, `contractor_plus_status`, `contractor_plus_open`, `contractor_plus_read`, `contractor_plus_click`, `contractor_plus_type`, `contractor_plus_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install contractor-plus-mcp        # or run it once: uvx contractor-plus-mcp connect
contractor-plus-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 contractor_plus_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 contractor_plus_agent.py status    # is Contractor+ ready in your Cotlet.dev account
python3 contractor_plus_agent.py guide     # Contractor+ screens and sign-in link
python3 contractor_plus_agent.py read      # open Contractor+, read the page, close the browser
python3 contractor_plus_agent.py tools     # list Cotlet.dev tools
python3 contractor_plus_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Contractor+ users

**Does Contractor+ have an API?**

Contractor+ has a public API with an account key, but it comes only with the Pro Team plan, together with Zapier. Cotlet.dev works in your own signed-in Contractor+ account on any plan, so your AI agent can create estimates, jobs and invoices.

**How do I connect Contractor+ to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Contractor+ once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Contractor+ API key.

**Is there a way to use Claude with Contractor+?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Contractor+ account.

**Is there a Contractor+ MCP server?**

Contractor+ has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted Contractor+ MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Contractor+ on Cotlet.dev](https://cotlet.dev/integrations/contractor-plus-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=contractor-plus&utm_content=find)
- [PyPI package contractor-plus-mcp](https://pypi.org/project/contractor-plus-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-contractor-plus-to-ai-agents-guide)

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
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
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
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/contractor-plus-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=contractor-plus

Start free: https://cotlet.dev/signup?app=contractor-plus&utm_source=github&utm_medium=readme&utm_campaign=contractor-plus
