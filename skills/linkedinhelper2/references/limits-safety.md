# Limits, Account Safety and Recovery: Linked Helper 2

Detail layer for SKILL.md §5. Every block carries its `Source:`. Where the vendor's own docs disagree with themselves, both figures are shown as `CONFLICT` with a conservative recommendation. Tags: `[LH-CLAIM]` `[LI-POLICY]` `[COMMUNITY]` `[UNVERIFIED]`.

**Provenance warning.** LH sells LinkedIn automation. Every "safe limit", success-rate percentage and competitor risk rating below is vendor-authored. LH's own blanket disclaimer: *"LinkedIn does not publish exact automation limits publicly. All thresholds below are community-tested ranges, vendor research, or practitioner consensus, not official LinkedIn policies."*

**Recency `[UNVERIFIED]`.** Nearly every LH blog post renders a dynamic "Updated August 2026" stamp rather than a publish date; one post's body still says a feature is "not functional for the majority of accounts as of August 2023" under a 2026 stamp. Treat all recency as unverified. Source: https://www.linkedhelper.com/blog/linkedin-automation-limits

## Contents

1. Risk framing · 2. LinkedIn-side limits · 3. Pending-invite ceiling · 4. LH2's own limit settings · 5. Stacking limits · 6. Working hours and pacing · 7. The rolling 24-hour counter · 8. Warm-up ramps · 9. Restriction triggers · 10. Restriction ladder and recovery · 11. Captcha / checkpoint / 2FA · 12. Proxies and IP · 13. Simultaneous use · 14. Manual behaviour that gets accounts restricted · 15. Extension detection · 16. Multi-account operations · 17. Campaign structure and message randomization · 18. Pre-flight checklist · 19. Antivirus false positives

## 1. Risk framing

**Vendor position** `[LH-CLAIM]`: *"it's legal to use Linked Helper, but it's against LinkedIn rules."* · *"Many things LinkedIn users do are against LinkedIn User Agreement and / or LinkedIn Professional Community Policies,"* including *"creating a false identity, connecting to people you do not know, managing multiple LinkedIn accounts on someone else's behalf, etc."* · *"Linked Helper does not hack LinkedIn, it can do only those things, which you can do manually!"* Not legal advice: vendor claim only. Source: https://support.linkedhelper.com/hc/en-us/articles/360015335040-Is-it-legal-to-use-Linked-Helper

**Vendor detectability claims** `[LH-CLAIM]`:

| Claim | Verbatim |
|---|---|
| Architecture | *"a standalone desktop browser with no extension ID to scan"* (not a Chrome extension) |
| Isolation | *"Each LinkedIn account has its own set of cache and cookies"* in separate instances |
| Fingerprint | *"Each LinkedIn instance generates random fingerprints"* so accounts don't look like one PC |
| IP | per-account proxy so *"each LinkedIn account has its own IP address"* |
| Behaviour | *"in-page navigation"* (searches for profiles instead of opening direct links) + *"randomized timeouts between every step"* |
| Defaults | 150 actions per account per day; randomized campaign start times |
| Vendor's own caveat | LinkedIn also uses *"behavioral analysis"*, and the tool *"cannot forbid you to change the default settings."* |

Source: https://support.linkedhelper.com/hc/en-us/articles/360015454919-Is-it-safe-to-use-Linked-Helper-Is-it-detectable

**The plain fact** `[LI-POLICY]`: LinkedIn's User Agreement prohibits software that scrapes or automates access. Accounts can be restricted or permanently closed. The vendor itself documents four restriction scenarios (§9) and a recovery playbook (§10) because they happen. The user owns that risk; state it once, then help. Source: https://support.linkedhelper.com/hc/en-us/articles/360015335040-Is-it-legal-to-use-Linked-Helper

## 2. LinkedIn-side limits

### 2.1 Invitations

| Limit | Value (exact strings) |
|---|---|
| Weekly invitation cap | *"about 200 per week"*; *"most LinkedIn accounts have a limit of 200 invitations per week"* |
| Safer weekly threshold | *"approximately 100 invites per week"* |
| Recipes-article range | *"approximately 150-200 invitations per week"* |
| Older/outdated figure | ~100 invites per week (article marks this as now outdated) |
| Personalized (with-note) invites, free account | *"about 5 personalized invites per month"* |
| Personalized invites, Premium | restriction removed |
| Re-invite after withdrawal | *"After withdrawing an invitation, you won't be able to resend an invite to the same recipient for up to three weeks."* |
| Limit reset | weekly; *"it is not possible to lift it in any way apart from waiting till another week."* Blog `[LH-CLAIM]`: resets *"exactly seven days"* after the first invite of the cycle: rolling, not calendar |
| Max 1st-degree connections | **30,000** `[LI-POLICY]` |

LinkedIn warning strings you will see: *"You've reached the weekly invitation limit"* · *"You're out of invitations for now"* · *"You've reached the invitation limit"*.

**CONFLICT: personalized invites, free account.** Recipes article: *"about 5 personalized invites per month"*. A different help-center article: **~10 per month**. Use the conservative **5/month**; describe it as "single digits per month on free, unlimited on Premium".

**CONFLICT: no-note invites, free account.** Help center: *"up to ~200/week"*. Blog: *"up to 100 safely"*. Use **100/week**.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015367499-I-m-getting-You-ve-reached-the-weekly-invitation-limit-warning-from-LinkedIn · https://support.linkedhelper.com/hc/en-us/articles/360016640720-I-m-getting-You-ve-reached-the-invitation-limit-warning-from-LinkedIn · https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit · https://support.linkedhelper.com/hc/en-us/articles/360015352260-Invitation-could-not-be-sent · https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits · https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit

### 2.2 Table 1: action limits by action type (blog, in full)

| Action | New / cold | Warmed, daily | Weekly | Ceiling / notes | Tag |
|---|---|---|---|---|---|
| Connection requests | 5–15/day (warm-up) | 20–50/day | ~100/week | 50+/day or 200+/week = "aggressive zone, high risk" | `[COMMUNITY]` |
| Connection requests | | 20–50/day | 100–200/week | flags at "80+/day" | `[LH-CLAIM]` |
| Connection requests | 10–15/day, ramp +5–10 every 10 days | up to 50/rolling 24 h | | | `[LH-CLAIM]` |
| Connection requests | | **>25/day cited as a restriction trigger** | | **CONFLICT: contradicts the 50/day rows** | `[LH-CLAIM]` |
| Connection requests (historical) | | ~500/day → restricted in ~2 weeks | | historical datapoint | `[LH-CLAIM]` |
| **Total actions (all types)** | | **~150/rolling 24 h** (most-repeated figure) | | LH varies totals ±~10%, so actuals run slightly under | `[LH-CLAIM]` |
| Total actions | | *"up to 120 actions"* safe | | **CONFLICT: contradicts 150** | `[LH-CLAIM]` |
| Direct messages (1st degree) | | ~100/day conservative; 20–60/day "safe" | 100–300/week | flags at "100+/day" | `[COMMUNITY]` |
| Message sequence cadence | | 4–6 messages over 5–10 days | | LH recommendation | `[LH-CLAIM]` |
| Profile views / visits | 10/day (wk 1) → 50/day (wk 3) | 50–150/day (conservative ~100) | 300–700/week | scraping guidance "max 100–200/day"; >200 risks restriction | `[COMMUNITY]`+`[LH-CLAIM]` |
| Profile opens **by direct URL** | | **40/rolling 24 h (LH default)**; ~50/day max advised | | direct-URL loading is itself a detection signal | `[LH-CLAIM]` |
| Search result pages loaded | | **100 pages/day (LH default)** | | **CONFLICT**: help center says **200/day**; use 100 | `[LH-CLAIM]` |
| Follows / unfollows | | ~100–150/day | | another post says *"unlimited number of people daily"*: **CONFLICT**; follows do **not** count against the invite cap | `[COMMUNITY]` vs `[LH-CLAIM]` |
| Post likes + comments (combined) | 5 posts (wk 1) | ~150/day | 150–400/week | 20–80/day given as "safe" elsewhere | `[COMMUNITY]` |
| Endorsements | | ~40–60/day | | | `[COMMUNITY]` |
| Group messages | | 10–15/day | | LH marketing elsewhere claims *"hundreds of people a day"*: **CONFLICT** | `[COMMUNITY]` vs `[LH-CLAIM]` |
| Event invitations | | 20–30/day | up to 1,000+/week (bulk invite of 1st-degree to your event) | no per-day cap stated in the event post → `[UNVERIFIED]` hard ceiling | `[COMMUNITY]`+`[LH-CLAIM]` |
| InMails | | 5–20/day | 20–100/week | credit-bound, §2.4 | `[COMMUNITY]` |
| New posts published | | 1–2/day | 3–7/week | | `[LH-CLAIM]` |
| Profile edits | | **1 change/day max** | | multiple same-day edits cited as a restriction trigger | `[LH-CLAIM]` |
| Pending (unaccepted) invites | | | | see §3: four incompatible ceilings | |

**Recommendations for the three conflicts above.** Total actions: **150 is the ceiling, not a target**; 120 is the vendor's own more conservative figure. Connection requests: **≤25/day** for any account without months of clean history; 50/day is for an established account only. Search pages: **100/day**.

Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/linkedin-jail · https://www.linkedhelper.com/blog/how-to-automate-linkedin-outreach · https://www.linkedhelper.com/blog/linkedin-account-restricted · https://www.linkedhelper.com/blog/linkedin-automation-security-study · https://www.linkedhelper.com/blog/automate-linkedin-risk-free · https://www.linkedhelper.com/blog/how-to-scrape-linkedin-data · https://www.linkedhelper.com/blog/safest-linkedin-automation-tools · https://www.linkedhelper.com/blog/linkedin-follow-vs-connect · https://www.linkedhelper.com/blog/use-linkedin-groups-to-generate-leads · https://www.linkedhelper.com/blog/hack-to-use-any-linkedin-event-to-boost-outreach-and-invites · https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use

### 2.3 Invitation capacity by tier (Table 3a)

| Tier | Weekly invites | Tag |
|---|---|---|
| Free / Basic | ~50–100/week | `[COMMUNITY]` |
| Free / Basic | up to 100 safely; *"up to 200"* on basic profiles | `[LH-CLAIM]` |
| Premium Career | ~100/week | `[COMMUNITY]` |
| Premium Business | ~100/week | `[COMMUNITY]` |
| Premium (any) | up to 200/week: *"no advantage over basic"* | `[LH-CLAIM]` |
| Sales Navigator Core | ~100–150/week | `[COMMUNITY]` |
| Sales Navigator (any) | up to **~250/week** | `[LH-CLAIM]` |
| Sales Navigator Advanced | ~150/week | `[COMMUNITY]` |
| Recruiter Lite | ~100–150/week | `[COMMUNITY]` |
| Any (SSI-dependent) | *"around 100–250, depending on your SSI score"* | `[UNVERIFIED]` |
| Any | *"typically 100–200/week"*; some accounts see undocumented **150–200+ per day** | `[UNVERIFIED]` |

**Operator read:** the only figure LH repeats consistently across the whole blog is **100 invites/week**. Everything above 100 is LH's own observation or product pitch. The dedicated SSI post contains **no** claim that SSI affects the invite limit: the SSI→limit link appears only in `multiple-linkedin-accounts` and is `[UNVERIFIED]`.

Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit · https://www.linkedhelper.com/blog/linkedin-automation-security-study · https://www.linkedhelper.com/blog/multiple-linkedin-accounts · https://www.linkedhelper.com/blog/1st-2nd-3rd-linkedin

### 2.4 InMail credits by tier (Table 3b)

| Tier | Credits/month | Max accumulation | Tag |
|---|---|---|---|
| Free | 0 | | `[LI-POLICY]` as stated |
| Premium Career | 5 | 15 | `[LI-POLICY]` as stated |
| Premium Business | 15 | 45 | `[LI-POLICY]` as stated |
| Sales Navigator Core | 50 | 150 | `[LI-POLICY]` as stated |
| Sales Navigator Advanced | "50+" | 150 | `[UNVERIFIED]` |
| Recruiter Lite | 30 (expandable to 120 max) | 120 | `[LI-POLICY]` as stated |
| Recruiter Professional Services | 100 | | `[LI-POLICY]` as stated |
| Recruiter (Corporate) | 150 | | `[LI-POLICY]` as stated |

**Refund rule:** every InMail **accepted, declined, or replied to within 90 days** is fully refunded. InMails to **Open Profile (Open Link) members are free and consume no credit**.

**CONFLICT: InMail credits, help center vs blog.** Help center: Sales Navigator *"20 InMails per month"*, Recruiter Lite *"30 InMails per month"*, Premium Career **3 free InMails**, Premium Essentials **5 InMails**. Blog: 50 (SN Core), 30 (Recruiter Lite), 5 (Premium Career), 15 (Premium Business). Only Recruiter Lite agrees. Plan on the **lower** figure of each pair and have the user read the live credit count in their LinkedIn UI first.

**Open-profile InMail volume** is a separate, larger allowance because it spends no credits: the recipe cites approximately *"800 InMails per month"* for most accounts, and as low as **100** for some.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360031167451-Do-I-need-paid-LinkedIn-subscription-to-use-your-service-What-advantages-can-I-get-with-a-paid-LinkedIn-subscription · https://support.linkedhelper.com/hc/en-us/articles/360016670759-How-to-send-free-InMails-to-Open-profiles · https://www.linkedhelper.com/blog/linkedin-inmail-vs-message · https://www.linkedhelper.com/blog/linkedin-recruiter-inmail · https://www.linkedhelper.com/blog/linkedin-automation-limits

### 2.5 What the subscription tier changes (help center)

Free / Basic: searches *"Limited by LinkedIn's Commercial Use Limit per 30 days"*; personalized invitations *"Recently restricted for many users"*. **Sales Navigator**: *"no LinkedIn Commercial Use Limit"*, *"20 InMails per month"*, advanced filters, filtering by recent posts and company followers. **Recruiter Lite**: *"no LinkedIn Commercial Use Limit"*, *"30 InMails per month"*, advanced talent-acquisition filters. **Premium Career**: still subject to the Commercial Use Limit, **3 free InMails**, *"Minimal practical benefit for lead generation."* **Premium Essentials**: still subject to the Commercial Use Limit, **5 InMails**, same caveat. Verbatim caveat: *"Neither Sales Navigator nor any other paid LinkedIn subscription automates your daily routine activities as Linked Helper does."* Source: https://support.linkedhelper.com/hc/en-us/articles/360031167451-Do-I-need-paid-LinkedIn-subscription-to-use-your-service-What-advantages-can-I-get-with-a-paid-LinkedIn-subscription

### 2.6 Search / result caps by tier (Table 3c)

| Tier | Result cap | Filters |
|---|---|---|
| Free / Basic | **1,000 people, or first 10 pages**; monthly **Commercial Use Limit** on searches: exact number never given → `[UNVERIFIED]` | keyword + Boolean, degree, current/past company, school, industry, profile language, location, service categories, "Talks about", "Open to" |
| Sales Navigator | **2,500 profiles per search** (*"up to 2500 users in one round"*) | + company size/type, seniority, current vs past title, years at company/in role, recent job changes, recent activity, postal-code radius, posted-content keywords, group membership, TeamLink, industry/company **exclusion** filters |
| Sales Navigator (contradicting) | *"roughly 1,000 profiles per search result page"*: **CONFLICT** with 2,500; use **1,000** when sizing a run | |
| Recruiter Lite | 2,500 | 20+ (education, skills, job function) |
| Recruiter Professional | 2,500; **30 out-of-network profile views/month** | 40+ (diversity criteria, skill assessments) |
| Recruiter Corporate | **unlimited out-of-network views**: LinkedIn's only tier with full account visibility | 40+ |

Help-center corroboration for regular LinkedIn: **1,000 profiles max per search request**; company People tab **1,000 records max**.

Sources: https://www.linkedhelper.com/blog/linkedin-advanced-people-search-for-automated-campaigns · https://www.linkedhelper.com/blog/search-linkedin-like-pro · https://www.linkedhelper.com/blog/sales-navigator · https://www.linkedhelper.com/blog/sales-navigator-automation · https://www.linkedhelper.com/blog/1st-2nd-3rd-linkedin · https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

Sales Navigator pricing in the same post is labelled "2025" under a 2026 stamp → `[UNVERIFIED]`; see `references/plans-and-platform.md` rather than quoting prices from here.

### 2.7 Messaging reach by connection degree (Table 3e)

| Degree | Free DM? | Full profile? | Contact info / email? | Reach route without an invite |
|---|---|---|---|---|
| 1st | Yes, unlimited (8,000 chars) | Yes | Yes (email, phone) | |
| 2nd | No | Partial | No | InMail; **shared group message**; **shared event message**; Open Profile |
| 3rd | No | Partial | No | same as 2nd (Premium/InMail or group/event) |
| Out-of-network | No | No | No | Recruiter Professional (30 views/mo) or Recruiter Corporate (unlimited) |

Key rule: *"you can reach out to contacts on the 2nd and 3rd levels through messages sent via LinkedIn groups and events without using InMail credits."* This is the main invite-free reach route: no invitation budget, no credits. Source: https://www.linkedhelper.com/blog/1st-2nd-3rd-linkedin

### 2.8 Company Page follow-invite credits (separate pool, Table 3f)

| Item | Figure |
|---|---|
| Old model | 100 invitations/week |
| Current model | **monthly credit pool**: historically 250/month, being cut to **as low as 50/month** in a staggered 2026 rollout (undated-2026 stamp → `[UNVERIFIED]` recency) |
| Reset | 1st of each month |
| Cost | 1 credit per invite; refunded (usually within **~72 hours**) when accepted; declined/ignored invites do **not** refund until monthly reset |
| Who may send | **Page admins only**, and only to their own **1st-degree connections** |
| Premium Page exception | may invite people who **reacted/commented/shared in the last 30 days** or who follow similar Pages: these engager invites **spend no credits** |

Source: https://www.linkedhelper.com/blog/how-to-invite-people-to-follow-your-linkedin-page-automatically

### 2.9 The two character limits that bear on safety

Connection-request note **300** chars (free accounts **5 notes/month**, Premium unlimited; LH advises under 300, ideally **120–240**): **CONFLICT** with the help center's "200-300" and "~10 personalized invites/month", §2.1. Direct message to 1st degree **8,000**, free and unlimited. All blog character limits are presented as LinkedIn's field limits but carry **no LinkedIn citation** → `[UNVERIFIED]` at source level. Group post, event-invitation message, page-follow invite, name-field and hashtag lengths are **not covered anywhere** → `[UNVERIFIED]`/absent; do not invent them. Full 28-field table in `references/templates.md`. Sources: https://www.linkedhelper.com/blog/linkedin-character-limit · https://www.linkedhelper.com/blog/linkedin-prospecting-messages

## 3. Pending-invite ceiling

The most contradicted number in the documentation set. **CONFLICT: four incompatible blog ceilings, plus four more from the help center.**

### 3.1 Table 1b: the four blog figures

| Stated ceiling | Withdrawal cadence advised | Source |
|---|---|---|
| 200–700 recommended; **~1,500 hard limit**; withdraw >3 weeks old | every 3 weeks | https://www.linkedhelper.com/blog/linkedin-automation-limits |
| Problematic at **"2K–2.5K+"** | every 2–3 weeks | https://www.linkedhelper.com/blog/automate-linkedin-risk-free |
| Keep under **~1,000** | every 2–3 weeks / 7–14 days | https://www.linkedhelper.com/blog/how-to-automate-linkedin-outreach · https://www.linkedhelper.com/blog/linkedin-scraper |
| **~1,500 soft threshold**; aged high-trust accounts stretch to 2,000–2,500 | 7–14 days; always withdraw >30 days | https://www.linkedhelper.com/blog/linkedin-pending-connections |

### 3.2 The help center's four figures (also mutually incompatible)

| Article | Ceiling |
|---|---|
| Limits article | *"no more than 200 - 500 sent pending invitations"* |
| Sent-invites-canceller article | *"only 200 - 500 pending invites"* |
| 400-error article | keep *"only 500-1000 active"* |
| "Invitation could not be sent" | if over **1,500** pending, withdraw down to **500-1,000** |

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use · https://support.linkedhelper.com/hc/en-us/articles/360015365379-How-to-cancel-sent-pending-invites · https://support.linkedhelper.com/hc/en-us/articles/360015352260-Invitation-could-not-be-sent

**Recommendation.** Treat none of the eight as authoritative. Conservative common denominator: keep pending at **200–500, never above ~500**, and replace guessing with hygiene.

### 3.3 The hygiene rule

- Target **200–500 pending**; withdraw stale invites **every 2–4 weeks** as a standing habit, not emergency cleanup.
- Semi-automatic: `Sent invites canceller plug-in` → `Functions` → `Sent invites canceller` → *"Choose the date. Linked Helper will cancel all invites sent before that date."* → `Start withdrawing`.
- Fully automatic: install *"Automatic sent invites canceller for Filter contacts out of my network (keep 1st level only)"* → open the inviting campaign → click `Filter contacts out of my network (keep 1st level only)` → enable *"Automatic sent invites canceller"*, set the age threshold (**default 30 days**).
- Manual check/withdraw: https://www.linkedin.com/mynetwork/invitation-manager/sent/
- Why: high pending/rejection ratios are a documented cause of **429** and of the email-verification-on-every-invite restriction (§9.1).

Also documented: **LinkedIn does NOT auto-expire sent invitations**: they count against you indefinitely until withdrawn `[LH-CLAIM]`. After withdrawing you **cannot re-invite for 3 weeks** `[LI-POLICY]` as stated, but the pending-connections post does *not* mention this rule → `[UNVERIFIED]`/contradicted by omission. Once pending ≥ ~20% of total sent, throughput degrades; keep acceptance rate **>25%** `[LH-CLAIM]`.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015365379-How-to-cancel-sent-pending-invites · https://support.linkedhelper.com/hc/en-us/articles/360016855839-Incorrect-connect-response-429 · https://www.linkedhelper.com/blog/linkedin-pending-connections · https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit

## 4. LH2's own limit settings

### 4.1 The overall cap

**`Settings` → `Limits`** → `Max actions per 24 hours`. Default / recommended: *"150 profiles per every 24 hours"*. Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

### 4.2 Advanced limits: full per-activity list with defaults

| Advanced limit (verbatim) | Default / recommendation | Note |
|---|---|---|
| `Employees Extractor` | not documented → `[UNVERIFIED]` | counts organizations loaded via the action |
| `Endorse my contacts` | **60 / 24 h** | per profile = 1 action regardless of skill count |
| `Follow / Unfollow profiles` | **150 / 24 h** | grouped with messaging/extracting |
| `Get Email from LH Email Finder` | not documented → `[UNVERIFIED]` | one profile = one action |
| `Inmail to 2nd/3rd contacts` | not documented → `[UNVERIFIED]` | credit-bound in practice, §2.4 |
| `Invite 2nd/3rd level contacts` | **50 / 24 h** (established account) | the number to lower first |
| `Load profile page` | not documented → `[UNVERIFIED]` | **MASTER limit**: *"priority over all other"* profile limits |
| `Load LinkedIn profile via URL` | **40 / 24 h** | prevents logouts; direct-URL loading is itself a signal |
| `Message to 1st connections` | **150 / 24 h** | overall messaging cap; image messages counted here |
| `Load LinkedIn search results` | **200 pages/day** (help center) vs **100 pages/day** (blog): **CONFLICT**, use 100 | collection from searches / company pages |
| `Post liking` | **100 / 24 h** (Boost Post: *"100 mentioned profiles per 24 hours"*) | counts liked posts, not profiles processed |
| `Remove from 1st connections` | not documented → `[UNVERIFIED]` | |

Recommended caps, verbatim from *"What kind of limits should I use?"*: invitations (2nd & 3rd level) *"50 per 24 hours"* · endorsements *"60 per 24 hours"* · messaging / following / extracting *"150 per 24 hours"* · Boost Post *"100 mentioned profiles per 24 hours"* · `Load LinkedIn profile via URL` *"40 per 24 hours"* · search collection *"200 search pages per day or approximately 2000 / 5000 profiles"* · overall *"150 actions per 24 hours by default"*. The same article says keep *"no more than 200 - 500 sent pending invitations"* and avoid direct profile-URL navigation because it causes LinkedIn logouts.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use · https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

### 4.3 Standard-licence activities capped at 20 / 24 h

`Invite to event` · `Invite to group` · `Invite to follow organization` · `Message to event attendees` · `Message to group members` · `Message with attached image` · `Post liking` · `Mention person in comment`. Pro lifts the cap. Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

### 4.4 `Smart Daily Limit Adjustment`

Randomizes daily action counts within a **10% gap by default**, so the account never repeats the same number. **The adjustment is downward only**: both documented examples describe sending *90–100% of* the configured limit, never above it, so it is not a reason to set the limit lower than you want. Worked example: *"with 50 invites per 24 hours, Linked Helper will be sending from 90% till 100%"*; the Limits article states the same setting as *"with 10% variation for inviting limit, daily number of invitations set will vary from 45 to 50."* → **45–50/day on a 50 setting**. To widen the range, raise **both** the limit and the percentage. Pair with a raised `Start time randomization` (Working Hours) to add a random pre-start delay, *"making campaigns appear more human-like"*. Sources: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper · https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

### 4.5 CONFLICT: limit precedence

Two verbatim, mutually exclusive rules:

> *"Advanced limits have priority over the daily limits"*: if the daily limit is 150 but
> `Load profile page` is 1 per 24 h, only 1 profile loads per day.

> *"Maximum Daily Actions limit always overrides any lower-level limits"*: a per-action limit above
> the daily cap is meaningless.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits · https://support.linkedhelper.com/hc/en-us/articles/360016640720-I-m-getting-You-ve-reached-the-invitation-limit-warning-from-LinkedIn

The docs cannot be reconciled. The behaviour that satisfies both readings: advanced limits only ever **lower** throughput; an advanced limit **above** `Max actions per 24 hours` has no effect. So set `Max actions per 24 hours` **at or above the sum of the per-activity limits you actually want**, set each advanced limit to its real target, then verify with one bunch and read the "Last 24 hrs actions" counter before scaling.

## 5. Stacking limits

Two limits on the same activity compose: a daily ceiling plus an hourly spread. Documented pattern:

```
Limit 1: 50 actions per 24 hours   (daily ceiling)
Limit 2: 3 actions per 1 hour      (hourly spread)
Result: 3 messages each hour, but never more than 50 per last 24 hours
```

The hourly limit is what stops the rolling counter (§7) being drained in one sitting; working hours alone do not. Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

**Worked configuration, 50 invites/day:** (1) install `Action steps delays plug-in`; (2) open the campaign workflow → `Invite 2nd and 3rd level contacts` → `Delay settings` tab; (3) `Bunch size` = **25**, `Timeout between bunches` = **12 hours** → *"Invite 25 profiles followed by a 12-hour timeout"*; (4) verify `Settings` → `Limits` → `Max actions per 24 hours` **≥ 50**. Source: https://support.linkedhelper.com/hc/en-us/articles/360015357459-How-to-limit-inviting-by-50-profiles-per-day

## 6. Working hours and pacing

**`Settings` → `Working Hours`:** per-weekday toggles `24 hours` or `Do not work` · time periods via `+`, then `Format and save` · **military (24-hour) time format** · `Start time randomization` adds a delay *"from the range you specified"* · the timezone display setting affects **representation only, not execution** · documented example *"Linked Helpers 2 will work only on Mondays and Thursdays."* · per-action override via the `Action working hours plug-in` (https://support.linkedhelper.com/hc/en-us/articles/11519759961234-Action-working-hours-plug-in): for agency work, agree hours with the client and *"Enable 'Action working hours' for customization."* Sources: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits · https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper

**Delay settings** (action → `Delay settings` tab, requires `Action steps delays plug-in`):

| Control | Default |
|---|---|
| `Bunch size`: profiles processed before a pause | **10** |
| `Timeout between bunches`: pause duration | **1 minute** |
| Text input method | *"Random is chosen by default"* |
| Timeout profile | *"not faster than FAST timeouts"*; **SAFE** for new or dormant accounts |

Verbatim: *"Default FAST timeouts are proven safe, but new or inactive accounts may benefit from SAFE timeouts."* Also available: `Delay between actions` (insertable workflow action) and `Postpone action start plug-in`. Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

**Why bursts are the most detectable pattern.** **30–120 s randomised delay between actions**; never fixed intervals: *"identical time intervals between actions"* is named as a detection signal `[COMMUNITY]`/`[LH-CLAIM]`. LinkedIn-side quote: *"The LinkedIn Algorithm identifies automation through patterns like identical timing intervals, repetitive messaging structures, and unnatural interaction speed."* Randomise campaign start times and configure business hours per action type. Blog working-hours window **9:00–18:00 local, weekends off** `[COMMUNITY]`, but `automate-linkedin-risk-free` gives **no** window at all, so the 9–18 figure comes from one post only and is not a documented default. Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/automate-linkedin-risk-free · https://www.linkedhelper.com/blog/linkedin-jail · https://www.linkedhelper.com/blog/linkedin-message-automation

## 7. The rolling 24-hour counter

It is **not** a midnight reset.

- *"Linked Helper counts actions that were made every last 24 hours period, not the last day or fixed period of 24 hours"*.
- *"Each action taken is added back exactly after 24 hours from the time it was performed."* Documented example: 150 invites starting at 10:00 → one slot frees at 10:00 the next day, another at 10:08, and so on.
- With campaigns running, *"as soon as one action slot is freed, Linked Helper starts to process profiles till there are no free action slots"*: the app refills continuously unless you add Working hours, Advanced limits or bunch delays.
- Default applied across all campaigns: **150 actions per day**.

Source: https://support.linkedhelper.com/hc/en-us/articles/360017039459-When-the-Last-24-hrs-actions-number-is-reset

**Operational consequences.** (1) A burst of 150 actions in one hour produces another burst at exactly the same hour 24 h later: a perfectly periodic signature. (2) After a burst the account is idle ~24 h, which is the dormant-then-spike pattern named as a trigger (§9.5). (3) Slots trickle back one at a time in spend order, so throughput smooths **only if** you never front-load. (4) The fix is mechanical: an hourly advanced limit (§5) and/or `Bunch size` + `Timeout between bunches` (§6).

## 8. Warm-up ramps

Two ramps are documented. They agree on shape; run the **slower** of the two when unsure.

### 8.1 Help-centre ramp: new or long-dormant account

| Stage | Activity |
|---|---|
| Weeks 1–2 | light activity only: scrolling the feed, following profiles, and **5 invitations from LinkedIn's "recommendations"** section. No automation volume |
| After 14 days | increase daily actions *"by 5 - 10 every 10 days or so"* |
| Invite ramp | **10–15 invites / 24 h** → **35 within one month** → **50 in the following month** |
| Steady state | settle at the standard limits in §4.2 |

Corroborating guidance for brand-new accounts with a thin network: build the network through LinkedIn's recommendation sections by inviting *"10-15 people daily"* before running any large-scale collection or invite campaign. Additional lever: switch the action's timeouts from **FAST** to **SAFE** via the `Action steps delays plug-in`. Sources: https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use · https://support.linkedhelper.com/hc/en-us/articles/360015619980-Linked-Helper-skips-profiles-while-collecting-No-profile-was-collected · https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper

### 8.2 Blog 4-week ramp `[COMMUNITY]`

| Week | Tool state | Connection requests/day | Profile views/day | Engagement / messages |
|---|---|---|---|---|
| 1 | **MANUAL ONLY, no tool running** | 5 | 10 | engage with 5 posts |
| 2 | introduce the tool | 10 | 20 | 5 automated messages/day |
| 3 | mid volume | 15–20 | 50 | 15 messages/day |
| 4+ | target operating limits | stay inside the safe thresholds | | withdraw pending invites older than 3 weeks |

Second, coarser blog ramp `[LH-CLAIM]`: new or dormant accounts start at **10–15 invites/day** and increase by **5–10 every 10 days**. Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/how-to-automate-linkedin-outreach

### 8.3 Merged day-by-day plan (use when the user wants one schedule)

| Days | Invites/day | Profile views/day | Other | Tool running? |
|---|---|---|---|---|
| 1–7 | 5, manual, from LinkedIn recommendations | 10 | engage with 5 posts, follow profiles, scroll feed | No |
| 8–14 | 5–10 | 20 | 5 automated messages/day | Yes, minimal |
| 15–21 | 10–15 | 50 | 15 messages/day | Yes |
| 22–30 | 15–25 | 50–100 | full workflow with warm-up steps | Yes |
| 31–60 | ramp to 35 (+5–10 every 10 days) | 100 | withdraw pending >3 weeks | Yes |
| 61+ | up to 50 | 100–150 | steady state at §4.2 limits | Yes |

**Dormant account:** treat exactly as a new account and restart from day 1: the **dormant-then-spike** pattern is itself a named trigger (§9.5).

**Quality gates before scaling** `[LH-CLAIM]`: acceptance rate **>25%** (below ~20% triggers faster throttling); **SSI 70+** before scaling automation: note the SSI→limit mechanism is `[UNVERIFIED]` (§9.7), so treat this as a vendor heuristic. Source: https://www.linkedhelper.com/blog/linkedin-automation-limits

## 9. Restriction triggers

### 9.1–9.4 The four documented scenarios

| # | Scenario | Meaning | What the user sees | Documented resolution |
|---|---|---|---|---|
| 1 | **Email verification demanded on EVERY invitation** | the account got many *"don't know"* dismissals (recipients clicking "I don't know this person"); LinkedIn now requires an email for invites to non-direct connections | every invite asks for the recipient's email; LH2 invite actions fail or stall on that prompt | withdraw pending invites then ask support to remove it · create a new account and merge connections · run multiple accounts for different segments · **wait 5-7 days** for automatic removal |
| 2 | **Invitation limits hit** | visiting many profiles rapidly or sending too many connection requests | *"You're out of invitations for now"* / *"You've reached the invitation limit"*; invites stop sending | weekly reset only; *"it is not possible to lift it in any way apart from waiting till another week"* |
| 3 | **"Your account has been restricted" on login** | identity verification required; LinkedIn enforces this against fake/duplicate accounts and **shared access**, automation tool or not | login inside the embedded browser lands on a restriction interstitial; no action can proceed | passes once identity is verified |
| 4 | **Suspension with an action-verification prompt** | most common cause: the account was accessed from **multiple locations/devices simultaneously**: LinkedIn's terms forbid account sharing | a prompt to *"verify you've performed certain actions"*, often after a proxy change, VPS move or a colleague logging in | complete the verification; fix the access pattern (§13) |

Prevention list from the same article: **warm up prospects before inviting** (visit profiles, follow, engage with their content) · personalize with the recipient's name and why you're reaching out · test sending times: **evenings are noted as more effective** · keep a complete, professional profile including a relevant background image. Source: https://support.linkedhelper.com/hc/en-us/articles/360017222880-My-LinkedIn-account-got-restricted-though-I-followed-your-recommendations

### 9.5 The blog's consolidated trigger list

**Behavioural:**

| Trigger | What it looks like from the user's side |
|---|---|
| Large batch of invitations in a short period | limit warning appears early in the week |
| Sudden activity jump from a previously quiet account (**dormant-then-spike**) | restriction lands within days of resuming |
| Low acceptance rate / *"I don't know this person"* clicks: named repeatedly as the **#1 human-side trigger** | email demanded on every invite (§9.1) |
| Identical messages at volume; identical timing intervals; unnatural interaction speed | throttling, delayed message delivery |
| Opening too many profiles directly by URL | logout mid-session (§14) |
| **>25 connection requests/day** cited as a trigger: **CONFLICT** with the 50/day "safe" figure on the same blog | |
| Multiple profile edits in one day | |

**Technical / infrastructure:** Chrome-extension presence (§15) · session cookie used from two IPs simultaneously: *"a guaranteed tell"* · new-device logins, VPN/proxy switches, IP changes, geolocation impossibilities (logins from distant places hours apart) · datacenter or shared IPs (fraud-scored by IPQualityScore) · profile violations: fake names, promotional posts with direct purchase links.

**Early warning signs, act before the block lands:** frequent CAPTCHAs · *"weekly invitation limit reached"* appearing unusually early · delayed message delivery · sudden drop in profile-view visibility.

Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/linkedin-jail · https://www.linkedhelper.com/blog/linkedin-account-restricted

### 9.6 Historical volume datapoints `[LH-CLAIM]`

~**500 invites/day** → restriction within ~**2 weeks**. Visiting **300–500 connections daily** to scrape emails can trigger verification demands or restrictions **within 2-3 weeks**. Sources: https://www.linkedhelper.com/blog/linkedin-automation-security-study · https://support.linkedhelper.com/hc/en-us/articles/360015553480-How-to-stay-safe-when-working-with-LinkedIn-manually

Sources: https://www.linkedhelper.com/blog/linkedin-automation-security-study · https://support.linkedhelper.com/hc/en-us/articles/360015553480-How-to-stay-safe-when-working-with-LinkedIn-manually

### 9.7 SSI and profile-view privacy: `[UNVERIFIED]`

No article in the FAQ, Recipes and tips or Issues & solutions categories (nor the `Visit & Extract profiles` reference page) addresses: SSI score or any effect of automation on it · whether profiles visited by Linked Helper appear in the target's *"Who viewed your profile"* · private/anonymous browsing mode and its interaction with `Visit & Extract profiles`. Do not assert any behaviour. The only adjacent documented fact: profile visiting is a first-class rate-limited activity (`Load profile page` is the **master limit**, *"priority over all other"* profile limits), implying visits are real logged-in page loads. Sources (limits statement only): https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits · (Visit & Extract, silent on the topic): https://support.linkedhelper.com/hc/en-us/articles/360016708400-Visit-Extract-profiles

## 10. Restriction ladder and recovery

**Ladder:** `CAPTCHA checks → temporary action throttling → temporary account restriction (2–14 days) → permanent restriction (rare)`. Source: https://www.linkedhelper.com/blog/linkedin-automation-limits

Two restriction **types** `[LH-CLAIM]`:

| Type | Duration | Requirement |
|---|---|---|
| **Identity-verification restriction** | no fixed duration; process takes **7–14 days** with access restricted meanwhile; expect **up to five rounds** of verification. New accounts often hit this **within 1–2 weeks** of creation | government photo ID matching the profile name exactly |
| **Automation-suspicion restriction** | temporary, *"a few hours or days"*, often self-resolving; typically clears **within seven days** | usually none beyond waiting |

Sources: https://www.linkedhelper.com/blog/linkedin-account-restricted · https://www.linkedhelper.com/blog/multiple-linkedin-accounts

**Recovery sequence (help center):**

1. **Stop the campaign runner.** Do not keep retrying into a restriction.
2. **Slow the machine down:** install `Action steps delays plug-in`; *"Increase or reset Delay settings to SAFE timeouts"*, then *"wait a few hours before you try again"*; **reduce daily limits** temporarily below the default 150 actions/day, then *"wait a couple of days"*.
3. **Clean up pending invites:** *"Withdraw all pending invites except recent 500, then retry"*: https://www.linkedin.com/mynetwork/invitation-manager/sent/
4. **Wait it out.** Typically lifts in **5-7 days**; LinkedIn itself says you may need to wait **up to one week** before sending invitations again.
5. **Only then contact LinkedIn support**, and *"without mentioning automation software"*.
6. **Restructure the campaign** before resuming: warm-up actions (Follow, Like/Comment) ahead of the invite step, and personalization with `{firstName}`, `{company}`, `{position}`.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360016855839-Incorrect-connect-response-429 · https://support.linkedhelper.com/hc/en-us/articles/360016640720-I-m-getting-You-ve-reached-the-invitation-limit-warning-from-LinkedIn · https://support.linkedhelper.com/hc/en-us/articles/360015367499-I-m-getting-You-ve-reached-the-weekly-invitation-limit-warning-from-LinkedIn

**Recovery sequence (blog, identity restriction):** stop **all** automation and outreach immediately → complete SMS phone verification → submit government ID (passport / driver's licence), clear photo, name matching the profile exactly → if stalled, open a Help Center ticket with screenshots and a written explanation → resume with **light manual engagement only for 1–2 weeks**; expect full recovery in **2–4 weeks** if behaviour stays clean. Sources: https://www.linkedhelper.com/blog/linkedin-account-restricted · https://www.linkedhelper.com/blog/linkedin-jail

**Expected timelines:**

| Situation | Timeline |
|---|---|
| Email-verification-on-every-invite restriction | automatic removal in **5-7 days** |
| Weekly invitation limit | resets weekly; no way to lift early |
| Restriction generally | lifts in **5-7 days**; LinkedIn says wait **up to one week** before inviting again |
| Automation-suspicion restriction | hours to days; typically clears **within 7 days** |
| Identity-verification restriction | **7–14 days**, up to 5 verification rounds |
| Full behavioural recovery afterwards | **2–4 weeks** of clean behaviour |
| Re-invite the same person after withdrawal | blocked **up to 3 weeks** |
| Temporary account restriction (ladder) | **2–14 days** |

**LinkedIn support, exact endpoints:** https://www.linkedin.com/help/linkedin/ask/TS-F-APPEAL (*"works even if not signed in"*) · https://www.linkedin.com/help/linkedin/ask/uuset · https://www.linkedin.com/help/linkedin/ask/uumt · https://www.linkedin.com/help/linkedin/ask/li-default · https://www.linkedin.com/help/linkedin/solve/contact

Emails: support@linkedin.com, support@cs.linkedin.com, linkedin_support@cs.linkedin.com, customerservice@linkedin.com, customer_service@linkedin.com, cs@linkedin.com, helpdesk@linkedin.com, mobile_support@linkedin.com. Social: Twitter/X **@LinkedInHelp**; LinkedIn's official Facebook page.

Verbatim: *"do not mention that you use automation software or violate their Terms and/or User Agreement."* Specifically avoid disclosing: use of automation software or extensions, connecting with people you don't know, any account-sharing practice. Source: https://support.linkedhelper.com/hc/en-us/articles/360016896859-How-to-contact-LinkedIn-support-directly

**What NOT to do:** do not create a second account during a restriction (risks permanent ban on both) · do not continue outreach · do not edit your profile or work history while restricted · do not keep retrying into a 429 / limit warning · do not mention automation to support. Sources: https://www.linkedhelper.com/blog/linkedin-account-restricted · https://support.linkedhelper.com/hc/en-us/articles/360016855839-Incorrect-connect-response-429

**Documentation gap `[UNVERIFIED]`.** The `escape-linkedin-jail` post promises appeal templates and per-stage timelines but contains **none**: no definition of "LinkedIn jail", no per-level timelines, no appeal wording, no re-ramp numbers. Do not invent an appeal template or timelines beyond the table above. Source: https://www.linkedhelper.com/blog/escape-linkedin-jail

## 11. Captcha / checkpoint / 2FA

**Status: mostly `[UNVERIFIED]`. Do not invent handling behaviour.**

The *"Errors when adding LinkedIn account"* article documents only two warnings, both about instance↔account binding:

| Warning | Meaning | Fix |
|---|---|---|
| **`Wrong Account`** | *"you are trying to access the LinkedIn account through the wrong instance (that was used to log in to another LinkedIn account before)"* | use the instance previously assigned to that account, or create a new instance; reassign licences between instances as needed |
| **`Email Already Exists`** | *"you already have the Linked Helper instance with the email address that matches the one you are trying to add"* | use the existing instance; unarchive it if not visible |

Source: https://support.linkedhelper.com/hc/en-us/articles/4408390475154-Errors-when-adding-LinkedIn-account

What *is* documented and bears on checkpoints: login happens inside the instance's embedded browser; if the session drops the fix is *"Allow Linked Helper to auto-login using saved credentials"* or **manual login via the `LinkedIn` menu in the left panel**. Any LinkedIn-side challenge is therefore solved **by hand in that embedded browser**. The login restriction and the *"verify you've performed certain actions"* prompt are in §9: both require manual verification inside LinkedIn. Sources: https://support.linkedhelper.com/hc/en-us/articles/360015510239-Error-Failed-to-prepare-collecting-occurs · https://support.linkedhelper.com/hc/en-us/articles/360017222880-My-LinkedIn-account-got-restricted-though-I-followed-your-recommendations

**`[UNVERIFIED]`, do not assert:** a 2FA/OTP entry field or flow in LH2 · a captcha-solving flow, automatic or assisted · any documented reaction to LinkedIn's *"unusual activity"* interstitial · wrong-password or proxy-failure error handling · whether campaigns auto-pause on a checkpoint. Frequent CAPTCHAs are documented only as an **early warning sign** of an approaching restriction (§9.5), not as something the tool handles. Source: https://www.linkedhelper.com/blog/linkedin-automation-limits

## 12. Proxies and IP

**Never ask for, echo, store or transmit proxy credentials.** Describe the UI steps; the user enters them.

**When a proxy is needed.** **Not needed** if you manage only your own account locally. **Recommended** for: your own account on a **VPS/server in another country** · **multiple accounts from different countries on one computer** · **colleague accounts on remote servers**. Purpose: mask the IP so (a) you can manage someone else's account from their geography, and (b) each of several accounts gets a unique IP.

**Supported types.** *"HTTP / HTTPS / SOCKS / SOCKS5 proxy, IPv4 only."* **IPv6 not supported** unless tunnelled to IPv4. Prefer **ISP, mobile or residential** over **datacenter**. **Dedicated IPs preferable to dynamic.**

**Fraud-score gate.** Assess with **IPQualityScore** or the built-in `Proxies` menu (Launcher). **Avoid fraud scores above 75**, or flags for **recent abuse, bot, proxy, VPN or crawler**. **CONFLICT**, help center: avoid **>75**; blog: **<30** = excellent. Use **<30** as the target and **75** as the absolute reject line. **Verify the real egress IP** in a browser: the IP a provider shows you may be a **gateway**. Latency **<100 ms** optimal `[LH-CLAIM]`.

**Built-in `Proxies` validation.** Location: *"Proxies menu of the Launcher"*. Uses *"ipqualityscore.com service…to define the Fraud score of your proxy IP address"* and flags proxies *"used by bots, crawlers, or VPN/proxy services"*. Reports country of origin, fraud score, historical bot/crawler usage. Status **Good** (no action) / **Bad** (*"replacement recommended to reduce the risk of issues when using LinkedIn"*). Supports *"IPv4 HTTPS or SOCKS proxies"* from any provider. Purely informational: *"nothing has changed: your accounts will continue working as expected."*

**Country and time zone.** *"Ensure your account settings show the same country as your proxy location."* **Match the proxy time zone with the LinkedIn account settings**: check at IPQualityScore, or pick the closest option when adding/editing account credentials. Restriction driver, verbatim: *"most of the restrictions/warnings happen because of using the same LinkedIn account from different locations."* Use a **static, not rotating** IP, the same one for manual and automated activity. **One IP per account, never shared**: *"Never share the same proxy across multiple accounts"*; shared IPs let LinkedIn cluster and ban the group.

**VPN vs proxy.** A VPN technically works *"provided your VPN doesn't block LinkedIn or Linked Helper servers"*, **but a VPN changes the entire PC's IP**. For **multiple accounts** use a **proxy, not a VPN**, so *"every account is being accessed from a unique IP address"*. Repeated `[LI-POLICY]` warning: *"LinkedIn does not endorse when you manage someone else's LinkedIn account"*.

**Blog success rates `[LH-CLAIM]`**, from LH's self-described *"$2,000 Proxy Testing Experiment"*:

| Proxy type | Success rate | Verdict |
|---|---|---|
| Mobile | **90%** | premium choice, closest to real user |
| ISP | **85%** | best speed/legitimacy trade-off |
| Residential | **75%** | fine at scale, needs **sticky** sessions |
| Datacenter | **10%** | avoid: trivially detected |

Country success rates: Canada **85%** · Germany **82%** · Netherlands **80%** · UK **78%**. **Avoid entirely** (all <40%): India, Brazil, Russia, China, Vietnam. Economics: premium IPs at **$4–5** with 85–90% success = true cost ~**$4.70 per working IP**; budget IPs at **$0.50–1** with 20–30% success cost more once lost accounts are priced in. The 27-parameter test framework covers fraud score, proxy/VPN detection flags, bot history, crawler association, abuse history, spam score, blacklist status, stability, packet loss, session duration, ASN diversity, subnet distribution, reverse DNS. Detection vectors named: ML pattern recognition · IP reputation scoring against global blacklists · behavioural analysis (typing speed, click patterns) · device fingerprinting · geolocation impossibility. **These are vendor-published, self-run figures with no independent verification and no disclosed methodology beyond the headline: quote them as vendor claims, never as measurements.** No proxy vendors are named anywhere. Source: https://www.linkedhelper.com/blog/proxies-linkedin-automation

**Provider info the help center publishes.** A proxy-provider **comparison table as a Google Sheet** rather than inline names: *"Linked Helper team conducted a review of several popular proxy providers and created a comparison table."* Named **non-proxy** partners on the same page: **LinkUnity** and **Topuzer** (account renting), **Linkedeal** (Sales Navigator discounts), **HostZealot** (servers with Linked Helper pre-installed, https://www.hostzealot.com/servers/linkedhelper). **No discount codes are published.**

Sources: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper · https://support.linkedhelper.com/hc/en-us/articles/360015358859-What-is-Proxy-for-What-proxy-do-I-need · https://support.linkedhelper.com/hc/en-us/articles/28140787960338-Proxy-validation · https://support.linkedhelper.com/hc/en-us/articles/360015342720-Can-I-use-Linked-Helper-with-VPN-program · https://support.linkedhelper.com/hc/en-us/articles/22773952344082-Special-offers

## 13. Simultaneous use

**LinkedIn in a browser or mobile app while a campaign runs.** Allowed, *"provided that there is no simultaneous activity on the LinkedIn account from several programs / devices"* and the account is accessed from the same location. *"avoid simultaneous activity in one and the same LinkedIn account from different programs (browsers, mobile apps, etc.)"*: this applies **even if the devices share the same IP**. Why: *"no human is capable of inviting 2nd-degree connections via Chrome browser and sending follow-up messages…at the same time. This behavior looks suspicious for LinkedIn."* Practical instruction: *"we recommend avoid activity via Chrome browser / mobile app when Linked Helper is performing any action."* Nuance, verbatim: *"the risk occurs when you are actively doing something in those sessions at the same time."*: multiple **sessions** are acceptable, simultaneous **active use** is the violation. Team/agency control: agree working hours with the client and use **Working Hours**; *"Enable 'Action working hours' for customization."* Sources: https://support.linkedhelper.com/hc/en-us/articles/360017023219-Can-I-use-LinkedIn-account-via-browser-mobile-app-when-Linked-Helper-is-running · https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper

**Several PCs.** You can install on multiple computers and log in on each. *"You won't be able to open several 'Launchers' at the same time"* on one PC (one launcher can hold many LinkedIn accounts). *"You won't be able to open the same LinkedIn account under one and the same Linked Helper account from several machines simultaneously."* *"We strongly do not recommend using the same LinkedIn accounts under different Linked Helper accounts from several machines at the same time."*: violates LinkedIn's terms, risks restriction or suspension. All data is local per machine; to switch machines you must *"move your data to another PC via backups"*. Source: https://support.linkedhelper.com/hc/en-us/articles/360016336859-Can-I-use-Linked-Helper-2-on-several-PCs

**The same account from two machines.** Do not. Beyond the vendor's prohibition, the blog names *"session cookie used from two IPs simultaneously"* as *"a guaranteed tell."* Parallel access from different locations/devices also triggers verification codes and is the most common cause of the action-verification suspension (§9.4). Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/multiple-linkedin-accounts

## 14. Manual behaviour that gets accounts restricted

The point of *"How to stay safe when working with LinkedIn manually?"* is that **manual** usage carries detection risk comparable to automation.

| Behaviour | Documented detail |
|---|---|
| **Pasted-URL / direct profile loading: the top danger** | opening profiles directly via URL (pasting links, or right-click → open in new tab) triggers LinkedIn's detection. Verbatim: *"If you open 50 profiles via URL in Chrome, then you most likely will be logged out."* Use LinkedIn's **search** to reach profiles instead. This is why LH2 caps `Load LinkedIn profile via URL` at **40 per 24 hours** by default |
| High-volume single-action bursts | visiting **300–500 connections daily** to scrape emails can trigger verification demands or restrictions **within 2-3 weeks**. Diversify activity |
| Simultaneous account access | multiple browsers/devices create separate login sessions that LinkedIn detects and penalizes (§13) |
| Geographic inconsistency | *"Germany in morning, USA at noon"* looks suspicious. Keep locations consistent, or use a proxy/VPN properly |
| Problematic Chrome extensions | LinkedIn can detect certain installed extensions that violate its policies **and may issue warnings even if the extensions aren't actively used.** Audit and remove them (§15) |

Source: https://support.linkedhelper.com/hc/en-us/articles/360015553480-How-to-stay-safe-when-working-with-LinkedIn-manually

**The pasted-URL trap in practice.** Users create this failure mode *while* running LH2: they paste a batch of profile URLs into Chrome to "check" the campaign's targets, or import a CSV and then open the same URLs by hand. Both spend the detection budget the tool is carefully rationing, and neither is counted by LH2's limits. The rule: reach profiles through LinkedIn search, and let the tool do URL loading inside its 40/24 h budget.

## 15. Extension detection

**All figures here are `[LH-CLAIM]`**: vendor-published research by the maker of the desktop alternative to browser extensions. Read the framing as marketing, the numbers as unverified. Methodology as described: 16 competing automation extensions de-minified and audited line-by-line; 7 cloud tools tested with 2 accounts each (14 accounts, all created from France, June 2026); exit IPs scored against IPQualityScore; LinkedIn's production JavaScript reverse-engineered.

**The detected-extension list and its growth:**

| Finding | Figure |
|---|---|
| LinkedIn's **Active Extension Detection (AED)** probe list | **38 extensions (2017) → 461 (2024) → 4,934 unique Chrome extension IDs (June 2026)** |
| File/extension pairs covered | **6,167** |
| Growth rate | **~12 new entries per day** |
| Named confirmation | **Dux-Soup confirmed on the AED list** (extension ID `ppdakpfeaodfophjplfdedpcodkdkbal`) |
| Extensions LH associates with warnings | **Apollo extension, Lempod, PhantomBuster / Phantoms** |

Mechanism: LinkedIn scans for prohibited extension IDs **plus associated local files** (fetchable via GET because extension IDs are persistent and visible at `chrome://system/`), and runs a **web worker** that strips script/style tags with their content, encrypts them and ships them server-side. A DOM **"Spectroscopy"** scanner searches the page for `chrome-extension://` substrings; page snapshots are encrypted and sent for server-side analysis.

**Device-fingerprint surface:** **48-point** device fingerprint (APFC/DNA system: graphics, audio, fonts, WebRTC local IP, automation flags), sent encrypted in API request headers · **timezone is collected twice** to expose partial spoofing · telemetry endpoint `li/track` batches **up to 29 events per request** · external anti-bot stack HUMAN/PerimeterX, Merchant Pool, Google reCAPTCHA v3 Enterprise · IP geolocation accuracy **~80% at state level, ~67% at city level**.

**Cloud-tool findings:** **9 tools** use the "cookie-bridge" session-upload model: *"one of the highest-risk setups."* Of 6 server-side tools, **5 assigned datacenter/proxy IPs**; IPQualityScore fraud scores **94–100** for most test accounts. **1 vendor gave both test accounts the same IP**; **3 unrelated tools** routed through the same upstream (HostRoyale, ASN 203020). Only **Meet Alfred** returned clean IPs (fraud score 0). **All 7 cloud tools lacked built-in IP reputation checking.**

**Architecture risk ranking `[LH-CLAIM]`:**

| Architecture | LH's rating | Stated mechanism |
|---|---|---|
| **Desktop app with own browser engine** (Linked Helper) | lowest | session stays on your machine/VPS; clicks carry `isTrusted === true`; no code injection |
| **Chrome extension** (e.g. Dux-Soup Pro/Turbo) | medium | clicks carry `isTrusted === false`; extension ID and local resource files detectable in-page |
| **Cloud / cookie-bridge** (Expandi, Dripify, HeyReach) | highest | `li_at` session cookie uploaded to vendor servers; vendor-assigned IPs |

**Explicitly absent: no ban-rate percentages by architecture.** Detection is described as *"a scoring model"* where signals accumulate, so the ranking is **directional, not quantified** → `[UNVERIFIED]` as a risk measurement.

**What it implies.** (1) The extension-ID surface does not exist for a desktop app, but the 48-point fingerprint, IP reputation and behavioural signals do: architecture removes one signal class, not the scoring model. (2) Extensions are detected **even when unused**, so running LH2 alongside an automation extension in Chrome still carries that signal (§14). (3) Because detection is cumulative, the levers that matter reduce many signals at once: pacing (§6), one clean static IP per account (§12), no simultaneous sessions (§13), varied campaign structure (§17).

Sources: https://www.linkedhelper.com/blog/linkedin-automation-security-study · https://www.linkedhelper.com/blog/bad-linkedin-extensions · https://www.linkedhelper.com/blog/safest-linkedin-automation-tools

## 16. Multi-account operations

Per-account infrastructure `[LH-CLAIM]`:

| Resource | Requirement |
|---|---|
| Disk | 2 GB min |
| CPU | 0.5–1 core |
| RAM | 4 GB min |
| Phone number | needed for verification codes |
| Email | registration + confirmations |
| Proxy | required whenever your location differs from the account owner's |
| Browser profile | separate, dedicated per account |

Capacity: a **16 GB RAM machine handles 4–5 accounts** simultaneously. Constraints: do **not** buy pre-made accounts: *"Most accounts for sale are fake and get banned within a week from registration."* · parallel access to one account from different locations/devices triggers verification codes · one IP per account, never shared (§12) · new accounts often hit identity verification **within 1–2 weeks** of creation (§10), so budget for it before promising throughput. Source: https://www.linkedhelper.com/blog/multiple-linkedin-accounts

**`[UNVERIFIED]`**: the blog gives **no LinkedIn policy citation** on whether multiple personal accounts are permitted. Do not assert that it is allowed, and do not claim the blog says it is forbidden; the blog is silent.

**30-account case study `[LH-CLAIM]`**, one fractional CMO operating solo: **30+ profiles on two Mac Minis**, ~20% on Pro plans, rest Basic · *"I usually bump up the total actions per day to about 300"* for connection requests: **2× LH's own published 150-action ceiling; treat as an outlier, not a recommendation** · prefers **no-note invitations**, actions spread through the day · claims **zero account bans** across 30 simultaneous profiles · claims **>100 hours/week** saved on a one-time licence rather than ~$80/user/month competitor pricing. Workflow, verbatim structure:

```
1. Identify TAM/SAM; download existing connections
2. Cross-reference with Sales Navigator target lists
3. Send automated connection requests
4. Deploy event / newsletter invitations
5. Scrape reactions + commenters for warm outreach
6. Export data; use AI to score contacts 1-10 on ICP fit
7. Push new connections to a shared spreadsheet via webhook
```

Source: https://www.linkedhelper.com/blog/running-30-linkedin-accounts

**Operator read:** the scaling story is horizontal (more accounts, each at safe limits), not vertical (one account pushed harder). The single vertical claim, 300 actions/day, contradicts the vendor's own default and rests on one anecdote. Never quote it as a limit.

## 17. Campaign structure and message randomization as safety controls

**Structure.** Verbatim problem statement: homogeneous activity (only invites and follow-ups) appears bot-like. The help center prescribes interleaving warm-up steps, the recommended 16-step diverse workflow:

```
 1. Follow profiles
 2. Delay between actions
 3. Like and comment posts/articles
 4. Delay between actions
 5. Invite 2nd/3rd level contacts
 6. Filter contacts out of my network (keep 1st level only)
 7. Delay between actions            (couple of days)
 8. Message to 1st connections
 9. Check for replies
10. Endorse my contacts
11. Message to 1st connections       (2nd follow-up)
12. Check for replies
13. Like and comment posts/articles
14. Message to 1st connections       (3rd follow-up)
15. Check for replies
16. Etc.
```

Shorter variant from the weekly-limit article: `Like and comment on posts` → `Delay (1-2 days)` → `Follow / unfollow profiles` → `Delay (1-2 days)` → `Invite 2nd/3rd level contacts` → actions 6-11 progressive messaging + reply checks with strategic delays. Timeout guidance: LH randomizes timeouts between micro-steps; **default FAST timeouts are "proven safe"**, new or inactive accounts should switch to **SAFE** via the `Action steps delays plug-in`. Sources: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper · https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit

**Message randomization.** LinkedIn detects patterns in repetitive messages. Use **at least two message variants** with spintax and variables: **Spintax** (randomly select from pools of phrases) · **Variations** (completely different messages with identical meaning) · **Custom Variables & IF THEN ELSE** (personalize and randomize simultaneously) · **complex combinations**: mix all methods, then verify with **Message preview**. Additional rules that reduce spam-flagging: **don't use links in invitations**: *"LinkedIn may flag them as spam"* · don't put a sales offer in the connection request; it reduces acceptance rate · skip the invite note entirely if you're unsure it will resonate. Cadence `[LH-CLAIM]`: **4–6 messages over 5–10 days**. Sources: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper · https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2 · https://www.linkedhelper.com/blog/linkedin-message-automation

## 18. Pre-flight checklist

**Phase 1: account onboarding**

- [ ] Establish account age and prior automation history. <12 months old or dormant → run the §8.3 ramp from day 1.
- [ ] Proxy only if needed (VPS abroad / multi-country / someone else's account). IPv4 HTTP(S)/SOCKS(5).
- [ ] ISP / residential / mobile, dedicated IP. Fraud score target **<30**, absolute reject **>75**; no bot/VPN/crawler flags.
- [ ] Verify the **real egress IP** in a browser: the provider-shown IP may be a gateway.
- [ ] LinkedIn account country **==** proxy country; time zone matched.
- [ ] Run `Proxies` menu validation; replace anything marked **Bad**.
- [ ] One IP per account, static not rotating, never shared.
- [ ] Audit Chrome for policy-violating LinkedIn extensions: detected even when unused.

**Phase 2: limits**

- [ ] `Settings` → `Limits` → `Max actions per 24 hours` = **150** (or 120 for the vendor's more conservative figure).
- [ ] Advanced limits: invites **50** (≤25 for a young account), endorsements **60**, messaging/follow/extract **150**, Boost post **100**, `Load LinkedIn profile via URL` **40**, search **100 pages/day** (conservative of 100 vs 200).
- [ ] `Max actions per 24 hours` set **at or above** the sum of the per-activity limits you want (limit-precedence CONFLICT, §4.5).
- [ ] `Smart Daily Limit Adjustment` on (**10%** default → 45–50 on a 50 setting).
- [ ] Hourly advanced limit on the highest-volume activity to prevent front-loading (§5).
- [ ] Verify with one bunch; read the "Last 24 hrs actions" counter before scaling.

**Phase 3: pacing**

- [ ] `Settings` → `Working Hours` set (not 24/7 unless deliberate); 24-hour format; `Start time randomization` raised.
- [ ] FAST timeouts default; **SAFE** for new/dormant accounts (`Action steps delays plug-in`).
- [ ] `Bunch size` / `Timeout between bunches` used to spread bursts (default 10 / 1 min; 25 / 12 h for 50 invites/day).
- [ ] Per-action working hours via `Action working hours plug-in` where a client's hours matter.

**Phase 4: campaign design**

- [ ] Warm-up before invite: Follow → Like/comment → Delay → Invite (§17).
- [ ] ≥2 message variants; spintax + variables + IF-THEN-ELSE; verify in **Message preview**.
- [ ] No links in invitation notes; no sales pitch in the connection request.
- [ ] `Check for replies` between every message step; cadence 4–6 messages over 5–10 days.
- [ ] Prefer group/event messaging for 2nd/3rd-degree reach (§2.7): no invite budget, no credits.

**Phase 5: ongoing hygiene**

- [ ] Pending invites kept **200–500**; withdraw every **2–4 weeks** (auto-canceller at **30 days**).
- [ ] Acceptance rate monitored; **>25%** target, act below ~20%.
- [ ] No simultaneous manual activity in Chrome/mobile while a campaign runs.
- [ ] Never open profiles by pasting URLs manually (50 URL-opens ≈ logout).
- [ ] Never run the same LinkedIn account from two machines at once.
- [ ] Profile edited at most **once per day**.
- [ ] Watch the early-warning set: frequent CAPTCHAs · weekly-limit warning appearing early · delayed message delivery · drop in profile-view visibility. Any of these → stop and re-ramp (§10) rather than waiting for the block.

**Phase 6: if a restriction lands**

- [ ] Stop the campaign runner. Do not retry.
- [ ] SAFE timeouts, reduced daily limits, wait hours-to-days.
- [ ] Withdraw all pending invites except the most recent 500.
- [ ] Wait **5-7 days**; expect **2–4 weeks** to full clean recovery.
- [ ] Only then contact support, via the §10 endpoints, **without mentioning automation**.
- [ ] Do not create a second account, continue outreach, or edit the profile while restricted.
- [ ] Restructure the campaign (warm-up steps + personalization) before resuming.

## 19. Antivirus false positives

Operational, not a security issue. Antivirus warnings are *"false-positive detections"* produced by heuristic algorithms against lesser-known software. Vendor evidence offered: digital signature on the installer, VirusTotal scan of the installer, VirusTotal scan of the executable. Recommended action: *"allow Linked Helper to run and add it to whitelist and reinstall if needed"*. No specific detection names are published → `[UNVERIFIED]` for any named detection string. Source: https://support.linkedhelper.com/hc/en-us/articles/360015995360-My-anti-virus-found-a-threat-Is-Linked-Helper-safe
