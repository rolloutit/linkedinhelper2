# Linked Helper 2 — Working Message Library

Ready-to-paste drafts with variables and fallbacks already wired. Adapt them — do not send them
as-is at volume; identical text across many accounts is exactly what gets detected.

**These are drafts written for this skill, not vendor copy.** The verbatim Linked Helper template
library, reproduced unaltered with sources, is in `references/templates.md` §7. Use that when the
user asks what Linked Helper itself publishes.

## How to read the notation

- `{firstName}` etc. — LH2 built-in variables, single curly braces, case-sensitive.
- `{cs_something}` — custom variable from your CSV (`Custom template variables plug-in`).
- `IF / THEN / ELSE` blocks — three separate UI fields in Template Builder → Advanced.
  The `IF` field takes **exactly one variable**, no text and no operators. It tests presence only.
- `{A|B|C}` — spintax; LH2 picks one variant at random.
- Character budgets: invite note — write to **200** (the docs give 200–300; 200 fits both) on a paid
  LinkedIn account, **0** on free beyond the monthly personalized-invite quota (5 or ~10/month,
  `CONFLICT` — assume 5); 1st-connection message **8,000**; InMail subject **200**,
  body **1,900**; group and event messages **8,000**; comments **1,250**.

**Every template below must be previewed against a real profile from the actual queue before launch.**

---

## 1. Invite notes (paid LinkedIn account, write to ≤200 characters)

No links. No pitch. The note buys the connection, nothing else.

### 1a. Company-anchored, with a safe fallback

```
IF   : {company}
THEN : Hi {firstName} — I work with {position}s at companies like {company}, mostly on
       [problem]. Thought it'd be useful to be connected.
ELSE : Hi {firstName} — I spend my time around [audience] working on [problem].
       Happy to connect if that's your world too.
```

### 1b. Mutual-connection anchored (three tiers)

```
IF   : {mutualSecondFullName}
THEN : Hi {firstName} — we share a few connections including {mutualFirstFullName}.
       Always glad to widen the circle in [field]. Happy to connect.
ELSE :
  IF   : {mutualFirstFullName}
  THEN : Hi {firstName} — I see we both know {mutualFirstFullName}. Happy to connect.
  ELSE : Hi {firstName} — your work in [field] crossed my feed. Happy to connect.
```

Numbers cannot be compared, so tier on which mutual-name variable exists, not on `{mutualTotal}`.

### 1c. Content-anchored (use only when you actually engaged with the post)

```
Hi {firstName}, your post on [topic] was the {clearest|most useful|most honest} thing
I read on it this week. {Sending a connection request|Reaching out} so I don't lose the thread.
```

### 1d. No note at all

Costs no personalized-invite quota, and the docs advise sending no note at all when you are not
confident the note will land (shorter notes are reported to accept better; no percentage is
published). On a free LinkedIn account beyond the monthly quota this is the **only** option.
Leave the `Message` tab blank.

---

## 2. First message after acceptance

Send 2–3 days after acceptance, not the same hour. Ask nothing that requires work to answer.

### 2a. Reciprocity-first (RRR: relevance, reward, request)

```
Thanks for connecting, {firstName}.

Since you're working in [field], you may find this useful: [one specific, genuinely useful
resource — no gate, no form].

No ask attached. If [problem] is on your list this quarter I'm happy to share what I've seen
work at other [industry] teams — just say the word.
```

### 2b. Position-anchored

```
IF   : {position}
THEN : Thanks for connecting, {firstName}. Curious — as {position}, is [specific problem]
       something your team owns, or does it sit elsewhere?
ELSE : Thanks for connecting, {firstName}. Curious whether [specific problem] is something
       your team owns?
```

### 2c. Short and honest

```
Appreciate the connect, {firstName}. I'll be straight: I work on [thing] for [audience].
Not pitching today — just glad to be connected, and here if it's ever relevant.
```

---

## 3. Follow-up sequence (three steps)

Put a `Check for replies` action between every pair of messaging steps, or people who answered
still get the next message.

### 3.1 Follow-up 1 — value, +4 to +7 days

```
{One more thing|Following up on this} that might be useful, {firstName}: [second specific
resource or observation, different in kind from the first].

[One sentence on what it's for.]
```

### 3.2 Follow-up 2 — the actual ask, +5 to +7 days

```
{firstName}, I'll make this concrete. We help [audience] with [outcome] — the pattern I see
most at [industry] companies is [specific observation].

Worth 15 minutes to compare notes? If not, no problem at all — I'll leave it here.
```

### 3.3 Follow-up 3 — clean close, +7 to +10 days

```
{firstName}, I'll assume the timing isn't right and stop here — no hard feelings.

If [problem] moves up your list later, my door's open. Good luck with [something specific
you actually know about them].
```

Do not add a fourth. The published cadence guidance ranges from 1–3 follow-ups to 4–6 total
messages (`CONFLICT`, see `references/templates.md` §8.4); three is inside both.

---

## 4. InMail (subject ≤200, body ≤1,900)

Free to Open Profiles — no InMail credit consumed. See `references/recipes.md` for finding them.

```
SUBJECT: {firstName}, quick question about [specific thing at their company]

Hi {firstName},

We've not met — I work with [audience] on [outcome].

[Two sentences of genuine, specific relevance to them or their company. If you cannot write
these two sentences, do not send the InMail.]

If [problem] is live for you, I can share what worked for [comparable company type] in about
15 minutes. If not, ignore this and I won't follow up.

[Name]
```

---

## 5. Group message (≤8,000 characters)

Only reaches profiles that carry that Group ID. Collected group members qualify; CSV/HTML uploads
only do via `Override platform` → `Change platform` → `Collect scope type` = Group ID.
Lead with the shared context.

```
Hi {firstName} — fellow member of [group name].

I noticed you [specific thing: role, post, comment]. I've been working on [topic the group
exists for] and wanted to reach out directly rather than through the group feed.

[One specific, useful thing.]

Happy to swap notes if it's relevant.
```

---

## 6. Event message (≤8,000 characters)

Only reaches profiles that carry that Event ID. Collected attendees qualify; CSV/HTML uploads only do
via `Override platform` → `Change platform` → `Collect scope type` = Event ID.
Reference the event honestly — they can check.

```
Hi {firstName} — we're both signed up for [event name].

{Since we'll both be there|Ahead of it}, I thought I'd reach out: I work on [topic] with
[audience], which is roughly what [session/theme] covers.

[One specific question or useful observation about the event's topic.]

Worth a quick conversation before or after?
```

---

## 7. Re-engagement of dormant 1st connections

```
{firstName}, we connected a while back and I never followed up properly — my fault.

Quick update on my side: [one sentence]. Since then I've been working on [topic] with
[audience].

If [problem] is anywhere on your list, happy to share what I've learned. If not, genuinely
good to be connected either way.
```

---

## 8. Recruiting outreach

```
IF   : {company}
THEN : Hi {firstName} — I'm hiring for a [role] and your work at {company} lines up closely.
ELSE : Hi {firstName} — I'm hiring for a [role] and your background lines up closely.
```

Body:

```
The short version: [team], [what they'd own], [salary range or band], [location / remote policy].

Not a fishing exercise — happy to send the full brief if you want to look, and equally happy
to hear "not now" and leave you alone.
```

State the range — it is the single question every candidate has, and withholding it costs you the
reply. (Advice, not a documented benchmark: the research found no published recruiting-outreach
figures.)

---

## 9. Reply handling

Once someone replies, stop the sequence. `Check for replies` handles that; `Ignore generic
replies` prevents a "Thanks!" from being treated as a real answer, and `Filter by message content`
routes on keywords.

### Positive

```
Great — thanks {firstName}. Does [day] or [day] work better? I'll send an invite with an
agenda so you know exactly what the 15 minutes covers.
```

### "Not now"

```
Understood, {firstName} — thanks for saying so rather than leaving me guessing.
I'll check back in [specific timeframe]. If anything changes before then, just reply here.
```

### "Not me / wrong person"

```
Thanks {firstName} — is there someone on your side who does own [area]? Happy to go through
you or reach out directly, whichever you prefer.
```

### Annoyed

```
Sorry {firstName} — that's on me. Removing you now; you won't hear from me again.
```

Then actually remove them: add them to the "Global Exclude" campaign and apply it via
`Functions` → `List Manager` → `Add unique`.

---

## 10. Pre-send checklist

- [ ] Previewed with a real profile from the queue, not a made-up one.
- [ ] Every variable has an `ELSE` branch or a `cs_*` default — no message can go out with a hole.
- [ ] ≥2 variants or spintax on every step.
- [ ] Character counts inside the limits above.
- [ ] No links in invitation notes.
- [ ] Nothing in the copy claims a shared context that does not exist.
- [ ] `Check for replies` sits between every pair of messaging steps.
