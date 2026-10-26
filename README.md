# ScrapeMonk MCP Workshop

Each participant takes one scenario folder. Inside is **a ticket from sales** — the
kind we actually get: business context, a competitor or two, and a vague-but-real ask.
Your job is to turn it into data, driving ScrapeMonk entirely through its agent.

This is the workflow we are testing, not a tutorial. In real life nobody rewrites the
sales ticket into technical steps first — they paste it to the agent and start talking.
Do that.

**The one rule: drive ScrapeMonk only through MCP.** No web app, no curl, no database.
Looking at the web app to *check* a result is fine. Doing the work there is not. If
something cannot be done through a tool, that is a finding — write it in your scenario's
`FINDINGS.md`. The gaps are as valuable as the successes.

## Before you start

1. Open ScrapeMonk in the browser and sign in.
2. **Jobs → Connect Agent.** Copy the command it shows you.
3. Paste it into your terminal. It looks like:

   ```
   claude mcp add --transport http scrapemonk https://app.dev.scrapemonk.io/api/mcp \
     --header "Authorization: Bearer ..."
   ```

4. **Restart Claude Code.** MCP tools register when a session starts, so a server added
   mid-session will not appear until you restart. This catches everybody once.
5. Check it worked — ask your agent to list your jobs. If it cannot see a `scrapemonk`
   tool, the restart did not happen.

> The token is your own browser session and **expires in 24 hours**. If tools stop
> working tomorrow, copy a fresh command from the same dialog.

## You cannot see the server

No logs, no shell, no database. Everything you learn about a running job comes back
through the agent's tools or the UI — and the most useful of those is the job's own
**event stream**. A job that looks stuck, a crawl that wandered somewhere you did not
ask it to go, a step that quietly refused: the job will usually have said so in an
event, and nowhere else.

So when something looks wrong, the first move is not to restart it. Ask the agent what
state the job is in and what it has reported. If the answer you get is thin, that is
worth writing down — a tool that cannot tell you why something stalled is a gap, and
we would rather hear it from you today than from a customer.

## You have about ninety minutes

Both shops in your ticket run to a few hundred products, but these shops are far bigger
than the range you were asked about and a crawl will happily keep going. **Cap it at
roughly 300 pages** so you get to the interesting part — the data — inside the session.

A capped catalogue is a partial one. That is fine. Saying it is complete when it is not
is the thing that causes damage, so report what you actually have.

## Done means

- Both competitor ranges extracted.
- A CSV of each in S3, produced by ScrapeMonk.
- You can answer the ticket: how many products, how many priced, and **how many appear
  on both sides** — stating what you matched them on.

That last one is the real question, and it is the one sales actually asked. A row with
a name, a price and a photo reads perfectly and matches nothing.

## Afterwards

Fill in `FINDINGS.md` while it is fresh — especially anything you wanted to do and
could not, and anything that surprised you about what the data turned out to be.
