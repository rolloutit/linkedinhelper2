# LinkedinHelper2

A Claude skill that turns Claude into a competent **Linked Helper 2** operator — the desktop
LinkedIn automation app. It knows the actual UI, the actual limits, the plug-in system, the
message-template syntax, and the failure modes that get accounts restricted.

Built from the official [Linked Helper help center](https://support.linkedhelper.com/hc/en-us)
(five of its six categories — News is not covered; 215 articles indexed, 107 read in full) and the
[Linked Helper blog](https://www.linkedhelper.com/blog),
with pricing, credits, requirements and feature names cross-checked against
[linkedhelper.com](https://www.linkedhelper.com) on **2026-09-01**.

## What it's good at

- **Designing campaigns** — objective → campaign template → action sequence → lead source, with
  the ordering rules and the plug-ins you must install first.
- **Setting safe limits** — the documented daily caps, the advanced per-activity limits, warm-up
  ramps for new and dormant accounts, and pacing that doesn't look like a burst.
- **Writing copy that works in the tool** — the 11 built-in variables, `{cs_*}` custom variables
  from CSV, the real IF-THEN-ELSE constraints (three UI fields, one variable, presence-only),
  spintax, Variations, and every documented character limit.
- **Reaching people without spending invitations** — group and event messaging, Open-Profile
  InMails, follows, page follow-invites, ranked by how good the evidence actually is.
- **Getting the data out** — CSV export with the complete field list, webhooks with the complete
  payload schema, the 14 named integrations (CRMs, ATS, email and marketing tools, Sheets),
  Zapier/Make/n8n, Google Sheets, Snov.io.
- **Fixing what's broken** — a symptom index keyed on the exact error strings
  (`Failed to prepare collecting`, `Incorrect connect response (429)`, `Disconnect fired`, …)
  with checks and fixes in triage order.
- **Recovering from a restriction** — the escalation ladder, the recovery playbook, the exact
  LinkedIn support endpoints, and realistic timelines.

## What makes it trustworthy

Three editorial rules are enforced throughout:

1. **Every fact carries its source URL.** All 443 `Source:` attributions (~275 unique URLs) were
   machine-verified against the research corpus — none were invented.
2. **Conflicts are shown, never reconciled.** Linked Helper's own docs contradict themselves on
   invite caps, pending-invite ceilings, personalized-invite allowances, InMail character limits,
   limit precedence, and the gap between the app's defaults and the vendor's own Safety Kit
   recommendations. 75 such cases are marked `CONFLICT` with **both** figures and both sources, plus a
   recommendation to use the conservative one. The skill never fakes precision it doesn't have.
3. **Gaps are labelled, not filled.** 158 `[UNVERIFIED]` markers cover behaviour nobody documents —
   captcha/2FA handling, RDP session persistence, per-operation AI credit rates, exact spintax
   grammar, A/B statistics. The skill is instructed to say "not documented, test it" rather
   than guess.

Claims are also tagged `[LH-CLAIM]` (vendor says it), `[LI-POLICY]` (LinkedIn's own rule) and
`[COMMUNITY]` so you always know what kind of evidence you're standing on.

## Install

### As a plugin (Claude Code / Cowork)

This repo is its own single-plugin marketplace, so two commands install it:

```bash
/plugin marketplace add rolloutit/linkedinhelper2
/plugin install linkedinhelper2@rolloutit
```

Verify with `/plugin list` (or the **Installed** tab of `/plugin`). If it doesn't activate
immediately, run `/reload-plugins`.

To try it before installing:

```bash
claude --plugin-dir /path/to/linkedinhelper2
```

### As a `.plugin` bundle (Cowork desktop)

A `.plugin` file is just this repo's contents zipped:

```bash
cd linkedinhelper2 && zip -r /tmp/linkedinhelper2.plugin . -x '*.git*' '*.DS_Store'
```

Send that file into a Cowork chat and it renders as an installable card.

### As a plain skill

Copy `skills/linkedinhelper2/` into your skills directory:

```bash
# project-level
cp -r skills/linkedinhelper2 .claude/skills/

# or user-level
cp -r skills/linkedinhelper2 ~/.claude/skills/
```

Then just ask normally — "help me set up a Linked Helper campaign for CTOs in Berlin", "why are my
invites failing with 429", "what's a safe invite volume on a two-month-old account" — and the skill
loads itself.

## Layout

```
linkedinhelper2/
├── README.md
├── LICENSE
├── .claude-plugin/
│   ├── plugin.json                 # plugin manifest
│   └── marketplace.json            # makes the repo installable as a marketplace
└── skills/linkedinhelper2/
    ├── SKILL.md                        # routing file: mental model, decision tables, guardrails
    ├── references/
    │   ├── actions.md                  # every action & plug-in, every menu, selection tables
    │   ├── campaigns.md                # queues & lists, lead sources, CSV import, exclusions, dedup
    │   ├── templates.md                # variables, IF-THEN-ELSE, spintax, char limits, verbatim copy
    │   ├── limits-safety.md            # limits, ramps, restriction recovery, proxies, multi-account
    │   ├── recipes.md                  # step-by-step playbooks + tactics ranked by evidence
    │   ├── troubleshooting.md          # symptom → cause → checks → fix, in triage order
    │   ├── integrations.md             # CRM, webhooks, export field lists, credits
    │   └── plans-and-platform.md       # pricing, plan gating, requirements, workspaces, VPS, backup
    └── assets/
        ├── campaign-plan-template.md   # fill-in plan before you touch the app
        ├── message-templates.md        # working copy library, variables and fallbacks wired
        ├── preflight-safety-checklist.md
        └── warmup-schedule.csv         # day-by-day ramp for a new or dormant account
```

`SKILL.md` is the only file loaded up front. The references load on demand, so a simple question
doesn't drag 6,000 lines into context.

## Before you use this

**Automating LinkedIn violates LinkedIn's User Agreement.** Accounts get restricted and sometimes
permanently closed. This skill is documentation of a commercial tool and of the safety practices its
own vendor publishes — it is not a promise that automation is safe or permitted, and it is not legal
advice. You own the risk on your own account.

The skill is also instructed never to ask for, store or transmit credentials — LinkedIn passwords,
2FA codes, licence keys, proxy credentials, CRM API tokens. It describes the UI steps and leaves the
secrets with you.

## Keeping it current

Linked Helper ships frequently and LinkedIn changes its limits without notice. The product-surface
facts (pricing, credits, requirements, integrations) are date-stamped **2026-09-01**. Re-verify
anything commercial or numeric before quoting it to a customer. Sources are in every block, so
re-checking is a matter of following the link.

Renaming: the skill's directory name, the `name:` in `SKILL.md`'s frontmatter, and the `name` in
`plugin.json` must match. They are all `linkedinhelper2` (lowercase — skill names can't contain
capitals). Change all three together if you rename it.

## Licence

MIT — see [LICENSE](LICENSE). Linked Helper is a product of its respective owners; this repository
is unofficial and not affiliated with or endorsed by Linked Helper or LinkedIn.
