# Facilitator notes — keep out of the participant folders

## The four shops, and why these

All four are Shopify, chosen by a two-stage check rather than by taste:

1. **`/products.json` answers.** If a shop serves it, it is not behind a bot wall. Every
   site that answered it crawled fine; every site that did not, failed. Car-parts
   retailers (FCP Euro, ECS Tuning, Autodoc, Turner) were all tried and all died in
   preanalysis with `Preanalysis failed: unknown` — Cloudflare. Do not substitute a shop
   without running this check first.
2. **A real crawl produced products.** Not a screen, an actual job.

| # | Shop | Seed | cap 40 run → pages / products |
|---|---|---|---|
| 1A | Mower Parts Group | `/collections/all` | 112 / **49** |
| 1B | Lawn Mower Parts World | `/collections/all` | 82 / **44** |
| 2A | Chainsaw Bars | `/collections/all` | 102 / **41** |
| 2B | Simply Bearings | site root | 83 / **43** |

Four of four produced products with **zero failed URLs**. Measured 2026-10-27.

## Why `/collections/all` and not the site root

A Shopify homepage ignores `?page=N`. Seed the crawl at the root and it synthesises
`/?page=2`, `/?page=3` … and every one returns the homepage again — the crawl spends its
budget re-fetching the same page. `/collections/all` paginates for real on 1A, 1B and 2A
(verified: page 1 and page 2 return different product sets).

**2B is the exception on purpose.** Simply Bearings renders its listings in JavaScript,
so `/collections/all` shows one product to a plain fetch and its collection pages look
identical to each other. The crawler renders JS and handles it; the root seed is what was
actually measured working. Leave it as it is.

## Scenario 2 is deliberately not a matched pair

Chainsaw Bars sells cutting gear; Simply Bearings sells drive components. They do not
overlap and the brief does not pretend they do — it asks for two price lists, not a
comparison. **MatchMonk is not part of this workshop**, so no scenario asks anyone to
match anything, and the deliverable is count / priced / currency per shop.

If that changes later, scenario 2 is the one to replace: pairing needs two shops carrying
the same manufacturer's parts, which is a much narrower search.

## The cap counts products, not pages

Changed 2026-10-26 (`33b419e9`). `max_pages`/`maxUrls` is now a number of **product
pages**; listings and pagination no longer spend it. A safety ceiling of 10× stops a
crawl that finds nothing.

This matters because of what it fixed: `JobMaintenanceService` was ending jobs at *N
fetched URLs* while the worker counted *product pages*, and the sweep is what finishes a
job. The ordinary shape of a crawl — collection page, its pager, then products — meant
jobs hit N in URLs before any product was fetched, got completed, and had every queued
product link marked `ignored`. They reported success with zero products. Twelve of
fourteen prep crawls died this way. If anyone sees a job "complete" suspiciously fast
with nothing in it, that is the shape to recognise, and it should not happen now.

Practical consequence: a 200-product cap fetches noticeably more than 200 pages. The
runs above fetched 82–112 pages for ~40 products.

## Concurrency

Jobs per account come from the tier, live from the WADM catalog:

| tier | concurrent jobs | crawlers |
|---|---|---|
| premium | 2 | 10 |
| platinum | 4 | 50 |

**Participants on premium get two concurrent jobs** — exactly the two their scenario
needs, with no headroom. A third job queues. Queued jobs wait; they do not fail (the
old behaviour where a refused job was marked `failed` is gone).

Workers are a **shared pool**, not per-person: the pool is sized by the sum of entitled
crawlers across users with active jobs, capped by `MAX_WORKERS` (20 on dev). Seven
premium participants ask for 70 crawler slots, which saturates the cap — fine, but
expect queueing at the start when everybody launches at once.

## What will go wrong

- **Tools missing after `claude mcp add`.** MCP registers at session start. They must
  restart Claude Code. This catches nearly everybody once.
- **Token expires in 24 hours.** The Connect Agent dialog hands out the signed-in user's
  own Auth0 token. If anyone's tools die, re-copy it.
- **Everyone starts at the same moment.** Worker VMs cold-start: boot, pull image, launch
  the browser. The first pages take a few minutes to appear. It is not broken.
- **`category_urls` seeds, it does not scope.** The crawler follows links out of the
  requested area and raises a `scope_drift` event saying so. The briefs do not mention
  this — it is one of the things they should find in the event stream. If nobody notices
  by the debrief, ask who checked where their crawl actually went.

## Questions worth asking in the debrief

- Which did you trust more, the preview or the finished data? Why?
- What did you have to do outside MCP, and what tool would have saved you?
- How many pages did your crawl fetch to get 200 products? Did that surprise you?
- Did you check where the crawl actually went, or only what it returned?
- Two parts differ only by a part number. Does your data tell them apart?
