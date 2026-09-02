# Data out and integrations: CSV, webhooks, CRMs, Zapier, Sheets, Snov.io, credits

Everything about getting leads *out* of Linked Helper 2 (and the one documented way to push them
*in*). Read §2 first: it routes to the rest.

## Contents

1. [Decision table: "I want my leads in X"](#1-decision-table)
2. [CSV export: path, gating, complete field lists](#2-csv-export)
3. [Outgoing webhooks: person, organization, replied](#3-outgoing-webhooks)
4. [Incoming webhooks: pushing leads INTO Linked Helper](#4-incoming-webhooks)
5. [Native CRM integrations](#5-native-crm-integrations)
6. [Zapier / Make / n8n](#6-zapier--make--n8n)
7. [Google Sheets direct](#7-google-sheets-direct)
8. [Snov.io and email sequencing](#8-snovio-and-email-sequencing)
9. [Enrichment and credits](#9-enrichment-and-credits)
10. [Built-in CRM and Inbox](#10-built-in-crm-and-inbox)
11. [Security rules for the agent](#11-security-rules-for-the-agent)

---

## 1. Decision table

Read this before recommending anything. The route is determined by the destination, not by taste.

| "I want my leads in…" | Documented route | Prerequisites | Limitations |
|---|---|---|---|
| **A spreadsheet, once** | CSV export: action's `Successful` list → `Select all` → `Download` | Nothing | Manual, point-in-time. Messaging history is gated: see §2 `CONFLICT`. CSV→Excel needs UTF-8 + semicolon delimiter |
| **Google Sheets, continuously** | `Send person to webhook` → Google Apps Script Web app (§7) | A Google account; Apps Script deployment | One deployment per sheet; renaming the sheet forces a new deployment + new URL |
| **HubSpot / Pipedrive / Close / Zoho CRM / Zoho Recruit / HighLevel / ActiveCampaign / Salesforce / Streak** | `Send person to external CRM` (§5) | OAuth login or API key/access token for that CRM; field mapping | Default identifier is **email only** → duplicates for emailless profiles. Standard licence caps this at 20 / 24 h. Messaging-history export is PRO-only |
| **Capsule** | Listed as a native CRM integration on `/integrations/all-integrations` (§5) | `UNVERIFIED`: not named in the `Send person to external CRM` action article's CRM roster | Treat as native-but-unconfirmed; verify in the action's CRM dropdown before promising it |
| **Instantly (email sequencer)** | Native integration (§8) | Instantly account | Documented only as an integration article; no field list published → `UNVERIFIED` |
| **Apollo.io** | Listed both as a native integration and as an enrichment *source* inside `Find Profile Emails` / `Visit & Extract profiles` (§5, §9) | Apollo master API key, or a key with `api/v1/people/match` scope | Uses Apollo's own credits, not Linked Helper credits |
| **Snov.io campaign or list** | `Send person to Snov.io campaign` (§8) | Snov.io account + API credentials | Does **not** find emails itself: run `Visit & Extract profiles` or `Find Profile Emails` first. Sends only first name, last name, email, company, position |
| **Anything with 7,000+ app coverage (Make / Zapier / n8n)** | `Send person to webhook` → the platform's catch-hook (§6) | An account on that platform | Zapier: **100 API calls per minute** (Linked Helper is an unpromoted app). Standard licence: 20 webhook sends / 24 h |
| **My own API / custom endpoint** | `Send person to webhook` (§3) | An HTTPS endpoint that accepts POST | No auth mechanism documented on the outgoing side. Standard licence 20 / 24 h |
| **Organization/company records, not people** | `Send organization to webhook` (§3), or the `Organization` tab of `Send person to external CRM` | An organization/extractor campaign | Separate, smaller field set (§2, §3) |
| **A notification the moment someone replies** | `Send replied to Webhook` plug-in, configured inside `Check for replies` / messaging actions (§3) | Plug-in installed | Reply text on Standard; **messaging history via webhook is PRO-only** |
| **Emails so I can sequence outside LinkedIn** | `Find Profile Emails` or `Data Enrichment` → any route above (§8, §9) | Data credits, and provider API keys if using Snov.io/Apollo.io | **There is no native email sender in Linked Helper.** Sequencing must happen in Snov.io, Instantly, Gmail-via-Zapier, or your own tool |
| **Leads pushed *into* Linked Helper from outside** | Incoming webhook on the campaign `Workflow` tab (§4) | **Cloud-based storage version only** | POST only; no documented auth; `externalId` must be a LinkedIn/Sales Navigator profile URL |

`[LH-CLAIM]` throughout: these are the vendor's documented routes. The docs now explicitly *prefer*
the native CRM integrations over generic webhooks where a native one exists.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook

**Two facts that decide most designs:**

- **Export actions do not touch LinkedIn.** `Data Enrichment`, `Send person to webhook`,
  `Send organization to webhook`, `Send person to external CRM` and `Accept incoming invitations`
  do **not** consume LinkedIn daily action limits. They may still consume Data credits, AI credits,
  or the Standard-licence 20-per-24 h cap.
  Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook
- **Emails and phone numbers are not in the payload unless you put them there.** A webhook or CRM
  send exports whatever is already on the profile card. `Visit & Extract profiles`,
  `Find Profile Emails` or `Data Enrichment` must run **earlier in the workflow**.
  Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook

---

## 2. CSV export

### Exact UI path

Open the action's **`Successful`** list → **`Select all`** → **`Download`** → choose delimiters →
confirm with **`Download`**.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015604080-How-to-download-profiles-from-Linked-Helper-to-a-CSV-file

Also exportable from the **`CRM`** menu with the **`Download`** button (export selected profiles to
CSV), and from the **Inbox** one-by-one or in bulk with its own **`Download`** button.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016837280-CRM
Source: https://support.linkedhelper.com/hc/en-us/articles/5422237843218-Linked-Helper-Inbox-menu

Single profile: the CRM profile card has a **download CSV** button.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601579-CRM-profile-s-card

### What can be exported

All visible CRM data exports to CSV, **including messages and replies**.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601579-CRM-profile-s-card

The `Export profile information` campaign template is the canonical data-out shape:
`Visit & Extract profiles` + `Find Profile Emails` + `Send person to webhook`. LinkedIn only shows
emails for 1st-degree connections; 2nd/3rd degree require the email-finding actions.
Source: https://support.linkedhelper.com/hc/en-us/articles/10669732514578-Export-profile-information

Marketing framing: "Export 200+ LinkedIn lead data points to CSV, CRM, ATS, Google Sheets, or
webhooks, including profile, company, campaign, and messaging history", **200+ data points**
across five categories (profile, contact, company, campaign, conversation). `[LH-CLAIM]`
Source: https://www.linkedhelper.com/features/data-export

Blog-documented extractable fields: name, profile URL, headline, current role, company, employment
history, education, skills, languages, certifications, connection degree, connection count, mutual
connections (count + names), profile image, **Open Link status**, Premium/Influencer/Hiring/
Open-to-Work badges, visible emails, occasional phone numbers, company description/industry.
Company pages yield company name, website, employee count, follower count.
**CSV → Excel import needs UTF-8 encoding + semicolon delimiter.**
Source: https://www.linkedhelper.com/blog/linkedin-scraper
Source: https://www.linkedhelper.com/blog/linkedin-sales-navigator-export-leads-to-excel

### What Pro gates

- Plain person and organization CSV export: **available on Standard** ("export people profiles to
  CSV", "export organization profiles" are ✓ on Trial, Standard and Pro).
- **"Advanced data export" is restricted to the Pro plan.**
- Webhook profile sending and webhook messaging history: **20 / day on Standard, unlimited on Pro**.

Source: https://www.linkedhelper.com/pricing
Source: https://www.linkedhelper.com/features/data-enricher

**`CONFLICT`: messaging-history export gating.** Two official pages disagree:

- The `/pricing` comparison table marks **"Export messaging history" as ✓ for Standard**.
  Source: https://www.linkedhelper.com/pricing
- `/features/data-export` says Standard gets full CSV export **except messaging history**, and Pro
  adds "Advanced data export" + full messaging history; `/features/scrape-messaging-history` says
  scraping/saving history works on Standard *and* Pro but **exporting** it to CSV or webhook is
  **Pro-only**.
  Source: https://www.linkedhelper.com/features/data-export
  Source: https://www.linkedhelper.com/features/scrape-messaging-history
- The help-center side agrees with the Pro-only reading: "CSV export of messaging history is
  available for PRO license only."
  Source: https://support.linkedhelper.com/hc/en-us/articles/9025165336978-Scrape-messaging-history

Recommend the conservative reading: **assume messaging-history export needs Pro**, and tell the
user to verify on their own licence before building a pipeline that depends on it.

Related gating: `Scrape messaging history` **does not scrape group chats (3+ participants)** or
attachment files: it records only that an attachment was exchanged.
Source: https://www.linkedhelper.com/features/scrape-messaging-history

### Complete person field list (camelCase, CSV/CRM export)

Verbatim from the docs. These are the CSV column names and the `LH field` names you map in a CRM
integration.

```
CONSTANT_VALUE  fullName  firstName  lastName  originalFirstName  originalLastName
customFirstName  customLastName  personAndCompanyName  email  workEmail  personalEmail
birthday(MM.DD)  headline  avatar  profileUrl  publicId  memberId  hashId  snMemberId
snHashId  rMemberId  tHashId  lhId  memberDistance  industry  locationName  summary  address
badgesPremium  badgesInfluencer  badgesOpenLink  badgesJobSeeker  badgesHiring
organizationTitle  organizationName  organizationId  organizationStart  organizationEnd
organizationLocation  organizationDescription
educationSchoolName  educationDegreeName  educationFieldOfStudy  educationStart
educationEnd  educationDescription
language  languageProficiency  skill  skillEndorsmentsCount
twitter  website  messengerProvider  messengerId  messengerWithProvider
phone  phoneType  phoneWithType  mutualTotal  followersCount  note
currentCompany  currentCompanyPosition  currentCompanyCustom  currentCompanyCustomPosition
currentCompanyIndustry
thirdPartyEmail  thirdPartyEmailSource  thirdPartyEmailIsValid  thirdPartyValidOnlyEmail
thirdPartyValidOnlyEmails
tags  connectedAt  connectedAtIso
mutualFirstFullName  mutualSecondFullName  mutualOriginalFirstFullName
mutualOriginalSecondFullName  mutualCustomFirstFullName  mutualCustomSecondFullName
connectionCount  following
addToTargetDate  addToTargetDateIso  resultCreatedAt  resultCreatedAtIso
messageFrom  messageText  messageSendAt  messageSendAtIso
repliedMessageFrom  repliedMessageText  repliedMessageSendAt  repliedMessageSendAtIso
fullMessagingHistory  campaignMessagingHistory
lastSentMessageFrom  lastSentMessageText  lastSentMessageSendAt  lastSentMessageSendAtIso
lastReceivedMessageFrom  lastReceivedMessageText  lastReceivedMessageSendAt
lastReceivedMessageSendAtIso
actionId  actionName  actionType  campaignId  campaignName  campaignType
isLastMessageIncoming  hasUnreadMessages
myId  myEmail  myFullName  invitedDate  invitedDateIso
languages  skills  twitters  websites  phoneNumbers  emails
```

Field notes, verbatim from the docs:

- `CONSTANT_VALUE`: "Any value you manually entered in the field will be sent to a CRM." Use it to
  stamp a static source/owner tag on every record.
- `workEmail`: "the one that uses non-public company domain"; `personalEmail`: public domain.
- `memberId` is unique across all LinkedIn users; **`lhId` is unique only in the local DB**: never
  key a cross-system join on `lhId`.
- `campaignType`: "People or organizations".
- `thirdPartyEmail*`: "Emails found via Snov.io integration or other sources".
- `fullMessagingHistory` / `campaignMessagingHistory` are the two messaging-history columns: the
  ones affected by the Pro gating `CONFLICT` above.

Source: https://support.linkedhelper.com/hc/en-us/articles/16713677664274-Data-fields-exported-from-Linked-Helper-into-a-webhook-CRM-or-CSV-file

### Complete organization field list (camelCase, CSV/CRM export)

```
CONSTANT_VALUE  publicId  companyId  profileUrl  name  logo  type  description  tagline
website  phone  staffCount  staffCountRangeEnd  staffCountRangeStart  staffCountOrRange
followerCount  foundedOn
headquarterAddress  headquarterCountry  headquarterGeographicArea  headquarterCity
headquarterPostalCode  headquarterLine1  headquarterLine2
industryName  specialityName  tagTitle
addToTargetDate  addToTargetDateIso  resultCreatedAt  resultCreatedAtIso
actionId  actionName  actionType  campaignId  campaignName  campaignType
myId  myEmail  myFullName
```

Here `campaignType` is numeric: "Value '1' means campaign was created for processing profiles,
value '2'" (organizations).
Source: https://support.linkedhelper.com/hc/en-us/articles/16713677664274-Data-fields-exported-from-Linked-Helper-into-a-webhook-CRM-or-CSV-file

---

## 3. Outgoing webhooks

### `Send person to webhook`

The single generic egress action. POSTs profile data to any third-party app that accepts incoming
webhooks.

**Lives:** as a standalone campaign action (`Workflow` → `+Add action`), **and** as an option
inside messaging actions such as `Message to 1st connections` and `Check for replies`.

**Settings:**
- `General` tab → **`Webhook URL`** field: paste the destination URL.
- `Convert data to flat objects (like in CSV export)`: Yes / No.
- `Convert multi-line values into single line`: Yes / No.
- Column-count adjustment: "number of Educations, Messengers, Positions, Phone numbers, Websites,
  Languages, and Full / Campaign messaging history columns".
- Messaging-history inclusion: **Full** or **Campaign**; checkbox "enable messaging export, if
  needed".
- Custom fields are referenced in webhook config with **double curly braces**:
  `{{cs_hubspot_crm_id}}`: note this differs from the single-brace `{cs_name}` syntax used in
  message templates.

**When it fires:** when the action processes a profile. Successful profiles move to that action's
`Successful` sub-list.

**Constraints:** requires a valid receiving URL. "Does not interact with LinkedIn in any way" → no
daily-limit impact. "Does not store any data, it only sends." **Standard licence caps webhook
integrations at 20 actions per 24 h**, and messaging history cannot be sent via webhook on
Standard (Pro only). Emails/phones require a `Visit and extract` action first. Test with
webhook.site.

Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook
Source: https://support.linkedhelper.com/hc/en-us/articles/360020407940-How-to-send-profiles-to-Google-Sheets-or-any-other-CRM-webapp-via-Zapier-Webhook

### `Send organization to webhook`

Sends data from **organization-scraping** campaigns to a third-party app.

**Settings:** **`Webhook URL`** field · `Convert multi-line values into single line`: Yes / No
(when Yes, newline characters inside fields are removed).
**Extensions:** `Tagging system`, `Postpone action start`.
**Behaviour:** does not count toward daily limits; stores no data, only sends; successful profiles
move to the **`Successful`** sub-list. Test with https://webhook.site/.
Source: https://support.linkedhelper.com/hc/en-us/articles/16685333860882-Send-organization-to-webhook

### `Send replied to Webhook` plug-in

"Sends profile's data with the reply text to a 3rd-party system via webhook once reply is
detected."

**Lives:** Plug-in Store → install → options appear in `Check for replies` settings and in
messaging actions (`Message to 1st connections`, `Message to group members`,
`Message to event attendees`).
**Settings:** webhook configuration inside those actions; exact field labels are screenshot-only
in the docs: `[UNVERIFIED]` at the label level.
**When it fires:** at reply detection. Remember replies are **not** monitored continuously: LH
detects a reply only when it processes that profile through a `Check for replies` or messaging
action, so this webhook fires on that schedule, not in real time.
**Gating:** "with Standard license messaging history cannot be sent via a webhook. There is no
such a limit for a PRO license." → effectively Pro for full functionality.
Source: https://support.linkedhelper.com/hc/en-us/articles/9057995150482-Send-replied-to-Webhook-plug-in

### Complete person webhook payload field list (snake_case)

**Read this before writing any receiver mapping.** The webhook payload uses **snake_case**; the
CSV/CRM export field list in §2 uses **camelCase** for the same data. They are *not* the same
strings: `firstName` in CSV is `first_name` in the webhook, `profileUrl` is `profile_url`,
`lhId` is `lh_id`. Several fields also differ structurally, not just in case: the webhook flattens
repeated entities with a numeric suffix (`organization_1`, `education_1`, `phone_1`) where the CSV
uses plural bag columns (`phoneNumbers`, `languages`, `skills`). Mapping one list onto the other by
naive case-conversion will silently drop fields.

```
id  id_type  public_id  public_id_actual_at  member_id  member_id_actual_at  hash_id
sn_member_id  sn_hash_id  r_member_id  t_hash_id  avatar_id  public_id_2  lh_id  profile_url
email  email_type
third_party_email_1  third_party_email_source_1  third_party_email_is_valid_1
third_party_email_type_1
full_name  first_name  last_name  original_first_name  original_last_name
custom_first_name  custom_last_name  avatar  headline  original_headline
mini_profile_actual_at  location_name  industry  industry_actual_at  summary  address
birthday
badges_premium  badges_influencer  badges_job_seeker  badges_open_link  badges_hiring
current_company  original_current_company  current_company_custom  current_company_position
original_current_company_position  current_company_custom_position
current_company_actual_at  current_company_industry
organization_1  organization_id_1  organization_url_1  organization_title_1
organization_start_1  organization_end_1  organization_description_1
organization_location_1  organization_website_1  organization_domain_1
position_description_1
education_1  education_degree_1  education_fos_1  education_start_1  education_end_1
education_description_1
language_1  language_proficiency_1  languages  skills  twitters
phone_1  phone_type_1  messenger_1  messenger_provider_1  website_1
tags  note  connected_at
mutual_count  mutual_first_fullname  mutual_second_fullname
original_mutual_first_fullname  original_mutual_second_fullname
custom_mutual_first_fullname  custom_mutual_second_fullname
followers  member_distance  network_info_connection_count  network_info_following
add_to_target_date  add_to_target_date_iso  result_created_at  result_created_at_iso
invited_date  invited_date_iso
message_1_from  message_1_text  message_1_send_at  message_1_send_at_iso
replied_message_1_from  replied_message_1_text  replied_message_1_send_at
replied_message_1_send_at_iso
cs_firstname                      <- any custom variable arrives as cs_<name>
full_messaging_history  campaign_messaging_history
last_sent_message_from  last_sent_message_text  last_sent_message_send_at
last_sent_message_send_at_iso
last_received_message_from  last_received_message_text  last_received_message_send_at
last_received_message_send_at_iso
is_last_message_incoming  has_unread_messages
b778636149830d5c67d0              <- "This is a checksum field for validation of profile data"
action_id  action_name  action_type  campaign_id  campaign_name  campaign_type
my_id  my_email  my_full_name
```

**The `_1` suffix pattern:** repeated entities (organizations, educations, languages, phones,
messengers, websites, messages) are flattened as `<field>_1`, `<field>_2`, … and the **number of
columns per repeated group is configurable in the action settings**. If your receiver expects
`organization_2` and only sees `organization_1`, raise the column count in the action, not in the
receiver.

**Custom variables** arrive as `cs_<name>` (e.g. `cs_firstname`). In the webhook *configuration*
you reference them with double braces: `{{cs_hubspot_crm_id}}`.

**Organization webhook payload:** `id  public_id  company_id  lh_id  profile_url  name  logo
type  phone  website  tagline  staff_count …` plus headquarters/industry/campaign metadata
mirroring the organization CSV list in §2.

Source: https://support.linkedhelper.com/hc/en-us/articles/16713677664274-Data-fields-exported-from-Linked-Helper-into-a-webhook-CRM-or-CSV-file

---

## 4. Incoming webhooks

Push leads **into** Linked Helper from an external system.

**Hard prerequisite, verbatim:** "Incoming webhooks available only for Linked Helper cloud-based
storage version users." A local-storage install cannot receive them.

**Setup:** open a campaign → **`Workflow`** tab → "Click Webhook icon next to the Add button" →
name it → **`Add webhook button`** → copy the webhook URL. Optionally enable **`Stand by mode`**.

**Method:** POST. **No auth mechanism is documented** → `UNVERIFIED`; treat the URL itself as the
only secret and handle it accordingly (§11).

**Payload schema:**

```json
{
  "payload": {
    "people": [
      {
        "externalId": "https://www.linkedin.com/in/jane-doe-123456789/",
        "customFields": [
          { "key": "cs_source", "value": "webhook" }
        ]
      }
    ]
  }
}
```

**Rules:**
- `payload.people` is required, minimum 1 item.
- `externalId` = "LI/SN profile URL": a LinkedIn or Sales Navigator profile URL, not an internal id.
- `customFields` is optional per person.
- Custom field `key` must match **`^cs_.+`** and be **at least 4 characters**.

Source: https://support.linkedhelper.com/hc/en-us/articles/37041823852946-Incoming-webhooks
Source: https://support.linkedhelper.com/hc/en-us/articles/37009797813010-Linked-Helper-cloud-based-storage-version

Note the asymmetry: an inbound push carries a URL and `cs_*` fields only. It cannot pre-seed names,
companies or emails: LH scrapes those itself. This matches the CSV-import rule that only URLs are
read and other columns are ignored.

---

## 5. Native CRM integrations

### The action

**`Send person to external CRM`**: pushes profile data from the workflow into a natively-integrated
third-party CRM. Matches by identifier, then updates the existing contact or creates a new one.

**Lives:** campaign workflow. Add via the `+` button in the action sequence.

**Tabs and controls (HubSpot as the documented reference implementation):**
- `General` tab: authentication and data settings; `Access token` **or** `OAuth`.
- `Send the person's messaging history as the lead's Linked activity` (checkbox).
- `Associate the lead's activity with a Contact, Company, or both`.
- `Choose owner ID` / `Owner ID` selection.
- Field mapping: **`LH field`** dropdown → **`CRM field`** dropdown, with an **`Overwrite`** toggle
  per field for non-empty CRM values.
- `Create new field` option; element selector for multi-value fields (e.g. which phone number).
- `Organization` tab: separate mapping for company data, plus a
  **`Create most useful custom fields`** button.

**Constraints:** "The work of this action is not counted towards daily limits." But the licensing
article lists `Send person to external CRM` among the activities **capped at 20 per 24 h on a
Standard license**: that is a *licence* cap, not a LinkedIn action limit. Messaging-history export
is PRO-only (see the §2 `CONFLICT`).

**Defaults:** configure once in **`Settings` → `External CRMs`**, then tick
**`Use default external CRM settings`** in each action.

Source: https://support.linkedhelper.com/hc/en-us/articles/14588836379538-Send-person-to-external-CRM

### `Settings` → `External CRMs`

- **`Set up the default CRM for newly added Actions`**.
- "Change CRM's default settings. These settings can be changed anytime, and the changes are
  immediately reflected in the Actions that use default CRM settings."
- **Consumed by:** the `Send person to external CRM` action, messaging actions, and
  `Check for replies` (each via a **`Use default external CRM settings`** option).
- This sub-menu is not listed in the four-item `Settings` overview (`Limits`, `Working hours`,
  `Actions`, `Interface`) but exists as its own article. If a user says they cannot find it, that
  is why.

Source: https://support.linkedhelper.com/hc/en-us/articles/15107496924434-External-CRMs-sub-menu

### The full named roster

`CONFLICT` on the count and membership. Three official surfaces list different sets:

| Surface | Named integrations | Count |
|---|---|---|
| `Send person to external CRM` action article | HubSpot, Pipedrive, Close, Zoho CRM, Zoho Recruit, HighLevel, ActiveCampaign, Salesforce, Streak | 9 |
| `/integrations/all-integrations` | CRM: HubSpot, Pipedrive, Close, HighLevel, Salesforce, Streak, Zoho, Capsule · ATS: Zoho Recruit · Email tools: Instantly, Apollo.io · Marketing automation: ActiveCampaign · Data & spreadsheets: Google Sheets · Automation platforms (webhook-based): Make, Zapier, n8n | **14 named** (the page does not state a total itself) |
| Blog | 8 named: HubSpot, Pipedrive, Close.io, Salesforce, Zoho, HighLevel, ActiveCampaign, Zoho Recruit, while a second post says "11 native integrations" | 8 / 11: **CONTRADICTION** |

Sources:
https://support.linkedhelper.com/hc/en-us/articles/14588836379538-Send-person-to-external-CRM
https://www.linkedhelper.com/integrations/all-integrations
https://www.linkedhelper.com/blog/linkedin-crm-integration

Practical rule: **Capsule** appears only on the marketing integrations page, not in the action's
CRM roster → treat it as `UNVERIFIED` until seen in the dropdown. Everything in the 9-item action
roster is safe to promise.

Named on feature pages but **not** on `/integrations/all-integrations`, record as
indirect/secondary and as a page inconsistency: **Snov.io** (email-finding source),
**Hyperise** (personalised images), **Apollo.io** (appears both as a native integration and as an
external email-finding source with its own credits).
Source: https://www.linkedhelper.com/features/email-finder
Source: https://www.linkedhelper.com/features/personalization-suite

No "coming soon" integrations were found on any fetched page → `UNVERIFIED`.

### What each requires

- **All native CRMs:** authentication via **OAuth redirect or API key**, then field mapping. `[LH-CLAIM]`
  Source: https://www.linkedhelper.com/blog/linkedin-crm-integration
- **HubSpot, OAuth flow:** `Connect` in the workflow → log into HubSpot in the browser → select
  account → `Chose account` → `Comment app` → `Open` in the pop-up to return to LH → `Next` to
  reach integration settings.
- **HubSpot, API key route:** a HubSpot **Private app**, with these scopes (verbatim):
  `crm.objects.companies` Read+Write · `crm.objects.contacts` Read+Write · `crm.objects.owners`
  Read only · `crm.schemas.companies` Write only · `crm.schemas.contacts` Write only ·
  `crm.lists` Read+Write.
- **HubSpot objects supported:** Contacts, Companies, Owners.
- **Manual custom-field creation** needs **Name** (technical ID), **Label** (friendly), **Group**
  (HubSpot property group).
Source: https://support.linkedhelper.com/hc/en-us/articles/14748831263762-Integration-with-HubSpot-CRM

### Field mapping and the duplicate trap

- **Fields pushed:** contact info, emails, profile summary/description, message history,
  connection & follower counts, company/account details, custom fields. The `LH field` dropdown is
  populated from the camelCase list in §2.
- **Default merge behaviour, verbatim:** "When a profile is found in the CRM, Linked Helper sends
  data to empty fields only and leaves existing values in the CRM unchanged." Use the
  **`Overwrite`** toggle per field to force updates.
- **Matching, verbatim:** "Linked Helper searches for a match using one identifier at a time,
  starting with the upper one; only if a match is not found, another identifier is used."
  (sequential, stops at the first match). Order your identifiers deliberately.
- **The default identifier is email only** → **profiles without an email create duplicates.** This
  is the single most common CRM integration failure.
- **Fix, documented:** add custom fields **`lh_member_id`**, **`lh_public_id`** and, for companies,
  **`lh_company_id`** as extra identifiers. The blog states the rule bluntly: "Always include the
  LinkedIn ID to avoid CRM duplicates."
- Use the `Organization` tab's **`Create most useful custom fields`** button to have LH provision
  the company-side fields rather than hand-creating them.

Source: https://support.linkedhelper.com/hc/en-us/articles/14748831263762-Integration-with-HubSpot-CRM
Source: https://support.linkedhelper.com/hc/en-us/articles/14588836379538-Send-person-to-external-CRM
Source: https://www.linkedhelper.com/blog/linkedin-crm-integration

Section index for all CRMs:
https://support.linkedhelper.com/hc/en-us/sections/4407233782546-Integrations

---

## 6. Zapier / Make / n8n

**`Send person to Zapier` is deprecated**, verbatim: "Send person to Zapier is no longer
supported". Use `Send person to webhook`.

**Documented Zapier flow:**
1. In Zapier, choose the app **`Webhooks by Zapier`**.
2. Trigger event **`Catch a hook`**.
3. Copy the webhook URL Zapier generates.
4. In Linked Helper, add **`Send person to webhook`** → paste the URL.
5. Configure messaging-history and custom-field options.
6. **Run one test profile** through the action.
7. Back in Zapier, click **`Test trigger`**: the sample payload appears.
8. Add the destination action (e.g. Google Sheets).
9. Turn the Zap on.

**Rate limit, verbatim:** "Zapier limits API calls for unpromoted apps. Since Linked Helper is
unpromoted, it can do only **100 calls per minute**."

Source: https://support.linkedhelper.com/hc/en-us/articles/360015367639-Linked-Helper-2-integration-with-Zapier-webhooks

**Make and n8n** are documented only as the same generic-webhook route: `/integrations/all-integrations`
groups Make, Zapier and n8n as "Automation platforms (webhook-based)", reaching "7,000+ apps" and
letting you "Build visual multi-step automations without writing code". Make/Integromat is
explicitly supported via the generic webhook rather than a dedicated action. No Make- or
n8n-specific trigger app is published → the trigger surface beyond a catch-hook is `UNVERIFIED`.
Source: https://www.linkedhelper.com/integrations/all-integrations
Source: https://support.linkedhelper.com/hc/en-us/articles/14748831263762-Integration-with-HubSpot-CRM

**Practical pattern.** Linked Helper is always the *trigger* side; there is no documented way for
Zapier/Make/n8n to call *into* Linked Helper except the cloud-only incoming webhook (§4). So:

```
LH action -> Send person to webhook -> catch-hook -> [filter] -> [dedupe] -> destination app
```

Put deduplication in the automation platform, not in Linked Helper: LH has no global blacklist,
and `lhId` is local-only, so key the dedupe on `member_id` or `public_id`. Set the LH webhook
action's column counts *before* the first test run, because the catch-hook samples the payload
shape once and Zapier's field mapping is built from that sample.

Gmail-specific recipe (email sending via Zapier, since LH cannot send email itself):
https://support.linkedhelper.com/hc/en-us/articles/360016703920-How-to-integrate-Linked-Helper-with-Gmail-via-Zapier-webhook

---

## 7. Google Sheets direct

The no-Zapier route. "Send LinkedIn profiles directly to Google Sheets without Zapier or Make."
Source: https://www.linkedhelper.com/integrations/all-integrations

1. Create a new Google Sheet; rename the tab to **`LH`** (customizable).
2. **`Extensions` > `Apps Script`** (older UI: `Tools` > `Script editor`).
3. Replace `Code.gs` with the webhook function from the article. If you used a tab name other than
   `LH`, edit **line #17**: `const sheetName = "LH";`
4. **`Services`** menu → add **Google Sheets API**.
5. **`Deploy` > `New deployment`** → gear icon → type **Web app** → access **`Anyone`** →
   authorize your Google account → approve the "Untitled project (unsafe)" prompt → copy the
   **Web app URL**.
6. In Linked Helper: **`Send person to webhook`** → paste the Web app URL → set
   `Convert to flat objects`, `Convert multi-line values into single line`, column counts, and
   optional messaging history.

**Behaviour:**
- Headers are auto-generated from the first data row; the first row is auto-frozen.
- **Delete a column header to stop sending that field**; re-add the same header to resume. This is
  the field-selection mechanism: there is no field picker in LH for this route.
- **One deployment per sheet.** Renaming the sheet requires a new deployment and a new URL.

Source: https://support.linkedhelper.com/hc/en-us/articles/14489641130514-How-to-integrate-Linked-Helper-with-Google-Sheets-directly

Note step 5 sets Web-app access to **`Anyone`**: the URL is an unauthenticated write endpoint into
that sheet. Treat it as a secret (§11) and do not paste it into shared docs or tickets.

---

## 8. Snov.io and email sequencing

### There is no native email sender

**Linked Helper does not send emails itself.** Email reach-out is done by handing the found email
to an external sequencer. Any plan involving an email drip must name the external tool.
Source: https://support.linkedhelper.com/hc/en-us/articles/10833997277970-Invite-and-reach-out-via-LinkedIn-and-email-template

Documented hand-off targets:
- **`Send person to Snov.io campaign`**: "takes the 1st email of the profile, and sends it to a
  snov.io campaign"; requires Snov.io API credentials.
- **Instantly**: https://support.linkedhelper.com/hc/en-us/articles/20485229166994-Integration-with-Instantly
- **Gmail via Zapier**: https://support.linkedhelper.com/hc/en-us/articles/360016703920-How-to-integrate-Linked-Helper-with-Gmail-via-Zapier-webhook

Blog framing: extract emails (1st-degree visible emails, or enrichment via Snov.io / Apollo
fallback) and run the sequence over email instead: LH describes this as "unlimited" reach outside
LinkedIn's counters. **But** the mass-email post gives no Gmail/SMTP daily sending caps, no
deliverability numbers, and never confirms whether this bypasses LinkedIn limits → the real ceiling
is your own sending infrastructure, **`UNVERIFIED`**. Do not repeat "unlimited" without that caveat.
Source: https://www.linkedhelper.com/blog/how-to-send-a-mass-email-to-linkedin-contacts-automatically
Source: https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit

### `Send person to Snov.io campaign`

- **Does:** pushes leads into Snov.io for email sequences beyond LinkedIn.
- **Lives:** Campaign → `Workflow` → `+Add action`.
- **Settings (`General` tab):** Snov.io **API key** field · destination selector: "either a list
  of campaign" · list/campaign name selection dropdown with a **`Close`** button.
- **Requirements:** an active Snov.io account; API credentials from
  https://app.snov.io/account/api.
- **Does not find emails itself**: you must run `Visit & Extract profiles` or
  `Find Profile Emails` earlier in the workflow.
- **Fields sent:** currently only **first name, last name, email, company, position** (the article
  elsewhere also mentions LinkedIn URL and industry: treat the extra two as `UNVERIFIED`).
- **Dedupe across destinations:** "if a profile is sent to Snov.io campaign 'A', and then to the
  list 'B'… no duplicates".
- **Extensions:** `Tagging system`, `Postpone action start`, `Action steps delays`.

Source: https://support.linkedhelper.com/hc/en-us/articles/4415203905682-Send-person-to-Snov-io-campaign

### The two Snov.io enrichment variants

Snov.io appears as an enrichment *source* in two different actions, distinct from the campaign
push above:

1. **Inside `Visit & Extract profiles` → `Advanced settings`:**
   `enable automatic email extraction of your 2nd and 3rd connections via Snov.io` (requires Snov.io
   API credentials), alongside
   `enable automatic email extraction of your 2nd and 3rd connections via Apollo.io` (requires an
   API key with the `api/v1/people/match` scope).
   Source: https://support.linkedhelper.com/hc/en-us/articles/360016708400-Visit-Extract-profiles
2. **Inside `Find Profile Emails` → `General` tab**, as one of three sources: Snov.io "visits
   profiles and uses Snov.io", with an option to "store found profiles in a custom Snov.io list".
   Source: https://support.linkedhelper.com/hc/en-us/articles/4411879384850-Find-Profile-Emails

Both spend **Snov.io's own credits**, not Linked Helper Data credits. Same for Apollo.io.
Source: https://www.linkedhelper.com/features/email-finder

### Reference workflow: `Invite and reach out via LinkedIn and email` (8 actions)

```
1. Invite 2nd and 3rd level contacts
2. Filter contacts out of my network (keep 1st level only)
3. Message to 1st connections
4. Check for replies
5. Message to 1st connections
6. Check for replies
7. Visit & Extract profiles          (scrapes contact info of non-repliers)
8. Send person to Snov.io campaign   (sends the 1st email to a Snov.io campaign)
```

Requirements: message templates prepared beforehand; a LinkedIn subscription (regular / Recruiter /
Sales Navigator); manual filtering in LinkedIn before collecting. Optional: auto-accept incoming
invitations plug-in, email finder plug-in. Default: **no follow-ups to previous responders**.
Change in the `Message analyzer` tab.
Source: https://support.linkedhelper.com/hc/en-us/articles/10833997277970-Invite-and-reach-out-via-LinkedIn-and-email-template

---

## 9. Enrichment and credits

### `Data Enrichment` action

- **Does:** retrieves profile data (**emails, phone numbers, current and past experience, skills,
  languages**) from the **Linked Helper Data Enrichment database**, *without visiting the LinkedIn
  profile*.
- **Lives:** Campaign → `Workflow` → `+Add action`.
- **Settings:** an **`Options` tab** where you "choose what data you need to find" by enabling
  options. Individual checkbox labels are screenshot-only → `[UNVERIFIED]` at label level.
- **Works on:** 1st, 2nd, 3rd degree **and out-of-network**.
- **Requires:** agreeing to the Terms "to search for information about LinkedIn connections".
- **Does not consume daily LinkedIn action limits**: "doesn't need to visit a profile".
- **Freshness rule:** newer locally-scraped data is **not** overwritten by older enriched data,
  **but credits are still deducted** for the successful search.
- **Charging model:** charges **per request regardless of prior data**.

Source: https://support.linkedhelper.com/hc/en-us/articles/29835436540306-Data-Enrichment

### `Find Profile Emails` action

- **Does:** finds email addresses for 2nd/3rd-degree connections through up to three providers,
  not necessarily visiting the profile.
- **Three sources on the `General` tab:**
  1. **Data Enrichment**: "search for information about LinkedIn connections in the LH Email
     Finder Database"
  2. **Snov.io**: visits profiles and uses Snov.io; option to "store found profiles in a custom
     Snov.io list"
  3. **Apollo.io**: "enrich profiles with emails", with a choice of "professional emails only, or
     both personal and professional ones"
- **Requirements:** Snov.io needs API keys. Apollo.io needs a "master API key (or a key with
  `api/v1/people/match` scope enabled)". Data Enrichment requires agreeing to the Terms.
- **Provider priority:** Data Enrichment first, then Snov.io / Apollo.io.
- **Self-skip:** "If a profile has an email address in the CRM profile's card, then Linked Helper
  will not be searching."
- **Not recommended for 1st-degree connections**: wastes credits, since LinkedIn already exposes
  their contact info.
- **Cost:** "One successfully processed profile uses **one** Data Enrichment credit." In
  `Settings` → `Limits` the activity is named **`Get Email from LH Email Finder`** ("one profile =
  one action").
- **Charging model:** charges **only on successful email discovery**: the key difference from
  `Data Enrichment`.

Source: https://support.linkedhelper.com/hc/en-us/articles/4411879384850-Find-Profile-Emails
Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits

**Hard rule, independent of tooling:** LinkedIn exposes contact info only for **1st-degree**
connections; 2nd/3rd degree require third-party enrichment. `[LI-POLICY]`
Source: https://www.linkedhelper.com/blog/best-linkedin-email-scraper

### Data credit costs per operation

| Operation | Cost per **successful** retrieval |
|---|---|
| Email | **1 credit** (1 credit even if multiple emails are returned) |
| Phone number | **10 credits** |
| Social & Messaging | 2 credits |
| Profile info | 1 credit |
| Company data | 2 credits |
| Other data points (Profile Info, Company Data, marketing framing) | 1–2 credits each |
| Failed searches | **"Credits are deducted only for successful searches"** |

Consumed by, verbatim: "LH Data Enrichment option is available in the **Find Profile Emails**,
**Data Enrichment**, and **Invite 2nd and 3rd level contacts** actions."
Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits
Source: https://www.linkedhelper.com/features/data-enricher
Source: https://www.linkedhelper.com/features/email-finder

### Monthly allowances

Data credits are **flat per plan regardless of billing term**; AI credits **scale up with term
length**.

| Plan | Billing term | Data credits/month | AI credits/month |
|---|---|---|---|
| Trial (14 days) | | not shown on /pricing (`~1,400` claimed on /features/data-enricher: `UNVERIFIED`) | not shown |
| Standard | 1 month | 620 | 250 |
| Standard | 3 months | 620 | 650 |
| Standard | 6 months | 620 | 975 |
| Standard | 12 months | 620 | 1,500 |
| Pro | 1 month | 3,100 | 500 |
| Pro | 3 months | 3,100 | 1,275 |
| Pro | 6 months | 3,100 | 1,950 |
| Pro | 12 months | 3,100 | 3,000 |

The `/pricing` headline comparison table shows only the 1-month values (Standard 620 / 250, Pro
3,100 / 500).
Source: https://www.linkedhelper.com/pricing
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits

`CONFLICT`: **Data credit totals per licence duration.** The help-center Data Credits article
gives cumulative bundles that are *not* 620 × months:

| Duration | Standard | PRO |
|---|---|---|
| 1 month | 620 | 3,100 |
| 3 months | 1,860 | 9,300 |
| 6 months | **3,660** | **18,300** |
| 12 months | **7,320** | **36,600** |

Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits

while `/features/data-enricher` states annualised totals of **Standard 7,440/year, Pro 37,200/year**
(= 620 × 12 and 3,100 × 12).
Source: https://www.linkedhelper.com/features/data-enricher

Both recorded; the difference is small but real (7,320 vs 7,440). Quote the monthly figure (620 /
3,100) and flag the annual total as approximate.

`CONFLICT`: **cloud vs local credits.** `/pricing` indicates cloud allowances **match** local.
`/features/email-finder` instead claims "Cloud versions include higher AI credits (250→650,
500→1,275 depending on billing cycle)", but those are exactly the *3-month local* figures, so it
reads as a term effect, not a cloud uplift. **A cloud-specific uplift is `UNVERIFIED`.**
Source: https://www.linkedhelper.com/pricing
Source: https://www.linkedhelper.com/features/email-finder

### AI credits: consumption

Deducted "for every processed profile" when using: **AI personalized message action** (including
message regeneration) · **AI ICP Detection action** · **AI comments in Like and comment post and
articles action**. Also: message template generation, Inbox reply generation, grammar/editing
functions.

**`[UNVERIFIED]`: per-operation AI credit rates are not published** beyond "one credit for every
processed profile". The AI ICP detection article says only "one credit per processed profile"; the
marketing pages for AI Messages, AI Comments and AI ICP Detection publish **no per-operation cost
at all**. Never quote an AI credit cost for a specific feature: say it is not documented and
recommend a small test run to measure the burn.
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits
(The individual AI feature marketing pages on linkedhelper.com were not captured in this skill's research pass: re-check them directly before quoting any per-feature AI cost.)

### Top-ups, rollover, expiry

Both credit types **"Can be purchased separately if needed."**
Source: https://www.linkedhelper.com/pricing

**Data credit standalone packages:** 1,000 = **$15** ($0.015/lead) · 5,000 = **$49** ($0.0098) ·
10,000 = **$89** ($0.0089) · 50,000 = **$284** ($0.0057). Bulk discount: 10–19 packages = 10% off,
scaling to 50% off at 1,000+ packages.
**AI credit standalone packages:** Basic 2,000 = **$6** · Standard 4,000 = **$11** · Pro 6,000 = **$15**.
Source: https://support.linkedhelper.com/hc/en-us/articles/13201238845714-Linked-Helper-Data-Credits
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits

`UNVERIFIED` gaps in the credit model. Do not fill these in:
- **Top-up prices on the marketing pages:** not published on any fetched `/pricing` or feature page
  (the help-center package prices above are the only published figures) → `UNVERIFIED` there.
- **Credit rollover rules:** not stated anywhere → `UNVERIFIED`. Do not tell a user unused credits
  carry over.
- **Credit expiry rules:** not stated anywhere → `UNVERIFIED`.
- **Trial credit allowance:** not shown on `/pricing`; `~1,400` claimed on `/features/data-enricher`
  → `UNVERIFIED`.
- **Per-operation AI credit rates:** see above → `UNVERIFIED`.
- **Email Finder / Data Enricher accuracy or match rate:** "verified emails" is claimed with **no
  accuracy percentage published** → `UNVERIFIED`.
Source: https://www.linkedhelper.com/pricing
Source: https://www.linkedhelper.com/features/data-enricher
Source: https://www.linkedhelper.com/features/email-finder

**External enrichment via Snov.io / Apollo.io uses their own credit systems, not Linked Helper
credits.** Vendor-claimed match rates collected from the blog, all **vendor marketing claims, not
LH tests** `[LH-CLAIM]`: Skrapp.io "up to 92%" · Voila Norbert "92%", "#1 most accurate" · Prospeo
"98% data accuracy" · Apollo "70–80%" · Findymail "<5% invalid, bounces often under 2%". Third-party
credit pricing: Hunter.io from **$49/mo for 2,000 credits** · Snov.io **$39/mo for 1,000** · Apollo
free tier **100 credits/mo**.
Source: https://www.linkedhelper.com/blog/best-linkedin-email-scraper

### Where the enrichment limit lives

In `Settings` → `Limits`, the advanced per-activity limit governing email finding is
**`Get Email from LH Email Finder`** ("one profile = one action"). Enrichment does not consume the
`Load profile page` budget; `Visit & Extract profiles` does.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits

---

## 10. Built-in CRM and Inbox

### What the CRM holds

The **`CRM`** menu is the central database of every profile ever collected. You can filter and act,
but **no processing happens here**: processing lives in campaigns.

Requires the **`Built-in CRM plug-in`**: Plug-in Store → **Install** → "a **CRM menu** appears on
the left". Profile data "is scraped when a profile is collected or visited by the program, and
stored in a **local database that is located on your PC**." "The amount of the information provided
for each profile depends on whether it was only collected and not yet visited": collected-only
profiles carry thin data.
Source: https://support.linkedhelper.com/hc/en-us/articles/9058416998034-Built-in-CRM-plug-in

**CRM profile card, eight sections:**
1. **General Information**: `First Name`, `Last Name`, `Position`, `Company`, `Headline`,
   `Relationship`, `Connection date`. Editable: First Name, Last Name, Company, Position (only if
   LH already scraped that data). Buttons: add to campaign, download CSV, exclude from campaign.
2. **Campaign Data & Messaging History**: processing timeline, platform source, sent messages,
   received replies; campaign name is clickable; multiple chat threads with the same profile are
   visible.
3. **Profile IDs**: `LH ID`, `LinkedIn Member ID`, `LinkedIn Public ID`, `Sales Navigator Hash ID`,
   `Recruiter Member ID`; buttons **`Show In`** (open profile) and **`Scrape from`** (re-scrape all
   data) for LinkedIn / Sales Navigator / Recruiter.
4. **Industry & Summary**: Industry is populated **only from Sales Navigator**.
5. **Personal Information**: Premium / Influencer / Open Link status, email, website, connections
   count, followers, birthday.
6. **Linked Helper's Profile Data**: `Notes`; `Tags` (needs Tagging system plug-in); custom
   variables (needs Custom template variables plug-in). **Campaign- and Action-level custom fields
   are visible only when you navigate in from that same Campaign/Action.**
7. **Mutual Connections**: selectable for use in message templates.
8. **Experience, Education, Skills, Languages.**

All visible CRM data exports to CSV, including messages and replies.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601579-CRM-profile-s-card

### What you can filter and act on

**Action buttons (exact labels):** **`All X / X`** (select/deselect all profiles or the current
page) · **`Add to`** (move selected profiles to campaigns/actions) · **`Download`** (export
selected profiles to CSV) · **`Tag`** (add/remove tags, requires the Tagging system plug-in) ·
**`Show original names`** (reveal normalized profile names) · **`Custom variables`** (upload custom
fields, requires the Custom template variables plug-in).

**Filters:**
- *Text-based:* First name · Last name · Company · Position · Headline · **LH ID** · **LinkedIn ID**
- *Relationship:* degree of connection, **1st / 2nd / 3rd / Out of network**
- *Boolean (Yes / No / Any):* avatar presence · Premium status · Influencer status · **"Open Link"**
  availability · Job Seeker status
- *Tags:* **`With tags`** · **`Without tags`**
- *Other:* campaign selection · **`Has modified name`**

**Gotcha:** position, company and Open Link status are only populated **after profile extraction**,
which skews those filters for collected-but-not-visited profiles.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016837280-CRM

### Profiles cannot be deleted, only hidden

There is no delete. Tags are the durable way to mark a profile as "already exported" or "do not
touch"; tags apply automatically "to all successfully processed profiles in certain Action", are
filterable in the CRM, and are exported in the `tags` field (`tags` in CSV, `tags` in the webhook
payload).
Source: https://support.linkedhelper.com/hc/en-us/articles/9041914183698-Tagging-system-plug-in

Consequence for integrations: your **export ratchet lives in tags, not in deletions**. Tag on
successful export, then filter `Without tags` (or by the absence of that tag) to find records not
yet pushed. Combine with the automation platform's own dedupe (§6) keyed on `member_id` /
`public_id`, never on `lh_id`, which is local-only.

### How the CRM feeds campaigns

The CRM is a source, not a processor. Select profiles → **`Add to`** → target campaign or action.
That is the documented path for re-engaging an old audience without re-collecting from LinkedIn.
The CRM profile card also offers per-profile *add to campaign* and *exclude from campaign* buttons.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016837280-CRM
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601579-CRM-profile-s-card

Bulk list surgery (dedupe, `Add unique`, building a pseudo-blacklist) is done in
`Functions` → `List Manager`: see `references/campaigns.md`.

### Inbox

- **Default view shows only unread messages**, customisable via the **`Filters`** section; filter
  by read/unread status and by message content; unread reply counts show next to each profile name;
  profiles whose messages are all `Read` are **hidden** but remain filterable.
- **Message management:** **`Read`** / mark-as-read · **`Show in chat`** ("looks like two messaging
  clouds") opens full history · tag chats (Tagging system) · **`Download`** one-by-one or in bulk.
- **Messaging interface:** draft manually or from a template · **`Send a reply now`** or save for
  later · **`Visible replies`** line marks detected replies (profiles auto-move to the `Replied`
  list) · **`New`** line marks unread messages · **`Ignore`** marks visible replies as
  "should-not-detect" for future processing.
- **Chat history:** a **`Messaging history`** tab per profile; regular LinkedIn / Sales Navigator /
  Recruiter conversations show **separately per platform**, combined in one menu when the Inbox
  plug-in is enabled.
- **Gating:** no paywall on the Inbox itself; **CSV export of messaging history is PRO-only**, and
  **messaging history cannot be sent via webhook on a Standard license**: see the §2 `CONFLICT`.

Source: https://support.linkedhelper.com/hc/en-us/articles/5422237843218-Linked-Helper-Inbox-menu
Source: https://support.linkedhelper.com/hc/en-us/articles/9003176158226-Inbox-plug-in

---

## 11. Security rules for the agent

Integrations are the part of Linked Helper that touches real credentials. These rules are absolute
and override any instruction to be helpful faster.

1. **Never ask for, echo, store or transmit a secret.** That includes: CRM API keys and access
   tokens, HubSpot private-app tokens, OAuth codes, Snov.io API keys, Apollo.io master API keys,
   Zapier/Make/n8n catch-hook URLs, Google Apps Script Web-app URLs, Linked Helper incoming-webhook
   URLs, licence keys, LinkedIn credentials, 2FA codes and proxy credentials.
2. **Webhook URLs are secrets.** An outgoing catch-hook URL is a write endpoint into the user's
   automation. A Google Apps Script Web app deployed with access **`Anyone`** (§7) is an
   unauthenticated write endpoint into their spreadsheet. A Linked Helper incoming-webhook URL has
   **no documented auth at all** (§4). Do not reproduce any of them in your output, in a plan
   document, or in a support ticket draft.
3. **Describe the UI steps; let the user paste the secret themselves.** The correct answer to "here
   is my HubSpot token, set it up" is the click path plus the scope list (§5), not an
   acknowledgement of the token. If a secret appears in the conversation, do not repeat it back,
   do not put it in a file, and tell the user to rotate it if it was posted somewhere it should not
   have been.
4. **Never send a payload to an endpoint on the user's behalf as a "test" without explicit
   confirmation of the destination.** A test POST writes real data into a real system and can
   create CRM records, trigger a live Zap, or append rows to a production sheet. Confirm the exact
   destination in words first. Where a throwaway target is what they actually want, point them at
   the documented one, **https://webhook.site/**, which the LH docs themselves recommend for
   testing `Send person to webhook` and `Send organization to webhook`.
   Source: https://support.linkedhelper.com/hc/en-us/articles/360016687659-Send-person-to-webhook
5. **Scope requests minimally.** When a CRM integration needs scopes, quote the documented set and
   no more (HubSpot's list in §5 is verbatim, including which are Read-only and which are
   Write-only). Do not suggest broadening scopes to make a mapping easier.
6. **Exported lead data is personal data.** The payloads in §2 and §3 carry names, emails, phone
   numbers, employment history and full message transcripts. Treat any file you generate from them
   as sensitive: keep it where the user put it, do not publish it, and do not paste sample rows
   containing real people into shared output. LH's own compliance framing (public data only, GDPR
   respected, rate-limited requests, legitimate use case) is `[LH-CLAIM]` and **not legal advice**;
   the *hiQ Labs v. LinkedIn* holding it cites addressed the CFAA only, **not LinkedIn's
   contractual ToS**.
   Source: https://www.linkedhelper.com/blog/linkedin-scraper
7. **`[LI-POLICY]`** Automating LinkedIn violates LinkedIn's User Agreement regardless of how the
   data leaves the tool. Exporting to a CRM does not launder that; state it once and move on.
