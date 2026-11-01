# ddos protection: What It Should Cost, What "Included" Really Means, and How to Pick a Setup That Survives an Attack

Most people searching for ddos protection fall into one of two camps. Either your server just got knocked offline and you need it to stop happening, or you're choosing hosting and want to know whether DDoS mitigation is something you pay extra for or something that comes with the box. This article covers both: how DDoS protection actually works, what it costs when it's sold separately, and why a growing number of small hosting operators buy their infrastructure from a provider that includes it by default — like Sharktech, a hosting company that started out in 2003 as a DDoS mitigation shop and still treats protection as a baseline feature rather than an upsell.

If you want the short version: Sharktech bundles automatic traffic scrubbing into every hosting plan, and its entry-level SmartVPS runs **$7.95/month, or $3.98/month on annual billing** — protection included. Most other providers charge separately for anything beyond basic filtering, and the big cloud options are scoped to their own ecosystems.

> **Quick pick:** For game servers, small SaaS, and anything with a public IP that attracts attacks, the SmartVPS entry plan at $3.98/mo (annual) is the sensible starting point — third-party reviews consistently report 60Gbps of DDoS protection bundled per IP. 👉 [Check current Sharktech SmartVPS pricing and deploy](https://bit.ly/SharKtech)

## What DDoS protection actually does

DDoS protection filters incoming traffic so attack packets get dropped before they reach your server. At the network level, that means rate limiting to slow down floods, blacklisting known malicious sources, and behavioral analysis that flags traffic patterns which look abnormal for your server. When an attack starts, traffic is automatically routed through scrubbing infrastructure, only clean traffic is forwarded, and your service stays up.

Sharktech's implementation runs this way: multi-layer filtering where attack traffic is automatically diverted to its firewall layer, with legitimate traffic passed through. The company's service page lists coverage against the attack types you'd realistically expect to see in the wild — UDP, ICMP and TCP SYN floods, HTTP GET and POST floods, Slowloris, NTP and DNS amplification, SSDP and SNMP reflection, Memcached reflection, Chargen, Ping of Death, Smurf, and reflected ICMP/UDP variants.

One detail worth knowing before you buy anything: mitigation modes are under your control. You can run scrubbing always-on, scrub only selected traffic, or trigger it only when an attack is detected. Always-on adds a tiny bit of filtering overhead; on-demand means nothing touches your traffic until something looks wrong. For game servers where latency matters, that choice is genuinely useful.

## The pricing problem with "buy protection separately"

Here's the math that most comparison articles skip. If you host somewhere that treats DDoS mitigation as a paid add-on, you typically discover the real price after the first attack — either in per-incident scrubbing fees, forced upgrades, or your host null-routing your IP and asking you to leave. Sharktech's own comparison of the three paths is blunt, and it matches how the industry actually behaves:

- **No protection:** hours or days offline, risk of all traffic being null routed, possible eviction from your network.
- **Self-implemented:** hundreds of thousands of dollars in hardware, potentially millions in network upgrades, plus a specialized network administrator with DDoS experience.
- **Protection included with hosting:** no software or hardware to install, and mitigation is already wired into the network.

The third option is only available if your host actually owns scrubbing capacity. Sharktech does — it built the mitigation business first and added hosting around it, which is why protection ships free with everything it sells.

And the threat isn't hypothetical. Akamai documented a memcached reflection attack against one of its customers peaking at **1.3 Tbps** — at the time, the largest ever recorded, more than double the previous Mirai botnet record. What makes memcached reflection dangerous is the amplification factor: a 210-byte request can trigger a 100 MB response, an amplification factor of roughly 500,000x, which is why a few tens of thousands of misconfigured servers were enough to generate that traffic without any botnet at all. Memcached reflection is one of the attack types on Sharktech's coverage list.

## Full plan and pricing breakdown

Sharktech's current lineup splits into three product lines: SmartVPS (the modern cloud platform), a legacy SSD VPS line, and bare-metal dedicated servers. All of them include DDoS protection.

**SmartVPS** is officially a resource-pool product: you buy a pool of CPU, RAM and NVMe rather than a fixed VM. The official product page confirms the entry configuration at **2 vCPU / 4 GB RAM with 40 GiB NVMe, 4TB monthly traffic and 1 IPv4 address**, scaling up to 128 vCPU / 256 GB at the top end. You can create one large machine or several small ones from the same pool, spread across data centers, and resize through the customer portal without redeploying. Add-on NVMe storage is priced at **$0.01/GiB/month** (up to 2,000 GiB, in 10 GiB steps), with additional traffic and IPv4 addresses configurable through sliders; IPv6 is free. Firewall rules and private networking between your own VMs are configurable in the management interface.

| Plan | vCPU / RAM / NVMe | Monthly | Annual (−50%) | Get it |
| --- | --- | --- | --- | --- |
| Tiny | 2 / 4 GB / 40 GB | $7.95/mo | **$3.98/mo** | [Order Tiny](https://bit.ly/SharKtech) |
| Small | 2 / 4 GB / 60 GB | ~$15.95/mo | ~$7.98/mo | [Order Small](https://bit.ly/SharKtech) |
| Medium | 4 / 8 GB / 80 GB | ~$39.95/mo | ~$19.98/mo | [Order Medium](https://bit.ly/SharKtech) |
| Large | 8 / 16 GB / 160 GB | $99.95/mo | $49.95/mo | [Order Large](https://bit.ly/SharKtech) |
| Colossal | 16+ / 32+ GB / up to 2000 GB | $299.99/mo | ~$149.99/mo | [Order Colossal](https://bit.ly/SharKtech) |

Every plan includes DDoS protection per IP, an IPv4 address plus free IPv6, full root access, a choice of Linux or Windows, a browser console that works even when your own network is down, and free migration from another host. A caution on the table above: the entry-level specs and price match Sharktech's official page exactly, but third-party listings disagree noticeably on the middle tiers — one listing prices Medium and Large at roughly $32 and $64 monthly, another at roughly $40 and $100, and they also differ on whether the port speed is 1Gbps or 10Gbps. Treat the middle rows as approximate and let the order page you land on be the final word.

The billing-cycle discount structure is where the real savings live, and it's confirmed on the official page — automatic, no coupon needed, with the full amount prepaid:

- Quarterly: 25% off
- Semi-annual: 35% off
- Annual: 50% off

That annual math is the number most reviews gloss over. The entry plan at $3.98/month works out to roughly **$47.76 per year** for an NVMe-backed VPS with enterprise mitigation included — less than a lot of shared hosting, with dedicated resources and full root.

**Legacy SSD VPS line.** The older line still circulates with promotional coupon pricing through affiliate channels, aimed at people who specifically want the 100 Mbps uplink version. Third-party listings currently show a coupon dropping the 2GB plan to $6.57/mo from $11.95, up through the 32GB plan at $105.57/mo. These codes come from third-party channels and may already be expired, so verify the discount actually appears in your cart before committing.

**Bare-metal dedicated servers.** Sharktech's official server page is specific: every bare-metal server includes a **10Gbps network port, 300TB/month of bandwidth, and 2TB NVMe M.2 storage**, with catalog configurations starting at **$219/month**. In-stock systems target delivery within 24 hours; custom CPU/memory/drive builds take longer because components have to be sourced, and the team confirms timing before you commit. You can upgrade the CPU, memory, storage and network interfaces after purchase, and all five data center locations — Los Angeles, Las Vegas, Denver, Chicago and Amsterdam — are selectable where stock allows. Third-party listings also surface promotional 1Gbps configurations around **$99/month** (a Xeon E3-1270v5 in Chicago or LA, down from $159, via promo code), which is worth hunting for if your workload fits an older Xeon.

👉 [Browse Sharktech's current bare-metal configurations](https://bit.ly/SharKtech)

## How much protection do you actually get?

This is the question where marketing materials get vague, so let's be precise about what's confirmed and what isn't.

Sharktech's own service page describes the protection included with hosted services as upgradeable up to 100Gbps. Third-party reviews consistently put the baseline at **60Gbps of mitigation per IP**, included on every plan down to the cheapest VPS, with capacity expandable well beyond that for enterprise needs. Either way, the relevant benchmark is attack size: reviews of the hosting space note that most volumetric attacks small and mid-size targets face land somewhere between 5 and 20Gbps. A customer running game servers — a category that gets attacked constantly — reported being hit with attacks ranging from 3 to 8Gbps, in their words, with servers that "never skip a beat."

For context on what NOT having protection costs: when the Akamai customer hit by that 1.3 Tbps memcached attack had mitigation in place and had rehearsed their response, they switched all traffic to scrubbing within five minutes and were down for less than ten. Without a scrubbing path, a single attack of that amplification class ends your uptime for as long as your upstream decides to drop your traffic.

## How this compares to the cloud and appliance options

The top search results for ddos protection are dominated by enterprise vendors, so a quick orientation on where each option fits:

- **AWS Shield** protects workloads running on AWS, in two tiers (Standard and Advanced). Fine if your infrastructure is already there; irrelevant if it isn't.
- **Azure DDoS Protection** similarly protects Azure virtual network resources, with costs that scale with your deployment and no upfront commitment.
- **Fortinet's FortiDDoS and Radware's DefensePro** are hardware/appliance-based mitigation platforms for organizations that want to own the scrubbing layer — priced and staffed accordingly, with Radware's own comparison acknowledging that appliance layers add licensing and setup overhead.
- **Sharktech** fits the gap between them: you get hosting and mitigation from the same network, priced like hosting.

The honest trade-off: cloud and appliance options integrate deeply with their own ecosystems and offer multi-terabit absorption capacity for the largest targets — Akamai's Prolexic network alone claims over 3.5 Tbps of scrubbing capacity across seven centers. If you're a bank or a CDN, that's your lane. If you're running game servers, a community site, a small SaaS, or a Minecraft host, paying enterprise pricing for capacity you'll never trigger makes little sense — and Sharktech explicitly markets to exactly that middle ground.

## Protecting servers hosted somewhere else

Sharktech also sells **Remote Network DDoS Protection** for servers that live on other networks. Traffic is diverted through cloud-based scrubbing nodes at the first sign of an attack, before it reaches your network — no migration required, and you choose between always-on filtering or attack-triggered filtering. The service covers applications, web servers, DNS servers, and large botnet-driven attacks. Pricing isn't published; it's subscription-based on usage, which means you'd need to talk to their team for a quote. If your servers are already hosted elsewhere and you're happy with the host, this is the relevant product rather than a migration.

## What the independent benchmarks show

Sharktech's own product page quotes HostAdvice's review directly: "With 6,000+ random IOPS, sub-millisecond network latency … Sharktech delivers genuine power." The fuller benchmark figures relayed through third-party reviews of the SmartVPS line are worth knowing, since VPS providers are notorious for overselling:

- 6,000+ IOPS on 4K random read/write, where most budget VPS plans land around 2,000
- Sub-millisecond network latency — 0.547ms to Google DNS, 0.835ms to Cloudflare
- About 19 GB/sec memory throughput
- 5.33 Gbps actual download on a 10Gbps port under stress, with no throttling while CPU, memory and disk were all loaded
- Multi-thread CPU scoring 7.65x single-thread, which suggests they aren't packing hosts to the ceiling

A separate VPSBenchmarks entry for the entry plan running on a Xeon Gold 6262V confirms the hardware claims with AES-NI and virtualization extensions enabled — the specs on the marketing page match what independent testing measured.

## FAQ

**Is the DDoS protection really free, or is it billed when an attack happens?**
It's included in the plan price for all hosted services, and third-party reviews confirm it's not a metered service that invoices you when an attack actually hits. Upgrades beyond the included capacity are where additional cost comes in.

**Will protection slow my server down?**
Only if you choose always-on scrubbing, and even then the impact is minimal filtering overhead. On-demand mode leaves traffic untouched until an attack is detected. You control this per your needs.

**What happens if I do nothing?**
Depending on your upstream provider: hours or days of downtime, all traffic null-routed, or eviction from the network entirely. In the US, launching these attacks is a federal offense under the Computer Fraud and Abuse Act — but that's cold comfort when your revenue is offline.

**Can I try the platform before committing?**
Sharktech doesn't advertise a free trial or a money-back window in the materials reviewed here, so the low-risk path is the monthly-billed entry plan at $7.95 before switching to the prepaid annual rate once you're satisfied.

**Can I add more storage or IPs later?**
Yes, through the customer portal. NVMe storage adds at $0.01/GiB/month up to 2,000 GiB, traffic can be extended up to 300TB, and additional IPv4 addresses are configurable — IPv6 is free.

## Choosing between them

Running game servers or anything attack-prone on a budget → the SmartVPS entry plan on annual at $3.98/mo, and skip the coupon-hunting. Need more headroom for a database-heavy app → step up a tier, still under $20/mo annualized, or just add NVMe at a penny per GiB instead of jumping plans. Want a whole physical machine that nobody else touches, with 10Gbps uplink → bare-metal from $219/mo, or one of the ~$99/mo promotional Xeon builds if the specs fit. Servers already hosted elsewhere and you just want the attacks to stop → ask about Remote DDoS Protection instead of migrating.

Two things to check before you order: confirm your preferred data center location has the configuration in stock (it affects the 24-hour delivery promise), and since annual billing is prepaid in full, double-check the plan specs and the discounted rate shown in the cart are what you expect — middle-tier listings vary between sources. Then grab the plan that fits: 👉 [See Sharktech's full plan lineup and current pricing](https://bit.ly/SharKtech)
