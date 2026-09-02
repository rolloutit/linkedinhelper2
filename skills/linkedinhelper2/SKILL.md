---
name: linkedinhelper2
description: Expert operator's manual for Linked Helper 2 (LinkedIn automation desktop app). Use this whenever the user mentions Linked Helper, LinkedHelper, LH2, or asks about building/fixing/scaling LinkedIn outreach campaigns, connection-invite sequences, message templates and variables, {firstName}/{cs_*} personalization, IF-THEN-ELSE message logic, daily action limits, warm-up ramps, account restrictions or "LinkedIn jail", proxies for LinkedIn, lead collection from LinkedIn/Sales Navigator/Recruiter search, group or event messaging, InMails, email enrichment, CRM/webhook/Zapier export, or Linked Helper plug-ins, queues, lists and troubleshooting. Grounded in the official Linked Helper help center and blog, verified 2026-09-01.
---

# Linked Helper 2 — Operator Manual

You are configuring and operating **Linked Helper 2** (LH2), a **desktop** LinkedIn automation
app. This skill makes you accurate about its actual UI, its actual limits, and the failure modes
that get accounts restricted.

## 0. Non-negotiables — read before answering anything

1. **Never invent a number.** Limits, prices, credit costs and character caps are all in the
   reference files with sources. If a figure is not there, say it is not documented and offer to
   check `support.linkedhelper.com`.
2. **Where sources conflict, show both.** The vendor's own docs contradict themselves on invite
   caps, pending-invite ceilings, personalized-invite allowances and limit precedence. The
   references mark these `CONFLICT`. Present both figures and recommend the conservative one.
   Never silently pick one.
3. **Respect `[UNVERIFIED]` tags.** A large set of behaviours (captcha/2FA handling, RDP
   persistence, A/B testing, per-operation AI credit rates, exact spintax grammar, SSI mechanics)
   is *not* documented anywhere. Do not assert them. Say "not documented — test on a throwaway campaign first".
4. **State the compliance reality once, plainly, then help.** Automating LinkedIn violates
   LinkedIn's User Agreement, which prohibits software that scrapes or automates access.
   Accounts can be restricted or permanently closed. The user owns that risk. Say it once at the
   start of a new engagement — do not moralize in every reply.
5. **Safety before volume.** If a requested configuration exceeds the documented safe ceilings in
   §5, say so and give the safe number alongside the requested one. Default to the conservative
   ramp for any account younger than 12 months or dormant.
6. **Never handle the user's LinkedIn credentials.** LH2 stores its own session locally. Do not
   ask for, echo, store or transmit passwords, cookies, 2FA codes, licence keys or proxy
   credentials. If a task appears to need them, describe the UI steps for the user to do it.
7. **Verify UI paths before asserting them.** Menu names below are verbatim from the docs as of
   2026-09-01. LH2 ships frequently; if the user says a control isn't where you said, believe
   them and check §"a feature isn't in my interface" in `references/troubleshooting.md` — the
   usual cause is an uninstalled plug-in, not a missing feature.

## 1. Mental model — get this right and everything else follows

**Two layers.**

| Layer | What it is | Menus |
|---|---|---|
| **Launcher** | account/licence manager, one per install | `LinkedIn Accounts`, `Licenses`, `Billing` (Orders & Invoices / Subscriptions / Data Credits), `Proxies`, `Workspace Management` |
| **Instance** | one running app per LinkedIn account | `Campaigns`, `LinkedIn` (embedded browser), `Collect`, `Functions`, `CRM`, `Inbox`, `Plug-in store`, `Settings` |

**Almost every feature is a plug-in.** If an action does not appear in the `+Add action` picker,
it is not installed. `Plug-in store` → install → it becomes available **for every instance** on
the account (account-wide, not per-instance). Categories: Action (23), Action extension (9),
Message action extension (6), CRM (3), Campaigns (4), Other (3). Most are on by default;
`Organizations extractor` is the documented exception and must be installed manually.
**This is the single most common cause of "the feature doesn't exist".**

**A campaign = an ordered workflow of actions + a set of lists.** Profiles enter the first
action's queue and flow top-to-bottom. Nothing happens to a profile that is not in some list.

**Campaign-level lists** (verbatim names): `Profiles to process` (a.k.a. Queue) · `Exclude list`
(the *rule*) · `Excluded` (the *result* of the rule) · `Processing` · `Replied` · `Successful` ·
`Failed` · `Processed` (aggregate) · `Accepted` (invite campaigns with network filtering only).

**Action-level lists:** `Profiles to process` · `Processed` · `Replied` · `Messaged` ·
`Successful` · `Skipped` · `Failed` · `Excluded` (needs `Exclude list plug-in`).

Two facts that explain most confusion:
- **`Failed` is terminal** — a failed profile stops progressing through the campaign.
- **Replies are not monitored continuously.** LH2 checks whether a profile replied *only when it
  processes that profile through the next messaging action*. No `Check for replies` step between
  messages ⇒ people who answered still get the follow-up.

**The runner is sequential, never parallel.** `Start campaigns runner` activates all *active*
campaigns and runs them one after another. Statuses: `Completed` (empty queue) · `Queued` ·
`Sleeping` (timeout/scheduled) · `Stopped` (manual, excluded from runner) · `Running`.
Priority = the **earliest `Start at`** across any action in the campaign — to push a campaign to
the front, set its `Start at` to a past date. Knobs: `Bunch size` (default **10** profiles per
action), `Timeout between bunches` (default **1 minute**). Big queues + tiny timeouts ⇒ one
campaign hogs the runner; raise the timeout (e.g. 2 h) to force switching.

**Ordering rule:** 2nd/3rd-degree actions must precede 1st-connection actions. LH2 auto-inserts
`Filter contacts out of my network (keep 1st level only)` between incompatible action types.
Reordering actions is only possible while Queue/Processed lists are empty.

## 2. How to work a request

Follow this order. Do not skip to a workflow before you know the account's age and the goal.

1. **Establish context** — LinkedIn account age and prior automation history; LinkedIn
   subscription tier (Free / Premium / Sales Navigator / Recruiter); LH2 licence (Standard vs
   Pro); local vs cloud storage; single or multi-account; is there a proxy/VPS.
2. **Pick the objective** — connections, replies/meetings, data/emails, or engagement. Each maps
   to a different campaign shape (§3).
3. **Pick the lead source** — this is the real constraint, not the action (§4).
4. **Set safety numbers first** (§5), then design the sequence to fit inside them. Never the
   other way round.
5. **Write the copy** with variables and fallbacks (§6).
6. **Wire the exits** — CRM, webhook, CSV, external CRM (`references/integrations.md`).
7. **Hand back a checklist** the user can execute in the UI, with exact menu paths and the list
   names above. Use `assets/campaign-plan-template.md`.

When the user reports something broken, go straight to `references/troubleshooting.md` and use its
triage order — do not redesign the campaign first.

## 3. Goal → campaign shape

Predefined templates available at campaign creation (verbatim): `Empty campaign` ·
`Invite & Follow Up` · `Messaging Sequence` · `Export profile information` · `Inmail sequence` ·
`Message sequence via event` · `Message sequence via group` · `Warm-up, invite, and follow-up` ·
`Invite 1st to follow Organization (Company / School)` · `Invite person to an event` ·
`Invite 1st connections to Group` · `Endorse 1st connections` · `Like & comment posts and
articles` · `Follow profiles` · `Invite and reach out via LinkedIn and email` · `Message chain to
warmed-up 1st connections` · `Send person to Snov.io campaign` · `Visit & Extract Profiles` ·
`Find profile emails` · `Remove 1st connections`.

| Objective | Start from | Core actions | Watch out |
|---|---|---|---|
| Grow network safely | `Warm-up, invite, and follow-up` | Follow → Like/comment → Delay → Invite → Filter out of network → Message → Check for replies | Each warm-up step has its own advanced limit; budget them together, not just the invite |
| Replies from existing 1st connections | `Message chain to warmed-up 1st connections` | Message → Check for replies → Message | No invite spend at all; safest volume play |
| Reach 2nd/3rd degree **without** invites | `Message sequence via event` / `via group` | Collect attendees/members → Message to event attendees / group members | Profiles must carry that Event/Group ID. CSV/HTML uploads work only via `Override platform` → `Change platform` → `Collect scope type` = Event/Group ID — see `references/recipes.md` |
| Reach 2nd/3rd degree with credits | `Inmail sequence` | InMail to 2nd & 3rd contacts | InMail credits; free to Open Profiles |
| Data / list building | `Visit & Extract Profiles` | Visit & Extract → Data Enrichment → export | Heaviest `Load profile page` consumer |
| Emails | `Find profile emails` | Find Profile Emails / Data Enrichment | Spends Data Credits (email 1, phone 10) |
| Warm an audience before selling | `Follow profiles`, `Like & comment posts and articles`, `Endorse 1st connections` | — | Endorsement = 1 action per profile regardless of skill count |
| Fill an event / group / company page | `Invite person to an event`, `Invite 1st connections to Group`, `Invite 1st to follow Organization` | — | Separate credit pools; Standard licence caps these at 20/24 h |
| Hygiene | `Remove 1st connections` (template); `Sent invites canceller` (`Functions` menu) | — | Withdrawn invite ⇒ cannot re-invite for up to 3 weeks |

Full action catalogue with settings, compatible plug-ins and degree requirements:
`references/actions.md`. Ready-made multi-step playbooks: `references/recipes.md`.

## 4. Lead sources — the real constraint

**Regular LinkedIn:** LinkedIn Search (**hard cap 1,000 profiles per search request**) · My
Network (all 1st-degree, one go) · School Alumni · Company Employees (People tab caps at 1,000) ·
Event attendees (`Events` → **Networking** tab → `See all`) · Groups you belong to (no
location/industry filtering) · Who viewed your profile · Sent invitations · **Post likers /
commenters — only offered when the post is opened by its direct URL** · Followers / Following ·
Company page followers (needs page admin) · Companies search (needs `Organizations extractor`).

**Sales Navigator:** advanced search, Saved Leads Lists, Saved Searches, Accounts lists.
**Recruiter:** SmartSearch, Project pages.
**External:** CSV/TXT of LinkedIn URLs, LH2's own CSV exports, and HTML-saved LinkedIn pages (the
documented workaround for unsupported pages).

Collect targets either a **Campaign list** (`Queue` **or** `Exclude list`) or an **Action list**
(that action's `Queue` only — no Exclude option).

**CSV/URL import:** campaign → `Queue`/`Exclude List` → `Add` → `Upload Profiles URLs` → paste or
choose file → `Import`. URLs only — names, tags and other columns are ignored. Documented ceiling
**45 profiles per 24 h** to avoid logouts; the `Load LinkedIn profile via URL` advanced limit
defaults to **40 per 24 h** — `CONFLICT`, use 40. A bare URL is sufficient for inviting,
messaging, endorsing, following and webhook export.

Six documented reasons profiles are skipped during collection, and the accepted URL formats, are
in `references/campaigns.md`.

## 5. Safety numbers — set these before designing anything

Path: **`Settings` → `Limits`** (overall) and per-activity **advanced limits**.

| Control | Documented default / recommendation |
|---|---|
| `Max actions per 24 hours` | **150** |
| Invites | **50 / 24 h** (established account) |
| Endorsements | 60 / 24 h |
| Messaging, follow, extract | 150 / 24 h |
| Boost post | 100 / 24 h |
| `Load LinkedIn profile via URL` | **40 / 24 h** |
| Search result pages | `CONFLICT` 100 / day (blog, = LH default) vs 200 / day (help center) — use **100** |
| Smart Daily Limit Adjustment | on, **−10%, downward only** — it sends 90–100% of the limit you set (50 → 45–50). It never exceeds your setting. |
| `Bunch size` / `Timeout between bunches` | 10 / 1 min |
| Text input method | `Random` (default) |
| Pacing | not faster than `FAST`; use `SAFE` for new or dormant accounts |

**The vendor's own Safety Kit numbers are much lower than the app defaults above** and the docs
never reconcile the two. `CONFLICT`: Safety Kit recommends **25–30 connection requests/day**,
**~150/week**, **50–60 messages/day**, **max 6 invites/hour**, and a **10–15 actions/day** warm-up;
one restriction-trigger article calls **more than 25 invites/day** a trigger in itself. Quote the
Safety Kit numbers to anyone who asks what is *safe*, and the table above for what the app *allows*.
Full both-sides treatment: `references/limits-safety.md`.

**New or dormant account ramp:** first 14 days feed-scrolling, follows and ~5 invites/day from
recommendations → **10–15 invites/day** → **+5–10 every 10 days** → ~35/day at month 1 → ~50/day
at month 2.

**The 24-hour counter is rolling, not a midnight reset.** Burning the whole daily allowance in one
hour leaves the account idle for ~24 h, which is also the most bot-like pattern available.

**Pending-invite hygiene is the highest-leverage habit.** Keep pending invites in the low
hundreds and withdraw stale ones every 2–4 weeks (`Sent invites canceller`, auto at 30 days).
Note: LH's own docs give **at least eight incompatible** pending-invite figures, from
"no more than 200 – 500" up to 2,500 — `CONFLICT`; treat none as a ceiling. Use the help center's
own conservative **200–500** and manage by hygiene.

**Limit precedence is contradicted in the docs** — one article says advanced limits win, another
says `Max actions per 24 hours` always overrides. `CONFLICT`. Practical rule: set the daily cap at
or above the sum of the per-activity limits you actually want, and verify with a small run.

**Proxies** are needed for a VPS abroad, multi-country operation, or running someone else's
account. IPv4 HTTP/HTTPS/SOCKS5; ISP/residential/mobile with a dedicated IP; **fraud score ≤75**;
proxy country must match the LinkedIn account's country; validate in the `Proxies` menu and
replace anything marked **Bad**.

Restriction triggers, the recovery playbook, LinkedIn support endpoints, extension-detection
findings and the full checklist: `references/limits-safety.md` and
`assets/preflight-safety-checklist.md`.

## 6. Personalization — exact syntax

**Built-in variables** (single curly braces, case-sensitive):

```
{lhid} {firstName} {lastName} {company} {position} {industry}
{mutualFirstFullName} {mutualSecondFullName} {mutualTotal} {memberId} {publicId}
```

**Custom variables** — needs `Custom template variables plug-in`. Form `{cs_<name>}`. CSV needs
`profile_url` plus at least one `cs_*` column; upload via campaign → `Queue` → `Custom fields`.
Scope: only profiles whose URLs came in that file. Priority, highest first:
**Action level > Campaign level > CRM level**.

**IF-THEN-ELSE** — needs the conditional plug-in. It is **three UI fields, not inline markup**;
the docs never publish an inline `{IF ...}` string, so build it in Template Builder → Advanced:

```
IF   :  {company}            <- exactly ONE variable, no text, no operators
THEN :  I saw you work at {company} ...
ELSE :  Hi {firstName}, ...
```

It tests **presence only** — never value comparison. `{mutualTotal} = 10`, `{company} !=
Microsoft` and `{cs_age} > 30` are **not supported**. Nesting is supported.

**Randomization:** spintax `{option A|option B|option C}` inside the body, and **Variations**
(separate whole messages, distributed equally). Use both — identical text at volume is a
detectable pattern.

**Character limits** (docs; see `references/templates.md` for the full 28-field table):

```
Invite note, free LinkedIn      0 beyond the monthly personalized-invite quota
                                CONFLICT: 5/month (blog) vs ~10/month (help center) - assume 5
Invite note, paid LinkedIn      200-300
Message to 1st connections      8,000-10,000
InMail subject / body           200 / 1,900   (one article says "up to 2000" - CONFLICT)
Group / event messages          8,000
Comments                        1,250
```

Always preview with a real profile before starting. Copy frameworks, verbatim templates and reply
handling: `references/templates.md` and `assets/message-templates.md`.

## 7. Exclusions and deduplication

**There is no global blacklist.** Verbatim: *"Linked Helper does not offer a blacklist that would
allow skipping all profiles from any current and new campaigns."* Build one: a dedicated
"Global Exclude" campaign with a single action, then `Functions` → `List Manager` → Source =
Global Exclude, Destination = new campaign → **`Add unique`**. CRM profiles cannot be deleted,
only hidden. Full dedup strategy, tag-based export ratchets and cross-account dedup:
`references/campaigns.md` §Exclusions and `references/recipes.md`.

## 8. Reference files — load on demand

| File | Load it when |
|---|---|
| `references/actions.md` | choosing or configuring any action/plug-in; which are 1st-degree-only, Pro-only, Premium-dependent; every instance and Launcher menu |
| `references/campaigns.md` | queue/list mechanics, lead sources, collection failures, CSV formats, exclusions, dedup, List Manager, cloning |
| `references/templates.md` | writing copy: variables, IF-THEN-ELSE, spintax, character limits, frameworks, verbatim templates, images |
| `references/limits-safety.md` | limits, ramps, restriction triggers and recovery, proxies, multi-account, pending-invite hygiene |
| `references/recipes.md` | multi-step playbooks: warm-up funnels, invite-free 2nd/3rd-degree reach, group/event harvesting, email discovery, re-engagement, recruiting |
| `references/troubleshooting.md` | anything broken — symptom → cause → checks → fix, in triage order |
| `references/integrations.md` | CRM, webhooks, Zapier/Make/n8n, Google Sheets, Snov.io, export field names, credits |
| `references/plans-and-platform.md` | pricing, Standard vs Pro gating, credit allowances, OS/hardware requirements, workspaces, VPS/cloud, backup |

## 9. Assets

- `assets/campaign-plan-template.md` — fill-in plan: objective, source, workflow, limits, copy, exits.
- `assets/message-templates.md` — copy library with variables and fallbacks already wired.
- `assets/preflight-safety-checklist.md` — run before starting any campaign.
- `assets/warmup-schedule.csv` — day-by-day ramp for a new or dormant account. It is a **derived
  synthesis**, not a document LH publishes: its `grounding` column marks which rows are documented
  milestones and which are interpolations, and its message ceiling follows the vendor's Safety Kit
  (50–60/day), not the app's 150 default. Cite the column when you use a row.

## 10. Source conventions used throughout

Every factual block in the references carries a `Source:` URL. Tags:

- `[LH-CLAIM]` — the vendor says it; not independently verified.
- `[LI-POLICY]` — LinkedIn's own documented rule or limit.
- `[COMMUNITY]` — practitioner consensus, not official.
- `[UNVERIFIED]` — not documented anywhere; do not assert it.
- `CONFLICT` — two or more incompatible official figures; both are shown.

Product surface (pricing, credits, requirements, integrations) verified against
`linkedhelper.com` on **2026-09-01**. Anything time-sensitive older than a few months should be
re-checked before you quote it.
