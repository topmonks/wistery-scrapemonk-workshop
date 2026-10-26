# Scenario 1 — Fairlawn Supply

**The prospect is invented for this exercise.** Fairlawn Supply — a distributor selling
replacement parts for walk-behind mowers, ride-ons and small engines to independent
repair shops. They want to see a demo built on their own market before they commit.
The two competitor shops below are real, and so is their data.

**What they asked for.** Current prices across the **mower and small-engine spares**
range at the two online retailers they named. Their repair-shop customers price-check
against both before ordering, and Fairlawn has no idea where they sit.

## Sites to pull

| | Shop | Range |
|---|---|---|
| **A** | Mower Parts Group | https://www.mowerpartsgroup.com/collections/all |
| **B** | Lawn Mower Parts World | https://lawnmowerpartsworld.com/collections/all |

Around **200 products from each** is enough. This is a demo, not a delivery.

## Where this sits

ScrapeMonk gathers → TidyMonk cleanses → MatchMonk matches → PriceMonk produces the
pricing strategy, which is what they are buying. Our step is the gathering and the
handoff: both ranges extracted and **landed in S3**.

## What to report back

Per shop: how many products you got, how many of them carry a price, and which
currency. Then say whether you would hand this on as it stands.

## Worth a look

Both shops are spare-parts catalogues — many small, near-identical items separated only
by a part number. Check whether what you extracted tells two similar parts apart.

Workshop rules and setup: [root README](../README.md). Anything you could not do
through the agent goes in `FINDINGS.md`.
