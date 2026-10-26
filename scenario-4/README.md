> **Scenario 4** — you are preparing the demo. Workshop rules and setup are in the
> [root README](../README.md). Record anything you could not do in `FINDINGS.md`.

# DEMO-3310 — Skyline FPV: demo data for the BetaFPV comparison

## Who they are

Skyline FPV are a Prague distributor of FPV parts — motors, frames, cameras, flight
controllers. We met them at DroneX and have had three calls since. They are interested
but not convinced — they have been pitched competitor monitoring before and it came
back as a spreadsheet nobody could use.

Their support queue is full of customers quoting two US shops at them. They cannot
tell whether they are genuinely expensive or just telling the story badly.

## What they asked for

They do not want a slide about what we could do. They asked to see **their own market,
with real numbers**, using the two competitors they named on the last call. If we can
show them a like-for-like comparison on a line that actually hurts, we win this.

BetaFPV is the brand in the complaints, because it is what the ready-to-fly crowd
buys. Demo on that.

## The two sites they named

| | Shop | Range to pull |
|---|---|---|
| **A** | RaceDayQuads | https://racedayquads.com/collections/betafpv-products (~181 products) |
| **B** | Pyrodrone | https://pyrodrone.com/collections/cinewhoop-bnf (~203 products) |

## Where this sits

The prospect is buying the end of the pipeline, not our bit. What they want is
**PriceMonk** telling them where to move their prices. To get there the data goes
ScrapeMonk → **TidyMonk** to cleanse → **MatchMonk** to match products across the two
shops → PriceMonk for the strategy.

Our job here is the first step, and the handoff: both ranges extracted and **landed in
S3**. **Barbora picks it up from there** on the MatchMonk side — the S3 file is where
our part ends and hers begins, so it needs to be something she can work with rather
than something she has to come back and ask about.

ScrapeMonk is playing second fiddle in this demo and that is fine — but if this step is
wrong, nothing downstream recovers.

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
