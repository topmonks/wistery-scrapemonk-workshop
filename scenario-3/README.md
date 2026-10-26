# Scenario 3 — Tailwind Components

**The prospect is invented for this exercise.** Tailwind Components — a distributor
supplying independent bike shops with drivetrain, brake and wheel parts. They want to
see a demo built on their own market before they commit; they have been pitched
competitor monitoring before and got back a spreadsheet nobody could use. The two
competitor shops below are real, and so is their data.

**What they asked for.** A like-for-like price comparison on the **Continental tyres**
line, using the two competitors they named. Their shops are undercut by walk-in
customers quoting online prices. They want to know if it is a few loss-leaders or the
whole range.

## Sites to pull

| | Shop | Range |
|---|---|---|
| **A** | Cambria Bike | https://cambriabike.com/collections/continental (~210 products) |
| **B** | Bicycle Warehouse | https://bicyclewarehouse.com/collections/continental-bike-tires (~215 products) |

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
