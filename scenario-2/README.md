# Scenario 2 — Brackenside Plant

**The prospect is invented for this exercise.** Brackenside Plant — a UK maintenance
contractor that keeps groundscare and light plant machinery running for councils and
estates. They buy consumables and replacement components from specialist suppliers and
want to see a demo built on their own buying before they commit. The two shops below
are real, and so is their data.

**What they asked for.** Current prices from the two suppliers they buy most from. The
ranges are different — one is cutting gear, the other is drive components — so this is
two separate price lists, not a like-for-like comparison.

## Sites to pull

| | Shop | Range |
|---|---|---|
| **A** | Chainsaw Bars | https://www.chainsawbars.co.uk/collections/all |
| **B** | Simply Bearings | https://simplybearings.co.uk/ |

Around **200 products from each** is enough. This is a demo, not a delivery.

## Where this sits

ScrapeMonk gathers → TidyMonk cleanses → MatchMonk matches → PriceMonk produces the
pricing strategy, which is what they are buying. Our step is the gathering and the
handoff: both ranges extracted and **landed in S3**.

## What to report back

Per shop: how many products you got, how many of them carry a price, and which
currency. Then say whether you would hand this on as it stands.

## Worth a look

Shop B is a very large catalogue — far more than you are being asked for. Decide what
you point the crawl at, and be able to say what you got and what you left behind.

Workshop rules and setup: [root README](../README.md). Anything you could not do
through the agent goes in `FINDINGS.md`.
