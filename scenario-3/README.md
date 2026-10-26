# Scenario 3 — Tailwind Components

**You work at Tailwind Components** (Girona, ES), a distributor of drivetrain, brake and wheel components for independent bike shops.

Tailwind supplies shops across Catalonia. Two large online retailers sell the same Shimano and SRAM parts direct to riders, and shops keep quoting their prices back.

Your job: get both competitors' catalogues into TidyMonk so the pricing team can
compare them against our own list.

## The two competitors

| | Shop | Start from this category |
|---|---|---|
| **A** | `cambria-bike.myshopify.com` — Cambria Bike | `/collections/mtb-road-brake-cables` (~192 products) |
| **B** | `bicyclewarehouse.com` — Bicycle Warehouse | `/collections/26-inch-bike-tires` (~194 products) |

Crawl **the category, not the whole shop**. Both shops carry thousands of products
and you have ninety minutes. Scoping the crawl is part of the job.

These two genuinely stock the same brands — Abus, Cane Creek, Continental, DT Swiss, Maxxis, Shimano among others — so a comparison
is possible. Whether your data supports one is the thing to find out.

## Rules

**Everything through MCP.** Ask your agent. Do not open the ScrapeMonk web app to do
the work, do not call the API with curl, do not touch the database. Looking at the web
app to *check* a result is fine — doing the work there is not.

If you want something and there is no tool for it, **write it in `FINDINGS.md`**. That
list is half the point of today.

## Done when

- [ ] Both categories crawled and extracted
- [ ] A CSV of each produced by ScrapeMonk and sitting in S3
- [ ] You can answer, per shop: how many products, how many priced, **which currency**
- [ ] You can say how many products appear in **both** catalogues, and on what basis
      you matched them

That last one is the real question. A row with a name, a price and a photo reads
perfectly and matches nothing.

## Worth knowing

- **Creating a job is not the same as running one.** Creating it learns the site and
  stops with an estimate. Starting it spends. Your agent should tell you which just
  happened — if it does not, ask.
- **Extraction asks before it runs.** The job stops at a preview so a person can look
  at a sample first. Look at it properly — that preview is the cheapest moment to
  catch a bad parse.
- **Check the currency before comparing anything.** Not every shop prices in the same
  one, and nothing in a spreadsheet will warn you.
- If a job seems stuck, ask your agent what state it is in before restarting anything.
- Both shops are on Shopify, which ScrapeMonk handles well. Neither has been crawled
  before, so the first job on each will run discovery — about a minute.

## Notes

Write what surprised you here, especially anything where you knew what you wanted and
could not get the agent to do it.
