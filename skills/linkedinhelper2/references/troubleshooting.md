# Linked Helper 2 — Troubleshooting Playbook
Symptom → cause → checks → fix. Every entry carries its `Source:`. Static reference data (OS support matrix, hardware sizing, default user-data folder paths, licence/plan gating, VPS specs) lives in `references/plans-and-platform.md` — this file keeps only the diagnostic material.

Support channels used by the fixes below: **info@linkedhelper.com** · Facebook Messenger **m.me/linkedhelpertool** · WhatsApp **+447727440361** · Help Center https://linkedhelper.zendesk.com/hc/en-us · availability **"7 days a week"**, average reply **"about 15 minutes"**. [LH-CLAIM]
Source: https://support.linkedhelper.com/hc/en-us/articles/360017185399-Need-help

## TRIAGE ORDER — run this sequence before anything else
1. **Is the plug-in installed?** The interface is plug-in driven and a **minimalist interface is the default for new users**. A missing action, list, field or button is almost always an uninstalled plug-in, not a bug and not a missing feature. Open `Plug-in store` and install the plug-in the doc names. → §B12.3
2. **Is the campaign `Sleeping` or `Queued` rather than broken?** Hover the campaign status → click **"See reasons"** → the popup lists every applicable reason verbatim. This is the app telling you the answer; read it before diagnosing anything. → §B1.1
3. **Is the Queue actually empty, or were profiles silently skipped at collection?** → §B1.2
4. **Are Advanced limits throttling below the daily cap** — especially `Load profile page`? → §B1.3
5. **Is a LinkedIn-side limit or restriction in play?** Read the exact warning string. → §B3, `references/limits-safety.md`
6. **Can you perform the same action manually in LinkedIn?** If manual also fails, it is LinkedIn-side and no app setting will fix it. → §B3.2, §B3.3
7. **Is the funnel missing `Filter contacts out of my network (keep 1st level only)`?** This is the single most common reason follow-ups never fire. → §B4.1
8. **Is the network/proxy reachable?** Run the browser diagnostic first — if the browser can't reach it, Linked Helper can't either. → §B8
9. **Is the build current?** `Check and install updates`. Updating is the de-facto fix when LinkedIn changes its layout. → §B12.5
10. **Still stuck** → Launcher → `Backup` → `Logs & data for developers`, then `Need help` → `Ask for support` with account email, instance ID, screenshots and a screen recording. → §Collect before contacting support
Source: https://support.linkedhelper.com/hc/en-us/articles/360015343160-Why-is-my-campaign-shown-as-sleeping-When-will-it-start

## SYMPTOM INDEX

| Symptom / verbatim error string | Section |
|---|---|
| Campaign status shows **"sleeping"**, nothing processes | B1.1 |
| `"You have reached LinkedIn limit"` | B1.1 |
| `"You've hit weekly invitation limit"` | B1.1 |
| `"You've hit LinkedIn personalized invitations limit"` | B1.1 |
| `"You have reached the Maximum Daily Actions limit"` | B1.1 |
| `"Linked Helper doesn't have profiles to process"` | B1.1, B1.2 |
| `"An action is paused due to too many recurring errors"` | B1.1, B12.5 |
| `"You are out of Advanced limits"` | B1.1, B1.3 |
| `"You are out of working hours"` | B1.1 |
| `"All your Actions paused due to time-out"` | B1.1 |
| "No contacts in queue" / Queue empty after collecting | B1.2 |
| Profile shows `"LinkedIn Member"` instead of a name | B1.2 |
| Profile shows `"Pending"` / `"Invite Sent"` and is skipped | B1.2 |
| Only 1–2 profiles processed per day despite a big queue | B1.3 |
| Everything ran in one burst, then idle ~24 h | B1.4 |
| `"Failed to prepare collecting"` | B2.1 |
| `Collect` dropdown offers no post likers/commenters option | B2.2 |
| A LinkedIn page isn't supported by `Collect` | B2.3 |
| Exported CSV has empty email columns | B2.4 |
| `"Incorrect connect response (429)"` | B3.1 |
| `"LinkedIn error. Incorrect connect response (400)"` | B3.2 |
| `"Your invitation to {profile_name} could not be sent"` | B3.3 |
| LinkedIn demands the recipient's email on every invite | B3.4 |
| "Invitations keep going out after I closed Linked Helper" | B3.5 |
| Follow-up messages never fire after an invite campaign | B4.1 |
| Group / event sequence sends message #1 but no follow-ups | B4.2 |
| Group/event messages silently do nothing for CSV-uploaded profiles | B4.3 |
| Same person receives the same message text twice | B4.4 |
| "Replies not detected at all" | B4.5 `[UNVERIFIED]` |
| `"Wrong Account"` | B5.1 |
| `"Email Already Exists"` | B5.2 |
| Repeated logout / login loop inside the instance | B5.3 |
| `"Your account has been restricted"` / "verify you've performed certain actions" | B5.4 |
| Captcha / security checkpoint / 2FA-OTP prompt | B5.5 `[UNVERIFIED]` |
| Same profile appears or is processed twice | B6.1 |
| Instance stuck on `"Initializing.."` | B7.1 |
| Installation fails on Windows | B7.2 |
| `"linked-helper.dmg is damaged and can't be opened. You should move it to the Bin"` | B7.3 |
| `"linked-helper can't be opened because it was not downloaded from the App Store"` | B7.3 |
| `"The application 'App Store' can't be opened"` | B7.3 |
| `"Disconnect fired"` on Ubuntu 24.04 | B7.4 |
| Cannot run Linked Helper as root (Linux) | B7.4 |
| `"Network Error: There is either a problem with your Internet connection or Linked Helper website is offline"` | B8.1 |
| `"Failed to load LinkedIn: network issue please check your network connection or proxy settings"` | B8.2 |
| Need to back up / restore / move an account between machines | B9.1 |
| Disk full / need to relocate the user-data folder | B9.3 |
| No Delete button for a campaign / CRM profile / LinkedIn account | B9.4 |
| Licence attached to the wrong account or instance | B10.1 |
| Can't open a second Launcher / same account on two PCs | B10.2 |
| Activation-key error | B10.3 `[UNVERIFIED]` |
| Campaigns stop when the PC is off / laptop closed | B11.1 |
| RDP disconnect vs sign-out behaviour | B11.3 `[UNVERIFIED]` |
| Antivirus flags Linked Helper / blocks the install | B12.1 |
| UI too small / notification sounds annoying | B12.2 |
| "A feature I read about isn't in my interface" | B12.3 |
| LinkedIn UI must be in English? | B12.4 `[UNVERIFIED]` |
| "LinkedIn layout change broke the app" / app freeze | B12.5 `[UNVERIFIED]` |
| "Sync problems" | B12.6 `[UNVERIFIED]` |

---

# B1. CAMPAIGN NOT RUNNING
## B1.1. SYMPTOM: campaign status shows **"sleeping"** / nothing is being processed
**Likely causes** — the app enumerates them itself; do not guess. Seven documented reasons, in the order they usually bite: LinkedIn-side limit hit · daily action limit hit · empty queue · action auto-paused on recurring errors · advanced limit exhausted · outside working hours · action timeout not yet elapsed. [LH-CLAIM]
**Checks**
1. **Hover over the sleeping campaign status.**
2. Click **"See reasons"** in the tooltip.
3. Read the popup — it lists every applicable reason verbatim.
**Fix** — match the verbatim reason to its remedy:

| # | Reason (verbatim) | Fix |
|---|---|---|
| 1 | `"You have reached LinkedIn limit"` — sub-strings `"You've hit weekly invitation limit"`, `"You've hit LinkedIn personalized invitations limit"` | Wait until next week, or upgrade to a Premium LinkedIn subscription. See `references/limits-safety.md`. |
| 2 | `"You have reached the Maximum Daily Actions limit"` | Raise it in `Settings` → `Limits`, or wait for the rolling 24 h counter to free slots (B1.4). |
| 3 | `"Linked Helper doesn't have profiles to process"` | Add leads to the campaign Queue — but first check they weren't skipped at collection (B1.2). |
| 4 | `"An action is paused due to too many recurring errors"` | Open the action's **Failed** list, read the error, screenshot it, contact support. |
| 5 | `"You are out of Advanced limits"` | Raise the specific Advanced limit in `Settings`. The article explicitly says raising defaults is **not recommended**. |
| 6 | `"You are out of working hours"` | `Settings` → `Working hours` → set the day to **"24 hours"** mode or widen the period. |
| 7 | `"All your Actions paused due to time-out"` | Adjust the action's **"Start at"** date, or reduce delays in `Postpone action start` / `Action steps delays` / `Delay between actions` plug-ins. |
**If that fails** — reason 4 is the escalation path: send support the Failed-list error text plus a screenshot (see §Collect before contacting support).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015343160-Why-is-my-campaign-shown-as-sleeping-When-will-it-start

## B1.2. SYMPTOM: "no contacts in queue" / Queue is empty although you collected profiles
**Likely causes** — profiles were silently skipped at collection time. Six documented causes, ranked by frequency in the article's own ordering:
1. **Duplicate inside this campaign/action** — *"Contact is already in one sub-list (Queue, Processed, Exclude) of the current Action/Campaign."* Linked Helper refuses to reprocess a profile through the same workflow.
2. **Profile displays `"LinkedIn Member"`** instead of a real name → out of your network depth; LinkedIn withholds its data. Nothing to fix app-side.
3. **Relationship filter doesn't match the action** — e.g. collecting **1st-degree** connections into an action built for **2nd/3rd-degree** contacts.
4. **Out-of-network results despite a 3rd-degree filter** — profiles lacking the **"3rd"** badge cannot be processed even when real names are visible.
5. **New account with a thin network** — insufficient network depth.
6. **Already-invited profiles fed into an Invite action** — profiles showing **"Pending"** or **"Invite Sent"** cannot receive a duplicate invite.
**Checks**
1. Open the campaign's `Queue` and the action's `Queue`, `Processed` and `Exclude` sub-lists — is the profile already sitting in one of them?
2. Look at the collected rows: how many read `"LinkedIn Member"`?
3. Compare the search's relationship filter against the action's connection-degree requirement (`references/actions.md`).
4. Check the search results for the **"3rd"** badge on the profiles that didn't come through.
5. Check LinkedIn's sent-invitations page for the profiles fed into an Invite action.
**Fix**
1. Restrict the search to **2nd-degree only** where the action requires it.
2. Match the relationship filter to the action's capability *before* collecting.
3. For a new account, warm up first — invite **"10-15 people daily"** from LinkedIn's recommendation sections, then collect at scale.
4. Route already-invited profiles to a messaging or follow-up action instead of an Invite action.
**If that fails** — send support the campaign name, the source search URL and a screenshot of the collection result count.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015619980-Linked-Helper-skips-profiles-while-collecting-No-profile-was-collected

## B1.3. SYMPTOM: invites/messages queue up but only 1–2 process per day
**Likely causes** — an **Advanced limit** is throttling below the daily cap. `Load profile page` is the **master limit** with "priority over all other" profile limits: with a daily limit of 150 but `Load profile page` set to 1 per 24 h, only 1 profile loads per day.
`CONFLICT:` the docs state two incompatible precedence rules.
- **"Advanced limits have priority over the daily limits"**
- **"Maximum Daily Actions limit always overrides any lower-level limits"** — i.e. a per-action limit set *above* the daily cap has no effect.

Both from the same source article. Practical rule: set the daily cap at or above the sum of the per-activity limits you actually want, then verify with a small run.
**Checks**
1. `Settings` → `Limits` → is `Max actions per 24 hours` ≥ the total you want?
2. In the same screen, walk every **Advanced limit** — is any set lower than your intended throughput?
3. Specifically: what is `Load profile page` set to?
**Fix**
1. Raise `Max actions per 24 hours` to at least your intended total.
2. Raise or reset the offending Advanced limit — `Load profile page` first.
3. Re-run a small bunch and confirm the throughput before scaling.
**If that fails** — re-read B1.1 reason 5, then B1.4 (the counter may simply be full).
Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

## B1.4. SYMPTOM: everything ran in one burst, now idle for a day
**Likely causes** — the 24-hour counter is **rolling, not midnight-reset**. Verbatim:
**"Linked Helper counts actions that were made every last 24 hours period, not the last day or fixed period of 24 hours"**; **"Each action taken is added back exactly after 24 hours from the time it was performed."** With a full queue, **"as soon as one action slot is freed, Linked Helper starts to process profiles till there are no free action slots"**. This is also the most bot-like pattern available. [LH-CLAIM]
**Checks**
1. `Settings` → `Limits` → read the "Last 24 hrs actions" number against the cap.
2. Check `Bunch size` and `Timeout between bunches` (`Action steps delays plug-in`; defaults **10** / **1 minute**).
3. Check `Settings` → `Working hours` — a wide window plus a big queue means one burst.
**Fix** — spread deliberately, pick one or more:
1. Raise `Timeout between bunches` and size `Bunch size` to match. Worked example for 50 invites/day: `Bunch size` = **25**, `Timeout between bunches` = **12 hours**.
2. Stack an hourly Advanced limit under the daily one.
3. Narrow Working hours.
**If that fails** — nothing is broken; wait out the rolling window and re-check the counter.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017039459-When-the-Last-24-hrs-actions-number-is-reset
Source: https://support.linkedhelper.com/hc/en-us/articles/360015357459-How-to-limit-inviting-by-50-profiles-per-day

---

# B2. COLLECTION / SCRAPING FAILURES
B2.2 and B2.3 assume collection starts at all. If `Collect` errors out, start at B2.1.
## B2.1. SYMPTOM: **"Failed to prepare collecting"**
**Likely causes**
1. **Not logged into LinkedIn** — session expired or authentication failed.
2. **LinkedIn glitch** — corrupted cached JavaScript prevents the page loading and yielding data. The article notes this is not exclusive to Linked Helper: the same glitch occurs browsing LinkedIn in Chrome.
**Checks**
1. Open the **`LinkedIn` menu in the left panel** — does the embedded browser show you logged in?
2. Does the target LinkedIn page render fully inside the instance?
**Fix — login path**
1. Let Linked Helper auto-login with saved credentials, **or**
2. Log in manually via the **`LinkedIn` menu in the left panel**.
**Fix — cache path**
1. **Stop the Campaigns runner** first.
2. **Right-click the LinkedIn webpage** inside the instance.
3. Choose **"Reload (and clear cache option)"** from the context menu.
4. Retry the collection.
**If that fails** — email **info@linkedhelper.com** with logs (§Collect before contacting support).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015510239-Error-Failed-to-prepare-collecting-occurs

## B2.2. SYMPTOM: the `Collect` dropdown offers no option for post likers/commenters
**Likely causes** — the post was opened from the feed rather than by its own URL. Verbatim requirement: this works only when **"a post is opened via its own unique URL."**
**Checks**
1. Look at the address bar inside the instance — is it the feed, or the post's own URL?
**Fix**
1. Click the **three dots** in the upper-right corner of the post.
2. Select **"Copy link to post"**.
3. Open the post by that link — click **"View Post"**, or paste the URL into Linked Helper's address bar.
4. The **`Collect`** dropdown now shows the likers/commentators options.
**If that fails** — `[UNVERIFIED]` the article does not state a maximum number of collectible likers/commenters, rate limits, or whether all are retrievable. Do not promise completeness.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015766440-Is-it-possible-to-collect-those-who-liked-or-commented-post

## B2.3. SYMPTOM: a LinkedIn page you want to harvest isn't supported by `Collect`
**Likely causes** — verbatim: **"Currently, Linked Helper cannot collect URLs from some pages."** The article does not enumerate which. [LH-CLAIM]
**Checks** — open the page inside the instance and open the `Collect` dropdown: is there any matching option?
**Fix A — any page whose HTML contains profile links** — open the target page and **scroll to load** all desired profiles → **right-click** → **"Save as"** → choose format **"Web page, Complete"** → upload the saved **HTML file** via Linked Helper's standard URL-upload function.
**Fix B — the Messaging page (advanced)**
1. Install an **auto-scroll extension**.
2. Open **Chrome Developer Tools** → **Network** tab; enable **"Disable cache"** and **"Preserve log"**; filter requests to **"Fetch/XHR"**.
3. Filter for **`voyagerMessagingGraphQL`**.
4. Scroll through all chats with the auto-scroll extension.
5. **Export the HAR file**, rename it with a **`.txt`** extension, in a text editor **replace `\"` with spaces**, then upload the modified file to Linked Helper.
**If that fails** — ask support whether that specific page type is on the roadmap; include the URL.
Source: https://support.linkedhelper.com/hc/en-us/articles/28438859259282-How-to-collect-profiles-from-unsupported-pages

## B2.4. SYMPTOM: exported CSV has empty email columns
**Likely causes** — three documented, ranked:
1. **2nd/3rd-degree profiles weren't run through an email finder.** *"E-mails are unavailable on the profile pages of 2nd and 3rd level contacts, so Linked Helper 2 won't be able to scrape them by simply visiting the profile pages."*
2. **1st-degree profiles weren't fully extracted.** Emails for 1st connections require the **`Visit & Extract profiles`** action specifically — email scraping is disabled in other actions **"for security purposes."**
3. **Profiles were downloaded straight from the Queue.** *"If you download profiles from Queue, there won't be any email addresses"* — they were never processed.
**Checks**
1. Which list did you export from — `Queue` or `Successful`?
2. Does the campaign contain a `Visit & Extract profiles` action, or only visiting actions?
3. What degree are the profiles? Was a `Find Profile Emails` action run for 2nd/3rd?
**Fix**
1. **1st-degree:** run **`Visit & Extract profiles`**, with a **`Filter contacts out of my network (keep 1st level only)`** step *before* it so you don't try to extract emails from people who haven't accepted yet.
2. **2nd/3rd-degree:** run the **`Find Profile Emails`** action (LH Email Finder / Snov.io / Apollo.io) — see `references/recipes.md`.
3. Export from the **`Successful`** list, never from `Queue`.
**If that fails** — `[UNVERIFIED]` no hit-rate percentages are published. A partially-empty column after a correct run is expected behaviour, not a defect; do not quote a coverage figure.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016685199-Why-don-t-all-contacts-in-a-CSV-file-have-e-mail-addresses

---

# B3. INVITES NOT SENDING
## B3.1. SYMPTOM: **"Incorrect connect response (429)"**
**Meaning:** HTTP **"429 Too Many Requests"** — **"you sent a lot of requests in a short period of time."** [LI-POLICY]
**Likely causes**
1. **"You've sent many invitations within a short amount of time."**
2. **"Many of your invitations have been rejected, ignored, or left pending by the recipients."**
**Checks**
1. `Settings` → `Limits` → invites per 24 h and the actual last-24-h count.
2. Is `Action steps delays plug-in` installed, and are the delays at SAFE timeouts?
3. Pending invite count at https://www.linkedin.com/mynetwork/invitation-manager/sent/
4. Acceptance rate — how many of the recent invites are still pending or were dismissed?
**Fix, in order**
1. Install the **`Action steps delays plug-in`**.
2. **"Increase or reset Delay settings to SAFE timeouts"** → then **"wait a few hours before you try again"**.
3. **Reduce daily limits** below the default 150 actions/day → then **"wait a couple of days"**.
4. **"Withdraw all pending invites except recent 500, then retry"**.
5. **Wait 5-7 days** for the restriction to lift automatically.
**If that fails** — contact LinkedIn support **without mentioning automation software**. Then, if Linked Helper still errors on a profile you can invite manually, send logs to support.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016855839-Incorrect-connect-response-429

## B3.2. SYMPTOM: **"LinkedIn error. Incorrect connect response (400)"**
**Meaning:** **"400 Bad Request — occurs when withdrawn profiles are being invited or when there are too many pending requests"**. [LI-POLICY]
**Likely causes**
1. Re-inviting a profile whose invitation you previously **withdrew** — LinkedIn enforces a **3-week waiting period**.
2. **Too many pending invitation requests** accumulated.
**Checks**
1. Review pending invites at https://www.linkedin.com/mynetwork/invitation-manager/sent/ — how many?
2. Was the failed profile previously invited and withdrawn? Check the same page's history and your `Sent invites canceller` runs.
3. **Verify manually:** try inviting the failed profile directly in LinkedIn. **"If you cannot send an invite manually, then you won't be able to send it via Linked Helper as well."** This single check tells you whether it is app-side at all.
**Fix**
1. Withdraw most pending invites, keeping only **500–1000** active.
2. If the profile was recently withdrawn, respect the **3-week cooldown** — remove it from the Invite action's queue and re-add later.
**If that fails** — if a manual invite succeeds but Linked Helper still 400s, that is the case worth escalating: send support the profile URL, campaign name and logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016812980-LinkedIn-error-Incorrect-connect-response-400

## B3.3. SYMPTOM: **"Your invitation to {profile_name} could not be sent"**
**Likely causes**
1. *"The contact was invited before but declined your invitation or you withdrew it later."* **"After withdrawing an invitation, you won't be able to resend an invite to the same recipient for up to three weeks."**
2. Too many sent invitations still pending — neither accepted nor rejected.
**Checks**
1. https://www.linkedin.com/mynetwork/invitation-manager/sent/ — count pending.
2. **Key diagnostic:** *"In both cases, you can't invite a current contact even manually!"* — try the manual invite. If manual also fails, this is LinkedIn-side, not an app bug.
**Fix**
1. If more than **1,500** pending, withdraw and maintain **500–1,000** going forward.
2. Wait out the up-to-three-week cooldown for withdrawn recipients.
`CONFLICT:` the pending-invite ceiling differs across LH's own articles — this one names **1,500** as the trigger point while B3.2's article says keep **500–1000**, and `references/limits-safety.md` records four incompatible ceilings (700 / 1,000 / 1,500 / 2,500). Treat none as authoritative; manage by hygiene and keep pending in the low hundreds.
**If that fails** — nothing to escalate if the manual invite also fails; that is LinkedIn's answer.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015352260-Invitation-could-not-be-sent

## B3.4. SYMPTOM: LinkedIn asks for the recipient's email address on every invitation
**Likely causes** — the account received many **"don't know"** dismissals; LinkedIn now requires email verification for invites to non-direct connections. [LI-POLICY]
**Checks**
1. Try one manual invite in LinkedIn — does the email field appear there too? (It will.)
2. Review recent invite targeting: were they plausibly relevant to your profile?
**Fix — four options, per the article**
1. Withdraw pending invitations, then ask LinkedIn support to remove the restriction.
2. Create a new account and merge connections.
3. Establish multiple accounts for different target segments.
4. **Wait 5-7 days** for automatic removal.
**If that fails** — this is an account-reputation state, not a settings problem. Pause invite campaigns entirely and switch to invite-free reach (`references/recipes.md`).
Source: https://support.linkedhelper.com/hc/en-us/articles/360017222880-My-LinkedIn-account-got-restricted-though-I-followed-your-recommendations

## B3.5. SYMPTOM: "invitations keep going out even after I closed Linked Helper"
**Likely causes** — not what it looks like. Verbatim: Linked Helper is **"not a cloud solution, it works locally on your PC and cannot perform any action when it is stopped."** What you are seeing are invitations **already sent** before shutdown, still pending on LinkedIn's side.
**Checks**
1. Open https://www.linkedin.com/mynetwork/invitation-manager/sent/ and read the **sent dates** — they will all pre-date the shutdown.
**Fix**
1. Withdraw them at https://www.linkedin.com/mynetwork/invitation-manager/sent/, or use the `Sent invites canceller` flow in `references/limits-safety.md`.
**If that fails** — if sent timestamps are genuinely *after* the app was stopped, that contradicts the vendor's own statement: send support the timestamps plus logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015359280-Invitations-are-being-sent-even-if-Linked-Helper-is-off-How-can-I-stop-that

---

# B4. MESSAGES NOT SENDING / REPLIES NOT DETECTED
## B4.1. SYMPTOM: follow-up messages never fire after an invite campaign
**Likely causes** — the funnel is missing the acceptance gate. Messaging actions require the profile to already be a 1st-degree connection.
**Checks**
1. Read the action order in the campaign. Required order:
   ```
   Invite 2nd and 3rd level contacts
     → Filter contacts out of my network (keep 1st level only)
       → Message to 1st connections
         → Check for replies            (auto-added)
   ```
2. Is the filter action present at all? The **"Invite & Follow Up"** template auto-inserts it whenever a messaging/endorsing/inviting-to-entity action follows an `Invite 2nd & 3rd contacts` action — a hand-built campaign may not have it.
3. Open the filter action's `Successful` list — **"only those who accepted your invitation will be moved to the Successful list"**. Profiles that haven't accepted stay in Queue and cycle.
4. Check its timeout: **minimum timeout between checks is 10 minutes** (lower values are refused to avoid LinkedIn detection). Mechanics are verbatim: *"once in 60 minutes it will automatically take all the profiles from the Queue, go to My Network page, and compare the profiles from the Queue to your 1st-degree connections."*
5. Are the profiles actually in the filter action's own queue? The action only processes profiles **already in its own queue** or manually added.
**Fix**
1. Insert `Filter contacts out of my network (keep 1st level only)` between the invite and the message action.
2. Reorder actions — note this is only possible while Queue/Processed lists are empty.
3. Set the check timeout at 10 minutes or more.
4. Give invitees time: nobody moves to `Successful` until they accept.
**If that fails** — send support the campaign's action list screenshot plus the filter action's Queue/Successful counts.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015485560-What-does-Filter-contacts-out-of-my-network-keep-1st-level-only-action-do
Source: https://support.linkedhelper.com/hc/en-us/articles/360016380399-How-To-Send-message-to-recently-added-LinkedIn-connections-from-a-certain-inviting-campaign

## B4.2. SYMPTOM: group / event message sequence sends message #1 but no follow-ups
**Likely causes** — by design, not a bug. Initial messages to group members and event attendees arrive in the recipient's **Incoming Requests** inbox, not Messages. **"Default setting prevents follow-ups unless initial request is accepted."** Acceptance moves the thread to the standard Messages inbox.
**Checks**
1. Open the **`Check for replies`** action's settings — is reply detection configured to recognise **"Message request accepted"** notifications?
2. Check the per-account group ceiling: **"For some LinkedIn accounts, the limit of messages to group members is lower compared to the other LinkedIn accounts."** Some accounts face a **10-message monthly limit across all groups**. [LI-POLICY]
3. For events, check degree: **"LinkedIn allows you to send messages to your 3rd-degree connections only"**. [LI-POLICY]
**Fix**
1. In the **`Check for replies`** action, set reply detection to recognise **"Message request accepted"** notifications as the acceptance signal. Only then do follow-ups fire.
2. If the account is on the low group ceiling, cut volume to fit the monthly cap and shift reach to events or InMail.
**If that fails** — see B4.3: the profiles may have no group/event scope at all.
Source: https://support.linkedhelper.com/hc/en-us/articles/4404650533394-How-to-filter-profiles-via-Sales-Navigator-and-send-them-free-messages-as-group-members
Source: https://support.linkedhelper.com/hc/en-us/articles/4413889042450-How-to-send-a-message-to-event-attendees-even-if-they-are-not-your-1st-degree-connections
Source: https://support.linkedhelper.com/hc/en-us/articles/4402404724626-Is-there-a-life-after-LinkedIn-weekly-invitation-limit

## B4.3. SYMPTOM: group/event messages silently do nothing for uploaded (CSV) profiles
**Likely causes** — profiles not collected from the group/event page carry no group/event scope, so LinkedIn has no context permitting the message. **"Event ID assignment is mandatory for non-event-collected profiles."**
**Checks**
1. Where did these profiles come from — the group/event page, or a CSV/Sales Navigator import?
2. Is the **`Override platform plug-in`** installed? Without it there is no `Change platform` button.
**Fix** — requires the **`Override platform plug-in`**:
1. Select the profiles in the **Queue**.
2. Click **`Change platform`**.
3. Set **`Collect scope type`** to **"Group ID"** (or **"Event ID"**).
4. Paste the ID/URL into the **`Collect scope id`** field.
5. **Save changes.**

For groups, the Group ID comes from the group's URL; for events, from the **"all attendees"** search URL.
**If that fails** — verify you are actually a member of the group / registered for the event, then send support the scope ID you set and the action's Failed list.
Source: https://support.linkedhelper.com/hc/en-us/articles/4404650533394-How-to-filter-profiles-via-Sales-Navigator-and-send-them-free-messages-as-group-members
Source: https://support.linkedhelper.com/hc/en-us/articles/4413889042450-How-to-send-a-message-to-event-attendees-even-if-they-are-not-your-1st-degree-connections

## B4.4. SYMPTOM: the same person receives the same message text twice
**Likely causes** — the profile entered a second campaign/action whose template repeats content already sent. Within one action Linked Helper already blocks duplicates (B6.1); cross-campaign it does not, unless configured.
**Checks**
1. Search the CRM / campaign lists for the profile — how many campaigns contain it?
2. Compare the two templates' text.
3. Is the **`Filter by message content`** plug-in installed?
**Fix**
1. Install the **`Filter by message content`** plug-in.
2. Populate **"The Previous message phrases field"** with text the prospect already received; the action then refuses to resend identical content.
3. Longer-term, de-duplicate across campaigns per B6.1.
**If that fails** — escalate with both message texts and both campaign names.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates

## B4.5. SYMPTOM: "replies not detected at all" `[UNVERIFIED]`
No help-center article documents a failure mode where `Check for replies` misses genuine replies. The documented controls are the **`Advanced settings for Check for replies plug-in`** and **`Ignore generic replies plug-in`** (`references/actions.md`). **Do not assert a fix.** Confirm the action exists in the sequence (B4.1), then route to support with logs (§Collect before contacting support). See §Unverified symptoms.
Source: none found — no help-center article in the FAQ, Recipes and tips, or Issues & solutions categories documents this symptom. Do not cite one.

---

# B5. LOGIN / SESSION / ACCOUNT-ADDING
## B5.1. SYMPTOM: **"Wrong Account"** warning when adding a LinkedIn account
**Likely causes** — *"you are trying to access the LinkedIn account through the wrong instance (that was used to log in to another LinkedIn account before)."*
**Root rule:** *"Linked Helper 2 links an instance to the very first LinkedIn account you logged in via the instance, and you can't use an already created instance for other LinkedIn accounts."*
**Checks**
1. Launcher → `LinkedIn accounts` → which instance was originally created for this LinkedIn email?
2. Filter to **"Archived"** — is the right instance archived rather than missing?
**Fix**
1. Use the instance previously assigned to that LinkedIn account, **or**
2. Create a new instance for the different account, and reassign licences between instances as needed (B10.1).
**If that fails** — send support the Linked Helper account email and the instance ID from the title bar.
Source: https://support.linkedhelper.com/hc/en-us/articles/4408390475154-Errors-when-adding-LinkedIn-account
Source: https://support.linkedhelper.com/hc/en-us/articles/360018187780-How-to-delete-a-LinkedIn-account-from-the-Launcher

## B5.2. SYMPTOM: **"Email Already Exists"** warning when adding a LinkedIn account
**Likely causes** — *"you already have the Linked Helper instance with the email address that matches the one you are trying to add."*
**Checks**
1. Launcher → `LinkedIn accounts` → set the filter to **"Archived"**. The instance is usually there.
**Fix**
1. Use the previously created instance with that email.
2. If it isn't visible, **unarchive** the archived account from the **"Archived"** filter in the `LinkedIn accounts` menu.
**If that fails** — escalate with the email address and a screenshot of both filters.
Source: https://support.linkedhelper.com/hc/en-us/articles/4408390475154-Errors-when-adding-LinkedIn-account

## B5.3. SYMPTOM: repeated logout / "login loop" inside the instance
**Likely causes** — ranked:
1. **Direct profile-URL navigation above the safe rate.** Verbatim: **"If you open 50 profiles via URL in Chrome, then you most likely will be logged out."** The default `Load LinkedIn profile via URL` limit of **40 per 24 hours** exists to prevent exactly this.
2. **Concurrent sessions** — you or a colleague also active in Chrome or the mobile app on the same account. Forbidden; see `references/limits-safety.md`.
3. **Changing location/IP between sessions** — **"most of the restrictions/warnings happen because of using the same LinkedIn account from different locations."**
**Checks**
1. Is `Load LinkedIn profile via URL` still at its default 40/24 h, or was it raised?
2. Is anyone else logged into that LinkedIn account concurrently?
3. Is the IP/geo stable between sessions, and does the proxy country match the account country?
**Fix**
1. Restore the `Load LinkedIn profile via URL` limit to 40/24 h.
2. Keep exactly one active session at a time.
3. Pin a consistent proxy/geo.
4. Log in manually once via the **`LinkedIn`** left-panel menu.
**If that fails** — see B5.4; the account may be under an active restriction.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015553480-How-to-stay-safe-when-working-with-LinkedIn-manually
Source: https://support.linkedhelper.com/hc/en-us/articles/360015349559-What-kind-of-limits-should-I-use
Source: https://support.linkedhelper.com/hc/en-us/articles/360017023219-Can-I-use-LinkedIn-account-via-browser-mobile-app-when-Linked-Helper-is-running

## B5.4. SYMPTOM: **"Your account has been restricted"** on login / "verify you've performed certain actions"
**Likely causes** — a LinkedIn-side restriction. The most common cause of the second variant: the account was accessed from multiple locations/devices simultaneously. [LI-POLICY]
**Checks**
1. Log into LinkedIn in a normal browser from the account's usual location — what does LinkedIn itself ask for?
2. How many devices/locations touched the account in the last 48 h?
**Fix**
1. Complete the **manual identity/action verification inside LinkedIn**. The app cannot bypass either scenario.
2. Then collapse to one session, one geo, and resume at reduced limits.
**If that fails** — the recovery playbook and LinkedIn support endpoints are in `references/limits-safety.md`. Do not restart campaigns until the restriction is lifted.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017222880-My-LinkedIn-account-got-restricted-though-I-followed-your-recommendations

## B5.5. SYMPTOM: captcha / security-checkpoint / 2FA-OTP prompt `[UNVERIFIED]`
No article documents a captcha-solving flow, a 2FA/OTP entry field, or a scripted response to LinkedIn's "unusual activity" interstitial. **Do not assert a fix.** Solve prompts by hand in the instance's embedded browser via the **`LinkedIn`** left-panel menu. See §Unverified symptoms.
Source: none found — no help-center article in the FAQ, Recipes and tips, or Issues & solutions categories documents this symptom. Do not cite one.

---

# B6. DUPLICATES
## B6.1. SYMPTOM: the same profile appears twice / gets processed twice
**Likely causes**
1. **The profile is in two different campaigns/actions.** Within one campaign or action, Linked Helper **"does not collect duplicates into the same Campaign or Action if a profile is already in the Queue / Processed / Exclude list."** Across campaigns it does not deduplicate unless you configure it.
2. **Collected from different platforms.** LinkedIn vs Sales Navigator produce **different profile IDs**. These **merge automatically** once Linked Helper scrapes the profile page — so a short-lived duplicate here is expected.
3. **Multiple LinkedIn accounts** working the same list.
**Checks**
1. Relevant list structure — where exactly does the profile appear?
   - **Action-level:** `Queue`, `Processed` (sub-lists `Skipped`, `Failed`, `Excluded`, `Messaged`, `Replied`, `Successful`).
   - **Campaign-level:** `Queue`, `Exclude list`.
2. For invites specifically, note the LinkedIn-side backstop: **"LinkedIn itself won't let you send invite twice to the same person."**
3. Is the **`Lists Manager`** plug-in installed?
**Fix — across campaigns, same account** — install the **`Lists Manager`** plug-in (Plug-in Store) → select the **source** campaign → select the **target** campaign → click **"Remove intersections between campaigns"**.
**Fix — across multiple LinkedIn accounts**
1. *Before* launching: download profiles from the campaign Queue, split the CSV across accounts, then upload each account's URLs into the **Exclude list** of the other accounts' campaigns.
2. *While running:* manually download the `Queue`/`Processing`/`Processed` lists from one account and upload them into the other account's campaign **Exclude list**.
3. Note that campaign copy between accounts deliberately does **not** carry profiles — *"Linked Helper does not move profiles to avoid reaching out to the same leads using different LinkedIn accounts."*
**Fix — same text sent twice:** `Filter by message content` plug-in (B4.4).
**If that fails** — there is no global blacklist; build one per `SKILL.md` §7 and `references/campaigns.md`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015588519-How-to-avoid-duplicates
Source: https://support.linkedhelper.com/hc/en-us/articles/360015334960-Will-Linked-Helper-send-invite-to-the-same-person-twice
Source: https://support.linkedhelper.com/hc/en-us/articles/360019349660-How-to-duplicate-clone-a-campaign-or-copy-it-to-another-LinkedIn-account

---

# B7. INSTALLATION & LAUNCH
Full OS support matrix and hardware sizing: `references/plans-and-platform.md`. Check the machine against it *before* debugging an install failure — ChromeOS is unsupported, ARM is unsupported, and 32-bit Windows is unsupported, and no fix below changes that.

## B7.1. SYMPTOM: instance stuck on **"Initializing.."**, never loads
**Likely causes** — (1) incorrect firewall settings; (2) incorrect `hosts` file, missing localhost entries.
**Checks** — is the OS firewall enabled at all? · on Windows, are there inbound rules named `linked-helper.exe`? · does the `hosts` file contain all four required entries?
**Required hosts entries (all platforms)**
```
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
fe80::1%lo0     localhost
```
**Fix — Windows**
1. Firewall: Start → search **Windows Defender Firewall** → ensure it is **enabled** → **Advanced settings** → **Inbound rules** → **"select all rules with 'linked-helper.exe' name and delete them"**.
2. Hosts: run **Notepad as administrator** → File → Open → `C:\Windows\System32\drivers\etc` → set file type to **"All files"** → open `hosts` → add the four entries → File → Save.
**Fix — Ubuntu**
1. Firewall: `sudo ufw status`. If inactive, whitelist ports **before** enabling:
   ```
   sudo ufw allow ssh
   sudo ufw allow 22/tcp
   sudo ufw allow 2222/tcp
   sudo ufw allow from any to any port 3389 proto tcp
   sudo ufw enable
   ```
2. Hosts: `sudo nano /etc/hosts` → add the four entries → Ctrl+O, Ctrl+X.
**Fix — macOS**
1. Firewall: Launchpad → System Preferences → Security & Privacy → **Firewall** tab → click the lock, enter password, **enable**.
2. Hosts: `sudo nano /private/etc/hosts` → add the four entries → Ctrl+O, Enter, Ctrl+X. **Restart Linked Helper after any change, on every platform.**
**If that fails** — this overlaps B8.1; run the browser diagnostic there, then send logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016524820-Linked-Helper-instance-won-t-load-but-stuck-on-Initializing

## B7.2. SYMPTOM: installation fails on Windows
**Likely causes** — unsupported platform · antivirus false positive · insufficient disk · missing Windows update · insufficient privileges.
**Checks** — **Windows 64-bit only** (32-bit is not supported) · **non-ARM processor** required · **Windows 7 x64** users need update **KB4457144** · **minimum 3 GB free space on the C: drive**.
**Fix**
1. Antivirus false positive → **"temporarily disable anti-viruses before installing"** (see B12.1).
2. Run the installer **as administrator**.
3. Free space on C: to at least 3 GB; apply KB4457144 on Windows 7 x64.
**If that fails** — send support the setup logs from `C:\%userprofile%\AppData\Local\SquirrelTemp\`. Navigate there in File Explorer, or click **"Open Setup Log"** if the popup appears during install.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015656279-Linked-Helper-installation-fails-on-Windows

## B7.3. SYMPTOM: macOS install errors
**Likely causes and fixes** — match the exact string:

| Exact error string | Cause | Fix |
|---|---|---|
| `"linked-helper.dmg is damaged and can't be opened. You should move it to the Bin"` | Browser downloaded the file incorrectly | Re-download the installer **using a different web browser** |
| `"linked-helper can't be opened because it was not downloaded from the App Store"` | Mac security restricted to App Store only | Allow unidentified developers (below) |
| `"The application 'App Store' can't be opened"` | macOS doesn't recognise the app as from an identified developer (rare) | Allow unidentified developers (below) |
**Fix — allow unidentified developers**
1. **macOS Big Sur+:** follow Apple's official guide for opening apps from unidentified developers.
2. **Catalina / Mojave:** System Preferences → Security & Privacy → **General** tab → **"Open Anyway"**.
3. **Terminal fallback** if the button doesn't appear: run `sudo spctl --master-disable`, then select **"Anywhere"** in security settings and retry the install.
**Checks** — confirm the chipset build matches the Mac (Intel vs Apple M-chipset) and the OS is at or above the supported minimum; see `references/plans-and-platform.md`.
**If that fails** — vendor statement for the security team: **"Linked Helper is safe and does not contain viruses or malware."** [LH-CLAIM] Then send support the exact error string and a screenshot.
Source: https://support.linkedhelper.com/hc/en-us/articles/360019376519-Issues-with-Linked-Helper-installation-on-Mac

## B7.4. SYMPTOM: Linked Helper cannot start on Ubuntu
### Issue A — instance fails with a **"Disconnect fired"** error on **Ubuntu 24.04**
**Likely cause** — Ubuntu 24.04 security updates restrict **unprivileged user namespaces**.
**Checks** — confirm the release is 24.04 (`lsb_release -a`) · confirm the error string is exactly `Disconnect fired`.
**Fix**
1. Open Terminal, run `sudo crontab -e -u root`, enter your password. If asked to choose an editor, enter **`1`** and press Enter.
2. Go to the end of the file and add these two lines:
   ```
   @reboot sudo sysctl -w kernel.apparmor_restrict_unprivileged_unconfined=0
   @reboot sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0
   ```
3. **Ctrl + S** to save, **Ctrl + X** to exit, **reboot**, then restart Linked Helper.

### Issue B — cannot run as **root**
**Likely cause** — *"Due to security restrictions, Linked Helper cannot be started on behalf of root user."*
**Fix** — create a new non-root user → add it to the **sudo** group → log in as that user → install and run Linked Helper under that account.
**If that fails** — Linux requires **Gnome GUI**; confirm the desktop environment against `references/plans-and-platform.md`, then send logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/19176827188370-Linked-Helper-cannot-start-on-Ubuntu

---

# B8. NETWORK / CONNECTIVITY
## B8.1. SYMPTOM: **"Network Error: There is either a problem with your Internet connection or Linked Helper website is offline"**
**Meaning:** *"Linked Helper 2 Launcher can't establish the connection with Linked Helper 2 servers due to different problems."*
**Likely causes** — VPN/proxy routing differing between browser and launcher · firewall/antivirus blocking · corrupted cached launcher files · unsynchronised system time · misconfigured hosts file · expired SSL certificates · blocked domains.
**Checks — run the browser diagnostic first; it splits the fix set in two**
1. Open **https://linkedhelper.com/member** in a browser with **no VPN/proxy extensions**.
2. Navigate its menus (**LinkedIn accounts**, **Licenses**) to confirm it works.
**Fix — if the browser works (Solutions #1–#5)**
1. **VPN/proxy:** install a free VPN (Windscribe / TouchVPN) if you have none and restart the launcher; **or** disable the existing VPN and restart; **or** disable system-wide proxy settings.
2. **Security software:** temporarily disable antivirus and firewall. **Kaspersky specifically:** disable **Network ports monitoring for port 443**.
3. **Clear launcher cache:** in File Explorer go to `%appdata%\linked-helper\Partitions`, rename **`linked-helper-launcher`** → **`linked-helper-launcher-old`**, then re-login.
4. **Synchronise time:** verify timezone and sync system time with an internet time server.
5. **Hosts file:** confirm the four localhost entries from B7.1 exist.
**Fix — if the browser also fails (Solutions #6–#8)**
6. **Whitelist these domains:**
   ```
   linkedin.com, *.linkedin.com, lnkd.in, *.lnkd.in
   linkedhelper.com, *.linkedhelper.com, api.linkedhelper.com,
   pas.linkedhelper.com, autoupdate.linkedhelper.com
   do0ca1hx6twig.cloudfront.net, *.cloudfront.net
   slideshare.net, *.slideshare.net
   paypal.com, *.paypal.com
   *.amazonaws.com, *.stripe.com, api.stripe.com
   ```
7. **Update SSL certificates:** install the ISRG root certificates from Let's Encrypt — **isrgrootx1**, **isrg-root-x2**, **lets-encrypt-r3**.
8. **Test a different network:** another PC, or a mobile hotspot, to isolate ISP/device issues.
**If that fails** — email **info@linkedhelper.com** with logs and which of the eight solutions you already tried.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017322679-Network-Error-There-is-either-a-problem-with-your-Internet-connection-or-Linked-Helper-website-is-offline

## B8.2. SYMPTOM: **"Failed to load LinkedIn: network issue please check your network connection or proxy settings"**
**Likely causes** — internet connectivity · VPN/proxy server problems · ISP-level LinkedIn blocking ·
**IPv6-only internet access** · firewall/antivirus interference · disabled system proxy settings.
**Checks**
1. **Test LinkedIn in Chrome** with VPN/proxy off. If it's unreachable in the browser, Linked Helper can't reach it either.
2. **Check IP protocol.** Linked Helper requires **IPv4**. Verify at https://whatismyipaddress.com/ — IPv4 looks like **"192.168.0.1"**, IPv6 like **"2001:0db8:0000:0000:0000:8a2e:0370:7334"**.
3. **Verify the proxy works.** Use Linked Helper's built-in **test connection** button, or test in Chrome via the **Best Proxy Switcher** extension, or validate at https://proxy6.net/en/checker
4. Confirm these aren't blocked: `linkedin.com`, `*.linkedin.com`, `lnkd.in`, `*.lnkd.in`, `slideshare.net`, `*.slideshare.net`.
**Fix**
1. **Adjust system proxy settings.** **Windows 10:** search **"Proxy settings"** → disable **"Automatically detect settings"**, **"Use setup script"**, and manual proxy options. · **macOS:** System Preferences → Network → select the service → **Advanced** → **Proxies** tab → uncheck all protocols. · **Ubuntu:** System Settings → Network → **Network proxy** gear button → select **"Disabled"**.
2. Obtain IPv4 connectivity if the ISP is IPv6-only.
3. Replace a proxy that fails the test-connection check (proxy requirements: `references/limits-safety.md`).
4. Temporarily disable antivirus; ensure the firewall is enabled with correct rules; test another PC or ISP.
**If that fails** — send support the IPv4/IPv6 result, the proxy checker output and logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017136120-I-get-Failed-to-load-LinkedIn-network-issue-please-check-your-network-connection-or-proxy-settings-error

---

# B9. DATABASE, BACKUP/RESTORE, DATA FOLDER, DELETION
## B9.1. SYMPTOM: need to move an account to another machine / recover from data loss
**Create a backup** — Launcher → **`LinkedIn accounts`** → **hover over** the LinkedIn account → **stop the instance** if needed → click **`Backup`** → select **`Export`** → save the file (e.g. to Desktop).
**Restore** — Launcher → **`LinkedIn accounts`** → hover over the account → stop the instance if needed → click **`Backup`** → click **`Import`** → select the backup file.
**CRITICAL WARNING (verbatim):** **"When a backup file is imported, current data will be overwritten."** / **"Restoring a backup file overwrites all current data for a LinkedIn account on a certain computer."** Export the current state before importing anything.
**Contents:** the LinkedIn account's **local database file**. The app stores **"most of the data locally on your computer"** — not in the cloud. This is also the supported way to move an account between machines (B10.2).
**If that fails** — `[UNVERIFIED]` no automatic-backup schedule or retention count is documented; do not promise one. Escalate with the backup file and logs.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016353900-How-to-backup-restore-your-Linked-Helper-data

## B9.3. SYMPTOM: disk full / need to relocate the user-data folder
**Likely causes** — the local database grew on the system drive. Default locations (full table in `references/plans-and-platform.md`): Windows `C:\Users\{username}\AppData\Roaming\linked-helper` · macOS `/Users/{username}/Library/Application Support/linked-helper/` · Linux `/home/{username}/.config/linked-helper/`.
**Checks** — free space on the drive holding the default path (Windows installs also need ≥3 GB on C:, B7.2) · **close all Linked Helper windows first, on every platform.**
**Fix — Windows** — create the new folder (e.g. `D:\linked-helper`) → move existing data from the AppData folder into it → Start → **"Edit the system environment variables"** → **Advanced** tab → **"Environment Variables…"** → add a **system** variable, Name **`LH_APP_USER_DATA_PATH`**, Value = new path (e.g. `D:\linked-helper`) → restart Linked Helper.
**Fix — macOS** — Finder → **"Go to Folder"** → `/Users/{username}/Library/Application Support/` → move the **`linked-helper`** folder to the new location → create/edit **`setENV.plist`** in `/Users/{username}/Library/LaunchAgents/` → add `launchctl setenv LH_APP_USER_DATA_PATH /your/new/path` → reboot.
**Fix — Ubuntu** — `sudo nano /etc/environment` → add `LH_APP_USER_DATA_PATH="/your/new/path"` → Ctrl+O to save, Ctrl+X to exit → move the data folder → restart Ubuntu.
**If that fails** — take a backup (B9.1) before any further attempt, then escalate.
Source: https://support.linkedhelper.com/hc/en-us/articles/360019392720-How-to-change-Linked-Helper-user-data-folder

## B9.4. SYMPTOM: "I need to delete a campaign / profile / LinkedIn account and there's no Delete button"
**Likely cause — this is by design.** Deletion is blocked to protect database consistency. Three separate cases, three separate workarounds.
**Campaigns** — cannot be deleted: *"it is not possible to delete a campaign from the Linked Helper 2 Instance as it may cause consistency issues in the database."*
**Archive instead:** install the **`Multi-campaigns runner plug-in`** (Plug-in store) → **Campaigns** → select the campaign → click **`Archive`**. **Unarchive:** Campaigns → **`Archived`** tab → select → **`Unarchived`** → switch back to the **`Main`** filter to confirm. `[UNVERIFIED]` the article does not state what happens to associated contacts.
**CRM profiles** — cannot be deleted: *"it is not possible to delete profiles out of CRM…because it might cause data consistency issues."*
**Hide instead:** install the **`Tagging system plug-in`** → tag the unwanted profiles **`deleted`** → apply a **"Without Tags"** filter to hide them → optionally use the `deleted` tag to push them into an **Exclude list** (needs the `Exclude list` plug-in).
**LinkedIn accounts in the Launcher** — cannot be deleted: *"it is not possible to delete a LinkedIn account out of your Linked Helper 2 Launcher permanently due to safety and possible database consistency issues."*
**Archive instead:** click **`Open`** on the account → **log out from LinkedIn** → click **`Stop`** to close the window → select the account → **`Edit Linkedin account credentials`** → **delete the password field** (optionally rename the email with an identifier, since *"this instance can't be used for another LinkedIn account"*) → click **`Archive`**.
**If that fails** — do not attempt manual database edits. Escalate to support.
Source: https://support.linkedhelper.com/hc/en-us/articles/360018168939-How-to-delete-archive-a-campaign
Source: https://support.linkedhelper.com/hc/en-us/articles/360015485399-Can-I-delete-profiles-from-CRM
Source: https://support.linkedhelper.com/hc/en-us/articles/360018187780-How-to-delete-a-LinkedIn-account-from-the-Launcher

---

# B10. LICENCE / ACTIVATION / MULTI-MACHINE
## B10.1. SYMPTOM: licence appears attached to the wrong LinkedIn account / instance
**Likely cause** — instance/licence confusion. **Rule:** an instance is permanently bound to the
**first** LinkedIn account logged in through it. Licences, however, *are* movable between accounts/instances.
**Checks**
1. Launcher → `Licenses` → which instance holds the licence?
2. Launcher → `LinkedIn accounts` → which instance is bound to the account you want to run?
**Fix**
1. Reassign the licence rather than recreating the instance — see the User-manual articles *"How to switch a license between your LinkedIn accounts in a workspace"* and *"How to switch orders, licenses, and data credits between your workspaces"*. Licence and workspace mechanics: `references/plans-and-platform.md`.
**If that fails** — escalate with the Linked Helper account email, both instance IDs and a screenshot of the `Licenses` menu.
Source: https://support.linkedhelper.com/hc/en-us/articles/4408390475154-Errors-when-adding-LinkedIn-account
Source: https://support.linkedhelper.com/hc/en-us/articles/360018187780-How-to-delete-a-LinkedIn-account-from-the-Launcher

## B10.2. SYMPTOM: can't open a second Launcher / same account on two PCs
**Likely cause — enforced by design.** [LH-CLAIM]
- **"You won't be able to open several 'Launchers' at the same time"** on one PC — one Launcher holds many LinkedIn accounts.
- **"You won't be able to open the same LinkedIn account under one and the same Linked Helper account from several machines simultaneously."**
- **"We strongly do not recommend using the same LinkedIn accounts under different Linked Helper accounts from several machines at the same time."**
**Checks**
1. Is a Launcher already running on this PC (tray/task manager)?
2. Is the same LinkedIn account open on another machine right now?
**Fix**
1. Use the single Launcher — it holds many LinkedIn accounts; you do not need a second one.
2. You *may* log out of one Linked Helper account and into another on the same PC — each keeps separate LinkedIn profiles and databases.
3. To work the account on a different machine, data is local per machine → **"move your data to another PC via backups"** (B9.1).
**If that fails** — running the same LinkedIn account from two machines also drives B5.3 and B5.4; stop doing it before escalating anything else.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016336859-Can-I-use-Linked-Helper-2-on-several-PCs

## B10.3. SYMPTOM: activation-key error `[UNVERIFIED]`
No article documents specific activation/key-rejection error strings. **Do not assert a fix.** Licence-purchase and activation happy-paths are in `references/plans-and-platform.md`. Route the exact error string to support. See §Unverified symptoms.
Source: none found — no help-center article in the FAQ, Recipes and tips, or Issues & solutions categories documents this symptom. Do not cite one.

---

# B11. VPS / RDP / 24-7 OPERATION
## B11.1. SYMPTOM: "campaigns stop when I turn off my PC / close my laptop"
**Likely cause — not a bug.** Verbatim: the standalone version **is not a cloud solution** — it
**"works locally on your PC, as well as all the data it collects is stored in a local database. Linked Helper cannot perform any action when it is stopped or when the PC is turned off."**
**Checks**
1. Does the machine sleep or hibernate on lid close?
2. Is the requirement genuinely 24/7, or would wider Working hours on a desktop suffice?
**Fix**
1. Install on a **remote server (VPS / dedicated server)**. Documented benefits: uninterrupted operation through PC failure/power/internet loss; access from anywhere; colleague/supervisor remote access; more simultaneous accounts on stronger hardware.
2. Server OS support, sizing and install-guide pointers: `references/plans-and-platform.md`.
**Operational caveat that bites on servers:** **"On Ubuntu, you need to approve the update by providing the user password, which means that you need to manually update Linked Helper from time to time"** — schedule a manual update check, or LinkedIn layout changes will accumulate (B12.5).
**If that fails** — escalate with the server OS, core/RAM allocation and account count.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015376519-Is-Linked-Helper-a-cloud-solution-Can-it-process-my-leads-while-PC-is-off
Source: https://support.linkedhelper.com/hc/en-us/articles/360016233680-How-to-run-Linked-Helper-in-a-cloud-remote-server

## B11.3. SYMPTOM: RDP session behaviour `[UNVERIFIED]`
Not documented anywhere in the help center: whether Linked Helper keeps running after you **disconnect** vs **sign out** of an RDP session; any registry/group-policy/command workaround to keep the GUI session alive; minimum **screen resolution**; server **sleep / lock-screen** settings; server **timezone** configuration steps. **Do not state RDP persistence behaviour as fact.**

One adjacent documented fact: Ubuntu server firewall guidance does whitelist RDP — `sudo ufw allow from any to any port 3389 proto tcp` (B7.1/B7.4).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015752540-How-to-install-Linked-Helper-on-a-VPS-virtual-private-server-with-Windows-OS

---

# B12. MISCELLANEOUS
## B12.1. SYMPTOM: antivirus flags Linked Helper / blocks the install
**Likely cause** — false positive. [LH-CLAIM] No detection names are published by the vendor, so record which product and which detection name you saw.
**Fix** — **"allow Linked Helper to run and add it to whitelist and reinstall if needed"**. Evidence to give a security team: installer digital signature plus two VirusTotal scans (installer and executable).
**If that fails** — see B7.2 (Windows install) and B8.1 solution #2 (Kaspersky port 443).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015995360-My-anti-virus-found-a-threat-Is-Linked-Helper-safe

## B12.2. SYMPTOM: UI too small / notification sounds annoying
**Fix** — **zoom level:** https://support.linkedhelper.com/hc/en-us/articles/10530825344530-How-to-change-Linked-Helper-zoom-level · **mute LinkedIn notification sounds:** https://support.linkedhelper.com/hc/en-us/articles/10536798577170-How-to-mute-LinkedIn-notification-sounds-in-Linked-Helper
Source: https://support.linkedhelper.com/hc/en-us/sections/360006011831-Frequently-asked-questions

## B12.3. SYMPTOM: "a feature I read about isn't in my interface"
**Likely cause** — the interface is plug-in driven. A **minimalist interface is the default for new users**; advanced features (List Manager, custom fields, logic operators) are toggled on via the **Plug-in store**. Plug-ins **"can be installed and removed at any time without ruining your campaigns workflow."**
**Checks** — open the **Plug-in store** menu and search for the plug-in the article names · installing makes the plug-in available for **every instance** on the account · `Organizations extractor` is the documented exception that is *not* on by default.
**Fix** — install the named plug-in from the **Plug-in store**, then re-open the action/campaign.
**If that fails** — check the build is current (`Check and install updates`, B12.5), and confirm the feature is not Pro-only or LinkedIn-subscription-dependent (`references/actions.md`, `references/plans-and-platform.md`).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015747600-Where-can-I-change-Linked-Helper-Interface

## B12.4. SYMPTOM: "LinkedIn's UI language must be English" `[UNVERIFIED]`
Commonly cited for LinkedIn automation tools, but **no help-center article states that LinkedIn's interface language must be set to English**. A targeted search returned only the unrelated *"How to convert English names to any other language?"* (message personalization) and *"Where can I change Linked Helper Interface?"* (plug-in-driven UI, B12.3). **Do not assert it.**
Source (searched, no such requirement found): https://support.linkedhelper.com/hc/en-us/articles/360015747600-Where-can-I-change-Linked-Helper-Interface

## B12.5. SYMPTOM: "a LinkedIn layout change broke the app" / "the app freezes" `[UNVERIFIED]`
Neither is documented as a named symptom with a fix. **Do not assert a cause.** The three documented handles closest to it:
1. The `"An action is paused due to too many recurring errors"` sleeping reason → check the **Failed** list, screenshot, contact support (B1.1 row 4).
2. The **"Reload (and clear cache option)"** right-click remedy for stale LinkedIn JavaScript (B2.1).
3. **`Check and install updates`** (https://support.linkedhelper.com/hc/en-us/articles/360017022919-Check-and-install-updates) and the **Change log** (https://support.linkedhelper.com/hc/en-us/articles/360019572979-Linked-Helper-2-Change-log) — updating is the de-facto fix when LinkedIn changes its layout.
**Working sequence:** update to the newest build → clear cache → send logs (§Collect before contacting support).
Source: https://support.linkedhelper.com/hc/en-us/articles/360015343160-Why-is-my-campaign-shown-as-sleeping-When-will-it-start

## B12.6. SYMPTOM: "sync problems" `[UNVERIFIED]`
Linked Helper is local-first — there is no multi-device sync to fail. Data movement between machines is manual, via **Backup → Export / Import** (B9.1). A separate **cloud-based storage version** exists, documented at https://support.linkedhelper.com/hc/en-us/articles/37009797813010-Linked-Helper-cloud-based-storage-version — not read for this pass; **flag any sync claim about it as `[UNVERIFIED]`**.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015376519-Is-Linked-Helper-a-cloud-solution-Can-it-process-my-leads-while-PC-is-off

---

# WHAT TO COLLECT BEFORE CONTACTING SUPPORT
**Export the logs — in-app:** Launcher → **`Backup`** → **`Logs & data for developers`**. This exports logs and a database archive, with **automatic upload to Linked Helper's servers**.
**Open the ticket:** left rail **`Need help`** → **`Ask for support`**. Fields: name, email, application version, message, **up to 5 files**.
**Always include**
- **"Linked Helper account email (can be found in the upper left corner of the Launcher)"**
- **LinkedIn instance ID from the title bar**
- The **verbatim error string** and which section of this file you already worked through
- Screenshots or related files (backups, CSV files)
- Screen recordings of the faulty process
- For install failures on Windows, the setup logs from `C:\%userprofile%\AppData\Local\SquirrelTemp\`
**Capture shortcuts**

| | Screenshot | Screen recording |
|---|---|---|
| Windows | **Ctrl + Prt Screen** | **Windows + G** (Win 10) |
| Mac | **Command + Shift + 3** | **Command + Shift + 5** |
**Other `Need help` menu items:** `Weekly invitations limit`, `Knowledge base`, `Video tutorials`, `Ask for support`, `Tip of the day`.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017185399-Need-help
Source: https://support.linkedhelper.com/hc/en-us/articles/360016353900-How-to-backup-restore-your-Linked-Helper-data
Source: https://support.linkedhelper.com/hc/en-us/articles/360015656279-Linked-Helper-installation-fails-on-Windows

---

# UNVERIFIED SYMPTOMS — DO NOT ASSERT A FIX
For every item below: the vendor's help center contains **no documented cause and no documented fix**. State that plainly, do the one or two documented adjacent checks named, then route the user to official support with logs (§Collect before contacting support). Never improvise a remedy and never present a plausible-sounding workaround as vendor guidance.

| Symptom | Status | Documented adjacent handles only |
|---|---|---|
| Captcha / security checkpoint / 2FA-OTP prompt | `[UNVERIFIED]` — no captcha flow, no OTP field, no scripted response to LinkedIn's "unusual activity" interstitial | Solve by hand in the embedded browser via the **`LinkedIn`** left-panel menu (B5.5) |
| `Check for replies` misses genuine replies | `[UNVERIFIED]` — no article documents this failure mode | Confirm the action is in the sequence (B4.1); the only documented controls are `Advanced settings for Check for replies plug-in` and `Ignore generic replies plug-in` (B4.5) |
| Activation-key / licence-key rejection errors | `[UNVERIFIED]` — no error strings documented | Licence happy-paths in `references/plans-and-platform.md`; send the exact string to support (B10.3) |
| RDP disconnect vs sign-out persistence, resolution minimum, server sleep/lock, server timezone steps | `[UNVERIFIED]` — not documented in the cloud overview or the Windows VPS guide | Ubuntu firewall guidance whitelists RDP: `sudo ufw allow from any to any port 3389 proto tcp` (B11.3) |
| "LinkedIn UI language must be English" | `[UNVERIFIED]` — no such requirement in any article | B12.4 |
| "LinkedIn layout change broke the app" / app freeze | `[UNVERIFIED]` — not a named symptom | `"An action is paused due to too many recurring errors"` → Failed list (B1.1 row 4); **"Reload (and clear cache option)"** (B2.1); `Check and install updates` (B12.5) |
| "Sync problems" | `[UNVERIFIED]` — local-first, no multi-device sync exists to fail; the cloud-based storage version was not reviewed | Manual movement via **Backup → Export / Import** (B9.1, B12.6) |
| Max collectible post likers/commenters, their rate limits, completeness | `[UNVERIFIED]` — not stated | B2.2 |
| Email-finder hit rates | `[UNVERIFIED]` — no percentages published | B2.4 |
| Automatic-backup schedule or retention count | `[UNVERIFIED]` — none documented | B9.1 |
| What happens to contacts when a campaign is archived | `[UNVERIFIED]` — the article is silent | B9.4 |
| Which LinkedIn pages `Collect` does not support | `[UNVERIFIED]` — the article does not enumerate them | Workarounds in B2.3 |
