# Message Writing and Personalization — Linked Helper 2

Detail layer for SKILL.md §6: variable syntax, conditional logic, character budgets, copy frameworks, verbatim templates, reply branching, AI generation, image attachment.

## Table of contents

1. [Built-in variables](#1-built-in-variables)
2. [Custom variables](#2-custom-variables)
3. [IF-THEN-ELSE](#3-if-then-else)
4. [Spintax and Variations](#4-spintax-and-variations)
5. [Character limits](#5-character-limits)
6. [Copy frameworks](#6-copy-frameworks)
7. [Verbatim template library](#7-verbatim-template-library)
8. [Reply handling and branching](#8-reply-handling-and-branching)
9. [AI-assisted personalization](#9-ai-assisted-personalization)
10. [Images and attachments](#10-images-and-attachments)
11. [Pre-send checklist](#11-pre-send-checklist)

---

## 1. Built-in variables

Single curly braces, case-sensitive, no spaces inside the braces. Exactly **11** documented tokens; anything else you have seen in a blog post or forum thread is `[UNVERIFIED]` — confirm in the UI before shipping copy that depends on it.

| Token | Resolves to | Empty when | Failure mode if unhandled |
|---|---|---|---|
| `{lhid}` | profile identifier in the internal Linked Helper CRM | never, once the profile is in a list | not for copy — use for CRM/webhook joins |
| `{firstName}` | first name **normalized by Linked Helper** | full name sits in one field, the profile is a company/entity, or a script LH2 cannot split | greeting collapses to `Hi ,` — the most visible tell of automation |
| `{lastName}` | last name normalized by Linked Helper | as `{firstName}`; also single-word display names | dangling space, truncated salutation |
| `{company}` | current company the profile works for | employer hidden, between jobs, freelancer with no company object, or field never scraped | `I saw you work at  ...` — hole mid-sentence |
| `{position}` | current company position | headline present but no structured current-role entry | `As a  at Acme` |
| `{industry}` | industry the profile works in | **frequently blank on regular LinkedIn** — industry data is largely Sales-Navigator-only, which is why the docs teach a Tagging workaround for industry segmentation | clause loses its subject; never build a core sentence on it in a regular-LinkedIn campaign |
| `{mutualFirstFullName}` | full name of a mutual connection | zero mutuals | `I noticed we both know ` |
| `{mutualSecondFullName}` | full name of **another** mutual connection | fewer than 2 mutuals | plural claim with a missing name |
| `{mutualTotal}` | total number of mutual connections | no mutuals; may render `0` | `we have 0 mutual connections` reads as broken |
| `{memberId}` | LinkedIn profile member ID | rarely | never in copy — dedup/CRM key only |
| `{publicId}` | LinkedIn profile public ID | obfuscated `/in/ACoAAA...` URLs | never in copy |

**The core failure mode.** LH2 does **not** refuse to send a message with an unresolved variable and does **not** substitute a default. The token resolves to an empty string and the message goes out with a hole in it. Every variable in a sentence whose grammar depends on it must be wrapped in an IF-THEN-ELSE with a generic ELSE (§3), or moved out of the load-bearing sentence.

- Only `{firstName}` is near-safe bare, and only on a hand-checked queue; otherwise nest a nameless ELSE (`Hi there,`).
- `{company}`, `{position}`, `{industry}` and every `mutual*` token are **conditional-only**.
- `{lhid}`, `{memberId}`, `{publicId}` are plumbing, not copy.
- Personalization is only as good as extraction. Extractable fields: name, profile URL, headline, current role, company, employment history, education, skills, languages, certifications, connection degree, connection count, mutual connections (count + names), profile image, Open Link status, Premium/Influencer/Hiring/Open-to-Work badges, visible emails, occasional phone numbers, company description/industry.

Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates
Source: https://www.linkedhelper.com/blog/linkedin-scraper

The blog never publishes an exhaustive built-in variable list; beyond `{company}` and the `cs_` convention, specific token names are `[UNVERIFIED]` at blog level. The 11 above come from the help center, which is the authoritative surface.
Source: https://www.linkedhelper.com/blog/if-then-else-operator-explained-how-to-create-super-custom-messages-in-linked-helper
Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template

---

## 2. Custom variables

**Plug-in requirement.** Requires the **`Custom template variables plug-in`** from `Plug-in store`. Without it the `Custom fields` button and `{cs_*}` resolution do not exist — a template containing `{cs_anything}` sends literal text or an empty string. Check this first when a user reports "my custom variable isn't working".

**Naming.** Form `{cs_<name>}`. Documented examples: `{cs_my_tracking_url}`, `{cs_translated_firstname}`, `{cs_gender_name}`, `{cs_event}`, `{cs_year}`, `{cs_where}`, `{cs_info_and_tech}`; blog adds `{cs_industry}`, `{cs_message}`, `{cs_opener}`, `{cs_avatar}`.

**CSV contract.**
- Verbatim: **"The name of the column with the custom field has to start with `cs_`"**.
- Minimum **two columns**: **`profile_url`** plus at least one `cs_*` column. Verbatim: *"you do not need to keep other columns except `profile_url`"*.
- The column header **is** the variable name — header `cs_opener` → `{cs_opener}`.
- CSV↔Excel round-trips need **UTF-8 encoding + semicolon delimiter**.

**Relaxed-prefix note.** The `Custom variables` internals article says the prefix requirement has been relaxed — *"Now, it's not required and you can choose any name for a column"* — but the plug-in page still documents `cs_`. `CONFLICT`, low stakes. **Keep `cs_` anyway:** both articles accept it, it prevents collisions with the 11 reserved built-in names, and it makes a template auditable at a glance.

**Upload path.** Campaign → `Queue` list → **`Custom fields` button** → select and upload the file.

**Scope limitation.** Verbatim: custom variables *"will work only with profiles whose URLs were uploaded with the file."* A profile collected by LinkedIn search and absent from the CSV has **no** value for any `cs_*` token. In a mixed queue (some CSV, some search) a `{cs_*}` without an ELSE silently blanks for part of the list.

**Three-level priority.**

```
Action level  >  Campaign level  >  CRM level
```

- **CRM level** — applies across all campaigns, but only to profiles in the uploaded file.
- **Campaign level** — *"the Campaign level has a higher priority than CRM level"*; applies to all actions of one campaign.
- **Action level** — *"action level has a higher priority than campaign and CRM levels"*; *"not available in any other action apart from the one it was uploaded to."*

**Worked example.** One profile, `linkedin.com/in/janedoe`, three uploads of the same column `cs_opener`:

| Where uploaded | Value |
|---|---|
| CRM level (global upload) | `your post on retention metrics` |
| Campaign "Q3 SaaS founders" | `your talk at SaaStr` |
| Action `Message to 1st connections` step 2 in that campaign | `the churn teardown you published` |

- In step 2's message → **`the churn teardown you published`** (action level wins).
- In step 4 of the same campaign, no action-level upload → **`your talk at SaaStr`** (campaign level wins; the action-level value is invisible outside its own action).
- In a *different* campaign for the same profile → **`your post on retention metrics`** (only CRM level is in scope).

Consequence: to change one message without touching the sequence, upload at action level. To fix a value everywhere, fix the CRM file **and** delete/replace the campaign- and action-level files shadowing it — editing the CRM file alone changes nothing where a higher level exists.

Source: https://support.linkedhelper.com/hc/en-us/articles/9035773558034-Custom-template-variables-plug-in
Source: https://support.linkedhelper.com/hc/en-us/articles/360015589860-Custom-variables
Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template
Source: https://www.linkedhelper.com/blog/linkedin-sales-navigator-export-leads-to-excel

---

## 3. IF-THEN-ELSE

**Plug-in names.** **"Conditional IF-THEN-ELSE operator for Message template editor"**, also called the **`IF-THEN-ELSE operator for Message template editor plug-in`** — same plug-in, two names across the docs. Listed as a compatible extension of `Message to 1st connections`, `Message to event attendees`, `Message to group members` and the invite actions.

**Three UI fields, not inline markup.** Configured in **Template Builder → Advanced UI** as three separate input lines. The docs **never publish an inline `{IF ...}` string** — do not promise the user markup they can paste into a body.

```
IF   :  {company}            <- ONE variable only, no text/operators
THEN :  I saw you work at {company} ...
ELSE :  Hi {firstName}, ...
```

**Hard constraint, verbatim:** *"One operator - one variable in the IF string. No text, symbols or mathematical operations (for example, `{mutualTotal}` = 10, `{company}` != Microsoft, or `{cs_age}` > 30 — expressions are not supported)."* No comparisons, no arithmetic, no string matching, no AND/OR, no literal text in the IF field. One token, nothing else.

**Presence-only semantics.** Verbatim: *"Linked Helper checks if the lead has the first variable with a value. If both the variable and the value exist, then the variant under the first THEN is sent."* The blog adds that detection is loose: *"any character in the column counts as a value"*. Design around it:
- A cell holding a space, `-`, `N/A`, `0` or `unknown` counts as **present** and fires THEN. Clean the CSV — blank means blank.
- `{mutualTotal}` can render `0` and still be "present", producing *"we have 0 mutual connections"*. Tier it (§3a) rather than testing it alone.
- You cannot branch on a threshold. For tiers, upload a pre-computed `cs_*` flag column.

**Nesting.** Single, multiple and nested clauses are supported. Chain by placing further IF-THEN-ELSE blocks **inside ELSE branches** — verbatim: *"we had the main IF condition, and we added two other message variations to the ELSE conditions."* Standard pattern: one branch per segment, plus a generic ELSE at the bottom so no-data profiles still get a sendable message.

Source: https://support.linkedhelper.com/hc/en-us/articles/9035926428306-IF-THEN-ELSE-operator-for-Message-template-editor-plug-in
Source: https://www.linkedhelper.com/blog/if-then-else-operator-explained-how-to-create-super-custom-messages-in-linked-helper

### 3a. Worked design — mutual-connection tiers

Documented pattern is 2+ mutuals / exactly 1 / none. Since the operator cannot compare numbers, drive tiers off **which name tokens exist**: `{mutualSecondFullName}` exists only at 2+ mutuals, `{mutualFirstFullName}` only at 1+.

```
IF   : {mutualSecondFullName}
THEN : Hi {firstName}, I noticed that we have {mutualTotal} mutual connections,
       including {mutualFirstFullName} and {mutualSecondFullName}. Curious what
       you are working on this quarter?
ELSE :
  IF   : {mutualFirstFullName}
  THEN : Hi {firstName}, it seems we both know {mutualFirstFullName}. I would like
         to connect and hear how you approach [topic].
  ELSE : Hi {firstName}, I have been following work in [field] and would like to
         connect.
```

Documented equivalent: mutuals ≥2 → *"I noticed that we have {mutualTotal} mutual connections…"*; exactly 1 → *"It seems we both know {mutualFirstFullName}…"*; none → generic greeting. The deepest ELSE still uses `{firstName}` bare — on an unvetted queue, nest one more level (`IF {firstName}` → THEN named, ELSE `Hi there,`).

### 3b. Worked design — company present/absent

```
IF   : {company}
THEN : Hi {firstName}, I saw you are at {company} — we work with teams solving
       [problem] at that stage. How are you handling it today?
ELSE : Hi {firstName}, I came across your profile while looking at people working
       on [problem]. How are you handling it today?
```

Rule: the ELSE must be a **complete, sendable message**, not the THEN with a gap. Rewrite the sentence, do not just delete the token. Same treatment for `{position}` and especially `{industry}`.

### 3c. Worked design — gender via `cs_gender_name`

Gender tailoring uses a custom field, not a built-in: upload a `cs_gender_name` column holding a salutation word ("Madame"/"Monsieur") and branch on presence.

```
IF   : {cs_gender_name}
THEN : {cs_gender_name} {lastName}, bonjour. [formal body]
ELSE : Bonjour {firstName}, [neutral body]
```

Presence-only testing means one column splits **two** ways. For three buckets (male/female/unknown) upload **two** columns, each populated for its own segment only, and nest:

```
IF   : {cs_madame}
THEN : Madame {lastName}, ...
ELSE :
  IF   : {cs_monsieur}
  THEN : Monsieur {lastName}, ...
  ELSE : Bonjour {firstName}, ...
```

Source: https://support.linkedhelper.com/hc/en-us/articles/360016381079-How-to-tailor-your-message-by-gender-of-the-recipient

**General recipe:** segment by the data you actually have → one IF per segment, most-specific first, nested down the ELSE chain → bottom ELSE needs **zero** variables beyond a safe greeting → preview every branch against a real profile that lands in it.

---

## 4. Spintax and Variations

Two different mechanisms; they solve different problems and combine.

**Spintax** — documented as *"Phrases enclosed in brackets with pipe separators generate random variants"*, i.e. a bracket-plus-pipe construct inside the message body: `{option A|option B|option C}`. Scope: **within one body**, at phrase level. One template, many surface renderings.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates

**Variations** — **entirely separate alternative messages, distributed equally across recipients.** Scope: **whole message**. You author N complete messages; LH2 rotates them so each gets roughly 1/N of the queue.

| | Spintax | Variations |
|---|---|---|
| Unit | a phrase inside one template | a complete alternative message |
| Distribution | random per send | **equal** across recipients (documented) |
| Use for | breaking up repeated wording, greetings, sign-offs | genuinely different angles, structures, CTAs |

**Combining both** — the recommended default, because identical text at volume is a detectable pattern and a spintax-only template still has one skeleton. Author 2–3 Variations differing in structure and CTA, then put spintax inside each for interchangeable phrases:

```
Variation 1:
{Hi|Hello|Hey} {firstName}, {thanks for connecting|glad we are connected}.
{What are you working on right now?|What is on your plate this quarter?}

Variation 2:
{firstName} — {good to connect|appreciate the connect}. I mostly work on
[topic]; {curious what your take is|would like to hear how you see it}.
```

Keep every variant inside the same character budget (§5), and wire the same IF-THEN-ELSE fallbacks into each — a fallback in Variation 1 does not protect Variation 2.

**What is NOT documented:**
- **Nested spintax** (a spin group inside another) — `[UNVERIFIED]`, no doc confirms it parses. Flatten instead.
- **Weighted spintax** — `[UNVERIFIED]`, no doc mentions weights; distribution inside a group is described only as "random". For a 70/30 split use Variations, not spintax.
- **Escaping a literal `{`, `|` or `}`** in copy — `[UNVERIFIED]`. Avoid literal braces and pipes.
- Whether spintax is evaluated **inside** an IF-THEN-ELSE branch — `[UNVERIFIED]`. Test on a two-profile campaign first.
- **Exact spintax grammar** (whitespace handling, nesting depth, escapes) is among the behaviours the docs never specify. `[UNVERIFIED]`.
- The blog lists spintax as a supported feature (automatic phrase variation) but **publishes no syntax at all** — the bracket+pipe form is help-center-only. `[UNVERIFIED]` at blog level. Source: https://www.linkedhelper.com/blog/linkedin-message-automation
- There is **no documented A/B report** telling you which Variation won. Tag or segment manually for attribution.

---

## 5. Character limits

### 5.1 LinkedIn field limits — full table

All from https://www.linkedhelper.com/blog/linkedin-character-limit unless a second source is named. Presented by LH as LinkedIn's field limits `[LI-POLICY as stated]`; none carry a LinkedIn citation, so every row is `[UNVERIFIED]` at source level.

| Field | Limit (chars) | Notes |
|---|---|---|
| **Connection request note** | **300** | Free accounts limited to **5 notes/month** with invitations; Premium unlimited. LH advises "under 300", ideally **120–240** |
| **Direct message (1st degree)** | **8,000** | free and unlimited to 1st-degree. One post says "up to 2,000 characters" for a welcome message — LH **style advice, not the field cap** |
| **InMail subject line** | **200** | same figure in `linkedin-inmail-vs-message` and `linkedin-recruiter-inmail` |
| **InMail body** | **1,900** | LH: InMails **under 400 chars perform 22% better** |
| Post / update | **3,000** | only ~**200 visible** before "See more" |
| Comment | **1,250** | |
| Article headline | **100** | |
| Article body | **110,000** | |
| Recommendation | **3,000** | |
| Headline | **220** | |
| About / summary | **2,600** | |
| Experience — job title | **100** | |
| Experience — description | **2,000** | |
| Skill (each) | **80** | |
| Publication title | **250** | |
| Publication description | **2,000** | |
| Text Ad headline | **25** | |
| Text Ad description | **75** | |
| Message Ad subject | **60** | |
| Message Ad body | **1,000** | |
| Dynamic Ad headline | **100** | |
| Dynamic Ad description | **150** | |
| Sponsored Content intro text | **150** recommended (max 3,000) | |
| Sponsored Content headline | **70** recommended (max 200) | |
| Sponsored Content description | **100** recommended (max 300) | |

Source: https://www.linkedhelper.com/blog/linkedin-character-limit
Source: https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit
Source: https://www.linkedhelper.com/blog/linkedin-prospecting-messages
Source: https://www.linkedhelper.com/blog/linkedin-inmail-vs-message
Source: https://www.linkedhelper.com/blog/linkedin-recruiter-inmail
Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template

**Not covered anywhere in the blog — do not invent:** group post, event invitation message, page-follow invite, first/last name fields, hashtag length, attachment limits. `[UNVERIFIED] / absent`.

### 5.2 LH2 action-specific limits

```
Invite (free LinkedIn account)      0 characters (no note allowed beyond the 10/mo quota)
Invite (paid LinkedIn account)      200-300 characters
Message to 1st connections          8,000-10,000 characters
InMail subject                      200 characters
InMail body                         1,900 characters
Group messages                      8,000 characters
Event attendees messages            8,000 characters
Comments                            1,250 characters
```

Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates

Per-action notes: `Message to group members` publishes **no** character limit in its own article; `InMail to 2nd & 3rd contacts` has a **mandatory subject line**.
Source: https://support.linkedhelper.com/hc/en-us/articles/5714464724754-Message-to-group-members
Source: https://support.linkedhelper.com/hc/en-us/articles/360016601420-InMail-to-2nd-3rd-contacts

### 5.3 Conflicts

**CONFLICT — InMail body.** **1,900** per the help center message-templates article and the blog character-limit table, vs **"up to 2000"** per the InMail template article as noted in the help center digest. **Use 1,900** (repeated and conservative). Practically irrelevant: target **under 400** anyway.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates
Source: https://www.linkedhelper.com/blog/linkedin-character-limit

**CONFLICT — invitation note length.** **300** per the blog table vs **200–300** (paid LinkedIn) per the help center. **Write to 200** — fits both and lands inside the 120–240 band.
Source: https://www.linkedhelper.com/blog/linkedin-character-limit
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates

**CONFLICT — message to 1st connections.** **8,000** (blog) vs **8,000–10,000** (help center). Irrelevant in practice; nothing you send should approach either.
Source: https://www.linkedhelper.com/blog/linkedin-character-limit
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates

**CONFLICT — free-account personalized invites.** **~10 personalized (with-note) invitations per month** vs **5 notes/month**. **Assume 5.** On a free account plan note-less invites and personalize the first message after acceptance.
Source: https://support.linkedhelper.com/hc/en-us/articles/360016435499-Working-Hours-and-Limits
Source: https://www.linkedhelper.com/blog/linkedin-weekly-invitation-limit

---

## 6. Copy frameworks

### 6.1 RRR — Relevance, Reward, Request

Developed by **Winning by Design**; reportedly improved outreach campaign success by **3x**. `[LH-CLAIM]`

- **Relevance** — personally targeted: recipient's name and company; shared connections; quote their LinkedIn summary; show knowledge of their business focus; connect shared interests. Verbatim examples: *"I saw that we share Brian Moe as a common connection"* · *"I saw that you focus on helping salespeople to attain their goals through high-impact coaching."*
- **Reward** — the benefit of connecting: how you have helped similar clients; the specific pain you solve; quantified value; how little effort is needed from them for a large return.
- **Request** — **one** clear CTA: ask for a referral, propose a discovery call, or pose an opening question.

Economics cited: a scheduled appointment with the right prospect costs B2B SaaS companies over **€300**; a 10-person sales team spends **~7,200 hours annually** setting up meetings — roughly **€540K** in yearly operating cost. The technique aims to cut per-appointment cost to **€45 or less**. `[LH-CLAIM]`

Mapped onto LH2 mechanics: Relevance = the IF-THEN-ELSE branch (§3); Reward = one sentence, no feature list; Request = a question, which is also what keeps the note inside 200 chars.

Source: https://support.linkedhelper.com/hc/en-us/articles/360015583559-How-to-make-your-LinkedIn-messages-3x-times-more-effective-using-the-RRR-technique

### 6.2 CCQ

**C**ommonality (shared connection, school, skill, group) → **C**ompliment (specific, personalised) → **Q**uestion (actionable, prompts a reply). Related three-beat opener: reference their work/content → express specific interest → ask a question or propose connecting.
Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template

### 6.3 Never sell on the first message

Core rule: avoid selling on first contact; build the relationship gradually. Four documented opening tactics: (1) **"Start the message off with a simple hello and an introduction"**; (2) ask questions relevant to their industry or their posts; (3) invite them to join a community (group, page); (4) **provide value first** (e.g. a free audit).

Why: a first-touch pitch **"lacks personalization"**, people resist **"hard sell"** tactics, and **"they don't know you"** yet. Two frameworks named: **Active Lead Generation** (direct outreach, 11 stages) and **Passive-Active** (profile optimization → content engagement → strategic outreach).

`[UNVERIFIED]` — this article gives **no** day-gap numbers and **no** complete templates. Use §6.4.
Source: https://support.linkedhelper.com/hc/en-us/articles/360018839719-Never-Sell-On-Your-First-LinkedIn-Message-The-Real-LinkedIn-Sales-Process

### 6.4 The documented numbers

**Invitations** — no sales offer in the connection request (it reduces acceptance); skip the note entirely if unsure it will resonate; **no links in invitations**, LinkedIn may flag them as spam.

**Messages to 1st connections** — use **custom variables** beyond the standard `{firstname}`; use **"IF|THEN|ELSE clauses"** to reference mutual connections or industry alignment; start with a casual follow-up (**"Thank you for accepting"**) before presenting an offer; **wait 2-3 days** between connection and the first message.

**Structure** — **"Break your huge message into 2 or 3 messages with the 3 - 7 days intervals between them."** Split messages containing multiple links or media into individual messages. Include images, infographics or videos to improve engagement. **Upload videos to LinkedIn rather than linking YouTube content.**

**Sequencing** — send messages **one-by-one** (not in bulk bursts) to appear human-like; insert **`Check for replies`** between message steps; the article's own example is a **14-step** sequence (profile auto-following → 2-3 day delays → sequential messaging → reply checking).

Core takeaway, verbatim: **"Do not be too intrusive; Avoid pushing people; Create structured and human-like messages."**
Source: https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2

**Length effects** — ideal connection-note range **120–240 characters**, shorter notes show higher acceptance (no % given); InMails **under 400 characters perform 22% better** `[UNVERIFIED]`.
Source: https://www.linkedhelper.com/blog/linkedin-prospecting-messages
Source: https://www.linkedhelper.com/blog/linkedin-inmail-vs-message

**Rates worth quoting**
- Personalised vs generic invite acceptance **~45% vs ~15%** `[LH-CLAIM]`; invite **with** a personalised note → reply **9.36%**, **without** → **5.44%** (cited to the Expandi H1 2025 report). Source: https://www.linkedhelper.com/blog/linkedin-message-automation
- Personalised vs generic InMail **166% higher** reply `[UNVERIFIED]`. Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template
- Regular DM reply once connected **18–25%** `[UNVERIFIED]`; InMail response rate **10–25%** — `CONFLICT` with **18–25%** stated elsewhere, both `[UNVERIFIED]`. Source: https://www.linkedhelper.com/blog/linkedin-inmail-vs-message · https://www.linkedhelper.com/blog/linkedin-recruiter-inmail
- Value-first; no pitch in message #1; CTA is a question, not a demo ask. Source: https://www.linkedhelper.com/blog/linkedin-prospecting-messages

---

## 7. Verbatim template library

Reproduced exactly as published. **Placeholder styles are inconsistent across LH posts** (`{First Name}`, `[First Name]`, `(Name)`, `{{post name}}`) — these are **not** LH2 variable syntax. Normalise every placeholder to the real tokens from §1/§2 before pasting into the template builder, or the literal text will be sent.

### 7.1 Invite notes and cold opens

**Competitor's commenters** — ~120 chars — invite note to people who commented on a competitor's post.
```
Hi {First Name}, I've just read your comment on {Competitor's Post}. Your
perspective on {Topic} really stood out to me! Have you ever considered
{YourQuestion}? I'd love to get connected and talk the topic further.
```

**Mutual connection** — ~200 chars — invite note where mutuals exist (pair with the §3a branch).
```
Hello {First Name}, I noticed we're both connected with {Mutual Connection}.
Their work in {Industry/Field} is impressive, much like your contributions.
I'm curious to learn more about your experience with {Relevant Topic} and
share insights from my end.
```

**Content-creator engagement** — ~120 chars — invite note after engaging with their post.
```
Hi {First Name}, your recent post on {Topic} was exceptional. It resonated
with our approach at {Your Company}. Let's connect and discuss this further.
```

**Industry peer** — ~180 chars — peer-to-peer invite note.
```
Hello {First Name}, your work on (call out specifically what you liked) at
{Company} caught my eye. I've been exploring {Industry Trend} and would love
to exchange ideas and perspectives with you. Mind connecting?
```

**Expert / SERP flattery** — ~220 chars — invite note to a visible industry expert.
```
Dear {FirstName}, I searched for experts in the {Industry} and found you at
the top of the SERPs. I'm working on (explain why you're reaching out), and I
see that you have impressive work experience. I would be glad to get in touch.
```

**Mutual-acquaintance bridge** — ~180 chars — invite note leaning on a shared network.
```
Hi {First Name}. I've recently contacted/explored/etc. the work of {mentions
of mutual acquaintances}. So, I thought you'd also be interested in getting
connected and talking the {Topic} over.
```

**Shared-struggle / genuine compliment** — ~160 chars — invite note or first message built on a real pain point.
```
Hi {FirstName} — I came across your post in {Topic}, which I struggled with
in the past. How do you manage to overcome {painPoint}? Curious to know and
exchange tips!
```

**Hyper-personalised cold open** — ~120 chars — shortest invite note; CCQ compressed.
```
Hi {firstName}, Been meaning to talk to you since I read your {{post name/
comment}}. Curious how do you do {your topic/services}?
```

### 7.2 Trigger-based messages

**Job-change congratulations** — ~200 chars — re-engagement / trigger message on a role change.
```
Congrats on your new role, [First Name]! [Job Title] sounds like a fantastic
step forward. I'm intrigued to learn about your new responsibilities and see
how we can collaborate in the future (offer a few opportunities) — you name it.
```

**Company-news reaction** — ~240 chars — trigger message on funding, launch or acquisition news.
```
Hi {First Name}, I just read about {Company's Recent News/Development} and
thought of connecting with you. How do you see this impacting your role and
the industry overall? I'd love to hear your insights and share a few thoughts
of my own.
```

**Profile-visitor reply** — ~200 chars — inbound-triggered message to people who viewed your profile.
```
Hey {First Name}, I noticed you've visited my LinkedIn profile. Is there
anything specific you were curious about? I'd be happy to share more about my
work at {Your Company} or discuss any potential collaborations.
```

**Post-engagement follow-up** — ~200 chars — first follow-up to likers/commenters of your own content.
```
Hi {First Name}, thanks for engaging with my article/post on {Topic}. I
noticed your interest in {Specific Point} and would love to delve deeper into
this with you. Perhaps there are synergies between our work?
```

**Former client, feedback request** — ~180 chars — re-engagement of dormant 1st-degree connections.
```
Hi {First Name}, as a valued former client, your feedback on our
{Product/Service} would be of the greatest help. Could we schedule a brief
call to discuss your experience and any improvements you'd suggest?
```

### 7.3 Event and webinar

**Event / webinar invite** — ~280 chars — event or webinar promotion; also the shape for `Message to event attendees`.
```
Hi {First Name}, We are colleagues in {Industry}, so I know how vital these
secret tips will be for {Indicate unique, useful information that will solve
a person's pain}. On the webinar, we'll share 10 techniques for attracting
followers who are ready to buy from you. Hope to see you online. Will
appreciate your feedback! {Date. Time. Link to registration.}
```

Source for every template in §7.1–§7.3: https://www.linkedhelper.com/blog/linkedin-prospecting-messages

### 7.4 Group message

**Group-message opener (SaaS sequence)** — `Message to group members`, second touch after an invite in the group-members drip.
```
Hello. Thank you for accepting the invite. Earlier, I wrote to you about a
product we made...
```
Source: https://www.linkedhelper.com/blog/linkedin-drip-campaign

### 7.5 Reply-handling replies

For inbound recruiter/offer messages — copy for the reply side of the funnel, not outbound.
```
Thanks for the suggestion...I would like to know more details about this role.
Can we schedule a call?
```
```
I'm currently working full-time and am not ready to change my job...We can
discuss the possibilities at least in [timeframe].
```
Source: https://www.linkedhelper.com/blog/how-to-respond-to-linkedin-messages-the-most-effective-and-automated-ways

### 7.6 Templates that do NOT exist — do not reconstruct them

The "20 connection messages" post is unusable as copy: **all 20 templates are truncated on the page** (each cuts off mid-sentence with "..."), and the article states **no** character limit and **no** acceptance-rate benchmark. Keep its use cases as a **trigger taxonomy**: common ground · new-contact classic · show interest · offer help · hyper-personalisation · follow-up · gather recommendations · request recommendations · post likers · event promo · webinar promo · post-event follow-up · lead magnet/trial · share resources · group co-member · search results · ask for advice · schedule a call · direct sales · numbers-driven.
Source: https://www.linkedhelper.com/blog/best-20-linkedin-connection-messages-for-sales-top-automation-tool

Also absent from the docs, so never presented as verbatim LH copy: a full InMail template, a recruiting outreach template, a complete re-engagement sequence. Build those from §6 and label them as your own construction. `[UNVERIFIED] / absent`.

---

## 8. Reply handling and branching

### 8.1 `Check for replies`

Monitors for replies to messages sent by **any** campaign action. Non-responders move to the next workflow action; responders route to the `Replied` list. Default check interval **3 hours**; minimum timeout **1 hour**; first run scrapes the "Last **200** messaging chats"; searches up to **40 profiles per queue check**. `Message analyzer` tab offers *"If no replies are found, move the contacts to Successful list"* with a delay in days/hours or **`never`**.

Copy consequence: **every message after the first must read as if the recipient said nothing** — that is exactly who receives it. Without a `Check for replies` step between two messages, LH2 only tests for a reply when it processes the profile through the next messaging action, so people who answered still get the follow-up. Never write "as I mentioned, did you see my last note?" into a step with no reply gate above it.

Gotchas that shape copy: opening threads **marks unread messages as read** (mitigate with `Settings → Actions → Leave responses unread when checking for replies`), and `Check for replies` **automatically disables the "Other" section** of the LinkedIn Messaging inbox.

`Advanced settings for Check for replies plug-in` adds, for non-1st-degree contacts messaged via InMail/group/event: `Treat events 'Message Request Accepted' as replies:` Yes/No and `Keep in queue permanently if request is not accepted:` Yes/No. With the first set to Yes, an acceptance with no text counts as engagement — so the next message must not assume a reply exists to answer.
Source: https://support.linkedhelper.com/hc/en-us/articles/360017905660-Check-for-replies

### 8.2 `Filter by message content`

Blocks a message if specified phrases or regex patterns are found in the previous conversation. Lives in the `Advanced settings` tab of `Message to 1st connections`, `Message to event attendees`, `Message to group members`. Settings: `Reject if any of previous messages sent by` — `You (1)` / `Contact (2)` / `Any of you (3)`; `Contains` filter field; match modes `At least one phrase [OR]` / `All phrases [AND]` / `Regular expression` (JavaScript ES6); `Add phrase` button.

Copy consequences:
- Give each sequence a **stable, unique phrase** in message #1 so you can later exclude everyone who already received it — this is how you avoid re-pitching a profile across campaigns.
- `All phrases [AND]` *"only triggers when all phrases exist within a single message, not across multiple messages in conversation"* — a two-phrase AND filter needs both phrases in one body.
- `Reject if a contact replied after #` and `Reject if you or LH messaged a contact after connection date` **take priority over** this filter.

Also usable for content-based segmentation of inbound: *"if 45 leads mention 'Salesforce', create targeted follow-ups explaining competitive advantages specific to that CRM."*
Source: https://support.linkedhelper.com/hc/en-us/articles/8982577824018-Filter-by-message-content-plug-in
Source: https://www.linkedhelper.com/blog/how-to-respond-to-linkedin-messages-the-most-effective-and-automated-ways

### 8.3 `Ignore generic replies`

Keeps a profile in the sequence despite a reply, when the reply matches a configured generic phrase like "Thanks for connecting." Lives in the `Advanced settings` tab of `Message to 1st connections`, `Message to event attendees`, `Check for replies`, `Message to group members`. Matching is **case-insensitive**; **RegExp is not supported**; before matching LH2 strips "symbols mentioned in the settings; emojis; all non-printing characters".

Copy consequences:
- Message #1 should not *invite* a one-word acknowledgement, or you burn a reply slot on "Thanks!". Ask a question that cannot be answered with a pleasantry.
- Populate the phrase list with the noise you actually get ("thanks for connecting", "thank you", "you too", "likewise") so those profiles stay in the drip.
- *"a profile can send several messages in response, and every message is counted as a separate phrase"*, and *"if a profile sends several messages, and at least one doesn't match with the phrases in the settings, the profile will be moved into replied list."*

Source: https://support.linkedhelper.com/hc/en-us/articles/16795759959186-Ignore-generic-replies-plug-in

### 8.4 Cadence rules from the blog

- *"Send 1–3 follow-ups with day-level delays. We recommend following up **no more than three times**."* Source: https://www.linkedhelper.com/blog/how-to-automate-linkedin-outreach
- **CONFLICT:** **4–6 messages spaced over 5–10 days** for optimal conversion — incompatible with "max three follow-ups". Both `[LH-CLAIM]`; prefer the conservative 1–3. Source: https://www.linkedhelper.com/blog/linkedin-message-automation
- Pause **5–7 days** before the intro/welcome message and again **5–7 days** before the follow-up if no reply. Source: https://www.linkedhelper.com/blog/linkedin-cold-message-template
- **CONFLICT** with the help center, which says **wait 2-3 days** between connection and the first message. Source: https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2
- Send during business hours — *"messages sent during business hours are more likely to be opened."* Only contacts inside a specific campaign queue receive auto-replies; correspondence history is retained for segmentation. Source: https://www.linkedhelper.com/blog/how-to-respond-to-linkedin-messages-the-most-effective-and-automated-ways
- Sequence skeleton to hang copy on: message #1 welcome/thank-you with **no pitch** at **day +2–3** after acceptance, message #2 first follow-up at **day +7–10**, message #3 final. Source: https://www.linkedhelper.com/blog/linkedin-automated-marketing-funnel-sales-funnel-automation-guide

---

## 9. AI-assisted personalization

### 9.1 The `AI personalized messages` action

Generates a bespoke connection request and follow-up messages per profile from that profile's data instead of one generic template.

- **Availability:** *"only as a part of Invite and follow-up template"* — it **cannot be added to an existing campaign**. Create the campaign from that template or you do not get the action.
- **Settings (verbatim):** `General goal of the reach out` · `Target language` · `Tone of voice` · `Goal per message` · `Auto-approve` · `Profile data used by AI` (an `Edit` button → data selection, pre-built templates or a custom list; fields can be marked **required**) · `Data freshness`.
- **Enrichment source:** `Data Enrichment` (instant, incomplete coverage) · `Visit and Extract` (slower, subject to daily limits, scrapes everything) · "No enrichment option" · `Data Enrichment` **with `Visit and Extract` as fallback**.
- **Approval flow:** with `Auto-approve` **off**, *"messages will be sent as drafts in **AI Drafts tab of the Campaign Inbox**, where you need to review them"* — edit individually or bulk-approve. The workflow **halts** pending review.
- **Numbers:** maximum follow-ups **with** an AI invitation **6**; **without** an AI invitation **7**; overall AI messaging action limit **7**. Profiles per campaign *"Limited only by AI credit balance"*.
- **Constraints:** **LinkedIn Premium, Recruiter, or Sales Navigator is required for AI personalized invitations.** Requires sufficient AI credits. A missing **required** data field moves the profile to the **`Failed` list** — and `Failed` is terminal, so it drops out of the sequence entirely.
- **Gotchas:** cannot change the follow-up count after creation; cannot regenerate a message once approved (manual editing allowed); goal/messaging changes apply **only to new profiles**, not to already-generated messages.

Source: https://support.linkedhelper.com/hc/en-us/articles/35934524524818-AI-personalized-messages

Related: `AI ICP detection action` scores leads against a free-text `Describe your ICP` with a `Minimum ICP match` threshold; below-threshold profiles land in **`Failed` with an error message** — rejection is a Failed entry, not a Skipped one.
Source: https://support.linkedhelper.com/hc/en-us/articles/36036881332882-AI-ICP-detection-action

### 9.2 AI credit honesty

Credits are deducted *"for every processed profile"* when using the **AI personalized message action** (including message regeneration), the **AI ICP Detection action**, and **AI comments in Like and comment post and articles** — also message template generation, Inbox reply generation, and grammar/editing functions.

**`[UNVERIFIED]` — per-operation AI credit rates are not published.** The only published figure is *"one credit for every processed profile"*. Do not quote a cost per generated message, per follow-up, per regeneration, or per ICP scoring. If the user needs a budget, say it is not documented and have them measure it on a 10-profile campaign against their credit balance.
Source: https://support.linkedhelper.com/hc/en-us/articles/35911233008914-Linked-Helper-AI-credits

### 9.3 ChatGPT-in-the-loop personalization

The documented manual alternative, which costs no AI credits.

```
1. Run "Visit and Extract Profiles" → export CSV
2. Feed Summary / Skills / Experience columns into ChatGPT
3. Collect generated openers
4. Paste into a new  cs_message  column in the same spreadsheet
5. Re-upload CSV to Linked Helper
6. Deploy via IF-THEN-ELSE with a generic ELSE fallback
```

Prompts, verbatim:
```
Create an engaging LinkedIn invitation message for users (of no more than 250
characters) using the summary: user #1 {copied summary excerpt from Excel
file} user #2 {copied summary excerpt from Excel file}.
```
```
Suggest a short message to a graphic designer on LinkedIn asking to connect
with them
```

Operating rules: **batch 10–20 messages per prompt** (exceeding the text limit produces errors); always build a **generic fallback** for profiles with no summary; prompt wording is brittle — *"summary" vs "bio" produces inconsistent outputs* and single word changes alter results substantially; **state the character limit explicitly** and specify tone (friendly / formal / funny) for consistency; ChatGPT 3.5 cannot reliably read Google Sheets links or LinkedIn profile URLs — paste the text.

Note the first prompt says "no more than 250 characters" while the invite-note target is **120–240** and the safe cap **200** (§5). Restate your own number in the prompt.
Source: https://www.linkedhelper.com/blog/how-to-use-chatgpt-for-linkedin-message-mail-personalization

---

## 10. Images and attachments

**Plug-in:** **`Attach personalized images`** — options include custom-field images and **Hyperise** personalized images.
Source: https://support.linkedhelper.com/hc/en-us/articles/9037034540818-Attach-personalized-images
Source: https://support.linkedhelper.com/hc/en-us/articles/360021618840-How-to-attach-images-to-LinkedIn-messages

Third-party personalized-image providers documented: **Uclic** (https://support.linkedhelper.com/hc/en-us/articles/4404354998034) and **Hyperize/Hyperise** (https://support.linkedhelper.com/hc/en-us/articles/4403979125394).

**The two limits that decide whether images are worth it.** **Messages with an attached image count against the `Message to 1st connections` limit** — they are not a free extra channel — and are **capped at 20 per 24 h on a Standard licence** (unlimited on PRO per the licensing article). So on Standard, image personalization caps the whole day at 20 image messages against a plain-text messaging budget of ~150/24 h. Use images on a high-value segment, plain text at volume.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates

Action-specific gotcha: for `Message to event attendees`, images can only be sent *"in a follow-up after initial message request was accepted"*.
Source: https://support.linkedhelper.com/hc/en-us/articles/4413984987026-Message-to-event-attendees

**Hyperise setup, as documented** — 10 steps: pick LH campaign template → define audience with LinkedIn filters → choose Hyperise for the message template → create Hyperise account (14-day trial) → design creative → get the personalised template link → set up custom variables in LH **including profile photos** → download and re-upload the CSV with recipient data → **map Hyperise variables to CSV columns** (e.g. `cs-avatar` holding the profile-photo URL) → launch. Supported dynamic elements: recipient name, company name, job title, profile photo, business logo, website screenshot, location; also personalised QR codes and AR markers; personalised websites and video too.

**No uplift benchmarks are given** for this integration. The post cites only generic stats (71% of customers expect personalisation; personalising brands see 40% more profit) — **do not attribute those to image personalisation.** `[UNVERIFIED]`
Source: https://www.linkedhelper.com/blog/hyperise-personalization-linkedin

**Other media.** **No voice or video message action is documented in the help center** — `[UNVERIFIED] / absent`, do not offer it.
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates
Include images, infographics or videos to improve engagement, and **upload videos to LinkedIn rather than linking YouTube content**; split messages containing multiple links or media into individual messages.
Source: https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2

---

## 11. Pre-send checklist

Run all twelve before starting the campaign. Each maps to a documented failure.

1. **Preview with a real profile from the actual queue** — not a hand-typed example. Preview one profile per IF-THEN-ELSE branch, including the bottom ELSE.
2. **Every variable has a fallback.** List each token in the body and name the branch that catches an empty value. `{company}`, `{position}`, `{industry}` and all `mutual*` tokens are conditional-only (§1). No fallback ⇒ the message ships with a hole.
3. **Confirm the `Custom template variables plug-in` and the IF-THEN-ELSE plug-in are installed** before trusting a preview — an uninstalled plug-in is the usual cause of "my variable did nothing".
4. **Confirm `cs_*` coverage matches the queue.** Custom variables resolve only for profiles whose URLs came in the uploaded file (§2). Mixed-source queues need a generic ELSE.
5. **Check which priority level your `cs_*` value comes from** (Action > Campaign > CRM) if you edited a file and nothing changed.
6. **Count characters, per branch and per variation.** Invite note: write to **200** (band 120–240; caps conflict at 200–300 / 300). InMail body: under **400**, hard cap 1,900. Variables expand — a long company name can push a 195-char note over.
7. **At least 2 Variations, plus spintax inside each** (§4). Identical text at volume is a detectable pattern. Wire the same fallbacks into every variation.
8. **No links in invitation notes** — LinkedIn may flag them as spam.
9. **No pitch in message #1.** First touch is hello + introduction, or a question, or value. Anything sellable goes in message #2 or later.
10. **`Check for replies` sits between every pair of messages**, and the follow-up copy reads correctly for someone who never answered.
11. **Placeholders normalised.** Search the template for `[`, `(`, `{{`, `{First Name}` and any other blog-style placeholder — those send as literal text.
12. **On a free LinkedIn account, plan note-less invites** (5–10 notes/month, `CONFLICT`; assume 5) and personalize the post-acceptance message instead. On a Standard licence with images, remember the **20/24 h** cap.

Source: https://support.linkedhelper.com/hc/en-us/articles/4404124631698-Tips-for-messages-sent-via-Linked-Helper-2
Source: https://support.linkedhelper.com/hc/en-us/articles/360015590120-How-to-create-message-templates
Source: https://support.linkedhelper.com/hc/en-us/articles/9035773558034-Custom-template-variables-plug-in
Source: https://www.linkedhelper.com/blog/linkedin-prospecting-messages
