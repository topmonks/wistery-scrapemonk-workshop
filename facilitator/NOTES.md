# Facilitator notes — keep out of the participant folders

## The seven pairs, and why these

Every pair is a **same-brand collection on both shops**, verified by reading each
shop's `/products.json` — no crawling. That is the recipe: a brand collection on both
sides gives products that genuinely correspond. Paired *product categories* do not —
an earlier draft paired "brake cables" against "26-inch tyres" and nothing matched.

| # | Company | Shop A | n | Shop B | n | A-side matched |
|---|---|---|---|---|---|---|
| 1 | Modular Row | noisebug `/doepfer-modules` | 175 | nightlife-electronics `/doepfer` | 111 | 155 (88%) |
| 2 | Kettle & Crank | theespressoshop `/rancilio` | 108 | espressoparts `/rancilio` | ~250 | 108 (100%) |
| 3 | Tailwind Components | cambria-bike `/continental` | 210 | bicyclewarehouse `/continental-bike-tires` | 215 | 188 (89%) |
| 4 | Skyline FPV | racedayquads `/betafpv-products` | 181 | pyrodrone `/cinewhoop-bnf` | 203 | 164 (91%) |
| 5 | Additiva Works | west3d `/bambu-bambu-lab-printer-accessories` | 187 | fabreeko `/bambu-labs` | 102 | 142 (75%) |
| 6 | Northfell Cycles | contenderbicycles `/shimano` | 174 | theproscloset `/shimano` | 273 | 153 (87%) |
| 7 | Lustre Supply | slimsdetailing `/koch-chemie` | 186 | carsupplieswarehouse `/automotive-protection-products` | 127 | 186 (100%) |

**Read that last column carefully.** It counts A-side products with a plausible
counterpart in B (same brand, two or more shared title words). It is many-to-one, so
true one-to-one pairs are capped at the smaller catalogue: about **111** for scenario 1,
**102** for 5, **127** for 7. Do not quote the bigger number to participants — if they
report a higher match count than the smaller catalogue holds, that is itself worth
catching in the debrief.

Scenario 5 is the only pair spanning several makers (Bambu Lab 107, BTT 29, a handful
of Phaetus). The rest are single-brand, which makes matching tractable inside the hour
but also means **brand alone will not discriminate** — they have to match on something
sharper, which is the point.

## Currency, deliberately uneven

Most shops price in **USD**. Three scenarios carry a real mismatch:
- **Scenario 1** — Nightlife Electronics is **CAD** against Noisebug's USD
- **Scenario 2** — The Espresso Shop is **GBP** against Espresso Parts' USD
- **Scenario 7** — Slim's is **GBP** against Car Supplies Warehouse's USD

Scenario 1 is the nastiest and the one to watch: CAD and USD figures sit in the same
range, so a side-by-side table looks entirely plausible while being wrong by about a
third. GBP against USD at least looks odd enough to prompt a question.

Nobody is told. The briefs for 2 and 7 say "one British and one American retailer",
and scenario 1 says "two North American retailers" — fair warning, if they are reading.
If a participant compares without noticing, that is the lesson, and it is the same one
that cost us a real client delivery.

## Timing, measured not guessed

Measured on scenario 4 end to end, both shops in parallel under one account:

| cap | pages | create → preview |
|---|---|---|
| 900 | ~900 | **25 minutes** |
| ~300 | ~300 | about 8 minutes |

**The briefs tell participants to cap at ~300.** With their own logins and two jobs
running in parallel, both shops should reach the preview inside ten minutes, leaving
the hour for the preview, the export and the matching — which is the actual content.

A cap is safe: at the limit the crawl stops and goes to the preview gate. It does not
fail. (An earlier prep batch failed at a low cap, but that was jobs queued many-deep
under one account, not the cap itself. The cap was blamed twice during prep and was
innocent both times — raising it from 30 to 600 did not stop the failures.)

**Extraction, measured 2026-10-26** on the two scenario-4 smoke jobs: 587 and 654
products from ~900-page crawls, both extracted in **about a minute** once a worker was
available. Field coverage was 100% on name, price and brand for both. The new
collections are smaller than those smoke jobs, so extraction will not be the slow part.

## Infrastructure — read this before the workshop starts

Dev had a full worker outage on 2026-10-26, fixed the same day. Two causes, both now
handled, but worth knowing if things look wrong tomorrow:

- **ARM capacity is gone.** `cax21`/`cax31`/`cax41` are sold out in every Hetzner
  location; only the 4GB `cax11` is left and the selector needs 8GB. Workers now run
  on **x86** (`cpx32`) from an x86 snapshot.
- **The x86 image killed every worker.** `sharp`'s linux-x64 binding is missing from
  the amd64 image, and it was imported at the top of a model that everything loads, so
  the worker died at boot, never registered, and was reaped. Fixed on master in
  `66bb1f32` by importing sharp lazily. The underlying image defect is SCR-400.
- **Consequence for tomorrow:** screenshots are not converted on x86 workers until
  SCR-400 lands, so **the preview may show fewer images than usual**. The parse data
  itself is unaffected. If someone asks why a preview looks thin on images, that is why.
- **The failure signature to recognise:** workers spawn, never register, get killed at
  ~200s as "orphans", and after three the autoscaler pauses spawning for ten minutes —
  so the pool reads as permanently empty. If that happens, it is not the participants.

## What will go wrong

- **Tools missing after `claude mcp add`.** MCP registers at session start. They must
  restart Claude Code. This catches nearly everybody once.
- **Token expires in 24 hours.** The Connect Agent dialog hands out the signed-in
  user's own Auth0 token. Fine for one day; if anyone's tools die, re-copy it.
- **Jobs queue.** Each account allows a small number of concurrent jobs. With their
  own logins they will not contend with each other, but one person starting four jobs
  will see the later ones wait.
- **A job that waits too long can end up `failed`.** Seen repeatedly during prep when
  many jobs were queued under one account. If it happens, it is not their fault.
- **`category_urls` seeds, it does not scope.** Asking for a 207-product category
  produced 901 pages — the crawler follows links out of the category. ScrapeMonk
  notices and raises a `scope_drift` event saying "100% of fetched pages are outside
  the requested area". Worth pointing at: the product caught its own limitation, and
  the brief asks them to look for it.

## Questions worth asking in the debrief

- Which did you trust more, the preview or the finished data? Why?
- What did you have to do outside MCP, and what tool would have saved you?
- How many products actually matched, and what did you match on? If it was the
  product name, how confident are you?
- Did anyone check the currency before comparing? When did you notice?
