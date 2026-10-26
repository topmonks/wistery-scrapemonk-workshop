# Scenario 5 — Additiva Works

**The prospect is invented for this exercise.** Additiva Works — a supplier keeping
print farms running with hotends, extruders and motion parts. They want to see a demo
built on their own market before they commit; they have been pitched competitor
monitoring before and got back a spreadsheet nobody could use. The two competitor
shops below are real, and so is their data.

**What they asked for.** A like-for-like price comparison on the **Bambu Lab
accessories** line, using the two competitors they named. Procurement places an order
in a fortnight and wants to know whether the margin on the accessory line is
defensible. Accessories are consumables, so customers reorder often and notice price
first.

## Sites to pull

| | Shop | Range |
|---|---|---|
| **A** | West3D | https://west3d.com/collections/bambu-bambu-lab-printer-accessories (~187 products) |
| **B** | Fabreeko | https://fabreeko.com/collections/bambu-labs (~102 products) |

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
