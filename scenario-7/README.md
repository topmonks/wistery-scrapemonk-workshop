> **Scenario 7** — you are preparing the demo. Workshop rules and setup are in the
> [root README](../README.md). Record anything you could not do in `FINDINGS.md`.

# DEMO-1573 — Lustre Supply: demo data for the Koch Chemie comparison

## Who they are

Lustre Supply are a Dublin distributor serving detailing studios — polishes, coatings,
machines, consumables. We met them at Waxstock and have had three calls since. They
are interested but not convinced — they have been pitched competitor monitoring before
and it came back as a spreadsheet nobody could use.

Two studios renegotiated on them this quarter citing online pricing. That line carries
a lot of their margin and they are currently holding neither price nor volume on
purpose.

## What they asked for

They do not want a slide about what we could do. They asked to see **their own market,
with real numbers**, using the two competitors they named on the last call. If we can
show them a like-for-like comparison on a line that actually hurts, we win this.

Koch Chemie is where their margin lives, so that is the range to put in front of them.

## The two sites they named

| | Shop | Range to pull |
|---|---|---|
| **A** | Slim's Detailing | https://slimsdetailing.co.uk/collections/koch-chemie (~186 products) |
| **B** | Car Supplies Warehouse | https://carsupplieswarehouse.com/collections/automotive-protection-products (~127 products) |

## Where this sits

The prospect is buying the end of the pipeline, not our bit. What they want is
**PriceMonk** telling them where to move their prices. To get there the data goes
ScrapeMonk → **TidyMonk** to cleanse → **MatchMonk** to match products across the two
shops → PriceMonk for the strategy.

Our job here is the first step, and the handoff: both ranges extracted and **landed in
S3**, in a shape the MatchMonk side can pick up without coming back to ask. ScrapeMonk
is playing second fiddle in this demo and that is fine — but if this step is wrong,
nothing downstream recovers.

## What matters about the data

MatchMonk can only join products on something stable — a GTIN or EAN, a manufacturer
part number, a brand plus a model. Not a product name. So the question to answer before
the demo is not "did you get the rows", it is **can these rows actually be matched**:
how many carry an identifier, and which field is it.

If a large share of the rows have nothing to join on, say so now. That is a far better
conversation to have with us than with the client, halfway through the demo.

**Around 300 products from each shop is plenty.** This is a demo, not a delivery. I
would rather have 300 rows that hold up under questioning than a full dump nobody has
checked — they *will* ask where a number came from.
