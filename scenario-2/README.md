> **Scenario 2** — you are preparing the demo. Workshop rules and setup are in the
> [root README](../README.md). Record anything you could not do in `FINDINGS.md`.

# DEMO-1144 — Kettle & Crank: demo data for the Rancilio comparison

**Raised by** Joost (Sales) · **For** Delivery · **Demo is Thursday**

## Who they are

Kettle & Crank are an Amsterdam wholesaler fitting out cafes — machines, grinders,
spares. We met them at World of Coffee and have had three calls since. They are
interested but not convinced — they have been pitched competitor monitoring before and
it came back as a spreadsheet nobody could use.

Three fit-outs this quarter were renegotiated mid-quote because the owner found the
same kit cheaper online. They have no idea whether that was clearance pricing or a
standing gap.

## What they asked for

They do not want a slide about what we could do. They asked to see **their own market,
with real numbers**, using the two competitors they named on the last call. If we can
show them a like-for-like comparison on a line that actually hurts, we win this.

Rancilio is most of what goes into a two-group install, so it sets the tone for their
whole quote. That is the line to demo on.

## The two sites they named

| | Shop | Range to pull |
|---|---|---|
| **A** | The Espresso Shop | https://theespressoshop.co.uk/collections/rancilio (~108 products) |
| **B** | Espresso Parts | https://espressoparts.com/collections/rancilio (~250 products) |

## Where this sits

The prospect is buying the end of the pipeline, not our bit. What they want is
**PriceMonk** telling them where to move their prices. To get there the data goes
ScrapeMonk → **TidyMonk** to cleanse → **MatchMonk** to match products across the two
shops → PriceMonk for the strategy.

Our job here is the first step, and the handoff: both ranges extracted and **landed in
S3** in a shape the rest of the chain can pick up. ScrapeMonk is playing second fiddle
in this demo and that is fine — but if this step is wrong, nothing downstream recovers.

## What matters about the data

MatchMonk can only join products on something stable — a GTIN or EAN, a manufacturer
part number, a brand plus a model. Not a product name. So the question to answer before
Thursday is not "did you get the rows", it is **can these rows actually be matched**:
how many carry an identifier, and which field is it.

If a large share of the rows have nothing to join on, say so now. That is a far better
Tuesday conversation than a demo where MatchMonk returns nothing in front of the client.

**Around 300 products from each shop is plenty.** This is a demo, not a delivery. I
would rather have 300 rows that hold up under questioning than a full dump nobody has
checked — they *will* ask where a number came from.
