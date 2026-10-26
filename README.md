# ScrapeMonk MCP Workshop

Each folder holds one scenario: a prospect who wants a demo built on their competitors'
real data. Your job is to produce that data, driving ScrapeMonk **only through MCP** —
no web app, no curl, no database. Checking a result in the web app is fine; doing the
work there is not.

If something cannot be done through a tool, that is a finding. Write it in your
scenario's `FINDINGS.md`. The gaps are the point.

## Setup

1. Open ScrapeMonk in the browser and sign in.
2. **Jobs → Connect Agent**, copy the command:

   ```
   claude mcp add --transport http scrapemonk https://app.dev.scrapemonk.io/api/mcp \
     --header "Authorization: Bearer ..."
   ```

3. Paste it into your terminal, then **restart Claude Code** — MCP tools only register
   at session start.
4. Ask your agent to list your jobs. If it sees no `scrapemonk` tool, the restart did
   not happen.

The token is your browser session and expires in 24 hours.

## The pipeline

ScrapeMonk gathers → **TidyMonk** cleanses → **MatchMonk** matches products across shops
→ **PriceMonk** produces the pricing strategy, which is what the prospect is buying.

Our step is the gathering and the S3 handoff. Nothing downstream can recover data that
was never collected, or that arrives with nothing to join on.

## You cannot see the server

No logs, no shell, no database. What you learn about a running job comes back through
the agent's tools or the UI — most usefully the job's own **event stream**. A job that
stalls, a crawl that went somewhere you did not ask it to, a step that quietly refused:
the job will have said so in an event and nowhere else.

So when something looks wrong, ask what state the job is in before restarting anything.
If the answer is thin, write that down — a tool that cannot say why something stalled is
a gap worth hearing about.

## Pages are not products

Your ticket asks for ~300 products per shop. A crawl is bounded in **pages**, and
listings, filters and pagination all count toward that. "300 products" and "300 pages"
are different instructions. Check what you actually got.

A partial catalogue is fine. Reporting it as complete is not.

## Done means

- Both ranges extracted, a CSV of each **in S3**.
- Per shop: product count, how many priced, which currency, and how many rows carry
  something MatchMonk could join on — and which field that is.
