> **Scenario 5** — you are preparing the demo. Workshop rules and setup are in the
> [root README](../README.md). Record anything you could not do in `FINDINGS.md`.

# DEMO-0912 — Additiva Works: demo data for the Bambu Lab accessories comparison

## Who they are

Additiva Works are a Rotterdam supplier keeping print farms running — hotends,
extruders, motion parts. We met them at Formnext and have had three calls since. They
are interested but not convinced — they have been pitched competitor monitoring before
and it came back as a spreadsheet nobody could use.

Their procurement team is placing an order in a fortnight and has asked whether the
margin on the accessory line is defensible. Nobody there can answer it with numbers.

## What they asked for

They do not want a slide about what we could do. They asked to see **their own market,
with real numbers**, using the two competitors they named on the last call. If we can
show them a like-for-like comparison on a line that actually hurts, we win this.

Accessories are consumables for their customers, so they reorder constantly and notice
price first. That is why this line is the one worth showing.

## The two sites they named

| | Shop | Range to pull |
|---|---|---|
| **A** | West3D | https://west3d.com/collections/bambu-bambu-lab-printer-accessories (~187 products) |
| **B** | Fabreeko | https://fabreeko.com/collections/bambu-labs (~102 products) |

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
