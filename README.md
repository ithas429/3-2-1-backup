# data backup: the 3-2-1 rule explained, backup types compared, and what offsite cloud storage really costs

Most searches for data backup come down to one of three jobs. You either want a strategy (how many copies, where they live), a mechanism (what kind of backup runs tonight and how long a restore takes), or a destination (the actual place your files end up). Most articles blur all three together and hand you a list of "best practices" without prices.

This one keeps them separate. You'll get the strategy, the mechanics, and real numbers for both a managed backup service and raw cloud storage, including what a terabyte actually costs at a provider like Sharktech versus the big three hyperscalers.

## What you're actually asking when you search "data backup"

Strip away the jargon and the question behind the keyword is usually one of these:

- "I have important files on one machine and I know that's bad. What do I do?"
- "My backup situation exists but I'm not sure it would survive a real disaster."
- "I need somewhere cheap to send backups from software I already run."

All three are legitimate, and they lead to different purchases. The first points toward a managed backup service. The second points toward fixing your strategy. The third points toward object storage or a cheap server you control. We'll get to all of them, but the strategy part comes first because it decides everything else.

## The 3-2-1 rule, and the two upgrades worth knowing

The 3-2-1 rule is the closest thing data protection has to a consensus. It's been around for decades and it survives because it maps to how data actually gets lost: drives die, laptops get stolen, ransomware encrypts everything it can reach.

> **3** copies of your data, on **2** different types of media, with **1** copy offsite.

Two modern variants are worth adding to your mental model:

- **3-2-1-1-0**: the extra "1" is one immutable or offline copy, a backup that physically cannot be overwritten or encrypted even if an attacker gets admin access. The "0" means zero errors when you test a restore. That last part is the one everyone skips and regrets.
- **Air gap vs. immutability**: an air-gapped copy is simply unreachable from your network, like a disk you unplugged. An immutable copy is reachable but write-protected at the storage layer. Air gaps are safer against novel attacks; immutable backups are faster to restore from. Mature setups use both ideas.

Why does "2 different media" matter? Because the failure modes differ. A NAS and an external USB drive are both in your house, but they fail for different reasons. Cloud storage adds a third failure domain entirely, which is why the offsite copy is the rule's non-negotiable core.

## Full, incremental, differential: the 30-second version

If you're configuring any backup tool, you'll hit these three words. They're simpler than they sound:

| Backup type | What it copies | Trade-off |
| --- | --- | --- |
| Full | Everything, every time | Fastest single restore; slowest to run, most storage |
| Incremental | Only changes since the last backup of any kind | Tiny and fast; restore needs the full chain, one broken link kills it |
| Differential | All changes since the last full backup | Middle ground; restore needs just the full + latest differential |

A common pattern is one full backup weekly with nightly incrementals, or a full monthly with daily differentials if you want shorter restore chains. If you're backing up over a home or office connection to cloud storage, incrementals plus deduplication and compression are what keep upload times and bills sane.

## The first real decision: managed backup, or your own tool?

Once the strategy is set, you face a fork. Path one is a **managed service**: you install an agent, someone else runs the storage, encryption, and retention. Path two is **bring your own tool**: restic, Borg, Veeam, Duplicacy, rclone, whatever you like, pointed at cheap storage you rent by the terabyte.

Neither is universally better. Managed wins on convenience and on having a vendor to call at 2 a.m. Your own tool wins on cost at scale and on control.

This is where Sharktech enters the picture, because they sell both paths. Sharktech is a hosting provider that's been around for about 20 years, runs data centers in Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam, includes 60 Gbps DDoS protection as standard on their services, and claims 99.999% uptime on their cloud platforms. Their two backup-relevant products are Acronis Cloud Backup (the managed path, powered by Acronis Cyber Protect) and S3-compatible Object Storage (the BYO-tool path). You can 👉 [see both backup services and current pricing here](https://bit.ly/SharKTech).

## Every current plan and price

Here's what their backup services cost right now, pulled from the official product pages. Acronis Cloud Backup is priced per billing cycle with a 200 GB base and per-GB overage; S3 Object Storage is a flat per-TB rate. The full picture:

| Service | Billing cycle | Base price | What's included | Extra storage rate | Order |
| --- | --- | --- | --- | --- | --- |
| Acronis Cloud Backup | Monthly | $4.00/mo | 200 GB cloud backup & protection | $0.02/GB | [ Start a monthly backup plan](https://portal.sharktech.net/aff.php?aff=1611&pid=648) |
| Acronis Cloud Backup | Quarterly | $8.00 / 3 months | 200 GB cloud backup & protection | $0.04/GB | [ Order quarterly and save](https://portal.sharktech.net/aff.php?aff=1611&pid=648) |
| Acronis Cloud Backup | Semi-annual | $12.00 / 6 months | 200 GB cloud backup & protection | $0.06/GB | [ Order the 6-month cycle](https://portal.sharktech.net/aff.php?aff=1611&pid=648) |
| Acronis Cloud Backup | Annual | $24.00 / year | 200 GB cloud backup & protection | $0.12/GB | [ Order annual backup](https://portal.sharktech.net/aff.php?aff=1611&pid=648) |
| S3 Object Storage | Monthly | $4.90/mo | 1 TB storage + 1 TB bandwidth included | $4.90/TB, configurable up to 100 TB | [ Get 1 TB of S3 storage](https://portal.sharktech.net/aff.php?aff=1611&pid=643) |

A few details the table can't hold:

- **Files Sync & Share add-on** (Acronis): $0.03/GB monthly, $0.06/GB quarterly, $0.12/GB semi-annually, $0.24/GB annually, added on top of backup storage if you want Dropbox-style sync.
- **Longer cycles discount the base but raise the per-GB overage.** The quarterly base works out to about $2.67/month versus $4 monthly, so prepaying still comes out ahead for most sizes.
- **S3 bandwidth**: the first terabyte is free, and their homepage lists additional bandwidth at $0.90/TB. At hyperscalers, egress is typically the line item that ruins your month, so a flat sub-dollar per-TB rate is genuinely unusual.
- The S3 order form scales from 1 TB up to 100 TB of storage and up to 10,000 TB of bandwidth if you're archiving seriously.

## How the Acronis data backup service works day to day

Ordering is a portal flow: pick a data center (Los Angeles, Las Vegas, Denver, Chicago, or Amsterdam), set your storage size on the configurator (it runs from 25 GB up to 100,000 GB), choose a billing cycle, and check out. Sharktech provisions the cloud storage target, then you install the standard Acronis agent on whatever you're protecting. Windows, Linux, and macOS are all supported, along with VMs, NAS devices, and mobiles.

From there you set a schedule, hourly or daily, and the rest is automatic. Encryption at rest, compression, and deduplication are built in, so the storage number you're paying for reflects deduplicated data, not raw file sizes. Acronis Cyber Protect also bundles anti-malware, URL filtering, and patch management alongside the backup engine, which is why it's pitched as "cyber protection" rather than plain backup.

To make the pricing concrete: 500 GB of protected storage on the monthly cycle is $4.00 plus 300 × $0.02, so **$10.00/month**. The same 500 GB prepaid annually is $24.00 plus 300 × $0.12, so **$60.00/year**, which works out to $5.00/month. That's arithmetic from the published rates; the order form shows your final figure before you pay, so use it as the source of truth for your exact size.

Restores run through the Acronis web interface or app, and you can pull individual files or whole systems. That flexibility matters more than people expect: "restore the entire machine" is for disasters, "restore the spreadsheet I overwrote at 4 p.m." is for Tuesday.

If that workflow sounds like what you want, you can 👉 [check current Acronis backup pricing and order here](https://portal.sharktech.net/aff.php?aff=1611&pid=648).

## The S3 route: cheap terabytes, your rules

If you already run backup software, or you're comfortable following a restic or Borg tutorial, object storage is the more interesting option. Anything that speaks the S3 API can target it, which covers essentially every modern backup tool, from homelab favorites to enterprise kits. DevOps teams also use it for CI/CD artifacts and release archives.

The pricing is where this gets attention-worthy. Sharktech charges **$4.90 per TB per month**, flat, with no commitment tiers. For context, current hot/standard object storage at the big providers runs approximately $18 per TB at Azure, $20 at Google Cloud, and $23.55 at AWS S3 Standard. So you're looking at roughly a quarter to a fifth of hyperscaler rates for infrequently accessed data like backups and archives.

The infrastructure behind it is triple-redundant storage clusters with 40G connectivity, which is more than enough for backup workloads where you're pushing and pulling large sequential files rather than serving millions of tiny reads. One honest caveat: Sharktech's S3 is built for the backup/archive/media use case, not for low-latency global CDN serving. If you need the latter, you already know, and you're already paying for it.

For the DIY crowd, you can 👉 [configure S3 storage from 1 TB to 100 TB here](https://portal.sharktech.net/aff.php?aff=1611&pid=643).

## When a whole server beats a backup service

There's a third path that fits some people better than either product above: rent an actual machine and make it the backup target. This makes sense when you have multiple terabytes of media, you run Proxmox or TrueNAS and want block-level replication to a second box, or you want ZFS snapshots on hardware you control.

Sharktech's current pricing on the infrastructure side, verified against their order pages and current listings:

| Product | Starting price | Notes |
| --- | --- | --- |
| Smart VPS | $7.95/mo | Xeon Gold, NVMe, unlimited VMs within your resource pool; 25% off quarterly, 35% semi-annual, 50% off annual |
| Public Cloud Small | $39.00/mo | OpenStack, 4–16 vCPU, 8–32 GB RAM, 300–2400 GB SSD |
| Public Cloud Medium | $79.00/mo | 8–32 vCPU, 16–64 GB RAM, 800–6400 GB SSD |
| Public Cloud Large | $249.00/mo | 32–128 vCPU, 64–256 GB RAM, up to 24 TB storage |
| Public Cloud Enterprise | $499.00/mo | 64+ vCPU, 128 GB+ RAM, effectively uncapped |
| Dedicated storage servers | from ~$219/mo (current listings) | Dual Xeon, 256 GB RAM, chassis with 12–24 drive bays |

The Smart VPS line deserves a note: you get a pool of CPU, RAM, and NVMe storage that you can carve into as many virtual machines as the pool allows, across any of their data centers. For a homelab-style replication target, the entry tier at $7.95 (which halves to under $4/month equivalent if you prepay annually) is hard to argue with. If you want to explore that route, 👉 [browse the VPS and cloud plans here](https://bit.ly/SharKTech).

The trade-off is the same one it's always been: when you build your own backup server, every failure mode is yours. The disk that silently dies, the update that breaks the snapshot job, the firewall rule that blocked replication for three weeks. A managed service trades a monthly fee for someone else's pager.

## Ransomware doesn't care about your feelings

The ugly truth about modern data loss is that hardware failure has been demoted. Ransomware is the headline threat now, and its whole playbook is finding every reachable copy of your data and encrypting it, including network shares and connected backup targets.

This is why the immutable or air-gapped copy from the 3-2-1-1-0 variant exists. A backup stored on a mounted drive or an always-connected NAS is inside the blast radius. Object storage with object-lock style protections, or a backup service that keeps versioned, tamper-resistant restore points, is not. Acronis Cyber Protect also runs behavioral detection that flags encryption-style activity, which is a useful tripwire, but treat it as a supplement to isolation, not a replacement.

And the "0" again: test a restore. A backup you have never restored from is a hope, not a backup. Pick a file, recover it, confirm it opens. Once a quarter is plenty. It takes ten minutes and it's the only way to know the whole chain actually works.

## Quick answers

**How often should data backup run?** For work documents and anything that changes daily, daily automated backups minimum. Databases and active projects justify hourly. The right question is "how much am I willing to lose," and the answer sets the schedule.

**External drive or cloud?** Both, ideally. The drive is your fast local restore; the cloud copy is the one that survives the fire, the theft, or the encryption event. If you can only afford one, the offsite copy is the one that matters, because local copies share fate with the machine.

**Is 200 GB enough?** For a laptop's documents, photos, and config, often yes, especially with deduplication and compression working in your favor. For media collections, VM images, or databases, no, and the per-GB overage or S3 per-TB math above is what you should be running.

**What does a realistic setup cost per month?** A managed 200 GB backup starts at $4.00, a realistic 500 GB runs about $10 monthly or $5 prepaid annually, and a terabyte of raw S3 storage for your own tooling is $4.90. Protecting a few machines well costs less than a streaming bundle. There's really no budget excuse left.

## The short version

Start with the boring, correct thing today: two extra copies, different media, one somewhere else, restore tested. Whether you get there with a managed agent like Sharktech's Acronis offering from $4.00/month, or by pointing restic at $4.90/TB S3 storage, matters far less than having the copies at all. If you're still deciding, 👉 [compare the backup plans and current pricing here](https://bit.ly/SharKTech) and pick the one you'll actually set up tonight.
