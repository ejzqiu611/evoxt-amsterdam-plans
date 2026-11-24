# Evoxt Amsterdam: Is the $2.99 Plan Enough, Which Plan Fits Your Workload, and How Fast Is It Really? (All 11 Plans Priced, Real Benchmarks, China Route Explained)

Amsterdam sits in Evoxt's Standard network tier. It starts at **$2.99/month** and tops out at 10 TB of monthly transfer on the VM-16. At every single price point, the Dutch location hands you roughly twice the bandwidth of Evoxt's Hong Kong and Osaka regions, and that's the strongest argument for picking the Netherlands over the Asian Premium locations if you don't specifically need CN2 routing.

Most people reading this should buy **VM-1 at $5.99** or **VM-1.5 at $6.95**. The rest of this page covers what the Amsterdam node actually is, all 11 plans with prices, which one fits which job, benchmark numbers from two independent tests, and the China routing you should understand before you pay.

> **Quick pick:** VM-1 ($5.99/mo) handles a single small site, a reverse proxy, a bot, or a light API. Add $0.96 and VM-1.5 ($6.95/mo) gives you a second core for the same RAM. Skip VM-0.5 unless you're running one process and nothing else.
>
> 👉 [Check current Amsterdam pricing and deploy a VM](https://bit.ly/EvoXt)

## Why Amsterdam, and what the network actually connects to

The Amsterdam location is physically in Haarlem, North Holland, inside the Amsterdam metro area, under ASN AS149440 (Evoxt Enterprise). It runs on KVM with native IPv4 and IPv6, SSD storage, and free weekly off-site backups.

The peering is the part worth checking. Evoxt connects this node to three exchanges, AMS-IX, ERA-IX, and NL-IX, plus multiple Tier 1 providers including Cogent, Arelion, GTT, NTT and CMI. AMS-IX alone carries peak traffic above 10 Tbps and links more than 875 networks across 70+ countries, which is why a server parked there reaches most of Europe in under 20 ms without bouncing through extra transit hops.

Measured latency from a 2024 iperf3 run on an Amsterdam VM: **8.1 ms to London**, **76.9 ms to New York**, **138 ms to Los Angeles**, and **204 ms to Singapore**. That covers the "is it good for Europe" question and the "can I serve US users" question at the same time. If you're handling personal data from EU visitors, the Netherlands also puts you inside GDPR jurisdiction, which simplifies the paperwork compared with a US or Asian host.

Evoxt's pricing page currently lists 12 selectable regions across three tiers: Standard (US, UK, Canada, Germany, Poland, Amsterdam, Tokyo, Malaysia, Australia), Premium (Hong Kong, Osaka), and Premium Plus (Malaysia Premium).

## All 11 Amsterdam plans, priced

Every plan below is the Standard tier, billed monthly in USD, and includes a 1 Gbps port, IPv4 + IPv6, KVM virtualisation, and weekly automatic off-site backups at no extra charge.

| Plan | vCPU / RAM | SSD | Monthly transfer | Price/mo | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB | 500 GB | $2.99 | [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB | 10 GB | 750 GB | $4.99 | [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB | 1 TB | $5.99 | [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB | 20 GB | 1.5 TB | $6.95 | [Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB | 2 TB | $11.99 | [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB | 30 GB | 3 TB | $14.99 | [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB | 4 TB | $23.99 | [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB | 60 GB | 5 TB | $29.99 | [Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB | 6 TB | $47.99 | [Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB | 80 GB | 8 TB | $60.95 | [Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB | 10 TB | $95.99 | [Deploy VM-16](https://bit.ly/EvoXt) |

The transfer column is where Amsterdam separates itself. The same $5.99 VM-1 gives you 1,000 GB in Amsterdam but only 500 GB in Hong Kong or Osaka. On the high end, VM-16 delivers 10 TB here versus 5 TB in the Premium tier, and 4 TB in Malaysia Premium Plus. If your workload moves real traffic (mirrors, media proxies, backup nodes, regional APIs), the Standard locations are effectively double the plan for the same money.

Evoxt's own pricing language is unusually blunt about the fee structure: "If you order a $2.99 plan. You will pay $2.99. We don't charge any extra bandwidth fees or any CPU burst fees." Nothing in the plan table contradicts that.

## Add-ons, and when upgrading beats adding resources

Resource pricing is flat across the Amsterdam node:

- Extra IPv4 address: **$3/month**
- Extra vCore: **$3/month**
- Extra RAM: **$2/GB/month**
- Extra transfer: **$3/TB** on Standard (Premium $12/TB, Premium Plus $24/TB)

The add-on menu is useful for one specific case and a bad deal in most others. Run the arithmetic:

- VM-1 plus 2 GB of RAM costs **$9.99** and leaves you with one core, 20 GB of storage and 1 TB of transfer. VM-2 costs **$11.99** and gives you two cores, 30 GB and 2 TB. For $2 more, the plan jump wins on every axis.
- Buying 1 TB of extra transfer costs **$3**. Moving from VM-1 to VM-1.5 costs **$0.96**, and you get a second core plus 500 GB more transfer on top.
- VM-0.5 to VM-1 is a $3/month difference that multiplies RAM by four, storage by four, and transfer by two.

Add RAM à la carte only when you're already on a plan with enough cores and storage and just need headroom for a JVM heap or a database cache. Otherwise, step up the ladder.

👉 [Compare VM-1 and VM-2 side by side before you pick](https://bit.ly/EvoXt)

## Which plan fits your workload

**VM-0.5 ($2.99)** is tighter than the spec sheet suggests. A 2026 test of this exact plan on Debian 12 reported 512 MB installed but **approximately 458 MB usable** once the OS was running. That leaves room for one lightweight process: a proxy, a monitoring probe, a small bot, a WireGuard endpoint. It will not run WordPress with a database comfortably, and it will not survive a MySQL instance plus a web server. If your plan involves a control panel, start at VM-1.

**VM-1 ($5.99)** is the default for a solo developer. One core, 2 GB RAM, 20 GB SSD and 1 TB of transfer is enough for a static or low-traffic WordPress site, a reverse proxy in front of an origin elsewhere, an API with modest concurrency, or a game server for a handful of players.

**VM-1.5 ($6.95)** is the value jump in the whole table. Ninety-six cents buys a second core and another 500 GB of transfer. If you're running anything that benefits from two threads (PHP-FPM workers, a Node process plus a build step, a small Postgres alongside an app), take this instead of VM-1.

**VM-2 ($11.99) and VM-3 ($14.99)** suit multi-site setups and small production workloads. VM-3 doubles your cores to four for $3 more than VM-2 while keeping 4 GB of RAM, so pick between them based on whether you're CPU-bound or memory-bound.

**VM-4 ($23.99) and above** are for workloads where 8 GB of RAM or more is a hard requirement: container hosts, larger databases, CI runners, game servers with many slots. VM-12 and VM-16 exist mainly for people who need many cores at a low per-core price and don't want to manage multiple machines.

## What the benchmarks actually show

Two independent tests on Amsterdam machines, run about 18 months apart, give a reasonable picture.

The **VM-1.5 test from November 2024** ran on an AMD EPYC Genoa platform with 2 cores reported at 3693.026 MHz and 1 GB of L3 cache. Disk I/O averaged **3242.7 MB/s** across three runs, with fio 4k mixed read/write around 542/543 MB/s. Geekbench 6 came in at **2833 single-core** and **4484 multi-core**. iperf3 hit 9.28 Gbps send and 9.39 Gbps receive against a 100G target in Amsterdam at 0.853 ms, 8.29/6.24 Gbps to London at 8.10 ms, 2.18/1.56 Gbps to New York at 76.9 ms, and 903 Mbps/1.06 Gbps to Singapore at 204 ms.

The **VM-0.5 test from May 2026** ran on a single core at 3.6 GHz with 458 MB usable RAM. Geekbench 5 scored **1606 single / 1811 multi**, SysBench single-thread CPU hit 5674, and memory bandwidth measured 70,583 MB/s read and 40,705 MB/s write. Even the $2.99 plan inherits the EPYC Genoa architecture, and the single-thread numbers back that up.

Two spec claims deserve a caveat. Evoxt advertises "**up to 6.0 GHz**" turbo, and the homepage footnote says the comparison data was collected in 2020 and may change. Both tests above reported clocks in the **3.6–3.7 GHz** range. Treat 6.0 GHz as a burst ceiling, not a sustained frequency, and judge the machine by the benchmark scores instead.

The second caveat is bandwidth. Every plan is officially a **1 Gbps port**, yet the 2024 test measured close to 9 Gbps locally. That's likely burst capacity or a port that isn't hard-capped on that host. Don't size a business model around 9 Gbps; size it around 1 Gbps and treat anything above as a bonus.

👉 [Deploy the VM-1.5 plan that produced these numbers](https://bit.ly/EvoXt)

## The China route: what you're actually getting

This is the section most reviews soften. Here it is straight: Amsterdam is a standard international route, not a China-optimised line.

A 2026 test on VM-0.5 measured a **national average of about 211 ms** from mainland China, split as China Telecom 199 ms, China Unicom 190 ms, China Mobile 253 ms. Return routing goes Telecom via Arelion/Cogent to AS4134 (163), Unicom via Arelion/Cogent to AS4837, and Mobile via Arelion to CMI. Outbound, Telecom uses 163 plus Cogent, Unicom uses AS4837 plus GTT through Frankfurt, and Mobile goes CMI through London plus Cogent.

There is no CN2, no CMIN2, no premium China transit anywhere in that path. If your users are in mainland China and latency is the product, this is the wrong continent and the wrong provider. If you're serving European users and occasionally reach Asia, 170–180 ms to the region and around 211 ms to China is normal for a European host and perfectly workable for API calls, crawlers, and background sync.

The same test measured roughly 9 ms to London, 130 ms to North America, 170–180 ms to Asia, and 270 ms+ to Oceania.

## IP quality and streaming: read this before you believe a YouTube review

Streaming results on this node depend heavily on which IP you're assigned. Two tests on the same provider, 18 months apart, disagreed:

- **November 2024:** Disney+ returned "No (IP Banned By Disney+)", Netflix resolved to "Originals Only", YouTube Premium and Amazon Prime showed the NL region, ChatGPT worked, Google Gemini did not.
- **May 2026:** the IP was flagged as an IDC datacenter address with low risk score and a clean blacklist. IPv4 supported Netflix, Disney+, TikTok and ChatGPT; IPv6 supported Netflix, Disney+ and ChatGPT but had partial limits on TikTok and Amazon Prime.

Both can be true at once because they're different IPs. Evoxt assigns from a pool, and streaming platforms change their detection constantly. If unblocking a specific service is the entire reason you're buying, order one month first and test the IP you actually get. Nobody, including this article, can promise you a clean unlock on a shared datacenter range. That test also recommended IPv4 over IPv6 for platform compatibility.

## What you'll actually pay

Evoxt's pricing page lists monthly rates only. It does not publish a yearly discount figure, and there is no separate setup fee or bandwidth overage charge beyond the $3/TB Standard rate listed above.

First-year cost at monthly billing:

| Plan | Per month | First 12 months |
| --- | --- | --- |
| VM-0.5 | $2.99 | $35.88 |
| VM-1 | $5.99 | $71.88 |
| VM-1.5 | $6.95 | $83.40 |
| VM-2 | $11.99 | $143.88 |

Billing cycles run from monthly up to three years prepaid, and you can top up an account balance to cover future invoices. Payment methods include credit card, debit card, PayPal, Bitcoin and USDt on Tron.

One thing to confirm yourself: refund terms aren't stated on the pricing or features pages, and third-party sources disagree, with two listing a 7-day window and an older affiliate write-up claiming 14 days. If the ability to back out matters to you, ask support before you pay rather than after.

👉 [Start with one month of VM-1 at $5.99 and test it](https://bit.ly/EvoXt)

## Who should skip Amsterdam

Skip this node if any of the following applies:

- **You need low latency to mainland China.** Mobile users will see 253 ms. There's no CN2 here, and no amount of plan upgrading fixes routing.
- **You want a managed control panel on the cheapest plan.** 458 MB of usable RAM won't carry cPanel, Plesk, or a full WordPress stack with MySQL.
- **You need a guaranteed streaming unlock.** Datacenter IPs rotate and platforms change policy. Buy a month, test, then commit.
- **You need multi-region failover with private networking across continents on a budget.** Evoxt offers private IPs between VMs, but a two-continent HA setup is a bigger project than a $6 VPS.

## Before you order

Match the plan to the job rather than to the price tag:

- **One process, one purpose** (proxy, probe, bot, VPN endpoint) → VM-0.5, $2.99.
- **One small site, API, or reverse proxy** → VM-1, $5.99.
- **Anything that wants two threads** → VM-1.5, $6.95, the best value in the table.
- **Multiple sites or a small production stack** → VM-2 or VM-3.
- **8 GB RAM or more** → VM-4 upward.

Two things to settle before checkout. First, confirm the plan has enough RAM to cover your OS plus your stack, because the 512 MB plan leaves roughly 458 MB after boot. Second, run your streaming or IP-reputation tests in month one rather than after a year of prepayment, since the address you get is the address you keep.

👉 [Pick your Amsterdam plan and deploy in a few minutes](https://bit.ly/EvoXt)
