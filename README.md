# ScrapeMonk MCP Workshop

A hands-on session. Each participant takes one scenario folder, plays a parts
distributor who needs competitor prices, and gets that data into TidyMonk.

**The one rule: drive ScrapeMonk only through MCP.** No web app, no curl, no
database. If something cannot be done through a tool, that is a finding — write
it down. The gaps are as valuable as the successes.

## Before you start

1. Open ScrapeMonk in the browser and sign in.
2. **Jobs → Connect Agent.** Copy the command it shows you.
3. Paste it into your terminal. It looks like:

   ```
   claude mcp add --transport http scrapemonk https://app.dev.scrapemonk.io/api/mcp \
     --header "Authorization: Bearer ..."
   ```

4. **Restart Claude Code.** MCP tools register when a session starts, so a server
   added mid-session will not appear until you restart. This catches everybody once.
5. Check it worked — ask your agent to list your jobs. If it cannot see a
   `scrapemonk` tool, the restart did not happen.

> The token in that command is your own browser session and **expires in 24 hours**.
> If tools stop working tomorrow, copy a fresh command from the same dialog.

## Your scenario

Open your folder — `scenario-1` through `scenario-7` — and read its README.
Each has a different company, a different market and two different competitors.

## Done means

- Both competitor catalogues extracted.
- A CSV of each in S3, produced by ScrapeMonk.
- You can state, for each site: how many products, how many priced, **which
  currency**, and whether the rows carry anything to match on.

That last one is the real question. A row with a name, a price and a photo reads
perfectly and matches nothing.
