> **Scenario 3** — you are preparing the demo. Workshop rules and setup are in the
> [root README](../README.md). Record anything you could not do in `FINDINGS.md`.

# DEMO-0788 — Tailwind Components: demo data for the Continental tyres comparison

**Raised by** Núria (Sales) · **For** Delivery · **Demo is Thursday**

## Who they are

Tailwind Components are a Girona distributor supplying independent bike shops —
drivetrain, brakes, wheels. We met them at Sea Otter Europe and have had three calls
since. They are interested but not convinced — they have been pitched competitor
monitoring before and it came back as a spreadsheet nobody could use.

Their shops are getting beaten up by their own walk-in customers, who arrive with a
phone showing a tyre cheaper than the shop's trade price. They want to know if that is
a few loss-leaders or the whole range.

## What they asked for

They do not want a slide about what we could do. They asked to see **their own market,
with real numbers**, using the two competitors they named on the last call. If we can
show them a like-for-like comparison on a line that actually hurts, we win this.

Show it per size and model. A blended average will not convince them, because they
already believe it is two or three hero products.

## The two sites they named

| | Shop | Range to pull |
|---|---|---|
| **A** | Cambria Bike | https://cambriabike.com/collections/continental (~210 products) |
| **B** | Bicycle Warehouse | https://bicyclewarehouse.com/collections/continental-bike-tires (~215 products) |

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
