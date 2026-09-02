# Linked Helper 2 — Action, Plug-in and Menu Reference

Detail layer for `SKILL.md`. Sources are verbatim official help-center URLs (Program overview category + User manual §7), verified 2026-09-01. Tags: `[LH-CLAIM]` vendor claim, unverified · `[LI-POLICY]` LinkedIn's own rule · `[COMMUNITY]` · `[UNVERIFIED]` not documented, never assert · `CONFLICT` two incompatible official figures, both shown.

## Table of contents

1. [How the plug-in system works](#1-how-the-plug-in-system-works)
2. [Action catalogue](#2-action-catalogue) — [2.1 invitation/connection](#21-invitation--connection-actions) · [2.2 messaging](#22-messaging-actions) · [2.3 engagement/warm-up](#23-engagement--warm-up-actions) · [2.4 invite-to-entity](#24-invite-to-entity-actions-org--event--group) · [2.5 data/scraping/enrichment](#25-data--scraping--enrichment-actions) · [2.6 AI](#26-ai-actions) · [2.7 export/integration](#27-export--integration-actions)
3. [Action-extension plug-ins](#3-action-extension-plug-ins)
4. [Message-action extension plug-ins](#4-message-action-extension-plug-ins)
5. [CRM-category and Campaigns-category plug-ins](#5-crm-category-and-campaigns-category-plug-ins)
6. [Menu reference](#6-menu-reference) — [6.1 Instance menus](#61-instance-menus) · [6.2 Settings sub-menus](#62-instance-settings-sub-menus) · [6.3 Launcher menus](#63-launcher-menus)
7. [Cross-cutting selection tables](#7-cross-cutting-selection-tables)
8. [What is NOT documented](#8-what-is-not-documented)

---

# 1. How the plug-in system works

*"In Linked Helper, most of the features are implemented in a form of plug-ins - small components that add a specific feature to the tool."* They *"can be easily installed and uninstalled at any time."* Once enabled, a plug-in *"becomes available for any LinkedIn account instance added to the Linked Helper account"* — **scope is account-wide, not per-instance**. Install path: `Plug-in store` menu → per-plug-in **`Install`** button.

| Category | Count | Holds |
|---|---|---|
| `Action` | 23 | primary workflow actions — the entries in the `+Add action` picker |
| `Action extension` | 9 | per-action add-on tabs (`Override platform`, `Postpone action start`, delays, `Action working hours`) |
| `Message action extension` | 6 | message-editor / message-analyzer add-ons (IF-THEN-ELSE, custom variables, images, filters) |
| `CRM` | 3 | `Built-in CRM`, `Inbox`, `Tagging system` |
| `Campaigns` | 4 | `Campaign Information`, `Multi-campaigns runner`, `Exclude list`, `List manager` |
| `Other` | 3 | account-level functions (`Accept incoming invitations`, `Sent invites canceller`, …) |

Most action plug-ins are **enabled by default**. The **documented exception is `Organizations extractor`**, which *"is not available in a Campaign by default"* and must be installed manually. Actions are added on the campaign's **`Workflow`** tab via the **`+Add action`** button (*"a plus sign button"*).

| Tab / injected control inside an Action | Appears when |
|---|---|
| `General` | always |
| `Message` | messaging actions, and `Invite 2nd and 3rd level contacts` |
| `Message analyzer` | messaging actions |
| `Advanced settings` | the matching per-action advanced-settings plug-in is installed (Invite / Filter-out-of-network / Check for replies); also the injection point for `Filter by message content` and `Ignore generic replies` |
| `Delay settings` | `Action steps delays plug-in` |
| `Tags` | `Tagging system plug-in` |
| `Options` | `Data Enrichment` action only |
| `Auto accept incoming invites` | `Auto accept incoming invites for Filter contacts out of my network…` plug-in |
| `Automatic sent invites canceller` | `Automatic sent invites canceller for Filter contacts out of my network…` plug-in |
| `Organization` | `Send person to external CRM` action |
| `Override platform` selector (in `General`) | `Override platform plug-in` |
| `Start at` postponement (in `General`) | `Postpone action start plug-in` |
| custom schedule (right side of the action) | `Action working hours plug-in` |

Source: https://support.linkedhelper.com/hc/en-us/articles/360016844320-Plug-in-store
Source: https://support.linkedhelper.com/hc/en-us/articles/10522915555858-Plug-in-store-menu

---

# 2. Action catalogue

## 2.1 Invitation / connection actions

### `Invite 2nd and 3rd level contacts`
Sends connection invitations, with or without a note, to **2nd- and 3rd-degree** contacts; once accepted, unlimited messaging becomes possible. Sales Navigator "Out of network" profiles are invitable via regular LinkedIn. Tabs: `General` (*"Install additional plug-ins to enhance the action"*) · `Message` — the note is **optional** (*"Invitation message not mandatory"*, may be blank). Collection platform (Basic LinkedIn / Sales Navigator / Recruiter) sets the processing platform unless overridden.
Free LinkedIn `[LI-POLICY]`: *"monthly limit of personalized invitations is 10 invites with text messages per month"*; delete the note or buy a paid subscription for more.
**CONFLICT — allowance without a note:** *"up to 800 invites monthly"* vs *"~10 invites/month with text for non-Premium; up to 200/week without text"* — both from the vendor; quote both, never reconcile.
Gotcha: if the profile already invited **you**, *"Linked Helper accepts their invitation instead, moving profile to Successful list (no failure/skip)"*. Plug-ins: `Override platform` · `Advanced settings for Invite 2nd and 3rd level contacts` · IF-THEN-ELSE · `Custom template variables` · `Tagging system` · `Postpone action start` · `Action steps delays`. Auto email lookup spends Data Credits.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016894599-Invite-2nd-and-3rd-level-contacts

### `Advanced settings for Invite 2nd and 3rd level contacts plug-in`
Adds an `Advanced settings` tab: *"save profiles as leads when processing them in Sales Navigator or send invitation anyway even if profile email is required."* Exact labels: `Check 'Save as lead' checkbox on the invitation popup in Sales Navigator` — **YES / NO** (needs Sales Navigator) · `If email required add email from the custom field` (enter the column name; needs `Custom template variables`) · `Get email from LH Email Finder if an email is required` (requires agreeing to *"contribute your LH CRM profiles data"*; spends Data Credits) · `Get the profile's email from snov.io for inviting` · `Get the profile's email from Apollo.io` (needs a *"master API key (or a key with 'api/v1/people/match' scope enabled)"*).
Gotcha: *"In case all sources are enabled, Linked Helper prioritize them in the order they appear in the settings tab, and if email is found not in the last option, then Linked Helper won't check other sources."*
Source: https://support.linkedhelper.com/hc/en-us/articles/9060332257298-Advanced-settings-for-Invite-2nd-and-3rd-level-contacts-plug-in

### `Filter contacts out of my network (keep 1st level only)`
Determines which queued profiles are now **1st-degree** by scrolling your "My Network" page and matching — it does **not** visit profiles individually. Accepted → `Successful`; not yet accepted stay in `Queue`. The standard acceptance gate in invite→follow-up funnels; LH auto-inserts it between incompatible action degrees. `General` tab: `Timeout between checks`, optionally *"limit an action to 50 profiles per day"*. Minimum timeout **10 minutes** (*"not possible to set timeout between checks to be less than 10 minutes"*); cycle default **60 minutes**. Gotcha: frequent triggering *"may attract LinkedIn attention"*. No licence or subscription gating.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016872779-Filter-contacts-out-of-my-network-keep-1st-level-only

### `Advanced settings for Filter contacts out of my network (keep 1st level only) plug-in`
Controls scroll depth on "My network" — matters most for CSV-uploaded profiles. `Check for newly added contacts until:` — `Previously added found` (**default**, scrolls until the latest already-processed profile is located) or `First invite date` (scrolls until a profile accepted on the invite date of the oldest queued profile). `Scroll down to` — *"rarely requiring adjustment"*, leave unchanged.
Gotcha: with the default, CSV-uploaded profiles whose invites were accepted *before* the previously found contact **can be missed** → use `First invite date` for CSV lists.
Source: https://support.linkedhelper.com/hc/en-us/articles/9060660347538-Advanced-settings-for-Filter-contacts-out-of-my-network-keep-1st-level-only-plug-in

### `Auto accept incoming invites for Filter contacts out of my network (keep 1st level only) plug-in`
Adds an `Auto accept incoming invites` tab to the Filter action. Before the Filter runs, it accepts **incoming** connection requests, but **only** from profiles previously added to the same campaign; all others are ignored. The tab has an enable switch; no further field labels published **[image-only]**.
Source: https://support.linkedhelper.com/hc/en-us/articles/9061021568786-Auto-accept-incoming-invites-for-Filter-contacts-out-of-my-network-keep-1st-level-only-plug-in

### `Automatic sent invites canceller for Filter contacts out of my network (keep 1st level only) plug-in`
Adds an `Automatic sent invites canceller` tab to **every** Filter action: *"Automatically cancels all pending invitations that are older than X days."* Cancelled invites leave the queue for **`Failed`** with the error `The invitation was canceled.` Default threshold **30 days**; checks run *"once every hour"*; guidance keep *"less than 1,000 pending invitations"*, recommended deletion window *"2-3 weeks"* `[LH-CLAIM]`. The "X days" field label is **[image-only]**. Only cancels profiles invited **via the current campaign** — not profiles collected from the Sent invites page.
Gotcha: `The invitation was canceled` is *"predefined behaviour"* and signals normal operation, **not** a campaign failure — do not troubleshoot it.
Source: https://support.linkedhelper.com/hc/en-us/articles/9001738277650-Automatic-sent-invites-canceller-for-Filter-contacts-out-of-my-network-keep-1st-level-only-plug-in

### `Accept incoming invitations plug-in` — a **function**, not an action
Bulk-accepts connection requests via the invitation manager, newest → oldest. Installs into the **`Functions`** menu. Settings: *"There any no settings for this function at all."* [sic] Cannot run simultaneously with campaigns; cannot accept selectively by date range; *"doesn't accept invitations to groups or organizations"*.
Gotchas: accepts **ALL** invitations unless you manually ignore unwanted ones first. *"Not included in daily statistics and doesn't affect daily limits."*
Source: https://support.linkedhelper.com/hc/en-us/articles/360019260080-Accept-incoming-invitations-plug-in

### `Sent invites canceller plug-in` — a **function**, not an action
Withdraws pending invitations sent **before a specified date**. Installs into the **`Functions`** menu. Single control: a **date field** — *"There are no other settings for this function except the date before which the pending invites will be deleted."* `[LI-POLICY]` after withdrawal *"you won't be able to resend an invite to the same recipient for up to three weeks"* (21-day minimum). Recipients get **no** notification; reminder emails stop immediately. While it runs, embedded-browser browsing is blocked. For unattended operation use the `Automatic sent invites canceller…` plug-in instead.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016922519-Sent-invites-canceller-plug-in

### `Remove from 1st connections`
Disconnects selected **1st-degree** contacts. *"There are no special settings for this Action, but you can always enhance it with available plugins."* Relevant ceiling `[LI-POLICY]`: LinkedIn's **30,000** 1st-degree connection limit. Has its own `Remove from 1st connections` per-activity limit in `Settings → Limits`. Plug-ins: `Tagging system` · `Postpone action start` · `Action steps delays` · `Override platform`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016778419-Remove-from-1st-connections

## 2.2 Messaging actions

### `Message to 1st connections`
*"used to send messages to 1st connections… for both sellers and recruiters who want to message their existing network"* — the workhorse follow-up/broadcast action. **1st degree only**, on *"1st level connections in regular LinkedIn, Sales Navigator, and Recruiter"*. `Message` tab: **Subject line only when sending via Recruiter**; template with images. `Message analyzer` tab, three rejection rules: `Reject if a contact replied after #` (*"If a reply is found, Linked Helper won't send a message to that person"*; needs a prior Invite/Message action above it) · `Reject if you messaged a contact after #` · `Reject if you or LH messaged a contact after connection date`. Reply detection adds a **`Replied` sub-list**.
Reply/history checking is **single-platform**: *"checks for replies or sent messages to the profile only in one platform… does not check messaging history in several platforms"*. Licence: **messages with attached images are Standard-capped at 20/24 h**; **messaging-history export via CSV or webhook is PRO only**.
Gotchas: duplicate guard — *"Linked Helper won't send a message if the last message is exactly the same as the one you're about to send"*; *"message history is checked only once"* per profile. Recruiter: message requests block follow-ups in the same thread until accepted, and *"Linked Helper does not create a new message requests"*.
Plug-ins: `Filter by message content` · `Ignore generic replies` · `Send replied to Webhook` · IF-THEN-ELSE · `Custom template variables` · `Attach personalized images` · `Tagging system` · `Postpone action start` · `Action steps delays` · `Override platform`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016659500-Message-to-1st-connections

### `InMail to 2nd & 3rd contacts`
Sends **InMails** to **2nd/3rd-degree** contacts without connecting — *"a must-have for recruiters"*. `Message` tab: **Subject line is mandatory** + template. `General` tab: `Keep attempts to send InMails even if you're out of LinkedIn InMail credits` (checkbox, **regular LinkedIn only**).
Subscription: paid InMails normally require **LinkedIn Premium**; *"a Sales Navigator subscription alone also enables InMails"* even without Premium. **Free InMails** go to *"Open link profiles"* (**2nd degree only**) — filter for Open profiles to exploit this. On Sales Navigator, paid InMails go only via Sales Navigator. On Recruiter, 1st-degree messages are called "InMails" and cost nothing. Credits are allocated by subscription; balance on the *"Premium subscription page"*.
Characters: subject **200**. **CONFLICT — body:** *"Body: up to 2000 characters"* vs the message-templates article's **1,900**. Use 1,900 as the working figure and state both. The signature counts toward the total.
Gotchas: after **4 consecutive** `Out of InMail credits` errors the campaign **pauses 4 hours** unless the override checkbox is on. A Sales Navigator user targeting a regular-LinkedIn profile gets `Incorrect platform` → fix with `Override platform`. `Replied` is a **campaign endpoint** regardless of remaining actions. Free-InMail Open-Profile flow: no reply in the period + request accepted → `Successful`, workflow continues.
Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601420-InMail-to-2nd-3rd-contacts
Source: https://support.linkedhelper.com/hc/en-us/articles/360016380079-How-to-send-InMails-to-2nd-3rd-connections-in-LinkedIn-Sales-Navigator-or-Recruiter-InMail-sequence-template

### `Message to group members`
Messages **2nd/3rd-degree** contacts in the **same LinkedIn group** as you — a documented way to *"overcome LinkedIn weekly invitation limit"*. **Group membership required, not ownership.** `Message` tab: template. `Message analyzer`: `Reject if a contact replied after #`, `Reject if you messaged a contact after #`. Licence: **Standard caps this at 20 actions per 24 h**; unlimited on PRO. Gotcha: reply detection requires *"another 'Message to group members' action above current action"*. No character limit published in this article `[UNVERIFIED]`. Plug-ins: IF-THEN-ELSE · `Custom template variables` · `Attach personalized images` · `Filter by message content` · `Ignore generic replies` · `Send replied to Webhook` · `Tagging system`.
Source: https://support.linkedhelper.com/hc/en-us/articles/5714464724754-Message-to-group-members

### `Message to event attendees`
Messages LinkedIn **event** attendees regardless of degree; bypasses weekly invitation limits. Attendees must be collected first. `Message` tab: template. `Message analyzer`: `Reject if a contact replied after #`, `Reject if you messaged after #`; reply detection adds a `Replied` sub-list. Published constraint `[LI-POLICY]`: *"LinkedIn allows you to send messages to your 3rd-degree connections only"*. Reply detection needs another messaging action above this one. Licence: **Standard caps this at 20 actions per 24 h**. Gotcha: images only work *"in a follow-up after initial message request was accepted"*. Plug-ins: IF-THEN-ELSE · custom variables · personalized images · message filtering · webhook · tagging · delays · platform override.
Source: https://support.linkedhelper.com/hc/en-us/articles/4413984987026-Message-to-event-attendees

### `Check for replies`
Monitors replies to messages sent by **any** campaign action. Non-repliers advance; repliers route to `Replied`. `General` tab: **Timeout between checks for replies**. `Message analyzer` tab: `If no replies are found, move the contacts to Successful list` with a specific delay (days/hours) or **`never`**. Default interval **3 hours**; **minimum timeout 1 hour**; first run scrapes *"Last 200 messaging chats"*; searches up to **40 profiles per queue check**. Single-platform only.
Gotchas: *"LinkedIn marks unread messages as read"* when LH opens threads — mitigate with `Settings → Actions → Leave responses unread when checking for replies`. *"Check for replies automatically disables 'Other' section in your LinkedIn Messaging inbox."* Replied profiles reach the workflow endpoint unless manually overridden.
Plug-ins: `Advanced settings for Check for replies` · `Send replied to Webhook` · `Ignore generic replies` · `Override platform` · `Tagging system` · `Postpone action start`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017905660-Check-for-replies

### `Advanced settings for Check for replies plug-in`
Adds a section to the **`Message analyzer`** tab, changing behaviour for **non-1st-degree** contacts messaged via InMail/group/event so an *accepted message request* counts as engagement. `Treat events 'Message Request Accepted' as replies:` — **Yes / No** (Yes → contacts move to `Replied` on acceptance, no text reply needed). `Keep in queue permanently if request is not accepted:` — **Yes / No** (Yes → contacts stay queued until they reply or accept). Both apply **only** outside 1st degree and rely on LinkedIn's technical `Message Request Accepted` notification.
Source: https://support.linkedhelper.com/hc/en-us/articles/9078280138258-Advanced-settings-for-Check-for-replies-plug-in

### `Scrape messaging history`
Finds the chat with a profile and exports **all** its messages into the Linked Helper Inbox, scrolling to *"the very beginning of the messaging history"*. Use for profiles *"never processed in Linked Helper"* before, e.g. to decide which campaign to assign a lead to. *"By default, no extra options are available."* Reviewing results in the built-in Inbox requires the **`Inbox` plug-in**. Licence: **CSV export of messaging history is *"available for PRO license only."*** Gotcha: processes profiles in the platform where they were collected unless overridden. Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/9025165336978-Scrape-messaging-history

## 2.3 Engagement / warm-up actions

### `Follow / unfollow profiles` *(article H1 reads "Profiles Auto-Follower" — same action)*
*"Following someone on LinkedIn allows you to see the person's posts and articles on your homepage without being connected to them."* A warm-up touch that notifies the prospect. `General` tab: toggle **`Follow`** / **`Unfollow`**. Primarily **2nd/3rd degree** — *"you already follow your 1st-degree connections by default, so there is no sense in processing your 1st degree connections"* (unless unfollowing). No Premium or PRO gating stated. Own `Follow / Unfollow profiles` limit in `Settings → Limits`. Gotcha: *"if profile cannot be followed, Linked Helper will put it into the 'Skipped' list and then to the next action"*. Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016777979-Follow-unfollow-profiles

### `Like and comment posts and articles`
Likes and optionally comments on posts/articles from the target's **Activity** page. Works for 1st and 2nd/3rd degree. `General` tab, exact strings: `Select how many posts and articles will be liked` (posts and articles set **independently**; doc example *"like 2 posts and 2 articles"*) · `Set Linked Helper up to ignore articles/posts older than X days` · `Enable commenting option to add a comment to the post or article` · `Template for post comments` (*"supports generic comments generated from template variations"*) · `AI-generated comments` (*"AI model creates unique comment based on the post content"*; options **tone**, **length**, **language**, optional **goal**).
Credits: **AI comments consume AI credits.** Licence: **Standard caps this at 20 actions per 24 h**; the `Settings → Limits` activity is `Post liking` and it counts **liked posts, not profiles processed**. Comment character limit **1,250** (message-templates article).
Gotchas: skips already-liked posts and moves to the next unliked item. **Comments only happen after a like** — *"Setting 0 likes prevents commenting."* Insufficient content → `Skipped` (or `Failed` if this is the final action). No posts/articles → skip to the next profile.
Source: https://support.linkedhelper.com/hc/en-us/articles/360018627020-Like-and-comment-posts-and-articles
Source: https://support.linkedhelper.com/hc/en-us/articles/10923541013394-Like-and-comment-posts-and-articles-template

### `Boost post`
Mentions (tags) queued profiles in **comments** on a specified post/article to raise its reach. `General` tab, exact strings: `Paste the direct URL to the post you'd like to boost` (via the post's three-dot menu → `Copy link to post`) · `Select how many profiles are to be mentioned in one comment` — **default 10** · `Set up a message if needed (optional) to add a comment to the post` (text optional; mentions alone suffice). Arithmetic: 100 queued profiles ⇒ 10 comments at the default; set 5 ⇒ 20 comments. For a post inside a group, **both** you and the mentioned profile must be group members. Licence: **Standard caps this at 20 actions per 24 h**; the limit name is `Mention person in comment`.
Gotchas: **no dedupe** — *"if a profile in the Queue was already mentioned by you in the comment under the post manually or automatically, then Linked Helper will process it anyway and mention it in another comment the second time"*. LinkedIn Pulse **articles** cannot be liked directly; find a post that mentions the article. Plug-ins: `Tagging system` · `Postpone action start` · `Action steps delays` · IF-THEN-ELSE · `Custom template variables`.
Source: https://support.linkedhelper.com/hc/en-us/articles/13876361925778-Boost-post

### `Endorse my contacts`
Endorses skills of **1st-degree** connections; *"Between 10-30% reciprocate."* `[LH-CLAIM]` Endorse Mode: **`First`** (*"endorse first X skills"*, falling through to later skills if the first are already endorsed — doc example: three already done → it endorses the *"4th, 5th, and 6th"*) · **`Specified`** (*"endorse the specified skill(s)"*) · **`All`** (*"endorse every skill which is not endorsed yet"*). In `Settings → Limits`, `Endorse my contacts` counts **per profile = 1 action** regardless of skill count; no maximum skill count published `[UNVERIFIED]`.
Gotchas: specified skill missing → `Successful` **without** endorsing. No skills at all → `Successful`. Profile blocks endorsements → `Skipped`. The action does not pre-verify skill count or endorsement history. Plug-ins: `Tagging system` · `Postpone action start` · `Action steps delays` · `Override platform`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016778159-Endorse-my-contacts

## 2.4 Invite-to-entity actions (org / event / group)

### `Invite to follow organization`
Invites your **1st-degree** connections to follow a company page. `General` tab: organization identifier or URL (required) — accepts `https://www.linkedin.com/company/[identifier]/`, a public ID, or a numeric company ID. `[LI-POLICY]` the page must have **5,000 or fewer followers** and have *"basic information"* filled in for the `Invite connections` button to be active. Page **admins** get *"monthly invitation credits which are shared across all Admins"*; for non-admins the limits are *"shared across all such pages"*. Credits reset monthly. Licence: **Standard caps this at 20 actions per 24 h**.
Gotchas: because credits are finite, docs *"recommend adding this action at the end"* of a workflow. Missing first/last name → LH visits the profile page first, spending `Load profile page` budget. Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016790340-Invite-to-follow-organization

### `Invite person to event`
Invites **1st-degree** connections to a LinkedIn event **you are also attending**, via native LinkedIn functionality. `General` tab: event identifier or URL — accepts the full `https://www.linkedin.com/events/[event-name][ID]/`, the bare numeric ID, or the combined named ID. `[LI-POLICY]` ceiling **maximum 1000 first-degree connections per week**; cannot invite to a **completed** event; cannot invite to a **private** event unless you are the organizer — as a non-organizer attendee the event must be **public**; *"Event visibility can't be changed once the event is created."* Licence: **Standard caps this at 20 actions per 24 h**. Gotcha: contacts need first and last names; if missing, LH visits the profile first to scrape them.
Source: https://support.linkedhelper.com/hc/en-us/articles/360018076640-Invite-person-to-event

### `Invite to group`
Invites **1st-degree** connections to join a LinkedIn group where you are a member or admin/manager. `General` tab: *"paste the URL of a group where you will invite profiles to"*. You must be a group **member** or **"manager/admin"**. A LinkedIn **daily invitation limit** applies — **the number is not published** `[UNVERIFIED]`; **accepted** invitations don't count toward it, **unaccepted** ones do. Licence: **Standard caps this at 20 actions per 24 h**. Gotcha: *"if the contacts that you are trying to invite doesn't have its first and last name scraped… Linked Helper 2 will first visit the contacts profile to scrape all available data before inviting"* — relevant for CSV lists. Plug-ins: `Tagging system` · `Postpone action start` · `Action steps delays` · `Override platform`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016853279-Invite-to-group

## 2.5 Data / scraping / enrichment actions

### `Visit & Extract profiles`
Visits profiles and extracts all available data including email and phone from the Contact info panel — the canonical "get me full profile data" action. Degree: **1st, 2nd and 3rd.** `General` tab: basic options, extended via the Plug-in Store. `Advanced settings` tab: `enable automatic extraction of profile's current organization` (for domain retrieval) · `enable automatic email extraction of your 2nd and 3rd connections via Snov.io` (Snov.io API credentials) · `enable automatic email extraction of your 2nd and 3rd connections via Apollo.io` (API key with `api/v1/people/match` scope).
**Hard cache rule:** *"to avoid issues with LinkedIn, this Action scrapes profile Contact info only if the cached data is older than 14 days."* Heaviest consumer of the `Load profile page` daily limit.
Gotchas: `Successful` profiles move to the next action's queue and are downloadable after processing. It also extracts organization data, which *"can make a separate `Organizations extractor` campaign unnecessary"*. Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016708400-Visit-Extract-profiles

### `Data Enrichment`
Retrieves **emails, phone numbers, current and past experience, skills, languages** from the **Linked Helper Data Enrichment database** *without visiting the LinkedIn profile*; source is crowdsourced from data users share from profiles they personally visited. Degree: **1st, 2nd, 3rd and out-of-network.** Requires agreeing *"with the Terms to search for information about LinkedIn connections."* Settings: an **`Options` tab** to *"choose what data you need to find"* (checkbox labels **[image-only]**; credit cost shown *"below the option you enabled"*) plus a `Data Freshness` staleness threshold.
Credits per successful retrieval: **Phone 10 · Email 1 · Social & Messaging 2 · Profile info 1 · Company data 2**.
Gotchas: **does not consume LinkedIn daily action limits** — *"doesn't need to visit a profile"*. Newer locally-scraped data is **not** overwritten by older enriched data, **but credits are still deducted**. Charged per **request** whether or not you already had the data — unlike `Find Profile Emails`, which self-skips.
Source: https://support.linkedhelper.com/hc/en-us/articles/29835436540306-Data-Enrichment

### `Find Profile Emails`
Finds emails for **2nd/3rd-degree** connections via up to three providers, not necessarily visiting the profile. `General` tab, in priority order: **`Data Enrichment`** (*"search for information about LinkedIn connections in the LH Email Finder Database"*) · **`Snov.io`** (visits profiles; option to *"store found profiles in a custom Snov.io list"*; needs API keys) · **`Apollo.io`** (*"enrich profiles with emails"*, choice of *"professional emails only, or both personal and professional ones"*; needs a master API key or one with `api/v1/people/match` scope — Apollo path `Settings > Integrations > API > Create new key`).
Credits: *"One successfully processed profile uses one Data Enrichment credit."* `Settings → Limits` activity: `Get Email from LH Email Finder` (*"one profile = one action"*).
Gotchas: Data Enrichment checked first, then Snov.io / Apollo.io. **Self-skips:** *"If a profile has an email address in the CRM profile's card, then Linked Helper will not be searching"*. Not recommended for 1st-degree connections — wastes credits. Results land in the CRM profile's email field.
Source: https://support.linkedhelper.com/hc/en-us/articles/4411879384850-Find-Profile-Emails

### `Auto-collect`
Schedules **recurring** collection from a LinkedIn source into a campaign. Supported sources, verbatim: *"regular LinkedIn search"*, *"My network page"*, *"Sales Navigator list"*. `General` tab: `source link` (editable) · `repeat interval` (editable). Setup: add the link → choose the collection location if the page supports several → *"set a cadence for collecting"*.
Gotchas: *"this action does not store profiles in the Profiles to process list"* — collected profiles go **straight to `Successful`** and on to the next action. Multiple Auto-collect actions can chain for different sources. After an initial run the action pauses *"for several hours or days"*. Requires manual initiation if the campaign queue is empty. Plug-ins: `Tagging system` · `Override platform` (collect on LinkedIn, process in Sales Navigator or vice versa) · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/18181808376210-Auto-collect

### `Employees extractor`
Turns **companies into employee profiles**: visits each company page, collects from its **People** tab, routes profiles to a chosen campaign. **A dedicated campaign type, not a workflow step** — install from the Plug-in Store, then create a campaign from the `Employees extractor` (or `Organizations extractor`) template. `General` tab: filter-by-keywords toggle · keyword input with boolean operators (`CEO NOT founder`, `founder NOT CEO`; *"with multiple keywords provided, Linked Helper will use them one after another to create several keyword search requests"*) · `maximum number of profiles to collect` (*"with the limit set to 60… collecting stops as soon as 60 employees are added"*) · campaign selection dropdown.
Numbers: default **1 000 profiles per company page**; LinkedIn hard ceiling **1000 records** regardless of filtering `[LI-POLICY]`. `Settings → Limits` has a dedicated `Employees Extractor` limit counting **organizations loaded**.
Gotchas: *"LinkedIn searches keywords on any place in profile pages"* → unintended matches; multi-word phrases **without quotes** fetch profiles containing **ANY** word; *"The Successful list of the current action is used to store processed companies, not profiles."*
Source: https://support.linkedhelper.com/hc/en-us/articles/18557567889426-Employees-extractor
Source: https://support.linkedhelper.com/hc/en-us/articles/22067310525074-Employees-extractor-template

### `Organizations extractor`
Scrapes data from LinkedIn **company and school pages** for market analysis; can also retrieve emails of 2nd/3rd connections. **A separate campaign type available only after install** — `Plug-in Store` → find "Organization Extractor plug-in" → **Install** → the option appears in the Campaigns list. *"Unlike any other Action, it is not available in a Campaign by default."* *"No extra settings by default"*; extend via the Plug-in Store. Gotcha: `Visit & Extract profiles` also extracts organization data, *"potentially making a separate campaign unnecessary"* — check before building one. Plug-ins: `Override platform` · `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017046700-Organizations-extractor

## 2.6 AI actions

### `AI ICP detection action`
Scores each lead against your Ideal Customer Profile by analysing the **full** profile (summary, experience, company descriptions), ranks candidates and lets only top matches proceed; detects hands-on experience, company type and nuance beyond keyword matching. Exact labels: **`Describe your ICP`** (free text, needs detail) · **`Profile data used by AI`** (data selection via an **`Edit`** button; pre-built templates or a custom field list) · **`Minimum ICP match`** (match-score percentage threshold) · enrichment source `Data Enrichment` (instant, incomplete) / `Visit and Extract` (slower, subject to daily limits, complete) / "No enrichment option" / `Data Enrichment` **with `Visit and Extract` fallback**.
Credits: consumes **AI credits**; per-operation rate **not published** `[UNVERIFIED]` — the AI-credits article states only *"one credit per processed profile"*. No Standard/PRO differentiation published.
Gotchas: profiles **missing required data fields** → **`Failed`**; profiles **below** the threshold → **`Failed` with an error message**. Rejection is expressed as `Failed`, not `Skipped` — do not read those entries as breakage.
Source: https://support.linkedhelper.com/hc/en-us/articles/36036881332882-AI-ICP-detection-action

### `AI personalized messages`
Generates a bespoke connection request plus follow-ups per profile from that profile's data. **Exists only as part of the `Invite and follow-up` template** — *"only as a part of Invite and follow-up template"*; it **cannot be added to an existing campaign**. Exact strings: `set the general goal of the reach out` · `set target language` · `choose tone of voice` · `set goal per message` · `enable Auto-approve option to send messages without manual review` · `Profile data used by AI` (**Edit** button; pre-built templates or a custom list, fields markable **required**) · enrichment source `Data Enrichment` / `Visit and Extract` / none / fallback · `Data freshness`.
Numbers: **max follow-ups with an AI invitation 6** · **max follow-ups without an AI invitation 7** · **overall AI messaging action limit 7**. Volume *"Limited only by AI credit balance"*.
Subscription: **LinkedIn Premium, Recruiter, or Sales Navigator is required for AI personalized invitations.** Requires **AI credits**; per-operation rate not published `[UNVERIFIED]`.
Gotchas: cannot change the follow-up count after creation; cannot regenerate a message once approved (manual editing allowed); with **Auto-approve off** messages land in the **AI Drafts tab of the Campaign Inbox** and the workflow halts pending review (edit individually or bulk-approve); goal/messaging changes apply **only to new profiles**; missing required fields → **`Failed`**.
Source: https://support.linkedhelper.com/hc/en-us/articles/35934524524818-AI-personalized-messages

## 2.7 Export / integration actions

### `Send person to external CRM`
Pushes profile data into a natively integrated third-party CRM; matches by identifier, then updates the existing contact or creates a new one. Tabs: `General` (authentication, data settings) · `Organization` (company field mapping). Documented controls (HubSpot example): `Access token` or `OAuth` authentication · `Send the person's messaging history as the lead's Linked activity` · `Associate the lead's activity with a Contact, Company, or both` · `Choose owner ID` · field mapping with an **`Overwrite`** toggle for non-empty fields · `Create new field` · element selection for multi-value fields.
Supported CRMs: **HubSpot, Pipedrive, Close, Zoho CRM, Zoho Recruit, HighLevel, ActiveCampaign, Salesforce, Streak.**
Limits: *"The work of this action is not counted towards daily limits."* Separately, the licensing article lists it among activities **capped at 20 per 24 h on a Standard license** — a **licence** cap, not a LinkedIn action limit; both statements are official and both apply. Messaging-history export is **PRO-only**.
Gotchas: default identifier is **email only** → duplicates for profiles without an email; docs recommend adding **`lh_member_id`** and **`lh_public_id`** as extra identifiers. Identifiers are searched **sequentially, stopping at the first match**. LH fills **empty** CRM fields only by default — use the Overwrite toggle to force updates. Defaults live in `Settings → External CRMs`, consumed via `Use default external CRM settings`.
Source: https://support.linkedhelper.com/hc/en-us/articles/14588836379538-Send-person-to-external-CRM

### `Send person to webhook`
POSTs profile data to any third-party app accepting incoming webhooks. Lives both as a standalone campaign action **and** as an option inside messaging actions such as `Message to 1st connections` and `Check for replies`. `General` tab: **`Webhook URL`**. Webhook settings: `Convert data to flat objects (like in CSV export)` — Yes/No · `Convert multi-line values into single line` — Yes/No · column-count adjustment · messaging-history inclusion (**Full** or **Campaign**). Emails/phones require a `Visit and extract` action first. Licence: **Standard caps webhook integrations at 20 actions per 24 h**, and **messaging history cannot be sent via webhook on Standard** (PRO only).
Gotchas: *"does not interact with LinkedIn in any way"* → **no daily-limit impact**; *"does not store any data, it only sends"*. Successful profiles → `Successful` sub-list. Test with webhook.site. Docs now prefer the native CRM integrations over generic webhooks.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook

### `Send organization to webhook`
Sends data from **organization-scraping** campaigns to a third-party app. Settings: **`Webhook URL`** · `Convert multi-line values into single line` — Yes/No (Yes strips newline characters inside fields). Does not count toward daily limits; stores no data, only sends. Successful profiles → `Successful` sub-list. Test with https://webhook.site/. Field names are in "Data fields exported from Linked Helper into a webhook, CRM, or CSV file". Plug-ins: `Tagging system` · `Postpone action start`.
Source: https://support.linkedhelper.com/hc/en-us/articles/16685333860882-Send-organization-to-webhook

### `Send person to Snov.io campaign`
Pushes leads into Snov.io for email sequences beyond LinkedIn. `General` tab: Snov.io **API key** · destination selector — *"either a list of campaign"* · list/campaign name dropdown with a **`Close`** button. Requires an active Snov.io account and API credentials from https://app.snov.io/account/api.
Gotchas: **does not find emails itself** — run `Visit & Extract profiles` or `Find Profile Emails` first. Currently sends only **first name, last name, email, company, position** (the article elsewhere also mentions LinkedIn URL and industry). Dedupe across destinations: *"if a profile is sent to Snov.io campaign 'A', and then to the list 'B'… no duplicates"*. Plug-ins: `Tagging system` · `Postpone action start` · `Action steps delays`.
Source: https://support.linkedhelper.com/hc/en-us/articles/4415203905682-Send-person-to-Snov-io-campaign

---

# 3. Action-extension plug-ins

### `Delay between actions`
A real workflow **step**, not a setting: *"checks when a profile was added to its Queue and moves it forward after a set amount of time."* Added via `+Add action`, sitting between two other actions. `General` tab: delay in **days and hours** (doc example 1 day / 24 hours). **No default published** `[UNVERIFIED]`. Profiles must have completed the preceding action successfully; works **per profile**. Gotcha: *"profiles will be released to the next Action Queue, not in bunches, but one by one"*. Docs call it *"a must for sellers"* between warm-up and outreach. Extension: `Override platform`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016687679-Delay-between-actions

### `Postpone action start plug-in`
Adds a **`Start at`** point (date + time) in the **`General` tab of every Action**: *"choose the date and time until which you want the action to be paused."* Settable to a **future or past** date. Behaviour: LH processes *"10 profiles in an Action and then puts it to sleep mode for 1 minute"*; automatic postponement fires *"in case Linked Helper encountered 4+ errors in a row"* → postponed **4 hours**.
Gotchas: *"By default, the priority is given to the Action with the earliest 'Start at' point and a non-empty Queue"* — this is the runner priority lever. To clear an automatic postponement, set the date **in the past** manually.
Source: https://support.linkedhelper.com/hc/en-us/articles/9038576674066-Postpone-action-start-plug-in

### `Action steps delays plug-in`
Adds a **`Delay settings` tab to every Action**, customising pauses between individual UI steps (clicking buttons, navigating profiles, typing text). **Text input method** — `Type` or `Random` (**default `Random`**); affects speed by message length. **Delay presets** — `Fast delays` (smaller range, faster) vs **`Safe delays`** (larger range, safer). **Bunch settings** — bunch size and timeout between bunches. The doc example uses a **"3 000 characters"** template against a *"50 profiles per day"* scenario to show how `Type` mode inflates runtime.
Gotchas: fresh or recently-inactive LinkedIn accounts should use **`Safe delays`**; large character counts + `Type` mode significantly increase processing time.
Source: https://support.linkedhelper.com/hc/en-us/articles/9042541509138-Action-steps-delays-plug-in

### `Action working hours plug-in`
Sets *"a custom schedule that affects only certain actions"*, independent of the global schedule. Appears on the **right side of every Action**. Time ranges (doc example *"from 10AM till 5PM"*); exact field labels **[image-only]**.
**Critical gotcha:** *"For an action both schedules are of equal priority which means the action won't work in the case at least one schedule forbids the activity."* Actions run only in the **intersection** of `Settings → Working hours` and the per-action schedule. **No overlap = the action never runs** — check this first when an action is stuck with a full queue.
Source: https://support.linkedhelper.com/hc/en-us/articles/11519759961234-Action-working-hours-plug-in

### `Override platform plug-in`
Adds a platform selector in the **`General` tab of each Action**: **LinkedIn / Sales Navigator / Recruiter**, overriding the platform a profile was collected on. Also lets you assign a LinkedIn **group or event ID** so messages go via a common group or event. Key use case: collect via Sales Navigator's superior filters, then send invitations through **regular LinkedIn**, because *"all messages sent via that platform will be lost once the Sales Navigator subscription is canceled."* Also the fix for the `Incorrect platform` InMail error.
Source: https://support.linkedhelper.com/hc/en-us/articles/9002026071698-Override-platform-plug-in

---

# 4. Message-action extension plug-ins

### `IF-THEN-ELSE operator for Message template editor plug-in`
*"makes message templates flexible with IF-THEN-ELSE operators to generate different message texts for different sets of variables"* — e.g. graceful fallback when `{company}` is missing. Appears in the **message template editor** as three text boxes: the **`IF string`**, the **`THEN string`**, the **`ELSE string`**. It is a **three-field UI, not inline markup**; no `{IF …}` syntax is published anywhere.
Constraints: **"One operator - one variable in the IF string"** — no text, symbols or mathematical operations in the IF string. *"Linked Helper checks only the presence of information, not its content"* — a null-check, never a comparison. Nesting depth **not documented** `[UNVERIFIED]`. Works with standard **and** custom variables. Relevant because *"Information for `{company}`, `{position}`, `{mutualFirstFullName}`, `{mutualSecondFullName}`, `{mutualTotal}` isn't always available"*.
Gotchas: *"vertical order of strings… doesn't start new lines"*; *"separation between different text boxes doesn't add spaces - they need to be inserted manually."*
Source: https://support.linkedhelper.com/hc/en-us/articles/9035926428306-IF-THEN-ELSE-operator-for-Message-template-editor-plug-in

### `Custom template variables plug-in`
*"extends message template editor with user-defined variables"* such as `{cs_my_tracking_url}` or `{cs_translated_firstname}`. Installs a **`Custom variables` button** in the CRM and in the queue list of any campaign. **"The name of the column with the custom field has to start with `cs_`"**; file format **CSV or XLSX**; required columns **`profile_url`** plus your custom fields (minimum two columns); example names `cs_event`, `cs_year`, `cs_where`, `cs_firstname`. Works *"only with profiles whose URLs were uploaded with the file."*
Gotchas: *"MS Excel doesn't support CSV files in the same way as .xslx files"* but can still open them; columns besides `profile_url` are optional and may be deleted or retained.
Source: https://support.linkedhelper.com/hc/en-us/articles/9035773558034-Custom-template-variables-plug-in

### `Attach personalized images`
Lets you send *"personalized text messages but personalized images as well"* to 1st-degree connections — replacing long text with *"tables, diagrams, and other stuff."* Installs **two attachment options in the message template editor**. Three methods: (1) a **custom variable holding a direct image URL** — requires `Custom template variables`; (2) **Uclic.co** integration; (3) **Hyperise.com** integration. Methods 2 and 3 need separate third-party subscriptions.
Licence: **messaging with attached images is capped at 20 per 24 h on a Standard license**; in `Settings → Limits` image messages count under the `Message to 1st connections` limit.
Gotchas: the custom-URL method *"may take more time to implement"* — server uploads, file download/re-upload and custom-variable prep. For `Message to event attendees`, images only work in a follow-up after the initial message request is accepted.
Source: https://support.linkedhelper.com/hc/en-us/articles/9037034540818-Attach-personalized-images

### `Filter by message content plug-in`
Blocks a message if specified phrases or regex patterns appear in the previous conversation. Injects into the **`Advanced settings` tab** of `Message to 1st connections`, `Message to event attendees` and `Message to group members`. Exact labels: `Reject if any of previous messages sent by` — **`You (1)`** / **`Contact (2)`** / **`Any of you (3)`** · `Contains` — filter field for phrases/expressions · match modes **`At least one phrase [OR]`** / **`All phrases [AND]`** / **`Regular expression`** · **`Add phrase`** button for multiple entries. Regex must be *"Javascript ES6 regular expressions"*.
**Priority gotcha:** `Reject if a contact replied after #` and `Reject if you or LH messaged a contact after connection date` **take priority over** this filter. `All phrases [AND]` *"only triggers when all phrases exist within a single message, not across multiple messages in conversation."*
Source: https://support.linkedhelper.com/hc/en-us/articles/8982577824018-Filter-by-message-content-plug-in

### `Ignore generic replies plug-in`
Keeps a profile in the sequence despite a reply, when the reply is a configured generic phrase like "Thanks for connecting." Injects into the **`Advanced settings` tab** of `Message to 1st connections`, `Message to event attendees`, `Check for replies` and `Message to group members`. Settings: a configurable phrase list plus symbol-stripping settings (field labels **[image-only]**). Before matching, LH clears *"symbols mentioned in the settings; emojis; all non-printing characters."*
Constraints: **RegExp is not supported.** Matching is **case-insensitive**, but *"any other symbols that are not in the settings will not be ignored."*
Gotchas: *"a profile can send several messages in response, and every message is counted as a separate phrase"*; *"if a profile sends several messages, and at least one doesn't match with the phrases in the settings, the profile will be moved into replied list."*
Source: https://support.linkedhelper.com/hc/en-us/articles/16795759959186-Ignore-generic-replies-plug-in

### `Send replied to Webhook plug-in`
*"sends profile's data with the reply text to a 3rd-party system via webhook once reply is detected."* Options appear in `Check for replies` settings and in messaging actions (`Message to 1st connections`, `Message to group members`, `Message to event attendees`). Field labels **[image-only]**. Licence gating: *"with Standard license messaging history cannot be sent via a webhook. There is no such a limit for a PRO license."* → effectively **PRO for full functionality**.
Source: https://support.linkedhelper.com/hc/en-us/articles/9057995150482-Send-replied-to-Webhook-plug-in

---

# 5. CRM-category and Campaigns-category plug-ins

### `Built-in CRM plug-in` (CRM)
*"allows you to manage contacts from all your campaigns in one place"* — filter, tag and download profiles to CSV across every campaign. Install → **a `CRM` menu appears on the left**. Gotchas: *"Profiles' data is scraped when a profile is collected or visited by the program, and stored in a local database that is located on your PC."* *"The amount of the information provided for each profile depends on whether it was only collected and not yet visited"* — collected-only profiles have thin data, skewing CRM filters. Full UI inventory: §6.1.
Source: https://support.linkedhelper.com/hc/en-us/articles/9058416998034-Built-in-CRM-plug-in

### `Inbox plug-in` (CRM)
*"provides you with the ability to see all the conversations Linked Helper scraped"* and lets you *"respond to leads directly from Linked Helper"* without opening LinkedIn. Install → **`Inbox` menu appears in the left rail**. Required to review `Scrape messaging history` output. Gotcha: each LinkedIn platform (regular, Recruiter, Sales Navigator) has a **separate inbox**; *"Linked Helper scrapes only from the platform processing that profile."*
Source: https://support.linkedhelper.com/hc/en-us/articles/9003176158226-Inbox-plug-in

### `Tagging system plug-in` (CRM)
*"assign tags to profiles in order to filter or group them across different lead generation funnels."* Install → a **`Tags` tab** *"appears in every Action settings"*; tags can also be applied manually from a list or from the CRM (**`Tag`** button). Modes: **manual** on profiles in a list, or **automatic** on profiles processed by an Action. Notable use: LinkedIn removed industry scraping for non-Sales-Navigator users; tagging is the documented workaround — run a filtered search, then bulk-assign an industry tag.
Source: https://support.linkedhelper.com/hc/en-us/articles/9041914183698-Tagging-system-plug-in

### `Campaign Information plug-in` (Campaigns)
Adds an **`Information` tab** displaying *"the campaign's description and other metadata you can refer to in the future."* Fields: campaign **name**, **description**, **status** (view-only), profile count — *"how many profiles are in the campaign's lists"*. Intended for tracking data sources across campaigns spanning different industries/locations.
Source: https://support.linkedhelper.com/hc/en-us/articles/9062726723858-Campaign-Information-plug-in

### `Multi-campaigns runner plug-in` (Campaigns)
Queues multiple active campaigns and auto-switches to the next when the current enters sleep mode. Note: *"in the latest version, campaign menu was modified and has multi-campaigns runner plug-in already enabled."* Controls: **`Start`** per campaign · **`Campaigns runner`** with a `Start campaigns runner` control · a queue interface showing all campaigns on one screen. **Only one campaign runs at a time**; the rest queue sequentially in the order started — deliberate, *"to avoid LinkedIn detecting excessive activity"*.
Gotcha: *"Only campaigns that were enabled with the 'Start' button in the campaigns menu, will be added to the 'Campaigns runner' queue. Campaigns which were stopped manually or not started yet, won't be added…"*
Source: https://support.linkedhelper.com/hc/en-us/articles/9000412073618-Multi-campaigns-runner-plug-in

### `Exclude list plug-in` (Campaigns)
*"allows you to stop Linked Helper from collecting or processing profiles excluded from a campaign or added to its Exclude list."* Install → appears in **any campaign's `Lists` tab**, adding `Exclude` next to `Queue`. Supports **CSV uploads of LinkedIn URLs** for batch exclusion.
Gotchas: when deleting excluded profiles you choose between **restoring them to their original queues** or **removing them from the exclusion only** (leaving them excluded). *"Those profiles who were not in the Excluded list… will not be added to the Queue."* Profiles queued *before* exclusion need manual re-queuing. **Per-campaign only — there is no native global blacklist.**
Source: https://support.linkedhelper.com/hc/en-us/articles/8984255221522-Exclude-list-plug-in

### `List manager plug-in` (Campaigns)
*"Manage groups of leads at the campaign and action levels by removing intersections, merging, or excluding lists in different campaigns."* Install → appears in the **`Functions`** menu. Operations, exact button labels: **`Add unique`** · **`Delete the same`** · **`Remove intersections between campaigns`** · **`Keep the same`**. Use for deduplicating leads across simultaneous campaigns, and as the mechanism for a synthetic global blacklist.
Source: https://support.linkedhelper.com/hc/en-us/articles/9058519082642-List-manager-plug-in

---

# 6. Menu reference

## 6.1 Instance menus

### `Campaigns` menu
Campaign groups on the **left sidebar**, full campaign list on the **right**. Capabilities: manage and queue multiple campaigns for sequential execution · review campaign activity (switch between **lead-gen activities** and **all activities**) · **download campaign activity reports** · sort by **number, name, status, or profile count**. Campaigns **cannot be deleted**, only archived — hover the campaign, click **`Archive`**; restore via the **`Archived`** tab.

| Campaign status | Meaning |
|---|---|
| `Running` | currently executing |
| `Queued` | active but waiting (another campaign is running, or Campaigns runner is off) |
| `Sleeping` | delayed by a timeout or a scheduled start |
| `Stopped` | manually halted; **won't restart** with Campaigns runner |
| `Completed` | no profiles in queue |
| `Draft` | never run |

Campaign tabs: **`Information`** (name, description, status, profile count — needs `Campaign Information`) · **`Workflow`** (*"view and set up your funnel of different Actions where profiles should be processed"*) · **`Lists`** (includes `Exclude` if that plug-in is installed) · **`Inbox`** with sub-tabs **`Replied` / `Sent` / `Scheduled` / `Unscheduled` / `Failed` / `Draft`** (plus the AI Drafts tab when `AI personalized messages` is in use) · **`Dashboard`** (performance metrics, issues to fix, messages to review, profile statistics, and detailed statistics with columns **`Queue` `Processed` `Successful` `Excluded` `Skipped` `Failed` `Replied` `Messaged`**).
Source: https://support.linkedhelper.com/hc/en-us/articles/360017228839-Campaigns-menu

### `LinkedIn` menu (embedded browser)
Navigation bar: **`Back`**, **`Forward`**, **`Refresh`** · address bar (it *"works only with LinkedIn and its premium services links"*) · **`Copy URL`** · zoom buttons · fast-navigation buttons for **`Regular LinkedIn`**, **`Sales Navigator`**, **`Recruiter`** (each needs an active subscription). On-profile controls: **`Add to`** / **`Add to CRM`** appear automatically (needs `Built-in CRM`) · tagging (needs `Tagging system`) · profile **notes** — available *"only if this profile is already part of Linked Helper's CRM"*.
**Browsing is blocked when:** (1) *"You have a campaign running or your Campaigns runner is active"*; (2) *"It is collecting or visiting profile(s) at the moment"*; (3) *"You have 'Sent invites canceller' running."* During these you can only observe; manual browsing requires stopping all automation.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017179880-LinkedIn-menu

### `Collect` menu
*"just another place where you can collect profiles"*, *"added for your convenience"* when the Multi-campaign runner plug-in is enabled.
**`Source` section:** dropdown of *"the source from which your contacts can be collected"*; *"the source will be displayed automatically"* if you are on a supported LinkedIn page. Rules: *"option to collect post likers or commentators is available only when you open a post via its direct URL"*; single-profile collection requires opening *"its LinkedIn page"*.
**`Target` section, two paths:** **Campaign list** — choose an existing campaign, or *"create a new campaign from a template right here"* · sub-list selector · choice between the campaign's **`Queue`** and **`Exclude`** list. **Action list** — dropdown for existing campaigns or template creation · action option selection · **`choose Action`** field; *"Actions do not have their own Exclude list, so it is possble to add profiles only to the Queue."* [sic]
Six documented skip reasons: (1) contact already in a sub-list of the current Action/Campaign; (2) LinkedIn shows "LinkedIn Member" instead of a real name; (3) Connection/Relationship filters set improperly; (4) relationship filter mismatches the search results; (5) a new account with few or no 1st-degree connections; (6) attempting to re-collect already-invited profiles.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017176100-Collect-menu

### `Functions` menu
Appears **only when** at least one of these is installed: **`List Manager` plug-in** (*"helps to manage contacts across your Linked Helper campaigns"*) · **`Sent invites canceller`** (*"can withdraw invites that were not accepted"*) · **`Accept incoming invitations` plug-in** (*"allows you to automatically accept incoming invitations"*). Functions run **outside** campaigns and generally do **not** count toward daily statistics/limits (explicitly stated for `Accept incoming invitations`).
Source: https://support.linkedhelper.com/hc/en-us/articles/360017185219-Functions-menu

### `CRM` menu
Per profile: first and last names · original names (if normalized) · position/company · headline · degree of connection · internal ID number.
Action buttons, exact labels: **`All X / X`** (select/deselect all profiles or the current page) · **`Add to`** (move selected profiles to campaigns/actions) · **`Download`** (export selected to CSV) · **`Tag`** (needs `Tagging system`) · **`Show original names`** · **`Custom variables`** (needs `Custom template variables`).
Filters — *text:* First name · Last name · Company · Position · Headline · **LH ID** · **LinkedIn ID**. *Relationship:* **1st / 2nd / 3rd / Out of network**. *Boolean (**Yes / No / Any**):* avatar presence · Premium status · Influencer status · **"Open Link"** availability · Job Seeker status. *Tags:* **`With tags`** · **`Without tags`**. *Other:* campaign selection · **`Has modified name`**.
Gotcha: position, company and Open Link status are only populated **after profile extraction**, which skews those filters for collected-but-not-visited profiles.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016837280-CRM

### `Dashboard` menu (statistics / analytics)
General metrics: **Acceptance rate** · **Reply rate** · **Overall activity** across campaigns. Controls: a **`Graph boundaries`** section for the time period · a campaign selector for *"all campaigns statistics or select the specific one"* · **download / export**. Status indicators shown: `Running` · `Queued` · `Sleeping` · `Stopped` · `Completed`. CRM connection counters: 1st · 2nd · 3rd level · Out of network.
**`Invited / Accepted` tab:** total invited · total accepted · acceptance percentage · per-date hover detail for daily Invited/Accepted · toggle filters for invited-only or accepted-only.
**`Messaged / Replied` tab:** total messaged (**excluding invitation messages**) · total replies · reply percentage of messages sent · per-date hover detail · optional filters isolating Messaged or Replied.
Per-campaign `Dashboard` tab adds performance metrics, issues to fix, messages to review, profile statistics, and detailed statistics with columns `Queue` / `Processed` / `Successful` / `Excluded` / `Skipped` / `Failed` / `Replied` / `Messaged`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017491719-Dashboard-menu

### `Inbox` menu (Linked Helper messenger)
View & filtering: **default view shows only unread messages**, customisable via the **`Filters`** section · filter by read/unread status and by message content · unread-reply count shown next to each profile name · profiles whose messages are all `Read` are **hidden** but remain filterable.
Message management: **`Read`** button / mark-as-read (moves the unread indicator below the replied message) · **`Show in chat`** button — *"looks like two messaging clouds"* — opens full history · tag chats (needs `Tagging system`) · **`Download`** one-by-one or in bulk.
Messaging interface: create a **draft message** manually **or from a template** · **`Send a reply now`** or *"save it for later"* · **`Visible replies`** line marks messages detected as replies (profiles auto-move to `Replied`) · **`New`** line marks unread messages below that threshold · **`Ignore`** button — marks visible replies as "should-not-detect" for future processing.
Chat history: a **`Messaging history` tab** reachable by clicking a profile name; regular LinkedIn / Sales Navigator / Recruiter conversations are shown **separately per platform**, combined in one menu when the Inbox plug-in is enabled.
Gating: no paywall on the Inbox itself; **CSV export of messaging history is PRO-only**, and **messaging history cannot be sent via webhook on a Standard license**.
Source: https://support.linkedhelper.com/hc/en-us/articles/5422237843218-Linked-Helper-Inbox-menu

### `Plug-in store` menu
*"A list of all available plug-ins."* Install / uninstall at any time; once enabled a plug-in *"becomes available for any LinkedIn account instance added to the Linked Helper account."* Control: an **`Install`** button per plug-in.
Source: https://support.linkedhelper.com/hc/en-us/articles/10522915555858-Plug-in-store-menu

### `Need help` menu
Five sections: (1) **Weekly invitations limit** — explains LinkedIn's **100 invites-per-week** restriction `[LI-POLICY]`; links to "Is there a life after LinkedIn weekly invitation limit?" (2) **Knowledge base** — opens a separate window to the Zendesk help center (linkedhelper.zendesk.com); subsections *Issues & solutions*, *User manual*, *News*. (3) **Video tutorials** — YouTube playlist at youtube.com/@LinkedHelper/playlists. (4) **Ask for support** — form requiring **Name and email**, **Application version**, **Message**, up to **5 files**; also "Facebook messaging" and "Whatsapp"; *"average reply time is about 15 minutes"* `[LH-CLAIM]`; include the Linked Helper account email, LinkedIn instance ID, screenshots and screen recordings. (5) **Tip of the day** — *"Contains useful information and tips about Linked Helper actions and features"*.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017185399-Need-help

## 6.2 Instance Settings sub-menus

The instance `Settings` menu publishes **four** sub-menus; an **`External CRMs`** sub-menu also exists with its own article but is not listed in that four-item overview.

| Sub-menu | Published purpose |
|---|---|
| **`Limits`** | *"set up limits to be on the safe side"* |
| **`Working hours`** | *"schedule Linked Helper work"* |
| **`Actions`** | *"extra global settings for actions"* |
| **`Interface`** | *"adjust zoom level of the instance interface"* |
| **`External CRMs`** | default CRM settings for newly added actions |

Source: https://support.linkedhelper.com/hc/en-us/articles/360017136580-Settings-menu

### `Settings` → `Limits`
*"In the Limits, you can set the maximum number actions per 24 hours period in order to avoid issues with LinkedIn as well as set the limit to a certain activity type."* The fields themselves exist only in a screenshot **[image-only]**; the authoritative list comes from the User-manual article "Working Hours and Limits".
- Overall cap field `Max actions per 24 hours`; default/recommended **150 profiles per every 24 hours**.
- **Advanced (per-activity) limits**, each independent: `Employees Extractor` · `Endorse my contacts` · `Follow / Unfollow profiles` · `Get Email from LH Email Finder` · `Inmail to 2nd/3rd contacts` · `Invite 2nd/3rd level contacts` · `Load profile page` (master limit, *"priority over all other"* profile limits) · `Load LinkedIn profile via URL` (default **40 per 24 hours**) · `Message to 1st connections` (image messages counted here) · `Load LinkedIn search results` · `Post liking` (counts liked posts) · `Remove from 1st connections`.
- Standard-licence-capped activities (**20 per 24 h**): `Invite to event` · `Invite to group` · `Invite to follow organization` · `Message to event attendees` · `Message to group members` · message with attached image · `Post liking` · `Mention person in comment`.
- **CONFLICT — limit precedence:** *"Advanced limits have priority over the daily limits"* vs *"Maximum Daily Actions limit always overrides any lower-level limits"*. Both official. Practical rule: keep `Max actions per 24 hours` at or above the sum of the per-activity limits you want, and verify with a small run.
- **Smart daily limits** randomize volume by a percentage: *"with 10% variation for inviting limit, daily number of invitations set will vary from 45 to 50."*
- Stacking is supported, e.g. `50 actions per 24 hours` + `3 actions per 1 hour`.

Source: https://support.linkedhelper.com/hc/en-us/articles/10522224820882-Limits-sub-menu
Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

### `Settings` → `Working hours`
*"In the Working hours section you can set up a timezone and working hours / days when this particular Linked Helper Instance is active."* Field-level UI is screenshot-only **[image-only]**. From the User manual: per-weekday toggles **`24 hours`** or **`Do not work`**; add time periods with **`+`** then **`Format and save`**; **military (24-hour) time format**. Interaction with `Action working hours`: both schedules have **equal priority** — the action only runs in their intersection.
Source: https://support.linkedhelper.com/hc/en-us/articles/10522320011666-Working-hours-sub-menu

### `Settings` → `Actions`
**One setting only** — the article states this is *"the only setting available there"*: **`Leave responses unread when checking for replies`**, which makes the tool *"open message dialogue options and click 'Mark as unread' button"* during reply checking. **Default state not published** `[UNVERIFIED]`. It counters the `Check for replies` side effect that *"LinkedIn marks unread messages as read"*.
Source: https://support.linkedhelper.com/hc/en-us/articles/12245848574738-Actions-sub-menu

### `Settings` → `Interface` (instance)
**Zoom level** — custom zoom plus a **`Switch to the default value`** toggle; syncs with the default set in the Launcher's Interface sub-menu. **Language** — English · **`French (Français)`** · **`Spanish (Español)`** · **`Portuguese (Português)`** · **`German (Deutch)`** [sic — spelled "Deutch" in the docs]. **Tool name and logo** — small logo, tool name field, big logo; tied to the **White Label**, affiliate and referral programs. **Sound** — LinkedIn notification sound toggle · other tool sounds toggle.
Source: https://support.linkedhelper.com/hc/en-us/articles/10521416479250-Interface-sub-menu

### `Settings` → `External CRMs`
**`Set up the default CRM for newly added Actions`**. *"Change CRM's default settings. These settings can be changed anytime, and the changes are immediately reflected in the Actions that use default CRM settings."* Consumed by `Send person to external CRM`, messaging actions, and `Check for replies` — each via a **`Use default external CRM settings`** option. The CRM roster is not in this sub-menu article; it is in the action article: HubSpot, Pipedrive, Close, Zoho CRM, Zoho Recruit, HighLevel, ActiveCampaign, Salesforce, Streak.
Source: https://support.linkedhelper.com/hc/en-us/articles/15107496924434-External-CRMs-sub-menu

## 6.3 Launcher menus

Launcher section article list (15): `LinkedIn Accounts menu` · `Licenses menu` · `Billing menu` (sub-menus `Orders & Invoices`, `Subscriptions`, `Data Credits`) · `Proxies menu` · `Workspace management menu` · `Get free license menu` · `Settings menu` (sub-menus `Linked Helper account`, `Machines`, `Interface`) · `Need Help menu` · `Check and install updates`.
Source: https://support.linkedhelper.com/hc/en-us/sections/360004661500-Launcher

### Launcher → `Settings`
Three sub-menus: **`Linked Helper account`** — *"managing your password and billing information"* · **`Machines`** — *"review different PCs on which you used Linked Helper"* · **`Interface`** — *"adjust Linked Helper Launcher zoom level"*. Field-level detail is not published `[UNVERIFIED]`.
Source: https://support.linkedhelper.com/hc/en-us/articles/10520187390226-Settings-menu

---

# 7. Cross-cutting selection tables

### 7.1 Reach non-1st-degree contacts WITHOUT spending an invitation
`[LI-POLICY]` context: LinkedIn's weekly invitation limit is 100 invites/week.

| Action | Mechanism | Cost / requirement |
|---|---|---|
| `InMail to 2nd & 3rd contacts` | native InMail | InMail credits + Premium (or Sales Navigator); **free** to Open Profiles, 2nd degree only |
| `Message to group members` | shared group membership | Standard capped 20/24 h; must be a member of the same group |
| `Message to event attendees` | shared event | Standard capped 20/24 h; attendees must be collected from that event first |
| `Boost post` | mention in a comment | Standard capped 20/24 h; both parties must be group members for group posts |

Source: https://support.linkedhelper.com/hc/en-us/articles/5714464724754-Message-to-group-members
Source: https://support.linkedhelper.com/hc/en-us/articles/4413984987026-Message-to-event-attendees

### 7.2 1st-degree-only actions
`Message to 1st connections` · `Endorse my contacts` · `Remove from 1st connections` · `Invite to follow organization` · `Invite person to event` · `Invite to group`. Everything else works on 2nd/3rd degree or across all degrees. Consequence: a 2nd/3rd-degree action must precede any of the above in a workflow, and LH auto-inserts `Filter contacts out of my network (keep 1st level only)` between incompatible types.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016659500-Message-to-1st-connections

### 7.3 LinkedIn subscription dependencies

| Capability | Requires |
|---|---|
| Paid InMails (`InMail to 2nd & 3rd contacts`) | LinkedIn **Premium**, or a **Sales Navigator** subscription alone |
| AI personalized invitations (`AI personalized messages`) | LinkedIn **Premium, Recruiter, or Sales Navigator** |
| `Check 'Save as lead' checkbox…` in Invite advanced settings | **Sales Navigator** |
| Subject line in `Message to 1st connections` | sending via **Recruiter** |
| Industry data on scraped profiles | **Sales Navigator** only — otherwise use the `Tagging system` workaround |
| Free InMails | target must be an **Open Profile**, 2nd degree |
| More than 10 personalized invites/month | a **paid** LinkedIn subscription |

Source: https://support.linkedhelper.com/hc/en-us/articles/360016601420-InMail-to-2nd-3rd-contacts
Source: https://support.linkedhelper.com/hc/en-us/articles/35934524524818-AI-personalized-messages

### 7.4 Licence gating — PRO-only and Standard-capped
**PRO-only capabilities surfaced in Program overview:** messaging-history CSV export (`Scrape messaging history`) · messaging history via webhook (`Send replied to Webhook`, `Send person to webhook`, `Send person to external CRM`) · removal of the 20-per-24 h Standard cap on every activity below.
**Standard licence capped at 20 actions per 24 h:** `Invite to event` · `Invite to group` · `Invite to follow organization` · `Message to event attendees` · `Message to group members` · message with attached image · `Post liking` (i.e. `Like and comment posts and articles`) · `Mention person in comment` (i.e. `Boost post`) · `Send person to external CRM` · webhook integrations.
Source: https://support.linkedhelper.com/hc/en-us/articles/9025165336978-Scrape-messaging-history
Source: https://support.linkedhelper.com/hc/en-us/articles/9057995150482-Send-replied-to-Webhook-plug-in

### 7.5 Credit consumption

| Action | Credit type | Published rate |
|---|---|---|
| `Data Enrichment` | Data Credits | Phone **10** · Email **1** · Social & Messaging **2** · Profile info **1** · Company data **2** per successful retrieval; charged per **request** even if you already had the data |
| `Find Profile Emails` (Data Enrichment source) | Data Credits | **1** per successfully processed profile; self-skips if the CRM card already has an email |
| `Get email from LH Email Finder` in Invite advanced settings | Data Credits | same LH Email Finder rate |
| `AI ICP detection action` | AI Credits | *"one credit per processed profile"*; per-operation rate **not published** `[UNVERIFIED]` |
| `AI personalized messages` | AI Credits | volume *"Limited only by AI credit balance"*; per-operation rate **not published** `[UNVERIFIED]` |
| `AI-generated comments` in `Like and comment posts and articles` | AI Credits | rate **not published** `[UNVERIFIED]` |
| `InMail to 2nd & 3rd contacts` | LinkedIn InMail credits (not LH credits) | allocated by LinkedIn subscription; free to Open Profiles |
| `Invite to follow organization` | LinkedIn page invitation credits | monthly, shared across admins; resets monthly |

Source: https://support.linkedhelper.com/hc/en-us/articles/29835436540306-Data-Enrichment
Source: https://support.linkedhelper.com/hc/en-us/articles/4411879384850-Find-Profile-Emails

### 7.6 Actions that do NOT consume LinkedIn daily limits
`Data Enrichment` · `Send person to webhook` · `Send organization to webhook` · `Send person to external CRM` · `Accept incoming invitations` (function) · `Sent invites canceller` and `List manager` (functions, run outside campaigns). These may still consume **Data credits**, **AI credits**, or a **Standard-licence 20/24 h cap**.
Source: https://support.linkedhelper.com/hc/en-us/articles/29835436540306-Data-Enrichment
Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook

### 7.7 Structural exceptions worth memorising
1. **Two actions require a dedicated campaign type, not a workflow step:** `Employees extractor`, `Organizations extractor`.
2. **One action cannot be added to an existing campaign at all:** `AI personalized messages` — it exists only inside the `Invite and follow-up` template.
3. **`Failed` is used for non-failures by two actions:** `AI ICP detection` writes below-threshold profiles to `Failed`; `Automatic sent invites canceller` writes `The invitation was canceled` to `Failed` as normal operation.
4. **`Auto-collect` skips `Profiles to process` entirely** — collected profiles go straight to `Successful`.
5. **`Employees extractor`'s `Successful` list holds companies, not profiles.**
6. **`Organizations extractor` is the one action plug-in not installed by default.**

Source: https://support.linkedhelper.com/hc/en-us/articles/36036881332882-AI-ICP-detection-action
Source: https://support.linkedhelper.com/hc/en-us/articles/18557567889426-Employees-extractor

---

# 8. What is NOT documented

Treat every item below as `[UNVERIFIED]`. Do not assert a value; say it is not documented and recommend testing on a throwaway campaign, or checking `support.linkedhelper.com`.

- **`Settings → Limits` and `Settings → Working hours` publish no field labels or defaults in text** — both are single-screenshot articles. Numbers must be sourced from the User-manual article "Working Hours and Limits".
- **Character limits are never published per action.** No Program-overview article states an invitation-note, message, InMail subject or comment character ceiling. (`Action steps delays` mentions a *"3 000 characters"* template only as a timing example.)
- **Per-operation AI credit rates** for `AI ICP detection` and `AI personalized messages` are not published.
- **`Invite to group` daily invitation limit** — stated to exist, number not given.
- **Field labels are screenshot-only** for: `Auto accept incoming invites…`, `Automatic sent invites canceller…` (the "X days" field), `Action working hours`, `Ignore generic replies`, `Send replied to Webhook`, `Data Enrichment` (the `Options` tab checkboxes), `Tagging system`.
- **`Delay between actions`** publishes no default delay value.
- **IF-THEN-ELSE nesting depth** is not documented.
- **`Settings → Actions` → `Leave responses unread when checking for replies`** — default state not published.
- **Maximum skill count for `Endorse my contacts`** is not published.
- **No character limit is published for `Message to group members`.**
- **Launcher `Settings` field-level detail** (`Linked Helper account`, `Machines`, `Interface`) is not published.
- **Naming inconsistency, not a bug:** `Follow / unfollow profiles` is listed under that name but the article H1 reads **"Profiles Auto-Follower"** — the same action.
- Coverage note: no article 404'd in the research pass. All 54 Plug-ins URLs and all 15 Instance URLs resolved.

Source: https://support.linkedhelper.com/hc/en-us/articles/10522224820882-Limits-sub-menu
Source: https://support.linkedhelper.com/hc/en-us/articles/360016777979-Follow-unfollow-profiles
