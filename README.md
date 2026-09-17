# windows dedicated server: Specs, Licensing, and Real Plan Prices Before You Overpay

Most people searching for a **windows dedicated server** fall into one of three camps: a developer with an ASP.NET or legacy .NET app that refuses to behave anywhere else, a business that needs Remote Desktop sessions or SQL Server on hardware it doesn't have to share, or someone running Windows-only software (trading bots, ERP systems, game servers with Windows-only mods) who has outgrown a VPS. The common thread is simple — the software demands Windows, and shared resources are now the bottleneck.

That combination creates a trap. A lot of hosting guides compare CPU, RAM, and bandwidth in detail, then completely skip the two things that actually blow up Windows budgets: **licensing costs that scale with core count**, and **setup fees or bandwidth caps** hidden in the fine print. This guide walks through the decisions in the order you'll actually face them — workload, license, hardware, provider — and then gets specific with a real provider's current plan lineup so you can see what actual numbers look like.

## When You Actually Need One

Let's be honest about the threshold question first, because plenty of people researching dedicated servers would be fine on something cheaper.

A Windows VPS handles light workloads well: a small IIS site, a single-user Remote Desktop box, a test environment. The problem starts when you hit resource contention. A VPS shares CPU time and disk I/O with other tenants, and if your neighbor is hammering the disk, your SQL queries wait. On a dedicated server, that variable disappears — the hardware is yours, full stop.

You're a genuine candidate for dedicated if any of these describe you:

- **You host multiple RDP sessions or a Remote Desktop Services setup.** Microsoft's own documentation notes Remote Desktop connects to machines running Windows Pro, Enterprise, Education, and Windows Server editions — and RDS workloads get ugly fast when I/O is shared.
- **You run SQL Server under real load.** Database engines are the classic noisy-tenant victim.
- **You have ASP.NET / .NET Framework apps that expect full control** of the server environment — custom GAC assemblies, COM components, third-party services.
- **You host game servers with Windows-specific tooling**, or application software your business depends on that only exists for Windows.
- **You need Active Directory or a Windows-specific network role** that you don't want living on cloud VMs priced by the hour.

If none of that applies and you're hosting a WordPress site on a Windows box out of habit — you can stop reading here and save yourself a few hundred dollars a month.

## The Licensing Catch Most Guides Skip

Here's the part that changes hardware decisions, and almost nobody puts it early enough in the buying process.

Windows Server is licensed **per CPU core**, not per server. Microsoft's current pricing puts a 16-core Standard pack at roughly $1,100–$1,200 MSRP, and Datacenter edition costs several times that. There's also the SPLA route — Service Provider License Agreement — which Microsoft partners use to rent Windows licenses month-to-month with no CALs required. Many hosts fold that rental cost into the monthly price; others expect you to **bring your own license (BYOL)**.

Why does this matter before you pick a server? Because a dual-CPU box with 36 cores might cost $259/month on hardware, but licensing 72 physical cores under Standard rules adds a serious chunk of change — potentially more than the server itself. A single-socket machine with fewer, faster cores can end up dramatically cheaper to run *in total cost* even if the sticker price looks similar.

> Practical rule: on Windows, total cost = hardware + license. Never compare plans on hardware price alone.

On the provider side, this splits the market into two behaviors. Some hosts quote you a "Windows dedicated server" price with the license baked in. Others — and this is worth confirming before checkout — hand you bare-metal access and let you install the OS yourself. Sharktech, for example, sells bare-metal servers with hardware-level access and lets you do a custom OS installation, with Linux and BSD available at no cost; third-party reviews of their dedicated offering note that Windows Server requires your own license key. That's the BYOL model: hardware is theirs, the Windows license is your problem. It's not a red flag — it's just a number you must add to your budget yourself.

## Sizing the Hardware Without Guessing

Once licensing is settled, the spec question gets much easier. Match the workload, not the brochure.

**CPU:** Web apps and RDP hosting care about clock speed per session — fewer fast cores beat many slow ones. Databases and virtualization want core count. If you're going to slice the box into VMs with Hyper-V, you need cores and RAM, and you should mentally double the RAM you first thought of.

**RAM:** 16GB is genuinely tight once SQL Server gets involved. 32GB is a sensible floor for a production Windows box; 64GB and up belongs to database servers, RDS farms, and virtualization hosts.

**Storage:** Two things matter: NVMe for anything database-shaped, and spare drive bays for when you need capacity later. A server with two filled bays and no free slots forces a migration down the road. This is one of the most overlooked specs on order pages — count the bays before you click.

**Bandwidth:** Read the fine print carefully. "300TB/month on 10Gbps" and "unmetered 1Gbps" are very different deals for different workloads. A file-heavy RDP server or a game server with heavy download traffic will feel a 300TB cap long before a quiet app server does. Also check whether the uplink is shared or dedicated.

**Location:** For RDP use, latency is your user experience. Pick a data center near the humans who will be typing into it. Chicago or Denver works well for US-wide coverage; Amsterdam serves Europe; Los Angeles suits Asia-Pacific-facing traffic.

## What a Good Provider Should Include (and Many Don't)

Before comparing specific plans, run any candidate through this checklist. The differences here often outweigh a $20/month price gap:

- **Free setup.** Plenty of hosts still charge $50–$150 to plug in a server. There's no reason to pay it in a competitive market.
- **DDoS protection included.** If it's a paid add-on, your real monthly price is higher than advertised. Game servers and anything publicly exposed should treat this as mandatory.
- **An uptime commitment in writing.** 99.99% is the standard for serious providers — that's about 52 minutes of downtime per year.
- **Hardware-level access and a management panel.** Being able to reinstall the OS, manage the machine out-of-band, and monitor hardware yourself saves support tickets and outage time.
- **Free OS choices.** Linux and BSD should cost nothing. Windows licensing will follow one of the two models above — just know which one before you commit.
- **Upgrade path.** Can you add RAM or swap drives later without a full migration and re-setup fee? Hardware you outgrow on day one is a sunk cost.
- **24/7 support with real humans.** When your Windows box drops at 3 a.m. on a Saturday, "submit a ticket and wait until Monday" is not a support plan.

## A Real Lineup: Sharktech's Current Bare-Metal Plans

To make this concrete, here's a full look at one provider's currently advertised dedicated lineup — Sharktech, a hosting company operating since 2003 with data centers in Los Angeles, Denver, Chicago, Las Vegas, and Amsterdam. Their angle is bare-metal: every plan includes hardware-level access, proprietary DDoS protection, 24/7 support, and **free setup**. Linux and BSD installs are free; Windows Server is bring-your-own-license territory.

These are the configurations currently listed on their dedicated servers page, all with 10Gbps uplinks and 300TB/month bandwidth (upgradeable to 40G or 100G):

| Plan | CPU | RAM | Storage | Network | Price (monthly) | Order |
| --- | --- | --- | --- | --- | --- | --- |
| Dual E5-2695v4 (2.5" bays) | 36 × 2.1 GHz | 64GB DDR4 | 2TB M.2 NVMe + 6 SATA/SAS bays | 10Gbps, 300TB/mo | $259 | [Order this plan](https://bit.ly/SharKTech) |
| Dual E5-2695v4 (3.5" bays) | 36 × 2.1 GHz | 64GB DDR4 | 2TB M.2 NVMe + 6 SATA/SAS bays | 10Gbps, 300TB/mo | $269 | [Get a sales quote](https://bit.ly/SharKTech) |
| Dual Xeon Gold 6248 | 40 × 2.5 GHz | 128GB DDR4 | 2TB M.2 NVMe + 3 SATA/SAS bays | 10Gbps, 300TB/mo | $299 | [Order this plan](https://bit.ly/SharKTech) |
| Dual Xeon Gold 6248 (2.5") | 40 × 2.5 GHz | 128GB DDR4 | 2TB M.2 NVMe + 6 SATA/SAS bays | 10Gbps, 300TB/mo | $309 | [Order this plan](https://bit.ly/SharKTech) |
| Dual Xeon Gold 6246 | 24 × 3.3 GHz | 128GB DDR4 | 2TB M.2 NVMe + 3 SATA/SAS bays | 10Gbps, 300TB/mo | $309 | [Order this plan](https://bit.ly/SharKTech) |
| Dual Xeon Gold 6248 (U.2) | 40 × 2.5 GHz | 128GB DDR4 | 2TB M.2 NVMe + 6 U.2 bays | 10Gbps, 300TB/mo | $329 | [Order this plan](https://bit.ly/SharKTech) |
| AMD EPYC 7702P | 64 × 2 GHz | 128GB DDR4 | 2TB M.2 NVMe + 10 U.2 bays | 10Gbps, 300TB/mo | $499 | [Order this plan](https://bit.ly/SharKTech) |
| Dual AMD EPYC 7702 | 128 × 2 GHz | 128GB DDR4 | 2TB M.2 NVMe + 10 U.2 bays | 10Gbps, 300TB/mo | $699 | [Get a sales quote](https://bit.ly/SharKTech) |

Every plan above can be upgraded during ordering or afterward — RAM scales to 1TB on most configs, NVMe and SSD options expand through the drive bays, and network upgrades to 40G/100G are listed on the order forms.

Notice something about this lineup that matters for **Windows workloads specifically**: nearly every machine is dual-socket with high core counts. Great value per core for Linux workloads, but if you're paying for a 72-core Windows Standard license on top of that $259 hardware bill, do the arithmetic first. The dual-socket strategy favors buyers running Hyper-V farms with plenty of Linux guests, or BYOL customers with existing per-core licenses. If you're a single-purpose Windows shop, ask the sales team about single-socket options — the company explicitly invites custom configurations when a listed spec doesn't fit, and their own page notes that non-standard hardware can be sourced through vendors. 👉 [Ask about a custom Windows configuration](https://bit.ly/SharKTech)

## The Billing Cycle Math Nobody Mentions

The monthly prices above aren't the whole story. Like most hosts, Sharktech discounts longer commitments — and the discounts are worth paying attention to because they're steeper than typical. Taking the $259/mo dual E5-2695v4 plan as the example:

- **Monthly:** $259/mo
- **Quarterly:** $738.15/qtr — about **$246/mo (5% off)**
- **Semi-annual:** $1,398.60/6mo — about **$233/mo (10% off)**
- **Annual:** $2,641.80/yr — about **$220/mo (15% off)**

Fifteen percent for annual prepay is a meaningfully better deal than the 5–8% many providers offer. On the EPYC plans it scales up too — the dual-EPYC box at $699/mo drops to roughly $594/mo on annual billing. If your workload is stable and the provider checks out on the points above, the annual commitment is where the real value sits. One honest caveat, though: prepaying a year to any host is a trust decision. Check reviews, test support responsiveness with a pre-sales question, and start monthly if you have any doubt. 👉 [Compare billing cycles on current plans](https://bit.ly/SharKTech)

Two operational notes from Sharktech's own documentation worth knowing before you order: they can't guarantee delivery in under 24 hours for customized bare-metal (hardware lead times being what they are), and their SLA covers hardware failures — RAM, processors, drives, boards — with a 99.99% uptime guarantee.

## What Users Actually Say

Reputation checks for mid-size hosting companies require some calibration, because review samples are small.

Sharktech holds a 3.5 out of 5 on Trustpilot across 13 reviews — a modest rating on a modest sample, with feedback skewing toward the extremes, both delighted and frustrated. The company also points to independent testing by HostAdvice recognizing it for uptime, service quality, and support, and its long-running clients include game hosting companies that specifically cite surviving multi-gigabit DDoS attacks as their reason for staying. A 20-year operating history with hosting-heavy clients is a decent durability signal; a 13-review Trustpilot page is a data point, not a verdict. The right move is the same one that applies to any of this market's providers: start with a shorter billing cycle, verify the DDoS filtering and RDP performance against your own workloads, then commit longer once the numbers hold.

## Frequently Asked Questions

**Can I use a Windows dedicated server as a personal Remote Desktop machine?**
Yes — this is one of the most common uses. You get a full Windows environment reachable via RDP from anywhere, running your applications 24/7 without keeping an office PC powered on. Note that RDP into Windows Server requires appropriate licensing; for multi-user Remote Desktop Services scenarios, RDS CALs apply on top of the server license.

**How much does the Windows Server license add per month?**
It depends on the route. Buying Standard outright runs around $1,100–$1,200 MSRP per 16-core pack (one-time), sized to your physical core count. SPLA rental through a host is month-to-month with no CALs required but recurs monthly. On a 72-core dual-socket machine, licensing can genuinely rival the hardware price — which is why single-socket plans are worth asking about for Windows.

**Is a Windows dedicated server harder to manage than Linux?**
Not harder, just different — arguably easier if your team already runs Windows environments, since the same PowerShell, Remote Desktop, and Microsoft tooling transfers. The learning curve is in Windows Server administration itself (roles, updates, RDS setup), not in the dedicated-server part.

**Dedicated, VPS, or cloud for Windows — which is right?**
VPS if budget matters and load is light; cloud if you need hourly elasticity and don't mind per-hour billing on a Windows license; dedicated when performance is non-negotiable, the workload runs 24/7 at high utilization, or licensing economics favor long-term hardware. High, steady utilization is exactly where dedicated wins.

**How long until the server is ready?**
Providers vary; Sharktech notes same-day delivery isn't guaranteed for customized bare-metal due to hardware supply, so plan a short lead time for custom configs. Standard configurations deploy faster.

## Bottom Line

A Windows dedicated server purchase is really two purchases — the hardware and the license — and getting either one wrong is expensive. Size the CPU to your licensing budget, count your drive bays before you need them, demand DDoS protection and free setup as standard, and put the data center near your users.

Sharktech's lineup makes a fair reference point for what the market currently offers: real bare-metal with hardware-level access, 10Gbps uplinks standard, free setup, genuine annual-billing discounts up to 15%, and DDoS protection baked into every plan across five locations. The Windows BYOL model means you'll handle Microsoft licensing yourself — annoying for some, but transparent, and often cheaper if you already own licenses. If your Windows workloads need the whole box and steady 24/7 performance, that profile fits. If your needs are lighter, a smaller plan or a monthly first cycle while you verify everything is the smarter opening move. 👉 [See the full current plan lineup](https://bit.ly/SharKTech)
