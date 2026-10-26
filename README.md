# ScrapeMonk MCP Workshop

Each participant takes one scenario folder. Inside is **a ticket from our own sales
team** — a prospect we met at a conference, warmed up over a few calls, who has now
asked to see a demo built on their real competitors' data. Your job is to produce that
data, driving ScrapeMonk entirely through its agent.

**Where ScrapeMonk sits.** The prospect is buying the end of the chain: ScrapeMonk
gathers, **TidyMonk** cleanses, **MatchMonk** matches products across shops, **PriceMonk**
turns that into a pricing strategy — which is the part they actually want. ScrapeMonk is
second fiddle here, and getting the data **into S3** in a usable shape is the whole of
our contribution. It is also the step that sinks the demo if it goes wrong, because nothing downstream can recover
data that was never collected or never joinable.

This is the workflow we are testing, not a tutorial. It is also the one we actually run
every week: the ticket arrives written for humans, nobody rewrites it into technical
steps first, somebody pastes it to the agent and starts talking. Do that.

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

## About that 300-product limit

Your ticket asks for roughly **300 products from each shop**. Both shops are far larger
than the range you were asked about, and left alone a crawl will happily keep going.

Mind the unit. A crawl is bounded in **pages**, and a page is not a product: listing
pages, filters and pagination all count toward it. So "300 products" and "300 pages"
are not the same instruction, and the gap between them is yours to work out. Check what
you actually ended up with rather than assuming the number you asked for is the number
you got.

A capped catalogue is a partial one. That is fine. Saying it is complete when it is not
is the thing that causes damage, so report what you actually have.

## Done means

- Both competitor ranges extracted.
- A CSV of each **in S3**, produced by ScrapeMonk. That is the handoff to TidyMonk.
- You can say, per shop: how many products, how many priced, which currency, and —
  the one that decides the demo — **how many rows carry something MatchMonk could
  actually join on**, and which field it is.

You are not matching the products yourself; that is MatchMonk's job. You are answering
whether it *could*. A row with a name, a price and a photo reads perfectly and matches
nothing, and that failure only becomes visible two steps later, in front of the client.

## Afterwards

Fill in `FINDINGS.md` while it is fresh — especially anything you wanted to do and
could not, and anything that surprised you about what the data turned out to be.
