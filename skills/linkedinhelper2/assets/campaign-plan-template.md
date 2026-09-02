# Linked Helper 2 — Campaign Plan

Fill every field before touching the app. An empty field is a decision you have not made yet.
Menu paths below are the real LH2 paths; `references/` files in this skill hold the detail.

## 1. Context

| Field | Value |
|---|---|
| Campaign name | |
| Objective (connections / replies / data / engagement) | |
| LinkedIn account age | |
| Prior automation on this account | |
| LinkedIn subscription (Free / Premium / Sales Navigator / Recruiter) | |
| LH2 licence (Standard / Pro) | |
| Storage (local / cloud) | |
| Runs on (desktop / VPS) | |
| Proxy in use (yes/no — never record credentials here) | |
| Success metric and target | |

## 2. Audience and lead source

| Field | Value |
|---|---|
| Who exactly (title, seniority, industry, geography, company size) | |
| Source (`references/campaigns.md` §Lead sources) | |
| Platform required for that source | |
| Hard cap on that source (e.g. 1,000 profiles per LinkedIn search) | |
| Search string / saved list / event / group / post URL | |
| Expected list size | |
| Collect target: campaign `Queue` or a specific action's `Queue` | |
| Profiles to pre-load into `Exclude list` | |

## 3. Plug-ins to install first

`Plug-in store` → install before building the workflow, or the action will not appear in `+Add action`.

- [ ] Primary action plug-in(s): ______________________
- [ ] `Action steps delays plug-in` (needed for `Bunch size` / `Timeout between bunches`)
- [ ] `Exclude list plug-in`
- [ ] `Multi-campaigns runner plug-in`
- [ ] `Custom template variables plug-in` (if using `{cs_*}`)
- [ ] `IF-THEN-ELSE operator for Message template editor plug-in` (if branching copy)
- [ ] `Tagging system plug-in`
- [ ] `List manager plug-in`
- [ ] Other: ______________________

## 4. Workflow

Actions in order, top to bottom. 2nd/3rd-degree actions must come before 1st-connection actions.

| # | Action (verbatim name) | Key settings | Delay / timing | Notes |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |

- [ ] A `Check for replies` step sits between every pair of messaging steps
      (replies are only detected when the next messaging action processes the profile).
- [ ] Reordering done before any profile entered a queue (reorder is locked afterwards).

## 5. Limits and pacing

| Setting | Path | Value |
|---|---|---|
| `Max actions per 24 hours` | `Settings` → `Limits` | |
| Invites / 24 h | `Settings` → `Limits` (advanced) | |
| Messages / 24 h | `Settings` → `Limits` (advanced) | |
| `Load LinkedIn profile via URL` / 24 h | `Settings` → `Limits` (advanced) | |
| Other advanced limits | | |
| Smart Daily Limit Adjustment | `Settings` → `Limits` | on, −____% (downward only) |
| Working hours | `Settings` → `Working Hours` | |
| Start time randomization | `Settings` → `Working Hours` | |
| `Bunch size` | action → `Delay settings` | |
| `Timeout between bunches` | action → `Delay settings` | |
| Text input method | action → `Delay settings` | `Random` |

Ramp plan if the account is new or dormant (see `assets/warmup-schedule.csv`): ______________________

## 6. Copy

For each message step: template text, every variable used, and the fallback when it is empty.

| Step | Character budget | Variables used | Fallback strategy | Variants |
|---|---|---|---|---|
| Invite note | | | | |
| Message 1 | | | | |
| Message 2 | | | | |
| Message 3 | | | | |

- [ ] Previewed with a real profile from the actual queue.
- [ ] Every variable has an IF-THEN-ELSE or `cs_*` fallback — no message can go out with a hole.
- [ ] At least 2 variants (or spintax) per step.
- [ ] No links in the invitation note. No pitch in the connection request.
- [ ] Character counts inside the documented limits.

## 7. Exits — where the data goes

| Field | Value |
|---|---|
| Tags applied at each stage | |
| CRM / webhook / CSV / external CRM destination | |
| Who follows up manually, and on what trigger | |
| Reply handling (`Filter by message content` / `Ignore generic replies`) | |

## 8. Exclusions

- [ ] "Global Exclude" campaign applied via `Functions` → `List Manager` → `Add unique`
- [ ] Existing customers / current pipeline excluded
- [ ] Cross-campaign dedup done
- [ ] Already-invited profiles not re-collected

## 9. Launch and review

- [ ] `assets/preflight-safety-checklist.md` completed
- [ ] Started with a small batch (10–25 profiles) and verified the first sends by hand
- [ ] Day-1 review: sends actually going out, no `Failed` cluster, no LinkedIn prompts
- [ ] Day-3 review: acceptance/reply rate vs target
- [ ] Weekly: pending invites withdrawn, limits still appropriate, copy refreshed
