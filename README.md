# rust dedicated server hosting: Real RAM Numbers, Annual Cost Math, and When a Cheap VPS Makes More Sense Than a Game Panel

Two things decide whether a Rust server actually plays well: how much RAM your map eats, and how fast a single CPU core runs. Panels, plugin ecosystems, and pricing tricks all come second. This guide walks through both halves of the rust dedicated server hosting decision — the managed game-panel hosts most buyers end up with, and the cheaper self-managed route on a KVM VPS like RackNerd's — using real RAM measurements and annualized costs, so you can match a plan to your server instead of guessing.

> **Quick picks**
> - **Managed and easy:** 8–12 GB of RAM runs roughly **$13–32/month** across the hosts compared below, with Oxide or Carbon plugins, wipe schedulers, and web RCON included.
> - **Self-managed and cheap:** if you're comfortable in a Linux terminal, RackNerd's annual KVM VPS tiers start at **$10.99/year**, and the 8 GB tier works out to about **$7.33/month**. 👉 [Check RackNerd's current KVM VPS specials](https://bit.ly/my-rn)
> - **One caution:** CoalHosting advertises Rust plans from €12/month, but the same page currently flags its Rust support as "coming soon." Treat those plans as not yet real.

## Two routes, one decision

Every Rust server runs on the same free piece of software Facepunch ships with the game: the Rust dedicated server binary. A hosting purchase just decides where that binary runs and who babysits it. Managed game hosts wrap it in a panel — switch Oxide or Carbon on with a click, schedule wipes, open RCON in a browser tab, restore backups from a menu. An unmanaged VPS gives you a root login and nothing else: you install SteamCMD, launch the server yourself, and own every cron job on the box.

Neither route is wrong. Managed hosting buys you convenience and faster default hardware; a bare VPS buys you maximum resources per dollar if you're willing to be the sysadmin. The RAM math below tells you how much server you actually need, and the cost math tells you what that server should cost on each route.

## How much RAM a Rust server actually needs

Map size is what grows Rust's memory footprint, not the player count — and this is the single most useful fact for choosing a plan, because most pricing pages nudge you toward thinking in player slots.

AcidNodes actually measured live Rust servers instead of copying wiki numbers: a 3000-size map runs a **4.9 GB** unreclaimable working set, peaking at 6.3 GB. A 4500-size map with players aboard peaked at **8.85 GB** — past an 8 GB cap, which means any "8 GB is enough" plan quietly stops being enough the day you grow the map. The Scrap Yard's operations notes agree from a different angle: a 100-slot server on a 3k map needs about 8 GB at wipe and climbs to 10–12 GB mid-wipe, and heavy plugin loads (NPC bots, raidable bases) add another 2–4 GB. CoalHosting's FAQ puts it in player terms: 50 players want 8–10 GB, 100 players want 12–16 GB, and below 6 GB the server struggles no matter how few people are on.

Putting the published guidance and the measurements together:

| Map size | Typical use | RAM to provision |
| --- | --- | --- |
| 2000–3000 | small private or light public server | 6–8 GB |
| 3000–3500 | standard public server with plugins | 8–12 GB |
| 3500–4500 | big map, plugins, full-pop wipe days | 12 GB+ |

The practical takeaway: plans below 6 GB are decoration for Rust. Eight gigabytes is the honest floor for a 3000 map with regular players, and if your worldsize slider goes to 4500 or beyond, budget 12 GB. Also worth knowing before you buy: Facepunch forces a map plus blueprint wipe on the first Thursday of every month around 2 PM ET, and mid-wipe is when RAM usage peaks — so provision for wipe day, not for Tuesday afternoon.

## Managed Rust hosts, compared

Five hosts currently publish Rust-specific plans, and their entry prices cluster between €12 and $32 a month. Here's what each advertises right now:

| Host | Entry price | Entry RAM | Mod support | Worth knowing |
| --- | --- | --- | --- | --- |
| The Scrap Yard | $9/mo | 2–4 GB | Oxide/uMod | Its own FAQ says Rust needs a 6 GB minimum, so the $9 Starter Rig is effectively not a Rust tier; the $18 Scrap King (4–8 GB) is the realistic start |
| ExtraVM | $12/mo | 6 GB | Vanilla, Oxide, Carbon | Ryzen 9 / i9 hardware, instant provisioning in US and EU only (Singapore/Sydney on request), Trustpilot 4.8/5, running since 2014 |
| NoBull Networks | $12.99/mo | 8 GB | Oxide and Carbon | No slot caps, 30-day money-back, publishes a 4.5 GHz single-core benchmark, caps node load at 60% |
| CoalHosting | €12/mo | 6 GB | Oxide/uMod | Plans listed but the page says Rust support is still rolling out — email-notification stage |
| AcidNodes | $32/mo | 12 GB | Carbon (runs Oxide plugins) | Priciest floor, but it measured live working sets before pricing, runs a Ryzen 9 9950X, and its worldsize slider goes to 6000 |

A few of those cells deserve a second look. The Scrap Yard selling a 2–4 GB "Rust" tier while its own knowledgebase says 6 GB minimum is exactly the kind of inconsistency you should catch before checkout. CoalHosting's "coming soon" note matters if you want to order today. And AcidNodes deliberately ships Carbon instead of Oxide for a practical reason: Oxide patches a DLL inside the game install, and on hosts that share game files between servers that patch can silently vanish on a rebuild, reverting your "modded" server to vanilla. Carbon touches nothing in the game tree, hot-loads .cs plugins without a restart, and runs Oxide plugins unmodified — same ecosystem, fewer surprises.

## The RackNerd route: a KVM VPS and your own terminal

RackNerd doesn't sell Rust game plans with a panel. It sells unmanaged KVM VPS — cheap, SSD-backed, with full root access and OS reinstalls from the client area — at prices managed Rust hosts can't match. You pick a tier and a location (Los Angeles, San Jose, Dallas, Chicago, New York, Atlanta, or Amsterdam), install Ubuntu or Debian, and build the server yourself. The trade is obvious: no wipe scheduler button, no plugin browser, no support ticket for "how do I add myself as admin." What you get instead is raw RAM and transfer at a fraction of managed pricing.

The annual KVM tiers RackNerd regularly offers look like this:

| Tier | vCPU | Storage | Annual price | Rust fit | Order |
| --- | --- | --- | --- | --- | --- |
| 1 GB | 1 | 20 GB SSD | $10.99/yr | No — even an empty small map won't fit | [ Order 1 GB](https://bit.ly/my-rn) |
| 2 GB | 1 | 30 GB SSD | $21.99/yr | No — not for Rust | [ Order 2 GB](https://bit.ly/my-rn) |
| 4 GB | 2 | 65 GB SSD | $43.99/yr | Bare minimum — tiny vanilla map, 2–3 friends | [ Order 4 GB](https://bit.ly/my-rn) |
| 6 GB | 3 | 80 GB SSD | $65.99/yr | Workable — 2000–3000 map, small private server | [ Order 6 GB](https://bit.ly/my-rn) |
| 8 GB | 4 | 100 GB SSD | $87.99/yr | Realistic floor — 3000 map with regular players | [ Order 8 GB](https://bit.ly/my-rn) |

RackNerd rotates its specials constantly, so treat the table as the shape of the lineup rather than a guarantee — the order page always shows the current specs and figures. Beyond these tiers, RackNerd also lists standard monthly plans and dedicated servers if a VPS ceiling ever gets in your way.

Honest limits, because they matter for this particular game: Rust rewards high single-thread clocks, and the cheapest annual VPS deals in this industry typically run older-generation Xeon processors rather than the 4.5–5 GHz EPYC and Ryzen chips managed Rust hosts advertise. The Scrap Yard tells its customers 5 GHz+ matters; NoBull publishes its 4.5 GHz benchmark for a reason. Check the CPU listed on RackNerd's plan page before ordering, and for anything beyond a chill private server, expect the tick rate to be the compromise you're accepting. Two more things to verify before paying: how the network handles DDoS attacks (ExtraVM and NoBull both bundle protection — ask RackNerd what's included), and the refund terms, since annual billing is the whole point of these deals and budget hosts are generally stricter than the 30-day money-back offers some managed competitors run. If those checks pass, 👉 [compare RackNerd's annual KVM tiers against whatever managed quote you're holding](https://bit.ly/my-rn).

## What a year of Rust hosting actually costs

Annualized, the gap between routes is real. Managed quotes above are monthly, so multiply by twelve and put them next to RackNerd's annual figures:

| Setup | Hardware class | Monthly equivalent | Yearly total |
| --- | --- | --- | --- |
| RackNerd 6 GB KVM (self-managed) | budget Xeon VPS | ~$5.50 | $65.99 |
| RackNerd 8 GB KVM (self-managed) | budget Xeon VPS | ~$7.33 | $87.99 |
| ExtraVM 6 GB (managed) | Ryzen 9 / i9 | $12 | $144 |
| NoBull Survivor, 8 GB (managed) | EPYC, 4.5 GHz | $12.99 | $155.88 |
| The Scrap Yard, Scrap King (managed) | NVMe, 4–8 GB | $18 | $216 |
| AcidNodes, 12 GB (managed) | Ryzen 9 9950X | $32 | $384 |

For like-for-like RAM, the managed premium runs about $70–80 a year. That premium buys three things: faster silicon (which Rust genuinely notices), a panel that turns wipes and backups into two clicks, and someone to email when the server misbehaves at 2 AM. Whether that's worth $75 a year is a personal question — for a four-person private server on a 2500 map, most people would rather keep the $75 and spend an afternoon on setup.

## Setting up Rust on a RackNerd VPS: the short version

The whole job fits in an evening:

1. Order a 6 GB or 8 GB tier in the location closest to your players, with annual billing.
2. Reinstall the OS from your client area onto a fresh Ubuntu or Debian image.
3. Install SteamCMD and pull the server: `app_update 258550 validate`.
4. Launch with your flags — `+server.worldsize 3000`, a `+server.seed` of your choosing, `+server.maxplayers` — and note that the game listens on port 28015 with RCON on 28016, so open both in the firewall.
5. Make yourself owner: `ownerid <your Steam64 ID>` then `server.writecfg`, so it survives restarts.
6. Drop Oxide or Carbon in for plugins; Carbon hot-loads .cs files from its plugins folder without a restart.
7. Set a cron job for wipes — weekly map wipes if your group likes fresh starts, and align the blueprint wipe to Facepunch's first-Thursday schedule. Snapshot the save folder before every wipe; restoring from a snapshot is your rollback when a wipe goes sideways.

None of these steps is hard, but each one is yours now. That's the deal you're making with an unmanaged box.

## FAQ

**How much RAM for a small private Rust server?** Six gigabytes covers a 2000–3000 map for a small group — a 3000 map measures a 4.9 GB working set — and eight gives you mid-wipe headroom.

**Can a 2 GB VPS run Rust?** No. Measured working sets start near 5 GB even on modest maps; 1–2 GB plans will crash on launch day.

**Oxide or Carbon?** Oxide has the largest plugin ecosystem; Carbon is a modern drop-in that runs Oxide plugins and avoids the shared-file DLL issue on hosts that reuse game installs.

**When is the forced wipe?** First Thursday of each month, around 2 PM ET, map and blueprints together. Most community servers also run map-only wipes weekly.

**Is RackNerd a Rust game host?** No. It's an unmanaged VPS provider — you get root, you install Rust yourself, and you set player limits yourself with `+server.maxplayers` since there are no slot concepts on a raw VPS.

## Before you order

Match the route to your situation. Hosting for two to five friends on a smallish map, happy in a terminal, want to spend as little as possible: a RackNerd 6–8 GB annual tier is the cheapest sane option, and your total cost lands under $90 a year. Want a public server, wipe-day raids, plugins configured from a panel, and a support inbox: pay the managed premium — NoBull's $12.99 Survivor tier for an 8 GB start, the Scrap King at $18 for a mid-size community, or AcidNodes at $32 if you already know you're running a 3500+ map. And if you want Oxide panels today, skip any host whose product page still says "coming soon."

Whichever way you go, confirm three things before paying: the actual CPU model and clock on the order page, whether RAM is dedicated or shared, and the refund terms. Then — if the cheap-and-hands-on route is yours — 👉 [start from RackNerd's KVM VPS specials page](https://bit.ly/my-rn) and pick the tier your map size calls for.
