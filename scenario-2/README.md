# Scenario 2 — Kettle & Crank

**Prospect.** Kettle & Crank, Amsterdam — espresso machines, grinders and spares for
cafe fit-outs. Met at World of Coffee, several calls since. Before committing they
want a demo built on their own market rather than a slide.

**What they asked for.** A like-for-like price comparison on the **Rancilio** line,
using the two competitors they named. Three fit-outs this quarter were renegotiated
mid-quote on online pricing. Rancilio is most of a two-group install, so it sets the
tone for the whole quote.

## Sites to pull

| | Shop | Range |
|---|---|---|
| **A** | The Espresso Shop | https://theespressoshop.co.uk/collections/rancilio (~108 products) |
| **B** | Espresso Parts | https://espressoparts.com/collections/rancilio (~250 products) |

Around **300 products from each** is enough. This is a demo, not a delivery.

## Where this sits

ScrapeMonk gathers → TidyMonk cleanses → MatchMonk matches → PriceMonk produces the
pricing strategy, which is what they are buying. Our step is the gathering and the
handoff: both ranges extracted and **landed in S3**.

## What to report back

Per shop: how many products, how many priced, which currency, and **how many rows
carry something MatchMonk could join on** — a GTIN or EAN, a manufacturer part number,
a brand plus model. Not the product name.

You are not matching the products; that is MatchMonk's job. You are answering whether
it could. If a lot of rows have nothing to join on, that is the finding — say it.

Workshop rules and setup: [root README](../README.md). Anything you could not do
through the agent goes in `FINDINGS.md`.
