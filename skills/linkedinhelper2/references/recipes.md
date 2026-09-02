# Linked Helper 2 — Recipes (executable playbooks)

End-to-end procedures with exact UI paths, pacing numbers and failure modes. Every factual block carries its `Source:` line.

Exclusion/dedup (R12), bulk tagging (R13), cloning/porting (R14) and the CSV catalogue (R16) are documented in `references/campaigns.md`; only the steps a recipe needs inline to be executable are repeated here.

## Recipe selection guide

| Situation | Recipe |
|---|---|
| New, dormant or previously restricted account | **R1** with `SAFE` timeouts + the ramp in `references/limits-safety.md` |
| Weekly invite cap exhausted | **R2** (router) → R3 / R6 / R7 / R4 |
| Reach out with zero invitations spent | **R7** — highest yield when the audience is Premium-heavy |
| Precise ICP and you share a group with them | **R3** |
| Conference / webinar / meetup audience | **R6** |
| Warmest possible cold list | **R9** (post likers and commenters) |
| Want an off-platform (email) channel | **R4** → **R5a**; **R5b** for other email providers |
| Re-engage the cohort that accepted one campaign's invites | **R8** |
| Target only prospects with 500+ connections | **R10** |
| Notes and first messages are not landing | **R11** |
| Two accounts working the same market | R14b + R12b in `references/campaigns.md` (cross-account exclusion mandatory) |
| Testing message variants | R14a clone with `Exclude profiles from the current campaign`; A/B stats `[UNVERIFIED]` |
| Recruiting / passive candidates | **R15** (derived — no published playbook) |
| Search returns less than the market contains | **R18** (boolean + X-ray) then **R19** (result caps) |
| Someone proposes a "limit bypass" | **§Tactics ranked by evidence** — check before building on it |
| Need a number to justify a plan | **§Benchmarks**, incl. the figures that do not exist |

Source: https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit

---

## R1. Multi-step warm-up funnel (the canonical safe sequence)

**Goal** — turn 2nd/3rd-degree strangers into replying 1st-degree connections without an invite-only pattern that reads as bot activity.

**Prerequisites** — LinkedIn: any tier (Free gets ~5 personalized invites/month; Premium removes that). LH2 licence: Standard. Plug-ins: `Action steps delays plug-in` (FAST vs SAFE timeouts, bunching) and `Delay between actions` as an insertable step. Credits: none. Copy: ≥2 message variants per messaging step.

**Steps** — build from the `Warm-up, invite, and follow-up` template, then match this 16-step reference workflow (verbatim order):

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

Compact variant (from the weekly-limit article), for fewer moving parts:

```
Action #1   Like and comment on posts
Action #2   Delay (1-2 days)
Action #3   Follow / unfollow profiles
Action #4   Delay (1-2 days)
Action #5   Invite 2nd/3rd level contacts
Action #6-11  Progressive messaging + reply checks with strategic delays
```

Copy rules: invitation note carries **no sales offer** (it lowers acceptance) and **no links** — "LinkedIn may flag them as spam"; if unsure the note lands, **send no note at all**. Message #1 after acceptance is a casual **"Thank you for accepting"**, not the offer, **2-3 days** after connecting. Break a long pitch into **"2 or 3 messages with the 3 - 7 days intervals between them."** Split multiple links/media across separate messages. Use ≥2 variants plus spintax, variables and IF-THEN-ELSE; verify with **Message preview**.

**Limits and pacing** — **3 messages maximum** ("Recommend maximum 3 messages to avoid appearing pushy"). `Check for replies`: minimum interval **10 minutes**, default cycle **60 minutes**. New/dormant accounts: timeouts to **SAFE**. Warm-up steps also consume the `Load profile page` budget — see `references/limits-safety.md`.

**Expected yield** — no funnel-level conversion figures in the research. Nearest number: warmed vs cold prospects **+10-20%** acceptance `[LH-CLAIM]` (§Benchmarks).

**Failure modes** — omitting step 6 breaks the funnel (messaging actions require 1st-degree status; the `Invite & Follow Up` template auto-inserts it). No `Check for replies` between messages ⇒ people who already answered get the follow-up. Burning the daily allowance in one hour leaves the account idle ~24 h on the rolling counter — the most bot-like pattern available.

Sources:
https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper
https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit
https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2
https://support.linkedhelper.com/hc/en-us/articles/360015485560-What-does-Filter-contacts-out-of-my-network-keep-1st-level-only-action-do

---

## R2. Reaching 2nd/3rd degree WITHOUT spending invitations — the four documented routes

**Goal** — keep prospecting after the weekly invite cap is exhausted.

**Prerequisites** — none for the router; each route carries its own.

**Steps** — pick the route the audience allows:

| Route | Mechanism | Recipe | Requires |
|---|---|---|---|
| 1. Group messaging | Free messages to fellow **group members**, filtered in Sales Navigator | **R3** | Sales Navigator + group membership + `Override platform plug-in` |
| 2. Event outreach | Message **event attendees** directly, no prior connection | **R6** | Access to the attendee list |
| 3. Open-profile InMails | Premium users with **Open profiles** accept **free** InMails (no credits) | **R7** | InMail sequence template |
| 4. Email extraction | `Find Profile Emails` → reach out off-platform | **R4 / R5** | Email-finder integration / API keys |

**Limits and pacing** — this article states LinkedIn allows **"approximately 150-200 invitations per week"**, and that free accounts are additionally limited to **"about 5 personalized invites per month"** (notes only); Premium removes that. Group-messaging caveat, verbatim: *"some accounts face a 10-message monthly limit across all groups."* `[LH-CLAIM]`

CONFLICT — weekly invitation ceiling. Help centre: **"approximately 150-200 invitations per week"**. The blog's limit-beating posts work from a **~100 invites/week** cap. Both vendor-published; plan against **100/week** and see `references/limits-safety.md`.
Sources: https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit · https://www.linkedhelper.com/blog/weekly-invite-limit-linkedin

**Expected yield** — none published per route; only R7 carries prevalence figures.

**Failure modes** — all four routes are audience-gated: no shared group, no event, a non-Premium audience or no discoverable email each kills one route outright. Check audience fit before building.

Source: https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit

---

## R3. Group harvesting → free messages to group members

**Goal** — free messages to precisely-filtered people who share a LinkedIn group with you, bypassing the invitation limit.

**Prerequisites** — LinkedIn **Sales Navigator** (the group filter lives there); **you must be a member of the target group**; **`Override platform plug-in`** (required for `Change platform`); `Tagging system plug-in` if harvesting **multiple** groups and tracking source groups. No credits.

**Steps**
1. Create the campaign from the **`Message sequence via group`** template. Configure the initial message. In **`Check for replies`**, set reply detection to recognise **"Message request accepted"** notifications.
2. Add follow-ups (optional): set the minimum delay between messages, keep to **maximum 3 messages**, configure conditional sending based on acceptance status.
3. In Sales Navigator: open the search page → apply filters (position, location, industry, headline) → apply the **group filter** for the target group → **copy the Group ID from the URL** → load the results page fully before collecting.
4. Collect: **`Collect`** → **`from current page`**. Profiles land in the campaign Queue.
5. Set the Group ID: open the **`Message to group members`** action workflow → **select all** profiles → **`Change platform`** → switch **`Collect scope type`** to **"Group ID"** → paste the ID into **`Collect scope ID`** → **Save changes**.
6. Review queued contacts, exclude unwanted profiles, verify templates.
7. **Start the campaign.**

Copy: message #1 is a *request*, so lead with group-relevant relevance (R11's RRR) — not a pitch. Follow-ups reach only those who accepted, so treat #1 as the permission ask.

**Limits and pacing** — safe-limits guidance: **10-15 group messages/day**. Some accounts get less: *"For some LinkedIn accounts, the limit of messages to group members is lower compared to the other LinkedIn accounts."* One help-centre article reports **a 10-message monthly limit across all groups** for some accounts.

CONFLICT — group-message volume. Safe-limits post: **10-15/day**. Groups posts: you *"can write to hundreds of people a day"*, no official cap stated. **Use 10-15/day.**
Sources: https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/linkedin-groups

`[UNVERIFIED]` — max groups joinable, max members scrapable per group, group-message character limit (`references/templates.md` lists group/event bodies at **8,000**).

**Expected yield** — the research gives none.

**Failure modes** — initial messages arrive as **requests, not direct messages**, landing in **Incoming Requests**; follow-ups **do not send** unless the recipient accepts. Skipping step 5 leaves the action with no group context. Multiple groups without `Tagging system plug-in` loses source attribution. Group discovery: keyword search matches group **names** only; check which groups industry leaders belong to (already vetted); avoid *"random spam groups where people mostly post promotional messages"*.

Sources: https://support.linkedhelper.com/hc/en-us/articles/4404650533394-How-to-filter-profiles-via-Sales-Navigator-and-send-them-free-messages-as-group-members
https://www.linkedhelper.com/blog/linkedin-groups · https://www.linkedhelper.com/blog/use-linkedin-groups-to-generate-leads · https://www.linkedhelper.com/blog/linkedin-automation-limits

---

## R4. Emails for 2nd/3rd-degree connections — integrated route (fastest)

**Goal** — get email addresses for out-of-network prospects so you can reach them off LinkedIn.

Why it is needed, verbatim: *"E-mails are unavailable on the profile pages of 2nd and 3rd level contacts, so Linked Helper 2 won't be able to scrape them by simply visiting the profile pages."*

**Prerequisites** — LinkedIn: any tier. LH2: campaign from the **`Find Profile Emails`** template. Optional API keys for **Snov.io** and/or **Apollo.io**. Credits: LH's own enrichment spends Data Credits (email 1, phone 10 — `references/plans-and-platform.md`); Snov.io/Apollo give **50 free profile searches**, then paid credits.

**Steps**
1. Create a campaign from the **`Find Profile Emails`** template.
2. Enable the integration(s) at setup: **LH Email Finder** (Linked Helper's own service) · **Snov.io** (corporate emails) · **Apollo.io** (personal **and** business emails).
3. Add API keys for Snov.io / Apollo.io if used.
4. Filter and **collect leads** into the campaign Queue.
5. **Run the campaign.**
6. Export from the **`Successful`** list.

Search order, verbatim: *"Linked Helper searches for profile emails using LH Email finder first, and in case no address is found, search is continied using snov.io integration."*

**Limits and pacing** — no per-day email-lookup ceiling published; the campaign is still bound by `Max actions per 24 hours` and the profile-visit budget.

**Expected yield** — no hit rate published. The research states only that **LH Email Finder finds mostly personal email addresses**.

**Failure modes** — **always export from `Successful`, never from `Queue`** (Queue exports carry no emails). Beyond 50 lookups Snov.io/Apollo require paid credits. `[UNVERIFIED]` — the article does not state the Data Credits cost per lookup.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015581980-How-to-get-emails-of-your-2nd-and-3rd-connections-in-LinkedIn
https://support.linkedhelper.com/hc/en-us/articles/360016685199-Why-don-t-all-contacts-in-a-CSV-file-have-e-mail-addresses

---

## R5. Emails via Snov.io — two documented variants

### R5a. In-action Snov.io enrichment during `Visit & Extract profiles`

**Goal** — enrich profiles with third-party emails while already visiting them.

**Prerequisites** — Snov.io account; API credentials from **https://app.snov.io/account/api**; Linked Helper installed (14-day free trial available); target 2nd/3rd-degree profiles.

**Steps**
1. Campaign menu → templates list → **`Visit & extract profiles`** → **`Create campaign`**.
2. **`Collect`** near the campaign Queue → choose the data source (LinkedIn search, saved list, etc.) → review.
3. Open the **`Visit & Extract`** action's **Advanced settings** → enable **"Extract emails from Snov.io for contacts out of my network"** → paste the API credentials from https://app.snov.io/account/api. Optionally configure saving emails to a Snov.io list.
4. **`Start campaign`** → monitor in the left menu → on completion open **`Successful`** → **`Select All`** → **`Download`** → choose the delimiter format (Google Sheets or MS Excel).

**Limits and pacing** — `Visit & Extract` is the heaviest `Load profile page` consumer; hold to the documented **150 extracts / 24 h** (`references/limits-safety.md`).

**Expected yield** — no hit rate published. Caveat verbatim: *"snov.io cannot extract every profile's email since sometimes there is no enough information provided"* — or the user opted out of email visibility.

**Failure modes** — emails land in the **`third_party_email`** column, not the standard email column; profiles also populate LH's **CRM**, visible on each profile card. Missing API credentials silently yields no third-party emails.

Source: https://support.linkedhelper.com/hc/en-us/articles/360020619780-How-to-extract-emails-of-your-2nd-and-3rd-degree-connections-via-Snov-io

### R5b. Manual 3-step domain→email route (any other email provider)

**Goal** — build a `first_name, last_name, organization_domain` file and bulk-resolve it with any provider.

**Prerequisites** — **`Organizations Extractor`** plug-in (the documented plug-in that is **not** installed by default); a third-party bulk-email account.

**Steps**
1. **Extract profile data:** create a **`Visit & Extract Profiles`** campaign, enable **"Extract current organizations"**, collect leads into the Queue, run it.
2. **Extract company domains:** install **`Organizations Extractor`** → create a new **organizations** campaign → add the companies from the previous campaign's **`Successful`** list → extract organization data to obtain **domain names** → build a CSV with exactly these columns: **`first_name`, `last_name`, `organization_domain`**.
3. **Resolve emails:** at Snov.io use **"Bulk Email Search"** → upload the 3-column CSV → run verification → download **verified (green)** and **potential (yellow)** emails. Verifier: **snov.io/email-verifier.html**

**Limits and pacing** — bound by the profile-visit and organization-extraction budgets plus the provider's quota: **50 profiles free**, then paid credits.

**Expected yield** — a CSV of verified and potential addresses; no hit-rate figure published.

**Failure modes** — multi-step and semi-manual; third-party account mandatory; wrong column names break the bulk upload.

Source: https://support.linkedhelper.com/hc/en-us/articles/360015581980-How-to-get-emails-of-your-2nd-and-3rd-connections-in-LinkedIn

---

## R6. Event harvesting → message attendees who are NOT 1st-degree

**Goal** — message LinkedIn event attendees without connecting first.

**Prerequisites** — access to the event's attendee list (Event ID or URL); **`Override platform plug-in`** **only** for profiles **not** sourced from the event page. No invitation spend, no InMail credit.

**Steps**
1. Create from the **`Message sequence via event`** template. Compose the initial message. In **`Check for replies`**, set reply detection to treat **"Message request accepted"** notifications as the acceptance signal.
2. Add follow-ups (optional): set minimum delays; keep total messages **under 3**; follow-ups go only to those who accepted.
3. Collect from LinkedIn: **"My events"** → select the target event → click the **attendees** link to reach the event search results → apply filters → in Linked Helper **`Collect`** → **`From current page`**.
4. Collect from external sources: upload **CSV / HTML / TXT** files of profile URLs. These **must** then be given an Event ID (step 5).
5. Assign the Event ID (mandatory for non-event-collected profiles): open the attendees list via the **"all attendees"** link → copy the **search URL** from the browser → **select the profiles in the Queue** → **`Change platform`** → set **`Collect scope type`** to **"Event ID"** → paste the Event ID/URL into **`Collect scope id`** → **Save changes.**
6. Review the **Queue** tab, exclude or tag unwanted profiles, review the **Workflow** tab action settings, click **`Start`**.
7. Export successful contacts as CSV afterwards.

Copy: anchor relevance in the shared event ("I saw you're attending X") — the strongest personalization token available here.

**Limits and pacing** — if **you organise** the event you may bulk-invite your **1st-degree connections to it "up to 1,000+ per week"**; another post puts safe event invitations at **20-30/day** — use 20-30/day. Per-day cap on messages *to attendees*: **not stated** → `[UNVERIFIED]`. Event-message character limit not stated in the blog; `references/templates.md` lists group/event bodies at **8,000**.

**Expected yield** — the research gives none.

**Failure modes** — **"LinkedIn allows you to send messages to your 3rd-degree connections only"**, so out-of-network attendees are unreachable. Message requests land in **Incoming Requests**, not Messages. Default setting blocks follow-ups until the initial request is accepted. Event ID assignment is **mandatory** for uploaded profiles. Vendor-noted risk: GDPR compliance and LinkedIn ToS — *"always review privacy policies and inform your team about ethical outreach practices."* `[LI-POLICY]`

Sources: https://support.linkedhelper.com/hc/en-us/articles/4413889042450-How-to-send-a-message-to-event-attendees-even-if-they-are-not-your-1st-degree-connections
https://www.linkedhelper.com/blog/hack-to-use-any-linkedin-event-to-boost-outreach-and-invites

---

## R7. Free InMails to Open profiles (no InMail credits consumed)

**Goal** — InMail Premium users who accept unsolicited InMails, without spending credits or invitations.

**What an Open profile is** — an **"Open Link"** / **"Open profile"** is a Premium account holder who has not disabled free InMails; these profiles carry **"a special hidden badge on their pages"**. It is a Premium-only setting the **recipient** enables, letting *"any LinkedIn member send you a message without being your connection."* Sending to one consumes **no InMail credit** — confirmed in two vendor posts.

**Prerequisites** — LH2 campaign from the **InMail sequence** template. Sales Navigator helps but is not required (three discovery methods below). No credits consumed for Open profiles; optionally enable **"Keep attempts to send InMails even if you're out of LinkedIn InMail credits"**.

**Steps — finding Open profiles (three methods)**

*Method A — via Sales Navigator*
1. Collect profiles from **Sales Navigator Search** (**not** the Leads list).
2. Open the campaign's **`Lists`** section.
3. Set the **"Open Link"** filter to **"No"**.
4. **Delete** all the non-Open profiles that surface.
5. **Remove the filter** — only Open profiles remain.

*Method B — Basic/Premium LinkedIn, filter trick* — apply the **"Service categories"** filter in your search, which **"automatically enables 'Open link' profile status."** Combine with the 2nd-degree connection filter if your account is restricted to 2nd degree.

*Method C — Basic/Premium LinkedIn, extract-then-filter*
1. Run a **`Visit & Extract profiles`** campaign.
2. Filter by **Premium** status and extract those profiles.
3. Filter the extracted results by **"Open link"** status.
4. Migrate the survivors into your InMail campaign.

**Steps — campaign setup**
1. Create from the template documented as **"How to send InMails to 2nd & 3rd connections in LinkedIn, Sales Navigator, or Recruiter (InMail sequence template)"**.
2. Write inside the exact limits: **subject up to 200 characters**, **body up to 2,000 characters**, and **the signature counts inside the character limit**.
3. Optionally enable **"Keep attempts to send InMails even if you're out of LinkedIn InMail credits"**.
4. Start the campaign.

**Limits and pacing** — Open-profile allowance **"approximately 800 InMails per month"** for most accounts, **as low as 100** for some; some accounts are restricted to **2nd-degree connections only**.

CONFLICT — Open-profile outbound volume. Help centre: **~800/month**, as low as **100**. Blog: *"some users report ~20 messages"* vs *"others 50-100+"* monthly; Recruiter Lite ~**100/month** free Open-Profile messages; Standard accounts "several hundred monthly". Treat the blog spread as `[UNVERIFIED]` and pace from the conservative end.
Sources: https://support.linkedhelper.com/hc/en-us/articles/360016670759-How-to-send-free-InMails-to-Open-profiles · https://www.linkedhelper.com/blog/linkedin-open-profile

CONFLICT — InMail body limit: this recipe's source says **2,000** characters, another article says **1,900** (`references/templates.md`). Write to **1,900**.

**Expected yield** — **Open-profile prevalence: 0.2-2% among non-Premium users; 15-50%+ among Premium users** `[LH-CLAIM]`. Targeting Premium users first is what makes this recipe economical. InMail reply figures are in §Benchmarks and contradict each other.

**Failure modes** — collecting from the Sales Navigator **Leads list** instead of **Search** breaks Method A. A low-Premium audience makes the recipe uneconomical. At scale the play is: Sales Navigator search → extract → filter on Open Link (an **extractable field**) → message that segment free, preserving credits for everyone else; LH pitches this for Recruiter, since *"Recruiter has no native one-click mass-InMail tool."*

Sources: https://support.linkedhelper.com/hc/en-us/articles/360016670759-How-to-send-free-InMails-to-Open-profiles
https://www.linkedhelper.com/blog/linkedin-open-profile · https://www.linkedhelper.com/blog/linkedin-recruiter-inmail · https://www.linkedhelper.com/blog/sales-navigator-automation

---

## R8. Re-engage the connections that accepted one specific inviting campaign

**Goal** — message the people who just accepted invitations from one particular campaign, not your whole 1st-degree list.

**Prerequisites** — Option 1 needs an existing campaign containing an **`Invite 2nd and 3rd contacts`** action; Option 2 needs nothing. No credits, no extra plug-ins.

**Steps — Option 1: extend the existing inviting campaign (preferred)**
1. Open the existing inviting campaign.
2. Add **`Filter contacts out of my network (keep 1st level only)`**.
3. Add **`Message to 1st connections`**.
4. Linked Helper **automatically adds a `Check for replies` action**.
5. Configure **`Check for replies`** to control the delay between messages and when profiles move to the success lists versus receive another message.

**Steps — Option 2: build fresh from a template**
1. Open the campaign templates list.
2. Select a pre-built template such as **"Invite and Follow Up"**.
3. Follow the template's guided setup.
4. Configure the messaging sequence and delays.

Copy: first message = **"Thank you for accepting"** class, **2-3 days** after acceptance; the offer comes in message 2 or 3, **3-7 days** apart.

**Limits and pacing** — `Check for replies` is the documented pacing control point (minimum interval **10 minutes**, default cycle **60 minutes**). Keep to 3 messages.

**Expected yield** — the research gives none.

**Failure modes** — Option 1 scopes messaging to that campaign's cohort only, which is the point; a generic `Message to 1st connections` campaign sprays the whole network instead. Skipping the network filter leaves the messaging action nothing valid to process.

Source: https://support.linkedhelper.com/hc/en-us/articles/360016380399-How-To-Send-message-to-recently-added-LinkedIn-connections-from-a-certain-inviting-campaign

---

## R9. Post-engagement targeting (collect likers and commenters)

**Goal** — build a lead list from people who engaged with a specific post: the warmest cold audience on LinkedIn.

**Prerequisites** — the post's own unique URL. **Hard requirement:** collection works only when **"a post is opened via its own unique URL."** Feed-opened posts show no collection options. No tier, plug-in or credit requirement documented.

**Steps**
1. Find the post.
2. Click the **three dots** in the post's upper-right corner.
3. Select **"Copy link to post"**.
4. Open the post via that link — click **"View Post"**, or paste the URL into Linked Helper's address bar.
5. Open the **`Collect`** dropdown — the likers/commentators options now appear.
6. Collect into a campaign Queue and feed it into R1's warm-up funnel, or into R3/R6 if a shared group or event exists.

**Limits and pacing** — likes + comments combined ~**150/day** per safe-limits guidance; a stricter post says **20-80/day**. Own publishing: **1-2 posts/day, 3-7/week**. The `Boost post` action (which mentions profiles in comments) is capped at **"100 mentioned profiles per 24 hours"**; `Post liking` has its own Advanced limit counting **liked posts**, not profiles processed.

**Expected yield** — no conversion figures. Only engagement benchmark published: LinkedIn **median engagement rate 0.41%** (Nov 2023) vs Instagram 2.49%, Facebook 1.65%, Twitter 1.33%.

**Failure modes** — a post opened from the feed offers no collect options at all; this is the usual cause of "the option doesn't exist". `[UNVERIFIED]` — no documented maximum number of collectible likers/commentators, no rate limit, no statement of whether *all* engagers are retrievable, no account-level restrictions. The vendor **warns against engagement pods**.

Sources: https://support.linkedhelper.com/hc/en-us/articles/360015766440-Is-it-possible-to-collect-those-who-liked-or-commented-post
https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use
https://www.linkedhelper.com/blog/boosting-linkedin-posts · https://www.linkedhelper.com/blog/running-30-linkedin-accounts

---

## R10. Quality filter: invite only prospects with 500+ connections

**Goal** — concentrate invitations on well-connected (usually more active) prospects.

Constraint, verbatim: *"Linked Helper does not have a filtering option for the number of connections."* This is therefore a **CSV round-trip** recipe; the steps are inline because it is not executable without them.

**Prerequisites** — Excel or Google Sheets; a campaign that visits profiles. No plug-in or credit requirement documented.

**Steps**
1. **Extract profiles:** add 2nd/3rd-degree connections to a campaign and let Linked Helper visit them — connection-count data is gathered automatically during profile visits.
2. **Export to CSV** from `Successful`. Locate the column **`network_info_connection_count`**.
3. **Filter in Excel:** import the CSV, sort/filter on `network_info_connection_count`, delete rows below **500**, keep the 500+ rows.
4. **Re-upload:** upload the edited CSV into the **`Invite 2nd & 3rd connections`** action and run.

Tip from the article: follower counts correlate closely with connection counts and can serve as an alternative sort key.

**Limits and pacing** — CSV/URL import ceiling: documented **45 profiles per 24 h** to avoid logouts, while the `Load LinkedIn profile via URL` advanced limit defaults to **40 per 24 h** — CONFLICT; use **40** (SKILL.md §4, `references/campaigns.md`).

**Expected yield** — the research gives none.

**Failure modes** — without the profile-visit pass the connection-count column is empty. Re-uploading the unfiltered export silently defeats the recipe.

Source: https://support.linkedhelper.com/hc/en-us/articles/360016704160-How-to-invite-only-those-who-have-more-than-500-connections

---

## R11. Message-writing playbooks: RRR, "never sell first", and the numbers

**Goal** — write invitation notes and first messages that get accepted and answered.

**Prerequisites** — `Custom template variables plug-in` for `{cs_*}` fields; the conditional plug-in for IF-THEN-ELSE (`references/templates.md`). No credits.

### R11a. The RRR technique — Relevance, Reward, Request

Developed by **Winning by Design**; reportedly improved outreach campaign success by **3x** `[LH-CLAIM]`.

1. **Relevance** — personally targeted: use the recipient's name and company; reference shared connections; quote their LinkedIn summary; show knowledge of their business focus; connect shared interests. Verbatim examples: *"I saw that we share Brian Moe as a common connection"* · *"I saw that you focus on helping salespeople to attain their goals through high-impact coaching."*
2. **Reward** — the benefit of connecting: how you have helped similar clients; the specific pain you solve; quantified value; how little effort is needed from them for a large return.
3. **Request** — one clear CTA: ask for a referral, propose a discovery call, or pose an opening question.

Economics cited: a scheduled appointment with the right prospect costs B2B SaaS companies over **EUR 300**; a 10-person sales team spends **~7,200 hours annually** setting up meetings — roughly **EUR 540K** in yearly operating cost. The technique aims to cut per-appointment cost to **EUR 45 or less**. `[LH-CLAIM]`

Source: https://support.linkedhelper.com/hc/en-us/articles/360015583559-How-to-make-your-LinkedIn-messages-3x-times-more-effective-using-the-RRR-technique

### R11b. Never sell on the first message

Core rule: no selling on first contact; build the relationship gradually. Four documented opening tactics: **"Start the message off with a simple hello and an introduction"** · ask questions relevant to their industry or posts · invite them to join a community (group, page) · **provide value first** (e.g. a free audit). Why: a first-touch pitch **"lacks personalization"**, people resist **"hard sell"** tactics, and **"they don't know you"** yet. Two frameworks named: **Active Lead Generation** (direct outreach, 11 stages) and **Passive-Active** (profile optimization → content engagement → strategic outreach).

`[UNVERIFIED]` — this article gives **no** day-gap numbers and **no** complete templates; use R11c.

Source: https://support.linkedhelper.com/hc/en-us/articles/360018839719-Never-Sell-On-Your-First-LinkedIn-Message-The-Real-LinkedIn-Sales-Process

### R11c. The numbers that do exist

**Invitations** — no sales offer in the request (it reduces acceptance); skip the note entirely if unsure it will resonate; **no links in invitations** (LinkedIn may flag them as spam).

**Messages to 1st connections** — use **custom variables** beyond the standard `{firstname}`; use **"IF|THEN|ELSE clauses"** to reference mutual connections or industry alignment; open with a casual **"Thank you for accepting"** before any offer; **wait 2-3 days** between connection and first message.

**Structure** — **"Break your huge message into 2 or 3 messages with the 3 - 7 days intervals between them."** Split messages containing multiple links or media into individual messages. Include images, infographics or videos. **Upload videos to LinkedIn rather than linking YouTube content.**

**Sequencing** — send messages **one-by-one** (not bulk bursts) to appear human-like; insert **`Check for replies`** between message steps. The article's own example is a **14-step** sequence: profile auto-following → timed delays (2-3 days) → sequential messaging → reply checking.

**Length** — InMails **under 400 characters** perform **22% better** `[UNVERIFIED]`; ideal connection-note length **120-240 characters**, shorter = higher acceptance (no % given).

Core takeaway, verbatim: **"Do not be too intrusive; Avoid pushing people; Create structured and human-like messages."**

Sources: https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2
https://www.linkedhelper.com/blog/linkedin-inmail-vs-message · https://www.linkedhelper.com/blog/linkedin-prospecting-messages

---

## R12-R14, R16. Exclusions, tagging, cloning, CSV workflows — pointers

Full detail in `references/campaigns.md`:

- **R12 exclusion and dedup** — tag-based export ratchet (`Successful` sub-list, `Tag` button, **"With tags"** / **"Without tags"** filters, bin icon), automatic within-campaign dedup, `Lists Manager` **"Remove intersections between campaigns"**, cross-account exclusion via CSV, `Filter by message content` plug-in, and hiding CRM profiles with a `deleted` tag (CRM profiles cannot be deleted). Sources: https://support.linkedhelper.com/hc/en-us/articles/360016661299-I-extracted-exported-LinkedIn-profiles-and-want-to-export-new-without-already-extracted · https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates · https://support.linkedhelper.com/hc/en-us/articles/360015485399-Can-I-delete-profiles-from-CRM
- **R13 bulk-tag from a CSV of profile URLs** — `Visit and extract` campaign + `Tagging system plug-in`. Source: https://support.linkedhelper.com/hc/en-us/articles/360016738299-Is-it-possible-to-tag-multiple-contacts-in-my-list-based-on-a-CSV-file-with-URLs
- **R14 cloning and porting** — `Clone` within an account (actions, settings and templates copied; **Queue profiles are NOT copied**); `Download` / `Upload campaigns` / `Choose file` / `Import` across accounts, needing the `Multi-campaigns runner plug-in` on both and version **> 2.54.27**. Source: https://support.linkedhelper.com/hc/en-us/articles/360019349660-How-to-duplicate-clone-a-campaign-or-copy-it-to-another-LinkedIn-account
- **R16 CSV catalogue** — the eight documented in/out patterns. Hard rule, repeated because recipes depend on it: exports from **`Queue`** contain **no email addresses** — always export from **`Successful`**. On `Download` you pick the delimiter format for **Google Sheets** or **MS Excel**. Source: https://support.linkedhelper.com/hc/en-us/articles/360016685199-Why-don-t-all-contacts-in-a-CSV-file-have-e-mail-addresses

Two cross-recipe rules: **porting a campaign moves no profiles** — *"Linked Helper does not move profiles to avoid reaching out to the same leads using different LinkedIn accounts."* If you move them manually, apply cross-account exclusion. **A/B testing:** clone within one account, change **one** variable, use **"Exclude profiles from the current campaign"** so arms draw from disjoint audiences; `[UNVERIFIED]` — no built-in split-test or per-variant statistics exist, and spintax / variations / IF-THEN-ELSE randomize without reporting performance.

Source: https://support.linkedhelper.com/hc/en-us/articles/23378382591250-How-to-stay-safe-when-managing-accounts-via-Linked-Helper

---

## R15. Recruiting and hiring-signal outreach

**Status: LARGELY `[UNVERIFIED]` as a dedicated recipe.** The help centre's Recipes and tips category contains **no** recruiting-specific or hiring-signal playbook. What follows is assembled from documented building blocks — present it to users as derived, never as vendor-documented.

**Prerequisites (per component)**
- **`Recruiter Lite`** subscription: **"no LinkedIn Commercial Use Limit"**, **"30 InMails per month"**, advanced talent-acquisition search filters. Source: https://support.linkedhelper.com/hc/en-us/articles/360031167451-Do-I-need-paid-LinkedIn-subscription-to-use-your-service-What-advantages-can-I-get-with-a-paid-LinkedIn-subscription
- **`Employees extractor`** action — pull people from target companies (`references/actions.md`; template article https://support.linkedhelper.com/hc/en-us/articles/22067310525074-Employees-extractor-template).
- **`Override platform plug-in`** — switches the platform an action uses; the InMail sequence template explicitly covers **"LinkedIn, Sales Navigator, or Recruiter"**. Source: https://support.linkedhelper.com/hc/en-us/articles/360016670759-How-to-send-free-InMails-to-Open-profiles
- **AI ICP detection** action — screen a queue against a described ideal profile (`references/actions.md`; per-operation AI credit rates are `[UNVERIFIED]`).

**Steps (DERIVED)**
1. Run **`Employees extractor`** against target companies.
2. Screen the queue with **AI ICP detection**.
3. Split the survivors: **R7** Open-profile InMail arm for Premium candidates; **R1** warm-up-then-invite arm for the rest.
4. Run **R4** `Find Profile Emails` on the unreachable remainder.
5. Optionally feed **R9** (engagers on hiring-adjacent posts) into step 3.

**Limits and pacing** — Recruiter Lite: **30 InMails per month** of paid credit; Open-profile InMails do not consume it (Recruiter Lite ~100/month free Open-Profile messages, `[UNVERIFIED]`). Everything else follows the standard per-action ceilings.

**Expected yield** — one weak figure: connected candidates show **46% higher** acceptance rate `[UNVERIFIED]`. Source: https://www.linkedhelper.com/blog/linkedin-drip-campaign

**Failure modes** — **"hiring signal" targeting (e.g. companies posting jobs) is `[UNVERIFIED]`**: no help-centre article documents a job-posting or hiring-intent data source inside Linked Helper. Sales Navigator's own filters would be the source; the help centre notes only that SN **"Enables filtering by recent posts and company followers"**.

---

## R18. Boolean and Google X-ray targeting

**Goal** — find more of the right people per search, and find profiles without LinkedIn logging a view.

**Prerequisites** — LinkedIn search box (any tier) for boolean; a browser for X-ray; Sales Navigator or Recruiter for the advanced filter fields. No plug-in, no credits.

**Steps — boolean in the LinkedIn search box.** Five supported operators, with the vendor's stated **precedence order**:

```
1. quoted phrases   ""      processed first
2. NOT                      applied next
3. AND
4. OR                       last
```

`AND` — all terms · `OR` — any of the terms · `NOT` — exclude a term · `""` — exact phrase as typed · `()` — group terms and control logic. Works in: the main search bar, the **Title** and **Company** advanced filter fields, and in Google via `site:`. Caveat, verbatim: *"In the Title field… search is limited to the **current position** only."*

Canonical example, verbatim:

```
("software engineer" OR developer) AND ("Python" OR "Django") NOT "Intern"
```

**Counter-tactic:** rather than one long AND-chain, split into **separate simpler searches** per job title — *"Dev Architect AND Senior AND Technical Director"* as three searches yields more and more accurate results than one query.

`[UNVERIFIED]` — wildcards, `+`/`-` operators and any search-box character limit are not documented anywhere on the blog.

**Steps — Google X-ray.** Operators: `site:` `intitle:` `inurl:` `""` `OR` `-` `*`. The eight query strings below are verbatim:

```
site:linkedin.com/in "sales manager" "Germany"
site:linkedin.com/in "hiring manager" "Google" "New York"
site:linkedin.com/in ("software engineer" OR "developer") -freelancer
site:linkedin.com/in ("data analyst") "gmail.com"
site:linkedin.com/in "head of operations" "Amsterdam" -jobs
site:linkedin.com/in "supply chain manager" "Unilever" "Singapore"
site:linkedin.com/in intitle:"project manager" "San Francisco"
site:linkedin.com/in "marketing director" AND ("Berlin" OR "Munich") -jobs
```

Single-operator forms shown:

```
site:linkedin.com/in
intitle:"product manager"
inurl:linkedin.com/in "marketing"
"sales development manager"
"hiring manager" OR recruiter
site:linkedin.com/in -jobs
"* at Google"
```

**Limits and pacing** — X-ray finds public profiles **without LinkedIn logging a profile view** and **without consuming search quota**. Feeding X-ray results into LH2 still spends `Load LinkedIn profile via URL` budget (**40 / 24 h** default; see R10's CONFLICT).

**Expected yield** — the research gives none.

**Failure modes** — `[UNVERIFIED]` / absent from the docs: country subdomains (`de.linkedin.com`), legacy `/pub/` paths, Google's own result caps. Boolean in the `Title` field matches only the **current** position, so past-role targeting silently fails.

Sources: https://www.linkedhelper.com/blog/linkedin-boolean-search
https://www.linkedhelper.com/blog/linkedin-xray-search · https://www.linkedhelper.com/blog/search-linkedin-like-pro

---

## R19. Beating LinkedIn's search-result caps

**Goal** — extract more than one search page's worth of an addressable market.

**Prerequisites** — Sales Navigator for exclusion filters, Spotlight-style signal filters and saved-search auto-collect. Free LinkedIn works for slicing only.

**Steps**
1. **Know the ceiling.** Free: **1,000 people / first 10 pages**. Sales Navigator & Recruiter: **2,500 per search**. CONFLICT — one post says "roughly 1,000 per search result page" for Sales Navigator, incompatible with 2,500 per search. Plan against **2,500 per search** and verify on a small run.
2. **Slice, don't stretch.** Split one large query into smaller segments by geography, seniority tier and company-size band; track visited/invited profiles so segments do not reprocess the same people (`references/campaigns.md`).
3. **Use Sales Navigator exclusion filters** — the real differentiator over free search: *"choose not to collect profiles from a specific industry/company."*
4. **Layer filters in these documented combos:** `job title + seniority + company size` · `geography + function + years in current role` · `saved lists by group membership` (pre-warmed outreach — feeds R3).
5. **Add Spotlight-style signal filters:** recent job changes, leads with recent LinkedIn activity, posted-content keywords, account alerts (layoffs, slowing growth, shared updates, news mentions), buyer-intent (profile views from saved accounts), **Open Link status** (feeds R7).
6. **Turn on auto-collect** — re-collect leads from a saved Sales Navigator or LinkedIn search page **every X days** automatically, so the pool refreshes without manual re-runs.
7. **Build lists title-first, not company-first:** *"start with a people search for the desired title"*, then narrow by location/company/industry.
8. **Use quota-free sources before stretching a capped search.** Collecting from **alumni pages** is *"noted as not counting toward search limits"*, alongside group members, post likers/commenters and network pages — cheap capacity once the Commercial Use Limit bites. Google X-ray (R18) consumes no search quota at all.
9. **Multi-account extraction trick (documented, high risk):** accumulate leads while a Sales Navigator subscription is active, then extract them using several basic LinkedIn accounts with no subscription, to parallelise throughput. See the ban-cluster warning in `references/limits-safety.md`.

**Lead sources ranked by warmth signal.** The vendor never publishes an explicit yield ranking (**absent — do not fabricate one**); this is the sources it names, ordered by the warmth signal each carries:

1. Your own post likers / commenters — strongest intent signal, free to message
2. Competitor post commenters — has a dedicated template
3. Event attendees (your event = free direct messaging) → R6
4. Group co-members (free messaging to 2nd/3rd degree) → R3
5. Company employee pages (org-chart penetration)
6. Alumni pages — explicitly **not counting toward search limits**
7. Sales Navigator saved searches / lead lists (best filters)
8. Regular LinkedIn search (capped at 1,000)
9. Recruiter search
10. CSV upload / email databases (enables invite-by-email — weakest evidence, see §Tactics)
11. Profile viewers ("who viewed your profile" — has its own template)
12. Hashtag search — surfaces influencers producing relevant content
13. Google X-ray — no view logged, no quota consumed
14. **LION / open networkers** — highest raw acceptance, lowest lead quality

**LION / open networkers.** LION = a member publicly signalling they accept requests from strangers. Find them by searching `LION` or `L.I.O.N.` in global search, prefixing niche terms (`attorney recruiter LION`), filtering by job title, or joining dedicated LION groups with thousands of members. **Measured acceptance: ~54% initially on a blank profile, then dropped to 43%** — the vendor calls this "excellent for new accounts" `[LH-CLAIM]`. Risks: feed spam, irrelevant inbound, scam exposure, and your **email and phone become more accessible**. Vendor caution: *"quantity doesn't always equate to quality."* Use as a **warm-up acceptance-rate booster on a fresh account**, not as an ICP list.

**Expected yield** — **extracting 6,000 leads takes ~40 days** at standard rates (150 visits/day). Size segments against that.

**Failure modes** — slicing without exclusion tracking re-processes the same people and burns the profile-visit budget; auto-collect on a badly-filtered saved search quietly fills the queue with off-ICP leads.

Sources: https://www.linkedhelper.com/blog/sales-navigator-automation
https://www.linkedhelper.com/blog/linkedin-advanced-people-search-for-automated-campaigns
https://www.linkedhelper.com/blog/linkedin-sales-navigator-export-leads-to-excel
https://www.linkedhelper.com/blog/how-to-scrape-linkedin-data · https://www.linkedhelper.com/blog/search-linkedin-like-pro · https://www.linkedhelper.com/blog/linkedin-open-networker

---

# Tactics that claim to beat limits — ranked by evidence quality

Strongest evidence first. Ranking is by how well the vendor's own material substantiates the tactic, not by the volume it promises. Never present a tactic from the bottom of this list as working.

**1. Event messaging — strongest of the group.** Free private messages to attendees, no connection and no InMail credit: *"If you're organizing a LinkedIn Event, you can privately message the attendees for free."* Dodges **both** the invite cap and the InMail pool. Bulk-invite your 1st-degree connections to the event **"up to 1,000+ per week"**; another post puts safe event invitations at **20-30/day** — use 20-30/day. Per-day attendee-message cap and event-message character limit **not stated** → `[UNVERIFIED]`. Risks named: GDPR and LinkedIn ToS. Procedure: **R6**.
Source: https://www.linkedhelper.com/blog/hack-to-use-any-linkedin-event-to-boost-outreach-and-invites

**2. Open Profile / Open Link — free InMails.** Sending to an Open Profile consumes **no InMail credit**, confirmed in two posts. Dodges the InMail pool and the invite cap. Open Link is an **extractable field**, which is what makes it operable at scale. Volume ceilings contradictory (CONFLICT in R7) → pace from the low end. Procedure: **R7**.
Sources: https://www.linkedhelper.com/blog/linkedin-open-profile · https://www.linkedhelper.com/blog/linkedin-recruiter-inmail

**3. Group messaging — free 2nd/3rd-degree DMs.** *"LinkedIn allows you to send messages to people who are not your direct contacts if you are members of the same group."* Exposed as **"Message to group members"**, reaching 2nd and 3rd degree *"without the need to invite all profiles to connect first."* Ceilings contradicted: safe-limits post **10-15/day** vs the groups posts' *"hundreds of people a day"* — **trust 10-15/day**. `[UNVERIFIED]`: max groups joinable, max members scrapable, character limit. Procedure: **R3**.
Sources: https://www.linkedhelper.com/blog/linkedin-groups · https://www.linkedhelper.com/blog/use-linkedin-groups-to-generate-leads · https://www.linkedhelper.com/blog/linkedin-automation-limits

**4. Company Page follow-invites — a separate credit pool.** Page admins invite their own 1st-degree connections to follow the Page, from a **different budget** than personal invites. Monthly pool historically **250/month**, being reduced to **as low as 50/month** in a staggered 2026 rollout; resets on the 1st; 1 credit per invite; refunded **~72 h** after acceptance; declines/ignores refund only at month reset. **Only Page admins** may send, and only to **their own 1st-degree connections** — the admin's network is the hard ceiling on Page growth. Best sub-tactic: on **Premium Company Pages**, invite people who **reacted/commented/shared in the last 30 days** or follow similar Pages — **these engager invites cost no credits at all.** Risks: burning credits on ineligible people; no refund on declines.
Source: https://www.linkedhelper.com/blog/how-to-invite-people-to-follow-your-linkedin-page-automatically

**5. Follow instead of connect.** One-way content subscription, no acceptance required; following **does not count against** the weekly invite cap. CONFLICT on the ceiling: the follow-vs-connect post says *"follow an unlimited number of people daily"*, the safe-limits post says **~100-150/day** — **use 100-150/day**. Secondary uses: warm-up (*"following first also increases the chance that someone checks out your profile and chooses to connect with you proactively"*); capacity relief near the **30,000** 1st-degree ceiling; make Follow the default CTA via `Settings > Visibility > Followers > Make Follow primary`.
Source: https://www.linkedhelper.com/blog/linkedin-follow-vs-connect

**6. Alumni pages — quota-free collection.** Collecting from **alumni pages** is *"noted as not counting toward search limits"*, alongside group members, post likers/commenters and network pages. Cheap, low-risk, no published ceiling.
Source: https://www.linkedhelper.com/blog/search-linkedin-like-pro

**7. Post engagement as a lead source.** Dodges **nothing** directly — it raises **acceptance rate**, which is itself the main throttling input. Ceilings: likes + comments combined ~**150/day** (or 20-80/day by the stricter post); **1-2 posts/day, 3-7/week**. Honesty note: the dedicated `boosting-linkedin-posts` post contains **none** of the scraping tactics, daily limits or acceptance-rate correlation data it appears to promise; its only benchmark is LinkedIn's median engagement rate **0.41%** (Nov 2023). It also **warns against engagement pods**. Procedure: **R9**.
Sources: https://www.linkedhelper.com/blog/boosting-linkedin-posts · https://www.linkedhelper.com/blog/running-30-linkedin-accounts

**8. Move off-platform to email.** Extract emails (1st-degree visible addresses, or Snov.io / Apollo enrichment) and run the sequence over email — described as "unlimited" reach outside LinkedIn's counters. **But** the mass-email post gives **no Gmail/SMTP daily sending caps, no deliverability numbers, and never confirms whether this bypasses LinkedIn limits** → the ceiling is your own sending infrastructure, `[UNVERIFIED]`. Procedure: **R4 / R5**.
Sources: https://www.linkedhelper.com/blog/how-to-send-a-mass-email-to-linkedin-contacts-automatically · https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit

**9. Multi-account horizontal scaling.** The blunt limit-beater: N accounts x ~100 invites/week. Highest setup cost and highest ban-cluster risk of any tactic here — one shared IP can take down the whole cluster. Per-account infrastructure cost, the 4-5 accounts per 16 GB machine figure and the 30-account case study are in `references/limits-safety.md`.
Source: https://www.linkedhelper.com/blog/running-30-linkedin-accounts

### 10. Invite by email — WEAKEST EVIDENCE. Treat as broken.

**What it is.** Upload a CSV of email addresses; LH sends connection invitations addressed to the **email** rather than through the normal profile-invite flow, using what the blog repeatedly calls *"an undocumented LinkedIn feature."* A personal note **is** allowed: *"In the action where the software invites 2nd and 3rd degree connections, it's possible to add a personal message."* Setup as documented: install LH → "People campaign" → template **"Invite by email & follow up"** → upload CSV or import from LinkedIn pages into the Queue → Start. Claims to dodge the ~100 invites/week cap.

**CONFLICT — the docs give three incompatible ceilings, plus a fourth worked example:**

| Claim | Source |
|---|---|
| "exceed the limit by 7 times" ≈ **700 email invites/week** | https://www.linkedhelper.com/blog/invite-someone-to-linkedin-by-email-beat-the-100-invites-week-limit |
| **100 the first day, then 20/day** on Standard ≈ **~220/week**; "unlimited" on Premium; up to **1,000 leads/week** | https://www.linkedhelper.com/blog/weekly-invite-limit-linkedin |
| *"100 invites per week are less effective than the possible **500 or 700** you can send with Linked Helper"* | https://www.linkedhelper.com/blog/mass-invites-grow-sent-connection-requests-on-linkedin-by-7-times |
| One worked example: **688 invites sent successfully** | https://www.linkedhelper.com/blog/automate-linkedin-risk-free |

700/week, ~220/week and 500-or-700/week cannot all be true; no post states which supersedes which. Whether email invites count against the 100/week cap is **never stated explicitly** — the implication is that they operate outside the native counter → `[UNVERIFIED]`.

**Status — the critical finding: the vendor has acknowledged the feature broken since 2023.** The `weekly-invite-limit-linkedin` post still contains: *"The feature we are discussing in the article is **not functional for the majority of accounts as of August 2023**"* — under a 2026 "updated" stamp. The `mass-invites` post is the only one with a real date: **published 2022-04-29, last updated 2023-09-11.**

**Operator conclusion: treat invite-by-email as largely dead / account-specific. Do not build a plan on it.** If a user asks for it, say the vendor's own page reports it non-functional for most accounts since August 2023, show the conflicting ceilings, and route them to tactics 1-3.

**Risk note.** Neither the invite-by-email nor the mass-invites post discusses account risk or ToS exposure at all — a notable omission for a tactic described as exploiting an undocumented feature. `[LI-POLICY]` automating LinkedIn access violates the User Agreement regardless.

Sources: https://www.linkedhelper.com/blog/invite-someone-to-linkedin-by-email-beat-the-100-invites-week-limit
https://www.linkedhelper.com/blog/weekly-invite-limit-linkedin
https://www.linkedhelper.com/blog/mass-invites-grow-sent-connection-requests-on-linkedin-by-7-times
https://www.linkedhelper.com/blog/automate-linkedin-risk-free

---

# Benchmarks

Every figure below is quoted by Linked Helper; most carry no primary citation. Quote them with the tag attached, or not at all.

### Acceptance rates

| Metric | Figure | Tag | Source |
|---|---|---|---|
| Personalised vs generic invite acceptance | **~45%** vs **~15%** | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-message-automation |
| Warmed vs cold prospects | **+10-20%** higher acceptance | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/how-to-automate-linkedin-outreach |
| LION acceptance, blank profile | **54%** initially, dropping to **43%** | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-open-networker |
| Connected candidates (recruiting) | **46% higher** acceptance rate | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-drip-campaign |
| Minimum safe acceptance rate | **>25%** (below ~20% → faster throttling) | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-automation-limits · https://www.linkedhelper.com/blog/linkedin-pending-connections |

### Reply / response rates

| Metric | Figure | Tag | Source |
|---|---|---|---|
| Invite **with** personalised note → reply | **9.36%** | cited to **Expandi H1 2025 report** | https://www.linkedhelper.com/blog/linkedin-message-automation |
| Invite **without** note → reply | **5.44%** | cited to **Expandi H1 2025 report** | https://www.linkedhelper.com/blog/linkedin-message-automation |
| InMail response rate | **10-25%** ("~300% higher than cold email") | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-inmail-vs-message |
| InMail response rate | **18-25%** vs ~**3%** cold email | `[UNVERIFIED]` — **CONFLICT with the 10-25% row; both vendor-published** | https://www.linkedhelper.com/blog/linkedin-recruiter-inmail |
| Regular DM reply, once connected | **18-25%** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-inmail-vs-message |
| Personalised vs generic InMail | **166% higher** reply | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-cold-message-template |
| InMail open rate | **57.5%** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-drip-campaign |
| InMail reply timing | **65% within one day; 90% within a week** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-drip-campaign |
| Email open-rate benchmark for comparison | **15-25% "good"** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-drip-campaign |
| Company followers more likely to respond | **81% more inclined** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-drip-campaign |

### Copy-length effects

| Metric | Figure | Tag | Source |
|---|---|---|---|
| InMails **under 400 characters** | perform **22% better** | `[UNVERIFIED]` | https://www.linkedhelper.com/blog/linkedin-inmail-vs-message |
| Ideal connection-note length | **120-240 characters**; shorter = higher acceptance (no % given) | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-prospecting-messages |
| Long pitch | split into **2 or 3 messages, 3-7 day intervals** | `[LH-CLAIM]` | https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2 |

### Engagement and SSI

| Metric | Figure | Tag | Source |
|---|---|---|---|
| LinkedIn median engagement rate | **0.41%** (Nov 2023) vs Instagram 2.49%, Facebook 1.65%, Twitter 1.33% | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/boosting-linkedin-posts |
| SSI bands | 0-100, four pillars at 25 points each (personal brand · finding the right people · engaging with insights · building relationships); 0-30 low · 31-69 moderate · **70+ high** · **80+ top-tier**; average by role **55-80** | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-ssi-score |
| SSI outcome claim | *"Top social sellers average SSI above 70"*; users above 70 *"generate 45% more opportunities"* | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-ssi-score |
| SSI → invite limits | "100-250 depending on your SSI score" | `[UNVERIFIED]` — the SSI post itself makes **no** claim that SSI affects invite limits or automation safety | https://www.linkedhelper.com/blog/multiple-linkedin-accounts |

Check SSI at `www.linkedin.com/sales/ssi` (no Premium needed).

### Operational throughput

| Metric | Figure | Tag | Source |
|---|---|---|---|
| Extracting **6,000 leads** | **~40 days** at standard rates (150 visits/day) | `[LH-CLAIM]` | https://www.linkedhelper.com/blog/linkedin-sales-navigator-export-leads-to-excel |
| 30-account operator | **10-50% of client meetings** attributed to LinkedIn; network grown **1,500 → ~10,000** connections; **>100 hours/week** saved; **zero bans** | `[LH-CLAIM]` — marketing | https://www.linkedhelper.com/blog/running-30-linkedin-accounts |
| Restriction/ban search demand | **12,050 monthly searches** across 9 English-speaking markets | `[LH-CLAIM]` — demand signal, not performance | https://www.linkedhelper.com/blog/linkedin-automation-security-study |

### Benchmarks the blog promises but never delivers — do not invent these

- **Conversion rates per funnel stage** — the funnel guide has **none**. https://www.linkedhelper.com/blog/linkedin-automated-marketing-funnel-sales-funnel-automation-guide
- **Acceptance-rate benchmarks** in the 20-messages post — **none**.
- **Uplift figures for image personalisation** — **none**.
- **Ban rates by tool architecture** — **none**, even in the vendor's own security study.
- **Email sending caps and deliverability rates** — **none**.
- **An explicit yield ranking of lead sources** — never published; R19's ordering is by warmth signal, not measured yield.
- **A/B split-test statistics** — no built-in split-test or per-variant reporting exists.
- **Per-recipe conversion figures** for R1, R3, R6, R8, R9, R10 and the group/event routes — none. Say so, and offer to check `support.linkedhelper.com`.
