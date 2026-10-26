# Facilitator notes — keep out of the participant folders

## The seven pairs, and why these

Every pair was verified to share real brands by reading `vendor` from each shop's
`/products.json` — no crawling. Pairs that share nothing cannot be compared however
well they scrape, and five of the first fourteen sites tried were single-brand shops
whose `vendor` is their own name. That is the `manufacturer_is_site` pattern the
quality card flags, in the wild.

| # | Company | Shop A | Shop B | Shared brands |
|---|---|---|---|---|
| 1 | Modular Row | detroitmodular.com | noisebug.net | 42 |
| 2 | Kettle & Crank | seattlecoffeegear.com | wholelattelove.com | 15 |
| 3 | Tailwind Components | cambria-bike | bicyclewarehouse.com | 35 |
| 4 | Skyline FPV | racedayquads.com | pyrodrone.com | 30 |
| 5 | Additiva Works | west3d.com | fabreeko.com | 18 |
| 6 | Northfell Cycles | chapter-2-cycle | worldwidecyclery.com | 15 |
| 7 | Lustre Supply | slims detailing | carsupplieswarehouse.com | 11 |

## Currency, deliberately uneven

Most shops price in **USD**. Two scenarios carry a real mismatch:
- **Scenario 6** — Chapter 2 Cycle is **SGD** against Worldwide Cyclery's USD
- **Scenario 7** — Slim's is **GBP** against Car Supplies Warehouse's USD

Nobody is told. If those two participants compare without noticing, that is the
lesson, and it is the same one that cost us a real client delivery.

## Timing, measured not guessed

A ~230-product category took **8 minutes** from create to extraction preview, then
**3 minutes** to extract 203–478 products. Budget 15 minutes per shop, 30 per
scenario, and the remaining hour for the questions that matter.

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
- **`max_pages` is not a safe way to cap.** Early prep runs with a low cap failed
  rather than stopping cleanly. Scope with the category URL instead, which is what the
  briefs say.

## Questions worth asking in the debrief

- Which did you trust more, the preview or the finished data? Why?
- What did you have to do outside MCP, and what tool would have saved you?
- How many products actually matched, and what did you match on? If it was the
  product name, how confident are you?
- Did anyone check the currency before comparing? When did you notice?
