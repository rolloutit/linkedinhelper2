# Campaigns, Lists, Lead Sources, Exclusions: Detail Reference

Detail layer for `SKILL.md` §1, §3, §4, §7: exact UI paths, verbatim strings, transition
semantics, failure modes. Every block carries its `Source:` line.

## Table of contents

1. [Creating and editing campaigns](#1-creating-and-editing-campaigns)
2. [The list system in full](#2-the-list-system-in-full)
3. [Bunches vs one-by-one processing](#3-bunches-vs-one-by-one-processing)
4. [Campaigns runner](#4-campaigns-runner)
5. [Lead sources in full](#5-lead-sources-in-full)
6. [Adding profiles: all six methods](#6-adding-profiles-all-six-methods)
7. [CSV / URL import](#7-csv--url-import)
8. [Exclusions, blacklist workarounds, deduplication](#8-exclusions-blacklist-workarounds-deduplication)
9. [Tagging system](#9-tagging-system)
10. [Built-in CRM](#10-built-in-crm)
11. [Cloning and porting campaigns](#11-cloning-and-porting-campaigns)
12. [Reference workflows, action by action](#12-reference-workflows-action-by-action)
13. [Duplicate causes and fixes](#13-duplicate-causes-and-fixes)

## 1. Creating and editing campaigns

### 1.1 Exact creation paths
| Situation | Path |
|---|---|
| **Without** the multi-campaign runner plug-in | Open the campaign tab → click `Create campaign` |
| **With** `Multi-campaigns runner plug-in` installed | `Campaigns` menu on the left rail → far right → `+ Create campaign` icon |

The creation dialog has exactly three steps: (1) give the campaign a name, (2) choose a campaign
template, (3) click `Create campaign`. `[LH-CLAIM]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360015754700-How-to-create-a-new-campaign-in-Linked-Helper

### 1.2 Full predefined template list (verbatim) and the workflow each produces

Names are verbatim from the creation dialog. Where the help center publishes the exact action list,
it is reproduced in §12.

| Template (verbatim) | Workflow it produces |
|---|---|
| `Empty campaign` | "a campaign that contains no action at all": you add every action yourself |
| `Invite & Follow Up` | Invite 2nd/3rd → filter to 1st → message → check replies → message → check replies (6 actions; see §12.1) |
| `Messaging Sequence` | Chained `Message to 1st connections` steps separated by `Check for replies` |
| `Export profile information` | Visit & extract → find emails → webhook export (3 actions; see §12.3) |
| `Inmail sequence` | InMail to 2nd & 3rd → check replies → InMail → check replies (4 actions; see §12.2) |
| `Message sequence via event` | Collect event attendees → `Message to event attendees` chain: works only for profiles collected from that event |
| `Message sequence via group` | Collect group members → `Message to group members` chain: works only for profiles collected from that group |
| `Warm-up, invite, and follow-up` | Follow / like / comment warm-up → delay → invite → filter out of network → message → check replies |
| `Invite 1st to follow Organization (Company / School)` | Invites existing 1st connections to follow a company or school page |
| `Invite person to an event` | Invites profiles to a LinkedIn event you own |
| `Invite 1st connections to Group` | Invites existing 1st connections into a group you manage |
| `Endorse 1st connections` | Endorses skills of 1st-degree profiles (one action per profile regardless of skill count) |
| `Like & comment posts and articles` | Engagement-only warm-up workflow against profiles' posts/articles |
| `Follow profiles` | Follow-only workflow (no invite spend) |
| `Invite and reach out via LinkedIn and email` | Invite + LinkedIn follow-ups combined with an email-enrichment/outbound branch |
| `Message chain to warmed-up 1st connections` | Message → check replies → message, against 1st connections only; no invite spend |
| `Send person to Snov.io campaign` | Pushes processed profiles into a Snov.io campaign |
| `Visit & Extract Profiles` | `Visit & Extract profiles` data-collection workflow (heaviest profile-load consumer) |
| `Find profile emails` | `Find Profile Emails` / enrichment workflow, spends Data Credits |
| `Remove 1st connections` | Disconnect hygiene workflow against 1st-degree profiles |
Source: https://support.linkedhelper.com/hc/en-us/articles/360015754700-How-to-create-a-new-campaign-in-Linked-Helper

### 1.3 Editing the workflow
| Operation | Exact path | Constraint |
|---|---|---|
| **Add action** | `Workflow` tab → `+Add action` → Actions menu → `Add` on the desired action | Action must be installed from `Plug-in store` or it is not in the picker |
| **Insert action** | Click the **Plus sign above/below** an existing action | |
| **Delete** | Hover the action → **Delete** | |
| **Reorder** | Hover the action → **move up/down** | **Only when that action's `Queue`/`Processed` lists are empty** |
| **Expand** | Hover the action → **Expand** | Shows the action's sub-lists |
| **Add a delay** | `Delay between actions` is itself an insertable action | |
Source: https://support.linkedhelper.com/hc/en-us/articles/360016470720-Workflow

### 1.4 Degree-ordering rule and auto-insertion

Rule, verbatim in effect: **2nd/3rd-degree actions must precede 1st-connection actions.** Linked
Helper **automatically inserts `Filter contacts out of my network`** between incompatible action
types. `[LH-CLAIM]`

Consequences: any invite action followed by a messaging action gets a network filter whether you
add one or not, and that filter is what moves acceptors forward: do not delete it, or messaging
actions receive still-pending profiles and fail. Because reordering requires empty
`Queue`/`Processed` lists, fix action order **before** collecting; later changes require a clone
(§11).
Source: https://support.linkedhelper.com/hc/en-us/articles/360016470720-Workflow

## 2. The list system in full

A workflow is "basically a sequence of actions, which you set up for your campaign"; profiles move
**top to bottom**. Some template articles describe actions "from the bottom to the top": **read the
workflow UI, not the prose order.** `[LH-CLAIM]`

### 2.1 Campaign-level lists (verbatim names)
| List | Exact meaning |
|---|---|
| `Profiles to process` (a.k.a. Queue) | Entry point: profiles in the first action plus manually added profiles. You can delete / exclude / filter here. |
| `Exclude list` | The **rule** list: "a list of profiles who either were excluded from the campaign at a certain step or those who were excluded before they get to the Profiles to process." |
| `Excluded` | The **result** of applying the rule: the subset that actually was in `Profiles to process` before exclusion. |
| `Processing` | Profiles actively moving through the workflow: all actions except the first, excluding manually added profiles. |
| `Replied` | Profiles that answered. See the caveat in §2.4. |
| `Successful` | Completed the **final** workflow action. |
| `Failed` | Could not be processed (network issue, profile unavailable, etc.). |
| `Processed` | Terminal aggregate = successful + excluded + failed + replied + messaged. |
| `Accepted` | Exists **only** in invite campaigns with network filtering enabled: profiles who accepted invites. |

### 2.2 `Exclude list` vs `Excluded`: the distinction that causes most confusion

Verbatim: **"Exclude is a list that sets the rule: these profiles must NOT be processed during the
campaign, while Excluded is the result of applying this rule."**

You **write into** `Exclude list` (collect / import / copy); you **read** `Excluded` to see who the
rule removed. A profile can sit in `Exclude list` forever without appearing in `Excluded`: that
just means it never entered the queue.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016640219-Linked-Helper-lists-explained

### 2.3 Action-level lists (verbatim names)

`Profiles to process` · `Processed` · `Replied` · `Messaged` · `Successful` · `Skipped` ·
`Failed` · `Excluded`.

| Action list | Exact meaning |
|---|---|
| `Profiles to process` | That action's own queue |
| `Processed` | Aggregate of the terminal sub-lists below |
| `Replied` | Answered before this action processed them |
| `Messaged` | "profiles who received messages before Linked Helper's scheduled send, triggering rejection filters" |
| `Successful` | Action completed for this profile |
| `Skipped` | Manually moved to the next action, **or** could not complete an optional activity such as follow / endorse / comment |
| `Failed` | Could not be processed; **retryable on temporary errors** |
| `Excluded` | Requires the `Exclude list plug-in` to exist as an action-level list |

**Documented flow:** `Profiles to process` → `Processing` → `Processed` → terminal (`Successful` /
`Failed` / `Replied` / `Messaged` / `Excluded`). Everything under `Processed` is terminal for that
action, and at campaign level **`Failed` terminates further campaign processing** for that profile:
a failed profile does not continue down the workflow. `[LH-CLAIM]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360016640219-Linked-Helper-lists-explained
Source: https://support.linkedhelper.com/hc/en-us/articles/360016470720-Workflow

### 2.4 Reply-detection caveat: read this before designing any sequence

Verbatim: **"Linked Helper is NOT continuously monitoring replies to your messages, it checks reply
of a certain profile to the previous message sent via the current campaign ONLY when processing it
via the next messaging action."** `[LH-CLAIM]`

Consequences: (1) a sequence with no `Check for replies` between messages **will** follow up on
people who already answered; (2) the `Replied` list is only as current as the last messaging
action's pass; (3) reply checking is **platform-specific**: no cross-check across LinkedIn / Sales
Navigator / Recruiter (§12.1).
Source: https://support.linkedhelper.com/hc/en-us/articles/360016640219-Linked-Helper-lists-explained

### 2.5 Manual moves and recovery operations

| Operation | Exact path | Effect |
|---|---|---|
| Skip one action for selected profiles | Select profiles in `Queue` → `More` → `Move to next action` | System marks them `Skipped` for that action so they are **not double-processed** |
| Retry failures | Select in `Failed` and retry | Documented as retryable **on temporary errors** only |
| Return exclusions to processing | Excluded profiles "can be returned to processing" | Reverses the exclusion for those profiles |
Source: https://support.linkedhelper.com/hc/en-us/articles/360016640219-Linked-Helper-lists-explained
Source: https://support.linkedhelper.com/hc/en-us/articles/360015589960-How-to-skip-profile-from-being-processed-by-a-certain-Action-of-Campaign

## 3. Bunches vs one-by-one processing

| Mode | When it happens | Behaviour |
|---|---|---|
| **By bunches** | A delaying setting exists on the action (e.g. `Delay between actions`) | The action processes several profiles in sequence before switching |
| **One-by-one** | No delaying action in the way | A single profile passes through consecutive actions until it hits a delaying action |

**Priority rule:** Linked Helper prioritizes **"the last action that has profiles in its 'Queue'"**
so contacts are pushed toward completion rather than piling up at the front of the funnel.
`[LH-CLAIM]`

A workflow whose late actions always hold profiles starves its own first action. If late-stage
follow-ups keep firing while nothing new is invited, this rule is the cause, not a bug.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016640219-Linked-Helper-lists-explained
Source: https://support.linkedhelper.com/hc/en-us/articles/360016470720-Workflow

## 4. Campaigns runner

Campaigns run **sequentially, never in parallel**: it "won't run 2 campaigns simultaneously, it will
run them one after another or switch between them." `[LH-CLAIM]`

### 4.1 Controls

| Control | Path / effect |
|---|---|
| Make campaigns active | `Campaigns` menu → select campaigns → `Start`; individual campaigns can also be started from the hover menu |
| `Start campaigns runner` | Activates all *active* campaigns |
| `Stop campaigns runner` | Halts all and sets statuses to `Queued` |

### 4.2 Statuses
| Status | Meaning |
|---|---|
| `Completed` | No profiles in queue |
| `Queued` | Active, waiting its turn |
| `Sleeping` | Timeout or scheduled start |
| `Stopped` | Manually halted; **excluded from the runner** |
| `Running` | Currently processing |

### 4.3 Priority and switching

- **Priority = the earliest `Start at` time across any action in the campaign.** To prioritize a
  campaign, set `Start At` in its workflow to a **past date**.
- **Switch triggers:** the current campaign goes to sleep, **or** another active campaign has a
  non-empty queue with an earlier `Start at`.
- When a sleeping campaign wakes, the runner **finishes the current `Bunch size` of the other
  campaign** before returning.

### 4.4 Tuning knobs and their practical consequences

| Knob | Default | Consequence |
|---|---|---|
| `Bunch size` | **10 profiles per action** | Bigger bunch = longer uninterrupted hold on the runner |
| `Timeout between bunches` | **1 minute** | Larger timeouts (e.g. 2 hours) **improve campaign switching** |

**Campaign hogging / starvation:** large queues + small timeouts keep one campaign hogging the
runner. Two levers: raise `Timeout between bunches` on the greedy campaign, and back-date a starved
campaign's `Start at`. A campaign left in `Stopped` is excluded from the runner entirely and is never
reached: a starvation cause that looks like a scheduling bug. `[LH-CLAIM]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360016509999-Campaigns-runner
Source: https://support.linkedhelper.com/hc/en-us/articles/9000412073618-Multi-campaigns-runner-plug-in

## 5. Lead sources in full

### 5.1 Regular LinkedIn
| Source | Hard cap / special requirement |
|---|---|
| **LinkedIn Search** | "limited by LinkedIn to **1000 profiles per search request**" `[LI-POLICY]` |
| **My Network page** | All 1st-degree connections; "It's possible to collect them all in one go" |
| **School Alumni** (university pages) | |
| **Company Employees** | Filter + collect staff of an organization |
| **Event attendees** | "My event page" → `Events` → **Networking** tab → `See all` → filter |
| **Groups** | Member lists of groups you belong to; **"No advanced filtering by location, industry, etc."** |
| **Who viewed your profile page** | **Limited results on free subscriptions** |
| **Sent invitations** | Profiles with pending invites |
| **Post likers / commenters** | Offered **only when the post is opened via its own unique URL** (see §5.4) |
| **Followers / Following pages** | |
| **Company page followers** | **Requires admin access to that company page** |
| **Companies search** | **Requires the `Organizations extractor` plug-in** (not installed by default) |

### 5.2 Sales Navigator / Recruiter / external
| Platform | Sources |
|---|---|
| **Sales Navigator** | Advanced search (seniority, tenure, company headcount, posted content), **Saved Leads Lists**, **Saved Searches**, Organizations search, Accounts lists |
| **Recruiter** | **SmartSearch** interface, **Project** pages |
| **External** | CSV / TXT files of LinkedIn URLs; Linked Helper CSV exports (preserve names, headlines, company data); **HTML-saved LinkedIn pages**: the documented workaround for unsupported pages |

Collect flow: "Click campaign name to dive into it and then hit **collect** button" in the left rail.
Source: https://support.linkedhelper.com/hc/en-us/articles/360020650460-How-to-filter-and-collect-profiles-via-Linked-Helper

### 5.3 Collect menu targeting: Campaign list vs Action list

| Target | Behaviour |
|---|---|
| **Campaign list** | Pick an existing campaign from a dropdown or create one from a template; choose sub-list = **`Queue` or `Exclude list`** |
| **Action list** | Pick campaign (or create), then a specific Action in the Workflow; **profiles go only to that action's `Queue`**: **no Exclude-list option** |

Use Action-list targeting to inject profiles mid-funnel (e.g. straight into a messaging step for
existing 1st-degree contacts); since that path has no Exclude option, apply exclusions at campaign
level.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017176100-Collect-menu

### 5.4 Sources not shown by default

Verbatim: "Not every source is displayed by default in the 'Collect' menu. For example, option to
collect post likers or commentators is available **only when you open a post via its direct URL**."

To surface them: **three dots** upper-right of the post → **"Copy link to post"** → open the post by
that link (**"View Post"**, or paste the URL into Linked Helper's address bar) → the `Collect`
dropdown now shows the likers/commentators options. `[UNVERIFIED]` no maximum count, rate limit, or
completeness guarantee is documented.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017176100-Collect-menu
Source: https://support.linkedhelper.com/hc/en-us/articles/360015766440-Is-it-possible-to-collect-those-who-liked-or-commented-post

### 5.5 The six documented reasons profiles get skipped during collection

1. The contact **already exists in a sub-list** of the current Action/Campaign.
2. LinkedIn shows **"LinkedIn Member"** instead of a real name.
3. **Connection/Relationship filters misconfigured.**
4. **3rd-degree filter set** but out-of-network profiles appeared.
5. **New LinkedIn account** with few or no 1st-degree connections.
6. Trying to collect **already-invited profiles** into invite actions.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017176100-Collect-menu

### 5.6 Collection failures (not the same as skipping)

**`"Failed to prepare collecting"`**. Two documented causes: (1) **not logged into LinkedIn**
(session expired / auth failed); (2) **LinkedIn glitch**: corrupted cached JavaScript stops the page
from loading and yielding data. Fix (login): let LH auto-login with saved credentials, or log in
manually via the **`LinkedIn` menu in the left panel**. Fix (cache): **stop the Campaigns runner**
first → **right-click the LinkedIn webpage** inside the instance → **"Reload (and clear cache
option)"** → retry. The same glitch occurs in plain Chrome; if it persists, email
**info@linkedhelper.com**.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015510239-Error-Failed-to-prepare-collecting-occurs

**Unsupported pages.** Verbatim: **"Currently, Linked Helper cannot collect URLs from some pages."**
(Not enumerated.) Workaround A (any page whose HTML contains profile links): open it, **scroll to
load** all desired profiles → **right-click** → **"Save as"** → format **"Web page, Complete"** →
upload the saved **HTML file** via the standard URL-upload function. Workaround B (Messaging page,
advanced): install an **auto-scroll extension**; **Chrome Developer Tools** → **Network** tab with
**"Disable cache"** + **"Preserve log"**, filter **"Fetch/XHR"**, then filter for
**`voyagerMessagingGraphQL`**; scroll all chats; **export the HAR file**, rename it with a **`.txt`**
extension, **replace `\\\"` with spaces** in a text editor, upload the modified file.
Source: https://support.linkedhelper.com/hc/en-us/articles/28438859259282-How-to-collect-profiles-from-unsupported-pages

## 6. Adding profiles: all six methods

| # | Method | Requirement / note |
|---|---|---|
| 1 | Any supported **LinkedIn platform** collection | Needs the matching subscription (Sales Navigator / Recruiter) |
| 2 | **CSV upload / paste links** | "upload profiles into your campaign from a CSV file on your Desktop or paste links", see §7 |
| 3 | **Built-in CRM** | Filter in CRM, select, add to campaign `Queue` **or** `Exclude list` |
| 4 | **Campaign/Action lists** | "add profiles from any step / list of a campaign" |
| 5 | **Post engagement** (likers/commenters) | Requires opening the post by its unique link (§5.4) |
| 6 | **List Manager plug-in** | Copies profiles between campaigns; `Functions` menu, Source/Target campaign selection |

Exact UI paths: campaign `Workflow` tab → click a list **or** the `Add` button · campaign `Lists`
tab → select `Queue`/`Exclude` → `Add contacts` · in any list, the `Add to` button for
cross-campaign copying.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015790859-How-to-add-profiles-to-a-campaign

## 7. CSV / URL import

**Menu path:** Campaign → `Queue`/`Exclude List` → `Add` → `Upload Profiles URLs` tab → choose file
or paste → click `Import`.
"Linked Helper can recognize URLs from almost any CSV formats with any possible delimiters." `[LH-CLAIM]`

### 7.1 Accepted URL formats

```
https://www.linkedin.com/in/williamhgates/
https://www.linkedin.com/in/<encoded-ID>/
https://www.linkedin.com/profile/view?id=<ID>
https://www.linkedin.com/sales/profile/<ID>,<code>,<name>
https://www.linkedin.com/sales/people/<encoded-ID>,<code>,<name>
https://www.linkedin.com/recruiter/profile/<ID>,<code>,<name>
```

**NOT supported (verbatim example from the docs):**

```
https://www.linkedin.com/recruiter/profile/19418076433,PTS,PTS
```

### 7.2 Hard rules
| Rule | Detail |
|---|---|
| **URL-only import** | "Linked Helper will take only URLs ignoring any other data such as first name, last name, tags." Tags and custom fields must be applied separately (§9, §8.6) |
| **No re-upload of known profiles** | Profiles already in `Queue`/`Exclude` lists are not re-uploaded |
| **Malformed URLs silently fail** | Incomplete/edited URLs (missing `https://`, truncated params) will not import |
| **A bare URL is enough** | Sufficient for invites, messaging, endorsing, following, and webhook/Zapier export |

### 7.3 Rate ceiling: CONFLICT

`CONFLICT:` the vendor publishes two incompatible figures for URL-imported profiles per 24 hours.

| Figure | Where |
|---|---|
| **45 profiles per 24 hours**: "maximum 45 profiles per 24 hours" to avoid LinkedIn logouts | Source: https://support.linkedhelper.com/hc/en-us/articles/360015613420-How-to-Upload-Profiles-URLs-into-Linked-Helper |
| **40 per 24 hours**: the `Load LinkedIn profile via URL` advanced limit **default** | Source: https://support.linkedhelper.com/hc/en-us/articles/360015613420-How-to-Upload-Profiles-URLs-into-Linked-Helper |

Do not reconcile. Present both; recommend the conservative **40**: the number the app itself
enforces by default.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015613420-How-to-Upload-Profiles-URLs-into-Linked-Helper

### 7.4 CSV workflow index

| Workflow | Direction | Key detail |
|---|---|---|
| Upload prospect URLs | in | CSV / HTML / TXT of profile URLs into a campaign `Queue` |
| Connection-count filter | out → in | Export, filter `network_info_connection_count` ≥ 500 in Excel, re-upload to `Invite 2nd & 3rd connections` |
| Bulk tagging by URL | in | `Visit and extract` campaign + `Tagging system plug-in` (§9.2) |
| Domain→email resolution | out → 3rd party | 3-column CSV: **`first_name`, `last_name`, `organization_domain`** → Snov.io **Bulk Email Search** |
| Email export | out | Download from **`Successful`**; Snov.io results land in the **`third_party_email`** column |
| Cross-account exclusion | out → in | Export `Queue`, split, upload each slice to other accounts' **Exclude lists** (§8.4) |
| Incremental export ratchet | out | Tag-and-strip via **"With tags"** / **"Without tags"** filters (§8.5) |
| Campaign portability | out → in | `Download` / `Upload campaigns` / `Choose file` / `Import`: settings only, **no profiles** (§11.2) |

**Hard rule:** exports from **`Queue`** contain **no email addresses**: always export from
**`Successful`**. Three documented causes of empty email columns: (1) 2nd/3rd-degree profiles never
run through an email finder: *"E-mails are unavailable on the profile pages of 2nd and 3rd level
contacts"*; (2) 1st-degree profiles not fully extracted: 1st-connection emails require the
**`Visit & Extract profiles`** action specifically, scraping being disabled elsewhere *"for security
purposes"*; (3) *"If you download profiles from Queue, there won't be any email addresses"*.
`[UNVERIFIED]` no hit rates published. **Delimiter choice:** on `Download` you pick **Google Sheets**
or **MS Excel** format.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016685199-Why-don-t-all-contacts-in-a-CSV-file-have-e-mail-addresses
Source: https://support.linkedhelper.com/hc/en-us/articles/360020619780-How-to-extract-emails-of-your-2nd-and-3rd-degree-connections-via-Snov-io
Source: https://support.linkedhelper.com/hc/en-us/articles/360016704160-How-to-invite-only-those-who-have-more-than-500-connections
Source: https://support.linkedhelper.com/hc/en-us/articles/360015581980-How-to-get-emails-of-your-2nd-and-3rd-connections-in-LinkedIn

## 8. Exclusions, blacklist workarounds, deduplication

### 8.1 There is no native global blacklist

Verbatim: **"Linked Helper does not offer a blacklist that would allow skipping all profiles from
any current and new campaigns."** `[LH-CLAIM]`

**Workaround 1: dedicated "Global Exclude" campaign.** (1) Create a campaign with a single action,
e.g. `Visit & Extract profiles`, named e.g. "Global Exclude". (2) Collect the profiles you never want
touched into it. (3) Apply to a new campaign via `Functions` → `List Manager` → Source = "Global
Exclude", Destination = target campaign → **`Add unique`**. Alternative path: `Lists` →
`Exclude list` → `Add contacts` → source `Lists` → select the "Global Exclude" campaign.

**Workaround 2: tag-based.** (1) Install `Tagging system` + `Built-in CRM` plug-ins. (2) Tag
profiles, e.g. tag `Global Exclude`. (3) In a new campaign: `Lists` → `Exclude list` →
`Add contacts` → source `CRM` → filter by the `Global Exclude` tag → `Select all` → `Add contacts`.

Neither is automatic: both must be re-applied to **every new campaign** at creation time.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016522660-Is-there-a-global-Exclude-list

### 8.2 List Manager operations (verbatim)

Install: `Plug-in Store` → `List Manager` → `Install`; access via the **`Functions`** menu.
| Operation (verbatim) | Function |
|---|---|
| **`Add unique`** | Transfers profiles from one campaign/list to another, excluding duplicates |
| **`Delete the same`** | Removes duplicate profiles between lists |
| **`Remove intersections between campaigns`** | Eliminates duplicates across entire campaigns |
| **`Keep the same`** | Retains only matching profiles between lists; removes all others |
Source: https://support.linkedhelper.com/hc/en-us/articles/9058519082642-List-manager-plug-in

### 8.3 Automatic deduplication within a campaign or action

Linked Helper refuses to add a profile that **"is already in the Queue / Processed / Exclude list"**
of the same Campaign or Action. `Processed` covers the sub-lists `Skipped`, `Failed`, `Excluded`,
`Messaged`, `Replied`, `Successful`. View both lists via the **`queue` button** on any action.
`[LH-CLAIM]`

LinkedIn-side backstop for invites: **"LinkedIn itself won't let you send invite twice to the same
person."** `[LI-POLICY]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates
Source: https://support.linkedhelper.com/hc/en-us/articles/360015334960-Will-Linked-Helper-send-invite-to-the-same-person-twice

### 8.4 Deduplication across campaigns and across accounts

**Across campaigns, same account**: `Functions` → `List manager`: set the source campaign in the
`Source` field, the target campaign in the `Target` field, then click **`Remove intersections between
campaigns`**: this copies the source's processed/queued contacts into the target's `Exclude list`.

**By message history**: `Filter by message content` plug-in → campaign → `Message to 1st
connections` → `Message analyzer` → `Filter by message content` → enter phrases in the
**`Previous message phrases`** field; profiles who already got matching content are excluded.

**Across multiple LinkedIn accounts** (no shared database, so entirely manual): *pre-campaign*:
split audiences with LinkedIn's own industry/demographic filters, or collect with one account,
download to CSV, split the file across accounts, upload to secondary accounts and exclude from the
primary; *mid-campaign*: download `Queue`/`Processing`/`Processed` lists from Account A, upload into
Account B's `Exclude list`, then reverse.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates

### 8.5 Tag-based export ratchets: never export the same profile twice

**Method 1: automatic tagging (needs `Tagging system plug-in`).** (1) Open the action (e.g.
`Message to 1st connections`) and configure it to **add a tag** to successfully processed profiles
(e.g. `new`). (2) Go to the **`Successful`** sub-list and select the profiles. (3) **Download** to
CSV via the standard export. (4) **Remove the tag:** click the **bin** icon next to it and confirm
removal from the downloaded profiles. (5) **Ongoing:** only untagged profiles receive the `new` tag,
so filter the **"With tags"** field to `new`, download that batch, remove the tag, repeat.

**Method 2: manual post-export tagging (no plug-ins).** (1) In **`Successful`**, **select all** →
**`Tag`** button → add a label (e.g. `exported`). (2) **Download** the tagged profiles to CSV.
(3) Return to `Successful` and put `exported` into the **"Without tags"** field: only untouched
profiles remain visible. (4) Download those, tag them `exported`, repeat.

Key UI labels: sub-list **`Successful`** · filter fields **"With tags"** / **"Without tags"** ·
button **`Tag`** · **bin** icon to remove a tag.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016661299-I-extracted-exported-LinkedIn-profiles-and-want-to-export-new-without-already-extracted

### 8.6 Skipping one action for one profile

Select profiles in `Queue` → `More` → `Move to next action`; they land in `Skipped` for that action
and are not double-processed.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015589960-How-to-skip-profile-from-being-processed-by-a-certain-Action-of-Campaign

### 8.7 CRM profiles cannot be deleted: only hidden

Deletion is impossible. Documented procedure: (1) install the **`Tagging system plug-in`**; (2) tag
the profiles **`deleted`**; (3) apply a **"Without Tags"** filter to hide them; (4) optionally use
the `deleted` tag to add them to an **Exclude list** (needs the `Exclude list` plug-in) so no
campaign reaches them.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015485399-Can-I-delete-profiles-from-CRM

## 9. Tagging system

### 9.1 What it does

Install from `Plug-in Store`; a **`Tags` tab appears in every Action's settings**. Tags apply
automatically **"to all successfully processed profiles in certain Action"**; manual tagging works on
a whole list or on selected profiles. Tags are **filterable in the CRM** and exported in the
**`tags`** field. `[LH-CLAIM]`

Tags are the only cross-campaign, cross-list attribute LH exposes, so they are the de-facto state
machine for what the list system cannot express: global blacklist (§8.1 method 2), export ratchet
(§8.5), soft-delete (§8.7), cohort labels. One tag per state; strip it when the state ends.
Source: https://support.linkedhelper.com/hc/en-us/articles/9041914183698-Tagging-system-plug-in

### 9.2 Bulk-tagging from a CSV of profile URLs

Prerequisites: a CSV of LinkedIn profile URLs; `Tagging system plug-in` installed; profiles already
stored in the CRM.
1. **Create a new campaign** from the **"Visit and extract"** template.
2. **Upload the profiles** from your CSV into the `Queue`; the system matches URLs against CRM entries.
3. **Verify mapping.** Uploaded profiles should display mapped CRM information. If they don't, they
   are either not in the CRM yet or stored under a different URL form (standard vs recruiter URL).
   **Fix:** visit the profiles so Linked Helper can scrape complete information.
4. **Install** the `Tagging system plug-in` if not already present.
5. **Apply tags:** select all profiles in the campaign, add the tag(s) via the tagging interface.
6. **Clean up:** delete the campaign action after tagging, or repurpose it.

Caveat (verbatim): *"This method cannot guarantee all profiles will be found by URL if the CSV file
was downloaded from a different Linked Helper instance"*: profiles can have multiple URL formats.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016738299-Is-it-possible-to-tag-multiple-contacts-in-my-list-based-on-a-CSV-file-with-URLs

## 10. Built-in CRM

The `CRM` menu is the central database of **every profile ever collected**; you can filter and act,
but **no processing happens there**: that only happens inside campaigns.

**CRM profile card, eight sections:**
| # | Section | Contents / limits |
|---|---|---|
| 1 | **General Information** | `First Name`, `Last Name`, `Position`, `Company`, `Headline`, `Relationship`, `Connection date`. Editable: First Name, Last Name, Company, Position (**only if LH already scraped that data**). Buttons: add to campaign, download CSV, exclude from campaign |
| 2 | **Campaign Data & Messaging History** | Processing timeline, platform source, sent messages, received replies; campaign name is clickable; multiple chat threads with the same profile are visible |
| 3 | **Profile IDs** | `LH ID`, `LinkedIn Member ID`, `LinkedIn Public ID`, `Sales Navigator Hash ID`, `Recruiter Member ID`; buttons **`Show In`** (open profile) and **`Scrape from`** (re-scrape all data) for LinkedIn / Sales Navigator / Recruiter |
| 4 | **Industry & Summary** | Industry is populated **only from Sales Navigator** |
| 5 | **Personal Information** | Premium / Influencer / Open Link status, email, website, connections count, followers, birthday |
| 6 | **Linked Helper's Profile Data** | `Notes` field; `Tags` (needs Tagging system plug-in); custom variables (needs Custom template variables plug-in). **Campaign- and Action-level custom fields are visible only when you navigate in from that same Campaign/Action** |
| 7 | **Mutual Connections** | Selectable for use in message templates |
| 8 | **Experience, Education, Skills, Languages** | |

**Filtering / adding to campaigns:** filter in the CRM, select profiles, add to a campaign `Queue`
**or** `Exclude list` (method 3 in §6). Tag filters (`"With tags"` / `"Without tags"`) are the
primary segmentation mechanism (§8.5, §8.7).

**Limits:** all visible CRM data exports to CSV including messages and replies, but profiles
**cannot be deleted, only hidden** (§8.7); the CRM performs no outreach of its own; Industry is
Sales-Navigator-only.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601579-CRM-profile-s-card
Source: https://support.linkedhelper.com/hc/en-us/articles/9058416998034
Source: https://support.linkedhelper.com/hc/en-us/articles/9003176158226

## 11. Cloning and porting campaigns

### 11.1 Clone within the same account

1. Go to the **`Campaigns`** menu → open the campaign → click the **`Clone`** button.
2. In the popup: name the copy, and choose profile handling, **"Exclude profiles from the current
   campaign"** or **"Copy Exclude list from the current campaign into a new one"**.

**What is copied:** **"all actions, action settings, and message templates from the original
campaign"**: **profiles in the `Queue` are NOT copied.** The clone and the original are **"two
separate instances and do not depend on each other."**

Because reordering requires empty `Queue`/`Processed` lists (§1.3), cloning is the documented way to
change a running campaign's action order: clone, reorder in the empty clone, then feed it.

`[UNVERIFIED]` no built-in A/B split-test or per-variant statistics feature is documented. For an
A/B arm, clone within one account, change **one** variable (message variant, delay, warm-up
presence), and use **"Exclude profiles from the current campaign"** so the arms draw from disjoint
audiences. Spintax, message variations and IF-THEN-ELSE randomize but do **not** report per-variant
performance.
Source: https://support.linkedhelper.com/hc/en-us/articles/360019349660-How-to-duplicate-clone-a-campaign-or-copy-it-to-another-LinkedIn-account

### 11.2 Copy to a different LinkedIn account

Prerequisites: **`Multi-campaigns runner plug-in`** installed on **both** accounts; Linked Helper
version **> 2.54.27**.
1. Open the campaign to clone → click the **`Download`** button in the upper-right corner.
2. Select the settings, then click **`Download`**.
3. On the **target** account: **`Upload campaigns`** → **`Choose file`** → select your file →
   **`Import`**.

**Critical limitation (verbatim):** *"Linked Helper does not move profiles to avoid reaching out to
the same leads using different LinkedIn accounts."* You must manually download and re-upload profiles
if you genuinely want them moved, and if you do, apply the cross-account exclusion procedure in
§8.4 so two accounts do not touch the same person.
Source: https://support.linkedhelper.com/hc/en-us/articles/360019349660-How-to-duplicate-clone-a-campaign-or-copy-it-to-another-LinkedIn-account
Source: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper

## 12. Reference workflows, action by action

### 12.1 `Invite and follow-up`: 6 actions

```
1. Invite 2nd and 3rd level contacts
2. Filter contacts out of my network (keep 1st level only)
3. Message to 1st connections
4. Check for replies
5. Message to 1st connections
6. Check for replies
```

Configured at creation: invitation message template · **auto-canceller settings** to withdraw
unaccepted invitations periodically · follow-up messaging for accepted connections · additional
follow-ups for non-responders. Behaviour notes:
- **Action 2** moves acceptors forward; rejects/pending stay in the queue for a **~1-hour recheck**.
  An optional plug-in auto-accepts incoming invites.
- **Action 3** excludes prior responders by default: change this in the `Message analyzer` tab.
- **`Check for replies`** monitors for a set number of days; non-responders move to `Successful`
  (final) or the next action. **A final `Check for replies` defaults to "never" (checks
  indefinitely); it auto-switches to a 1-day delay if you append another action.**
- Reply checking is **platform-specific**: no cross-check across LinkedIn / SN / Recruiter.
- Before launching, the `Queue` list lets you exclude, delete, tag, or download profiles.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016430260-How-to-invite-2nd-and-3rd-connections-and-send-a-follow-up-message-Invite-and-follow-up-template

### 12.2 `Inmail sequence`: 4 actions (2-message version)

```
1. InMail to 2nd & 3rd contacts
2. Check for replies
3. InMail to 2nd & 3rd contacts   (follow-up; requires the first message to have been accepted)
4. Check for replies
```
Source: https://support.linkedhelper.com/hc/en-us/articles/360016380079-How-to-send-InMails-to-2nd-3rd-connections-in-LinkedIn-Sales-Navigator-or-Recruiter-InMail-sequence-template

### 12.3 `Export profile information`: 3 actions

```
1. Visit & Extract profiles     (job history, skills, languages, emails, company data)
2. Find Profile Emails          (LH Email Finder / Snov.io / Apollo for 2nd & 3rd)
3. Send person to webhook       (HubSpot, Salesforce, Zapier, etc.)
```
Source: https://support.linkedhelper.com/hc/en-us/articles/10669732514578-Export-profile-information

### 12.4 `Employees extractor`: 3 stages

```
1. Organizations extractor / company search collection
2. Employees extractor  (visits each company People tab; keyword + per-company cap)
3. -> Queue of the target campaign named in the action settings
```

Stage 3 is **not** an action in this campaign: the extractor writes into the `Queue` of whichever
campaign is named in the action settings. Create the destination campaign first.
Source: https://support.linkedhelper.com/hc/en-us/articles/22067310525074-Employees-extractor-template

## 13. Duplicate causes and fixes

**Symptom:** the same profile appears twice, or gets processed twice.

| Cause | Fix |
|---|---|
| **Same person collected from different platforms** (LinkedIn vs Sales Navigator) produces **different profile IDs** | None needed: these **merge automatically** once Linked Helper scrapes the profile page |
| **Overlap between two campaigns on the same account** | Install the **`Lists Manager`** plug-in (Plug-in Store) → select the **source** campaign → select the **target** campaign → click **"Remove intersections between campaigns"** |
| **Overlap across multiple LinkedIn accounts, before launch** | Download profiles from the campaign `Queue`, split the CSV across accounts, then upload each account's URLs into the **Exclude list** of the other accounts' campaigns |
| **Overlap across multiple LinkedIn accounts, while running** | Manually download the `Queue`/`Processing`/`Processed` lists from one account and upload them into the other account's campaign **Exclude list** |
| **Same message text sent twice** | `Filter by message content` plug-in: set the **`Previous message phrases`** field to text the prospect already received; the action then refuses to resend identical content |
| **Expecting a cross-account campaign copy to carry its audience** | It never does, by design: *"Linked Helper does not move profiles to avoid reaching out to the same leads using different LinkedIn accounts."* Move profiles manually (§11.2) |

**Already prevented automatically on a single account** (§8.3): LH **"does not collect duplicates
into the same Campaign or Action if a profile is already in the Queue / Processed / Exclude list."**
Action-level lists covered: `Queue`, `Processed` (`Skipped`, `Failed`, `Excluded`, `Messaged`,
`Replied`, `Successful`); campaign-level: `Queue`, `Exclude list`. LinkedIn-side invite backstop:
**"LinkedIn itself won't let you send invite twice to the same person."** `[LI-POLICY]`
Source: https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates
Source: https://support.linkedhelper.com/hc/en-us/articles/360015334960-Will-Linked-Helper-send-invite-to-the-same-person-twice
Source: https://support.linkedhelper.com/hc/en-us/articles/360019349660-How-to-duplicate-clone-a-campaign-or-copy-it-to-another-LinkedIn-account
