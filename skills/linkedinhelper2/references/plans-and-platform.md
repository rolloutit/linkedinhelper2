# Plans, Credits, Platform and Data Management — Linked Helper 2

Commercial and platform reference for `SKILL.md` §2 and §8: prices, gating, credits, OS/hardware,
workspaces, VPS, folder paths, backup. Symptom-driven diagnostics are in
`references/troubleshooting.md`; proxy *safety* rules are in `references/limits-safety.md`.

> **All pricing, credit and system-requirement figures below were verified against
> `linkedhelper.com` and `support.linkedhelper.com` on 2026-09-01.** Prices and credit allowances
> change without notice. **Re-check the live page before quoting any figure to a customer or
> putting one in a proposal.** If you cannot re-check, quote the figure *with* its date and say it
> needs confirmation.

## Table of contents

1. [Pricing](#1-pricing)
2. [Licence ↔ LinkedIn account mapping](#2-licence--linkedin-account-mapping)
3. [Standard vs Pro — the gating table](#3-standard-vs-pro--the-gating-table)
4. [Credits](#4-credits)
5. [Local vs cloud storage — how to choose](#5-local-vs-cloud-storage--how-to-choose)
6. [Platform support and sizing](#6-platform-support-and-sizing)
7. [Workspaces and multi-account operation](#7-workspaces-and-multi-account-operation)
8. [Proxies at the account level](#8-proxies-at-the-account-level)
9. [Cloud, VPS and 24/7 operation](#9-cloud-vps-and-247-operation)
10. [Data management](#10-data-management)
11. [Sending logs to support](#11-sending-logs-to-support)
12. [Marketed feature names vs help-center names](#12-marketed-feature-names-vs-help-center-names)
13. [Known contradictions](#13-known-contradictions)

## 1. Pricing

Two product variants — **Local-based storage** and **Cloud-based storage** — each in three tiers:
Trial / Standard / Pro. Quoted figures are **per month on a prepaid 3/6/12-month term**, not
monthly-cancellable prices.

### 1.1 Local-based storage — USD, verified 2026-09-01

| Term | Standard /mo | Standard total | Pro /mo | Pro total |
|---|---|---|---|---|
| 1 month | $15.00 | $15 | $45.00 | $45 |
| 3 months (−11%) | $13.33 | **$40** | $40.00 | **$120** |
| 6 months (−33%) | $10.00 | **$60** | $30.00 | **$180** |
| 12 months (−45%) | $8.25 | **$99** | $24.75 | **$297** |

Per-month figures from `/pricing`; bolded per-term totals are published by the help center and match
exactly (13.33×3=40, 8.25×12=99, 40×3=120, 24.75×12=297). `[LH-CLAIM]`
Source: https://www.linkedhelper.com/pricing · https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts

### 1.2 Cloud-based storage — USD, verified 2026-09-01

| Term | Standard /mo | Standard total | Pro /mo | Pro total |
|---|---|---|---|---|
| 1 month | $29.90 | $29.90 | $59.90 | $59.90 |
| 3 months (−11%) | $26.60 | $79.80 `[UNVERIFIED]` | $53.30 | $159.90 `[UNVERIFIED]` |
| 6 months (−33%) | $20.00 | $120.00 `[UNVERIFIED]` | $40.00 | $240.00 `[UNVERIFIED]` |
| 12 months (−45%) | $16.50 | $198.00 `[UNVERIFIED]` | $33.00 | $396.00 `[UNVERIFIED]` |

Only per-month figures are published; **cloud per-term totals are not displayed anywhere** — those
above are arithmetic and marked `[UNVERIFIED]`. Read them off the checkout page before quoting.
Cloud runs ~2× local for Standard, ~1.33× for Pro. USD only; no EUR/GBP pricing → `[UNVERIFIED]`.
Source: https://www.linkedhelper.com/pricing

### 1.3 Bulk licence discounts (single invoice) — verified 2026-09-01

| Licences on one invoice | Discount |
|---|---|
| 10–19 | 10% |
| 20–49 | 20% |
| 50–74 | 30% |
| 75–99 | 35% |
| 100–999 | 40% |
| 1,000+ | 50% |

Stacks on the term discount; the only documented volume mechanism. No refund policy or other
discount route is published → `[UNVERIFIED]` `[LH-CLAIM]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts

### 1.4 Trial — verified 2026-09-01

- **14 days**, marketed as "14-Day Full Feature Access", "Explore Standard & Pro capabilities",
  "24/7 Support".
- **No payment card required** — the homepage repeats "100% Free. No card."
- **Trial credit allowance is blank** in both credit rows of the `/pricing` table.
  `CONFLICT:` `/features/data-enricher` implies **~1,400 Data credits over the 14 days**; `/pricing`
  shows **no figure**. Treat 1,400 as `[UNVERIFIED]`; have the user read `Billing` → `Data Credits`
  after signup instead of planning against it.
- Trial throughput caps are not stated → `[UNVERIFIED]`.

Source: https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/ · https://www.linkedhelper.com/features/data-enricher

## 2. Licence ↔ LinkedIn account mapping

### 2.1 The rule, verbatim

> "1 license = 1 LinkedIn account (You can't use one license on two accounts simultaneously, but you
> can switch it anytime.)"

Help center: "A license cannot be used for two LinkedIn accounts simultaneously" but it can be
switched; it also **cannot run simultaneously on multiple computers**. `[LH-CLAIM]`
Source: https://www.linkedhelper.com/pricing · https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts

### 2.2 Switching a licence between accounts

Path: Launcher → `Licenses` → hover the licence record → `Attach to LinkedIn account` → select the
instance → `Assign`.

Two operating models: **single licence, sequential** — one licence reattached by hand across
several accounts, so "accounts can't work simultaneously" and only the attached instance runs; or
**multiple licences, simultaneous** — one licence per instance, all accounts running at once with no
reattaching.

Two hard bindings: **an instance is permanently bound to the first LinkedIn account logged in
through it** (the licence moves, the instance does not — a wrongly-created instance cannot be
repurposed); and **you cannot open two Launchers on one PC**, plus **"You won't be able to open the
same LinkedIn account under one and the same Linked Helper account from several machines
simultaneously"** — the same account under *different* Linked Helper accounts on several machines is
"strongly not recommended". Switching a licence does not move data (local per machine); moving
machines means a backup/restore (§10.3). `[LH-CLAIM]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360015219400-How-to-manage-multiple-LinkedIn-accounts · https://support.linkedhelper.com/hc/en-us/articles/360016336859-Can-I-use-Linked-Helper-2-on-several-PCs · https://support.linkedhelper.com/hc/en-us/articles/4408390475154-Errors-when-adding-LinkedIn-account

### 2.3 There is no team, agency or enterprise price tier

`/pricing` has **no team, agency, multi-seat or enterprise tier** and no "contact sales" route →
`[UNVERIFIED]`. What agencies actually do:

1. **Buy N licences**, one per LinkedIn account, taking the bulk discount at 10+ (§1.3).
2. **Use Workspaces as the management layer** (§7): billing, integrations, proxies and a Data-credit
   vault sit in the workspace with role-based permissions; licences/assets are reassignable when
   staff change. LinkedIn accounts are the "operational layer".
3. **White Label Customization** — agencies can "replace Linked Helper brand" with their own.
4. **Cross-Account Campaign Cloning** and **Direct Lead Mobility** are cloud-variant only
   ("Available with Cloud DB"). Maximum workspaces/seats/accounts: not stated → `[UNVERIFIED]`.

Source: https://www.linkedhelper.com/features/workspaces · https://www.linkedhelper.com/pricing

## 3. Standard vs Pro — the gating table

### 3.1 The single mechanism: a 20-per-24h cap on "advanced actions"

Standard is not feature-locked out of most things — it is **rate-capped at 20 actions per 24 hours**
on a set of "advanced" activities. Marketing calls this **"Limited advanced actions (20/day)"**
(Standard) vs **"Unlimited daily actions"** (Pro).

**Capped activities as the help center lists them** (10): `Like and comment posts and articles` ·
`Message to group members` · `Message to event attendees` · messaging **with attached images** ·
`Invite to group` · `Invite person to event` · `Invite to follow organization` ·
`Send person to external CRM` · webhook integrations · `Boost post`.

**The same gating as `/pricing` rows it** (9 rows, different granularity):

| Row on /pricing | Trial | Standard | Pro |
|---|---|---|---|
| Messages/day limit | (blank) | **20/day** | **Unlimited** |
| Message to event attendees | ✓ | 20/day | Unlimited |
| Webhook profile sending | ✓ | 20/day | Unlimited |
| Webhook messaging history | ✓ | 20/day | Unlimited |
| Invite to LinkedIn event | ✓ | 20/day | Unlimited |
| Invite to follow company | ✓ | 20/day | Unlimited |
| Invite to join group | ✓ | 20/day | Unlimited |
| Like and comment posts | ✓ | 20/day | Unlimited |
| Auto-tag under "Boost post" | ✓ | 20/day | Unlimited |

`CONFLICT:` the lists disagree on scope — the help center caps `Message to group members`,
messaging-with-images and `Send person to external CRM`, which `/pricing` does not name, while
`/pricing` adds a blanket **"Messages/day limit 20/day"** (capping *all* messaging) plus "Auto-tag
under Boost post". Rule: **assume the union is capped on Standard**; volume on anything in either
list means Pro, not a workaround. `[LH-CLAIM]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts · https://www.linkedhelper.com/pricing

### 3.2 What Pro adds beyond removing the cap — verified 2026-09-01

| Capability | Standard | Pro |
|---|---|---|
| All ten/nine capped activities above | 20 / 24 h | **Unlimited** |
| **Advanced data export** | not available | ✓ ("Advanced data export restricted to Pro plan") |
| **Messaging-history export** to CSV | **not available** (see CONFLICT below) | ✓ full history |
| **Messaging-history export** via webhook | **not available** | ✓ |
| Webhooks (profile sending) | 20 profiles/day | Unlimited |
| Data credits included per month | 620 | 3,100 |
| AI credits included per month (1-month term) | 250 | 500 |

`CONFLICT: messaging-history export gating.`
- `/pricing` marks **"Export messaging history" ✓ for Standard**.
- `/features/data-export`: Standard gets full CSV export **"except messaging history"**.
  `/features/scrape-messaging-history`: scraping/saving works on both tiers but **export to CSV or
  webhook is Pro-only**. Licensing article: "**Standard cannot export messaging history**". Inbox
  plug-in article: "CSV export … **available for PRO license only**", "messaging history cannot be
  sent via webhook on a Standard license".
- **Four sources say Pro-only, one (the pricing table) says Standard.** Show both, plan for
  **Pro-only**, and have the user verify before promising a deliverable that depends on it.

Source: https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/data-export · https://www.linkedhelper.com/features/scrape-messaging-history · https://www.linkedhelper.com/features/data-enricher · https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts · https://support.linkedhelper.com/hc/en-us/articles/9003176158226-Inbox-plug-in

### 3.3 Not gated at all — ✓ on Trial, Standard and Pro alike

Invite connections · message follow-ups and sequences · reply detection · advanced conversation
filtering · InMails · `Message to LinkedIn group members` (per `/pricing`; the help center caps it —
§3.1 CONFLICT) · AI Personalized Messages · AI Message Generator · AI Text Editor · AI Replies ·
AI Comments · AI ICP Detection · unlimited campaigns · custom campaign builder · performance
dashboard · smart custom settings · working-hours settings · advanced message template editor ·
custom variables (CSV/CRM) · export people profiles to CSV · export organization profiles · custom
notes (CRM) · tagging and auto-tagging · full-profile data scraping · Contact Data Enrichment ·
auto-accept invitations · cancel pending invitations · follow profiles · endorse skills · remove
unwanted connections · free + premium LinkedIn support · Sales Navigator support · Recruiter
support · profile/org page search · post-engagement lists · 1st-level connections · school alumni
pages · custom Sales Navigator lists · recruiter projects · pending-invitations list · direct
profile pages · LinkedIn group members · CSV import. `[LH-CLAIM]`

"Unlimited campaigns" is a licence statement, not a safety statement — the limits in
`references/limits-safety.md` bind regardless of tier. **Pro removes the licence cap, not
LinkedIn's**: "Linked Helper cannot remove or bypass limits imposed by LinkedIn".
Source: https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/smart-invitations

## 4. Credits

Two independent, non-interchangeable currencies: **Data credits** (enrichment) and **AI credits**
(generation). Both are held per workspace; balance in Launcher → `Billing` → `Data Credits`.

### 4.1 Included Data credits — verified 2026-09-01

`/pricing` presents Data credits as **flat per month regardless of term**: Standard **620/mo**, Pro
**3,100/mo**. The help center instead publishes per-term totals included with the licence:

| Term total (help center) | 1 mo | 3 mo | 6 mo | 12 mo |
|---|---|---|---|---|
| Standard | 620 | 1,860 | **3,660** | **7,320** |
| Pro | 3,100 | 9,300 | **18,300** | **36,600** |
| (620 / 3,100 × months) | = | = | 3,720 / 18,600 ✗ | 7,440 / 37,200 ✗ |

`CONFLICT: 6- and 12-month Data-credit totals.` Help center gives 3,660 / 7,320 (Standard) and
18,300 / 36,600 (Pro); `/features/data-enricher` gives annualised **7,440** and **37,200** (= 620×12,
3,100×12), consistent with flat-per-month. Gap = 120 Standard / 600 Pro per year — quote the
**lower** help-center figure when sizing an enrichment project and have the user read the real
balance in `Billing` → `Data Credits`. **Cloud vs local:** `/pricing` indicates cloud allowances
**match** local; no cloud Data-credit uplift is documented → `[UNVERIFIED]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits · https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/data-enricher

### 4.2 Included AI credits — verified 2026-09-01

AI credits **scale with term length** (unlike Data credits). Both sources agree here.

| Tier | 1 mo | 3 mo | 6 mo | 12 mo |
|---|---|---|---|---|
| Standard | **250** | 650 | 975 | **1,500** |
| Pro | **500** | 1,275 | 1,950 | **3,000** |

The `/pricing` headline table shows only the 1-month values (Standard 250, Pro 500).

`CONFLICT: claimed cloud AI-credit uplift.` `/features/email-finder` claims "Cloud versions include
higher AI credits (250→650, 500→1,275 depending on billing cycle)" — but those are **exactly the
3-month local figures**, i.e. a term effect mislabelled as a cloud benefit, and `/pricing` shows
cloud = local. **A cloud AI-credit uplift is `[UNVERIFIED]`** — never sell cloud on credit volume.
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits · https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/email-finder

### 4.3 Data-credit consumption per operation — verified 2026-09-01

Cost per **successful** retrieval: **Email / find profile email = 1 credit per profile** (1 credit
even if several emails come back) · **Phone number = 10 credits per search** · Social & Messaging =
2 · Profile info = 1 · Company data = 2. Marketing framing for the rest: "1–2 Data credits each".

Which actions spend them: "LH Data Enrichment option is available in the **Find Profile Emails**,
**Data Enrichment**, and **Invite 2nd and 3rd level contacts** actions."

`CONFLICT: charging on failure.` `/features/data-enricher` says "**Credits are deducted only for
successful searches**"; the help center says "**Data Enrichment charges per request regardless of
prior data**" and only **Find Profile Emails** charges "only on successful email discovery". Budget
pessimistically: `Data Enrichment` = cost × profiles **attempted**, `Find Profile Emails` = cost ×
successes. Phone lookups at 10 credits are where budgets die — a 620-credit Standard month is
**62 phone lookups** or **620 emails**.

Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits · https://www.linkedhelper.com/features/data-enricher · https://www.linkedhelper.com/features/email-finder

### 4.4 AI-credit consumption per operation

Credits are deducted "for every processed profile" when using the **AI personalized message**
action (**including message regeneration**), the **AI ICP Detection** action, **AI comments** inside
`Like and comment post and articles`, and also message-template generation, Inbox reply generation
and grammar/editing functions.

**Per-operation rate is not published** beyond "one credit for every processed profile"; the
marketing pages publish no rate at all → `[UNVERIFIED]`. Never compute an AI-credit budget as if
the rate were known — give the mechanism (every processed profile *and every regeneration* costs
credits) and have the user watch the balance across a 50-profile test run. Model names are not
disclosed → `[UNVERIFIED]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits · https://www.linkedhelper.com/features/

### 4.5 Top-ups — verified 2026-09-01

`/pricing` says both types "**Can be purchased separately if needed**" but publishes **no top-up
prices**. The help center does:

**Data-credit packages:** 1,000 = **$15** ($0.0150/lead) · 5,000 = **$49** ($0.0098) ·
10,000 = **$89** ($0.0089) · 50,000 = **$284** ($0.0057). Package bulk discount: 10–19 packages =
10% off, scaling to **50% off at 1,000+ packages**.

**AI-credit packages:** Basic 2,000 = **$6** · Standard 4,000 = **$11** · Pro 6,000 = **$15**.

Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits · https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits · https://www.linkedhelper.com/pricing

**Rollover and expiry — `[UNVERIFIED]`.** No rollover or expiry policy is stated on any page
checked — whether unused monthly allowances carry over, and whether purchased packages expire, is
undocumented. Never tell a user credits do or
do not roll over; point them at `Need help` → `Ask for support`. Also `[UNVERIFIED]`: refund policy,
non-USD currencies, credit-package refunds.
Source: https://www.linkedhelper.com/pricing

**External enrichment does not use LH credits.** Snov.io and Apollo.io enrichment run on **their
own credit systems**, billed by them. A user with an Apollo/Snov key can bypass LH Data credits
entirely for email discovery — see `references/integrations.md`.
Source: https://www.linkedhelper.com/features/email-finder

## 5. Local vs cloud storage — how to choose

**This is about where the lead database lives, not where the app runs.** In both variants **actions
execute locally on the machine running LH2**. Safety Kit calls it a "Hybrid Cloud Architecture":
"Local execution for actions; cloud sync for data/CRM", with "Team Sync, Global CRM & Inbox".

| | **Local-based storage** | **Cloud-based storage** |
|---|---|---|
| Lead DB / campaign data | local database file on that PC | synced to LH's cloud |
| Where actions run | that PC | that PC (unchanged) |
| Price (Standard, 12 mo) | $8.25/mo | $16.50/mo |
| Backup | **your job** — manual `Backup` → `Export` (§10.3) | cloud backup included `[LH-CLAIM]` |
| Access from a second machine | requires backup/restore file transfer | Team Sync / Global CRM & Inbox |
| Cross-Account Campaign Cloning | not available | ✓ "Available with Cloud DB" |
| Direct Lead Mobility | not available | ✓ "Available with Cloud DB" |
| 24/7 running | needs the PC or a VPS on 24/7 | **still needs the PC or a VPS on 24/7** |

Decision rules:

- **One operator, one machine, cost-sensitive** → local, with a calendar reminder for manual
  backups; local storage has no safety net if the disk dies.
- **A team or agency, several people touching the same leads** → cloud; cross-account cloning and
  lead mobility are the only genuinely cloud-exclusive features documented.
- **"Run campaigns while my laptop is closed"** → **neither variant solves this**; cloud syncs data,
  not execution. The documented answer is a VPS or dedicated server (§9).
- **Credits are not a reason to pick cloud** — §4.2 CONFLICT.

Source: https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/safety-kit · https://www.linkedhelper.com/features/workspaces · https://support.linkedhelper.com/hc/en-us/articles/360015376519-Is-Linked-Helper-a-cloud-solution-Can-it-process-my-leads-while-PC-is-off

## 6. Platform support and sizing

**It is a desktop application, not a browser extension.** Homepage: "Desktop app, not a Chrome
extension". Safety Kit: "No vulnerable browser extensions", "100% local browser sessions instead of
a Chrome extension", "Your session and cookies stay strictly local on your machine" `[LH-CLAIM]`.
Source: https://www.linkedhelper.com/ · https://www.linkedhelper.com/features/safety-kit

### 6.2 Supported OS and minimum versions — verified 2026-09-01

| OS | Minimum version | Architecture | Notes |
|---|---|---|---|
| **macOS** | **12.0 (Monterey) or higher** | Intel **and** Apple silicon (M1–M4) | download the build matching the chipset; check via `About This Mac` |
| **Windows desktop** | **Windows 10 or higher** | **x86-64 only**, no ARM | older versions discontinued **Q1 2025** |
| **Windows Server** | **Windows Server 2016 or higher** | **x86-64 only** | "Windows Server Core needs .NET Framework 4.6.2 to be installed" |
| **Linux** | **Ubuntu 18.04 (Bionic Beaver) or higher** | **x86-64 only** | **GUI required** — "Gnome GUI is mandatory" |
| **ChromeOS / Chromebook** | **unsupported** | — | — |

Below macOS 12.0 or on an underpowered machine, the documented recommendation is a remote server.
Two narrower lists exist elsewhere: the cloud article names only **Windows Server 2022/2019/2016**
and **Ubuntu 22.04/20.04** as *server* OSes, and **Ubuntu 24.04** has a documented `Disconnect
fired` failure (`references/troubleshooting.md`). Installers: macOS Apple Silicon and Intel
(`linked-helper.dmg`), Windows (`linked-helper.exe`), Ubuntu (`linked-helper.deb`). **Version
number, release date and installer sizes are not published** → `[UNVERIFIED]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015376939-What-Linked-Helper-hardware-and-software-requirements-are · https://support.linkedhelper.com/hc/en-us/articles/360019288740-Can-Linked-Helper-run-on-my-Mac · https://www.linkedhelper.com/downloads · https://support.linkedhelper.com/hc/en-us/articles/360016233680-How-to-run-Linked-Helper-in-a-cloud-remote-server

### 6.3 Minimum system requirements — verified 2026-09-01

| Accounts running simultaneously | Free RAM | CPU real cores | Disk |
|---|---|---|---|
| 1 | **2.5 GB** | 0.5–1 | 4 GB |
| N (formula) | **0.5 GB + 2 GB × N** | **0.5 × N** | 2 GB + 2 GB × N |
| 6 (worked example in the docs) | **12.5 GB** | **3** | **14 GB** |

**Per additional LinkedIn account: +0.5 real core and +2 GB RAM** ("one processor thread if
multi-threading is supported"), plus +2 GB disk.

`CONFLICT: single-account minimum RAM.` The same help-center article gives **2.5 GB free RAM** in
the table but states a single-account minimum of **"4 GB RAM, 1 core, 4 GB disk"** in prose. Quote
**4 GB** as the floor — the higher figure is the safe one to plan against.

**Comfortable** (not minimum) spec: **"at least 8GB of RAM"**, fast **SSD 128 GB+**, **4+ cores**.
VPS sizing is published separately and sits *above* the formula (§9.2), i.e. the docs recommend
headroom. **Windows:** `/downloads` states files **must be stored on disk "C" only** — see the §13
CONFLICT, since the user-data-folder article documents moving data to `D:\`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015376939-What-Linked-Helper-hardware-and-software-requirements-are · https://www.linkedhelper.com/downloads · https://support.linkedhelper.com/hc/en-us/articles/360016233680-How-to-run-Linked-Helper-in-a-cloud-remote-server

## 7. Workspaces and multi-account operation

### 7.1 What a workspace is

A workspace is "a place that allows you easily collaborate with your colleagues" and **holds
licences, LinkedIn accounts, Data credits and users**. On registration "a default workspace is
created". It is the *management* layer; account instances are the *operational* layer.

- **Switch:** upper-left corner of the Account Manager (Launcher) window. **Create:**
  `Add workspace button` in the workspace list. **Manage:** Launcher → `Workspace Management`, users
  under the `Workspace users` tab.
- **Invite a user:** `Workspace Management` → "Invite user button in the upper right corner" →
  email → choose role → `Invite`. **Transfer an asset** (order, licence, Data credits): hover the
  item → `Transfer button`.

Source: https://support.linkedhelper.com/hc/en-us/articles/32476462157202-Linked-Helper-workspaces

### 7.2 Two independent permission axes

| Axis | Level | Can |
|---|---|---|
| **Workspace role** | **Owner** | full control: transfer ownership, rename/delete workspace, manage users, buy licences, transfer orders/licences/Data credits. **Only one per workspace** |
| | **Admin** | transfer orders/licences/Data credits, add/remove users, manage access lists, buy licences, manage proxies, change roles, edit billing |
| | **Member** | add LinkedIn accounts, view accessible accounts; no admin functions |
| | **Guest** | view accessible LinkedIn accounts only; **cannot manage campaigns** |
| **Per-account access** | **Owner** | everything incl. **password access** and transfer |
| | **Manager** | create/edit campaigns, assign proxies/licences, manage access except ownership |
| | **Editor** | create/edit campaigns, assign proxies/licences |
| | **Viewer** | read-only |

Every user has a workspace role *and* an access level per account. Delegating campaign work without
handing over LinkedIn passwords = **Member + Manager/Editor**, never account Owner.
Source: https://support.linkedhelper.com/hc/en-us/articles/32476462157202-Linked-Helper-workspaces

### 7.3 Adding multiple LinkedIn accounts

Path: Launcher → `LinkedIn Accounts` → `Add new` → email + password → `Add`. The **password is
optional** — omit it and the user logs in manually inside the instance, which is the safer default
for delegation. Licence models and the switching path: §2.2.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015219400-How-to-manage-multiple-LinkedIn-accounts

### 7.4 Shared vs isolated

| Shared across the account / workspace | Isolated per instance |
|---|---|
| **Plug-ins** — once enabled, a plug-in "becomes available for **any LinkedIn account instance** added to the Linked Helper account" (account-wide, not per-instance) | LinkedIn session and cookies |
| Licences, Data credits, AI credits (workspace vault) | Campaigns, lists, queues |
| Billing, orders, invoices | Local database file |
| Proxies (defined once, assigned per account) | CRM records, Inbox, messaging history |
| Workspace users and roles | Settings, including `Limits` |
| Integrations (workspace level) | Device fingerprint ("isolated sandboxes" with "separate cookies and randomized device fingerprints") `[LH-CLAIM]` |

Consequences and documented constraints:

- **Installing a plug-in for one account installs it for all of them** — you cannot keep a client's
  instance minimal that way, and "the feature isn't in my interface" is almost never per-instance.
- **`Settings` → `Limits` are per instance** — a ramp on one account does not protect the others.
- **No cross-account exclusion list**; cross-account dedup is a manual export/import exercise
  (`references/campaigns.md` §8).
- **Cross-Account Campaign Cloning** and **Direct Lead Mobility** are cloud-variant only.
- **"Adding users without a license is allowed only for your first workspace"** — additional
  workspaces need at least one purchased licence before users can be added.
- An instance is permanently bound to the first LinkedIn account logged in through it (§2.2).
- Maximum workspaces, seats and accounts per workspace: `[UNVERIFIED]`.

Source: https://support.linkedhelper.com/hc/en-us/articles/10522915555858-Plug-in-store-menu · https://support.linkedhelper.com/hc/en-us/articles/32476462157202-Linked-Helper-workspaces · https://www.linkedhelper.com/features/workspaces · https://www.linkedhelper.com/features/safety-kit

## 8. Proxies at the account level

Setup mechanics only. Every rule about *when a proxy is required for safety*, fraud scores, country
matching, residential vs datacentre and multi-account IP isolation is in
**`references/limits-safety.md` §12 and §16** — do not duplicate or re-derive it here.

**Add a proxy:** Launcher → `Proxies` → `Add new` → choose protocol (**HTTP / HTTPS / SOCKS /
SOCKS5 IPv4**) → IP + port → login/password **if private** → `Test and save`.

**Assign:** `Proxies` → hover the proxy → `Assign to LinkedIn accounts` → select instance(s) →
`Assign`.

Authorization fields are mandatory **only for private proxies**. Proxies are defined at workspace
level and assigned per account: managing them needs workspace **Admin/Owner**, assigning one needs
**Manager/Editor** on that account (§7.2).

A proxy belongs in a licence/account setup when the instance runs on a **VPS or dedicated server
abroad** (server IP will not match the account's country); when the operator runs **someone else's
account** (agency, VA, client work); or when **multiple accounts** run from one machine or server —
the vendor rule is "**One proxy. One account**", "Unique IP per account".

`Never ask for, echo, store or transmit proxy credentials.` Give the UI path and let the user type
the login and password. Validation is the built-in `Test and save` plus the `Proxies` health check —
the docs describe an "IPQualityScore audit that checks fraud scores" `[LH-CLAIM]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015219400-How-to-manage-multiple-LinkedIn-accounts · https://www.linkedhelper.com/features/safety-kit

## 9. Cloud, VPS and 24/7 operation

### 9.1 "Campaigns stop when I turn off my PC" — not a bug

Verbatim: the standalone version **is not a cloud solution** — it "works locally on your PC, as well
as all the data it collects is stored in a local database. **Linked Helper cannot perform any action
when it is stopped or when the PC is turned off."**

Documented fix: install on a **remote server (VPS or dedicated)**. Stated benefits: operation
through PC failure, power or internet loss; access from anywhere; colleague/supervisor remote
access; more simultaneous accounts on stronger hardware. Do **not** offer the Cloud-based storage
plan as the answer — it syncs the database, not execution (§5).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015376519-Is-Linked-Helper-a-cloud-solution-Can-it-process-my-leads-while-PC-is-off

### 9.2 Documented VPS / dedicated-server facts

- **Server OS:** "Windows Server 2022 (2019/2016) and Ubuntu 22.04 (20.04)". "Linked Helper
  functions and features are the same for all supported operating systems."
- **Sizing:** "at least 2GB of RAM and from **0.5 real core per LinkedIn account**". Published
  worked configs: **1 account → 2 vCores / 4 GB RAM**; **3 accounts → 4 vCores / 12 GB RAM**.
- **Scale guidance:** 1–2 accounts → VPS · ~10 → dedicated server · **50–100 → multiple mid-size
  servers** (splitting prevents I/O throttling). "A dedicated server is recommended for running
  multiple LinkedIn accounts simultaneously, especially if there are more than 10."
- **Ubuntu update caveat:** Windows auto-updates silently; **"On Ubuntu, you need to approve the
  update by providing the user password"** — budget a recurring manual update task.
- **Named providers** `[LH-CLAIM]`: **HostZealot** (pre-installed, filterable by account capacity),
  **Ionos** (VPS + dedicated, manual install), **InterServer** ("up to 23 accounts per server").
- Windows Server 2016+ in the official OS list is the closest thing to a VPS/RDP endorsement.
  **No statement permits or prohibits cloud servers, VMs or remote desktop** → official cloud/VPS
  support is `[UNVERIFIED]`.
- Install guides: Windows VPS `.../articles/360015752540` · Windows dedicated
  `.../articles/360019352920` · Ubuntu `.../articles/360017057960` (on support.linkedhelper.com).

Source: https://support.linkedhelper.com/hc/en-us/articles/360016233680-How-to-run-Linked-Helper-in-a-cloud-remote-server · https://support.linkedhelper.com/hc/en-us/articles/22773952344082-Special-offers · https://www.linkedhelper.com/downloads

### 9.3 RDP session behaviour — `[UNVERIFIED]`

**None of the following is documented anywhere in the help center** (the cloud overview article and
the Windows VPS install guide were both checked): whether LH2 keeps running after you **disconnect**
from an RDP session versus **sign out** · any registry/group-policy/command workaround to keep the
GUI session alive · minimum **screen resolution** · server **sleep / lock-screen** requirements ·
server **timezone** steps (only the *principle* of matching proxy ↔ account timezone is documented,
`references/limits-safety.md`).

Do not state RDP persistence as fact. Safe advice: test with a short campaign, disconnect (do not
sign out), check processed counts an hour later. The only related documented fragment is the Ubuntu
firewall rule whitelisting RDP: `sudo ufw allow from any to any port 3389 proto tcp`. Note LH2
requires a GUI (Gnome mandatory on Ubuntu, §6.2) — a headless server is not an option.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015752540-How-to-install-Linked-Helper-on-a-VPS-virtual-private-server-with-Windows-OS

## 10. Data management

### 10.1 User-data folder — default paths

```
Windows          C:\Users\{username}\AppData\Roaming\linked-helper
macOS            /Users/{username}/Library/Application Support/linked-helper/
Linux / Ubuntu   /home/{username}/.config/linked-helper/
```

Windows install-time logs live separately:

```
C:\%userprofile%\AppData\Local\SquirrelTemp\
```

Source: https://support.linkedhelper.com/hc/en-us/articles/360019392720-How-to-change-Linked-Helper-user-data-folder · https://support.linkedhelper.com/hc/en-us/articles/360015656279-Linked-Helper-installation-fails-on-Windows

### 10.2 Moving the user-data folder — the documented fix for a full disk

One environment variable does it: **`LH_APP_USER_DATA_PATH`**.

**Windows** — (1) close all Linked Helper windows; (2) create the new folder, e.g.
`D:\linked-helper`; (3) move the existing AppData data into it; (4) Start →
**"Edit the system environment variables"**; (5) **Advanced** tab → **"Environment Variables…"**;
(6) add a **system** variable `LH_APP_USER_DATA_PATH` = the new path; (7) restart Linked Helper.

**macOS** — (1) close all windows; (2) Finder → **"Go to Folder"** →
`/Users/{username}/Library/Application Support/`; (3) move the `linked-helper` folder to the new
location; (4) create or edit `setENV.plist` in `/Users/{username}/Library/LaunchAgents/`;
(5) add `launchctl setenv LH_APP_USER_DATA_PATH /your/new/path`; (6) reboot.

**Ubuntu** — (1) close all windows; (2) `sudo nano /etc/environment`; (3) add
`LH_APP_USER_DATA_PATH="/your/new/path"`; (4) `Ctrl+O` to save, `Ctrl+X` to exit; (5) move the data
folder and restart Ubuntu.

Take a backup (§10.3) **before** moving anything. Note the §13 CONFLICT with the "disk C only"
statement on `/downloads`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360019392720-How-to-change-Linked-Helper-user-data-folder

### 10.3 Backup and restore

**Create a backup** — (1) open the **Launcher**; (2) `LinkedIn accounts` menu; (3) **hover over**
the account; (4) **stop the instance** if needed; (5) click `Backup`; (6) select `Export` and save
the file.

**Restore** — Launcher → `LinkedIn accounts` → hover the account → stop the instance if needed →
`Backup` → `Import` → select the backup file.

**Warn before every restore, verbatim:** "**When a backup file is imported, current data will be
overwritten.**" / "Restoring a backup file overwrites all current data for a LinkedIn account on a
certain computer."

**Contents:** that account's **local database file**. The app stores "most of the data locally on
your computer" — not in the cloud (local variant). This is also the **supported way to move an
account between machines**: back up on the old PC, restore on the new one.

**No automatic-backup schedule or retention count is documented** → `[UNVERIFIED]`. On local
storage, treat manual backups as a scheduled task: before an app update, before moving the data
folder, before a machine migration, and on a routine cadence.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016353900-How-to-backup-restore-your-Linked-Helper-data

### 10.4 What cannot be deleted — and the hide-instead-of-delete reality

**Deletion is blocked by design, to protect database consistency.** Three objects, three
workarounds. Never tell a user to "just delete it".

**Campaigns — cannot be deleted.** Verbatim: "it is not possible to delete a campaign from the
Linked Helper 2 Instance as it may cause consistency issues in the database."
*Archive instead:* install the `Multi-campaigns runner plug-in` (Plug-in store) → `Campaigns` →
select the campaign → `Archive`. *Unarchive:* `Campaigns` → `Archived` tab → select → `Unarchived` →
switch back to the `Main` filter to confirm. What happens to the campaign's contacts is not stated
→ `[UNVERIFIED]`.

**CRM profiles — cannot be deleted.** Verbatim: "it is not possible to delete profiles out of
CRM…because it might cause data consistency issues."
*Hide instead:* install the `Tagging system plug-in` → tag the unwanted profiles `deleted` → apply a
**"Without Tags"** filter to hide them → optionally use the `deleted` tag to push them into an
`Exclude list` (needs the `Exclude list` plug-in).

**LinkedIn accounts in the Launcher — cannot be deleted.** Verbatim: "it is not possible to delete a
LinkedIn account out of your Linked Helper 2 Launcher permanently due to safety and possible
database consistency issues."
*Archive instead:*
1. Click `Open` on the account, then **log out from LinkedIn**.
2. Click `Stop` to close the window.
3. Select the account → `Edit Linkedin account credentials`.
4. **Delete the password field.** Optionally rename the email with an identifier, since "this
   instance can't be used for another LinkedIn account".
5. Click `Archive`.

Two consequences: (a) the database only ever grows — hence the disk-full fix in §10.2; (b) there is
no "clean slate", so a global exclusion list must be *built* (`SKILL.md` §7,
`references/campaigns.md`).
Source: https://support.linkedhelper.com/hc/en-us/articles/360018168939-How-to-delete-archive-a-campaign · https://support.linkedhelper.com/hc/en-us/articles/360015485399-Can-I-delete-profiles-from-CRM · https://support.linkedhelper.com/hc/en-us/articles/360018187780-How-to-delete-a-LinkedIn-account-from-the-Launcher

## 11. Sending logs to support

> **WARNING — never transmit logs yourself.** LH2 logs and the database archive can contain
> LinkedIn session data, cookies, message bodies, contact records and account identifiers. **Never
> upload, email, attach, paste, pipe or otherwise transmit a user's logs or backup files anywhere.**
> Give the user the procedure below and let them send it through the official channel. If a log or
> backup is handed to you, do not forward it and do not quote session tokens, cookies or credentials
> out of it. The in-app export route **auto-uploads to Linked Helper's servers** — say so before the
> user clicks, so the upload is their informed choice.

**Route A — in-app (auto-uploads):** Launcher → `Backup` → `Logs & data for developers` — exports
logs plus a database archive **with automatic upload to Linked Helper's servers**.

**Route B — support form:** left rail `Need help` → `Ask for support`. Fields: name, email,
application version, message, **up to 5 files**. Also named: Facebook messaging, WhatsApp; "average
reply time is about 15 minutes" `[LH-CLAIM]`.

**Always include:** "Linked Helper account email (can be found in the upper left corner of the
Launcher)" · the **LinkedIn instance ID** from the title bar · application version · screenshots or
related files (backups, CSV files) · a screen recording of the faulty process.

**Capture shortcuts:** Windows screenshot `Ctrl + Prt Screen`, recording `Windows + G` (Win 10);
macOS screenshot `Command + Shift + 3`, recording `Command + Shift + 5`.

Other `Need help` items: `Weekly invitations limit`, `Knowledge base`, `Video tutorials`,
`Ask for support`, `Tip of the day`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017185399-Need-help · https://support.linkedhelper.com/hc/en-us/articles/360016353900-How-to-backup-restore-your-Linked-Helper-data

## 12. Marketed feature names vs help-center names

Users arrive quoting the website; the UI often names the same thing differently or splits it across
a plug-in and an action. Translate before saying a feature does or does not exist.

| Marketed name (linkedhelper.com) | What it is in the app | Notes |
|---|---|---|
| **Smart Invitations** | `Invite 2nd and 3rd level contacts` action + warm-up actions | Standard capped at 20/day on the advanced variants |
| **Message Sender** | `Message to 1st connections` + `Check for replies` actions | "Check-for-Replies… automatically pauses the sequence for anyone who gets back to you" |
| **Outreach Sequences** / **Workflow Builder** | Campaign builder + campaign templates | "30+ automated actions", "unlimited campaigns" |
| **Personalization Suite** | Message template editor + `Custom template variables plug-in` + Hyperise images | "Up to 7 AI messages per campaign" |
| ↳ **Personalized Images** | Hyperise integration | not listed on `/integrations/all-integrations` |
| **AI Messages** / **AI LinkedIn Message Generator** | `AI personalized message` action | spends AI credits, incl. regeneration |
| **AI Comments** | AI comments inside `Like and comment posts and articles` | tone Friendly/Professional/Casual; "1-2 to 5+ sentences" |
| **AI ICP Detection** | `AI ICP Detection` action | unmatched → `Failed` list, qualified → `Successful` and continue |
| **AI Text Editor** / **AI Replies** | Inbox reply generation, grammar/editing functions | separate rows on `/pricing`, all tiers |
| **Auto Commenter & Liker** | `Like and comment posts and articles` action | "150 actions/24h by default"; Standard 20/day |
| **Boost Post** (page: post-booster) | `Boost post` action | default **10 profiles mentioned per comment** |
| **Event Inviter** | `Invite person to event` action | up to **1,000 event invites/week** to 1st-degree |
| **Skill Endorser** / "Endorse My Contacts" | `Endorse 1st connections` action | reciprocation claimed "up to 30%" / "~10–30%" |
| **Follow/Unfollow Profiles** | `Follow profiles` action | no feature-specific follow limit published → `[UNVERIFIED]` |
| **Email Finder** / "Profile Email Finder" | `Find Profile Emails` action | 1 Data credit per profile |
| **Data Enricher** | `Data Enrichment` action | 50+ data points; charges per request |
| **Data Export** | CSV export + webhooks + CRM actions | "200+ data points" across 5 categories |
| **Scrape Messaging History** | `Messaging history` tab / Inbox plug-in | export is Pro-only (§3.2 CONFLICT) |
| **Workspaces** ("Collaborative Workspaces") | Launcher → `Workspace Management` | Cross-Account Campaign Cloning + Direct Lead Mobility = Cloud DB only |
| **Safety Kit** | `Settings` → `Limits`, working hours, pacing, `Proxies` | a marketing bundle name, not a menu |
| **Warm-up Actions** | `Follow profiles`, `Like and comment…`, `Endorse 1st connections` | Safety Kit recommends "10–15 actions per day" |
| **Hybrid Cloud Architecture** | the Cloud-based storage plan variant | data sync only; actions still run locally |

Marketing headline counts, for recognition only: "30+ features in your toolkit" / "30+ Automated
Actions" / "30+ Action Types"; 300,000+ users; 10,000 businesses; 9 years; 180 countries; Capterra
4.9, G2 4.5, Trustpilot 4.8. `[LH-CLAIM]` — social proof, not capability.

Source: https://www.linkedhelper.com/ · https://www.linkedhelper.com/features/safety-kit · https://www.linkedhelper.com/features/personalization-suite · https://www.linkedhelper.com/features/auto-commenter-liker · https://www.linkedhelper.com/features/post-booster · https://www.linkedhelper.com/features/event-inviter · https://www.linkedhelper.com/features/email-finder · https://www.linkedhelper.com/features/data-enricher · https://www.linkedhelper.com/features/data-export · https://www.linkedhelper.com/features/scrape-messaging-history · https://www.linkedhelper.com/features/workspaces

## 13. Known contradictions

Marketing site vs help center. **Show both figures; recommend the conservative one; never silently
pick.** Verified 2026-09-01.

| # | Item | Figure A | Figure B | Handling |
|---|---|---|---|---|
| 1 | **Messaging-history export gating** | `/pricing` marks "Export messaging history" **✓ for Standard** | `/features/data-export`, `/features/scrape-messaging-history`, the licensing article and the Inbox plug-in article all say **Pro-only** | Plan for **Pro-only** (4 sources to 1); have the user verify in their instance |
| 2 | **Trial Data credits** | `/pricing`: **blank / no figure** | `/features/data-enricher`: **~1,400 over 14 days** | 1,400 is `[UNVERIFIED]`; read the real balance in `Billing` → `Data Credits` |
| 3 | **Cloud AI-credit uplift** | `/features/email-finder`: "Cloud versions include higher AI credits (250→650, 500→1,275)" | `/pricing`: cloud allowances **match** local; 650/1,275 are exactly the **3-month local** figures | Cloud uplift is `[UNVERIFIED]`; treat it as a term effect |
| 4 | **6/12-month Data-credit totals** | Help center: Standard **3,660** / **7,320**; Pro **18,300** / **36,600** | `/features/data-enricher` + flat-620 framing: Standard **3,720** / **7,440**; Pro **18,600** / **37,200** | Quote the **lower** help-center figure |
| 5 | **Scope of the Standard 20/day cap** | Help center lists **10** activities incl. `Message to group members`, images, `Send person to external CRM` | `/pricing` lists **9** rows incl. a blanket "Messages/day limit 20/day" and "Auto-tag under Boost post" | Assume the **union** is capped |
| 6 | **Charging on failed enrichment** | `/features/data-enricher`: "Credits are deducted only for successful searches" | Help center: `Data Enrichment` charges **per request regardless of prior data**; only `Find Profile Emails` is success-only | Budget `Data Enrichment` per attempt |
| 7 | **Single-account minimum RAM** | Requirements table: **2.5 GB** free RAM | Same article's prose: **"4 GB RAM, 1 core, 4 GB disk"** | Quote **4 GB** |
| 8 | **Windows storage location** | `/downloads`: files "must be stored on disk **C** only" | User-data-folder article documents moving data to **`D:\linked-helper`** via `LH_APP_USER_DATA_PATH` | The move is documented and supported; mention the "C only" statement and suggest a backup first |
| 9 | **Supported Ubuntu / server OS range** | Requirements: **Ubuntu 18.04 or higher** | Cloud article: only **Ubuntu 22.04 / 20.04** and **Windows Server 2022/2019/2016** | For servers, stay on **22.04 / 20.04**; 24.04 has a documented `Disconnect fired` failure |
| 10 | **Skill Endorser reciprocation** | "up to 30%" | "approximately 10–30%" — same page | Both recorded; it is marketing either way `[LH-CLAIM]` |
| 11 | **Integration lists** | Snov.io and Hyperise named on feature pages | Absent from `/integrations/all-integrations` | Treat as indirect/secondary integrations |

**`[UNVERIFIED]` in this file's scope — do not assert any of these:** per-operation **AI credit**
rates and AI model names · credit **rollover/expiry** and package refunds · **cloud per-term
totals** (arithmetic only, §1.2), non-USD currencies, refund policy · trial credit allowance and
trial throughput caps · team/agency/enterprise tier, maximum workspaces/seats/accounts · app
**version number**, release date, installer sizes · official **cloud/VPS/RDP support statement**,
**RDP disconnect vs sign-out** persistence, minimum RDP resolution, server sleep/lock-screen and
timezone steps · automatic-backup schedule or retention · what happens to contacts when a campaign
is archived · Email Finder / Data Enricher accuracy percentages · LinkedIn's own official
invite/action limits (LH publishes only its own recommendations — `references/limits-safety.md`).
Source: https://www.linkedhelper.com/pricing · https://www.linkedhelper.com/features/data-enricher · https://www.linkedhelper.com/features/email-finder · https://www.linkedhelper.com/features/data-export · https://www.linkedhelper.com/features/scrape-messaging-history · https://support.linkedhelper.com/hc/en-us/articles/360016768020-Licensing-Standard-and-PRO-licenses-Pricing-and-discounts · https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits · https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits · https://support.linkedhelper.com/hc/en-us/articles/360015376939-What-Linked-Helper-hardware-and-software-requirements-are · https://support.linkedhelper.com/hc/en-us/articles/360019392720-How-to-change-Linked-Helper-user-data-folder · https://support.linkedhelper.com/hc/en-us/articles/360016233680-How-to-run-Linked-Helper-in-a-cloud-remote-server · https://www.linkedhelper.com/downloads
