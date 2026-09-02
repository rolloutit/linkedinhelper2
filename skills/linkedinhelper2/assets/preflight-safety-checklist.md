# Linked Helper 2: Pre-flight Safety Checklist

Run this before starting any campaign, and again whenever volume increases.
Numbers are the documented defaults and recommendations; sources and every `CONFLICT` are in
`references/limits-safety.md`. Where two official figures disagree, this checklist uses the
conservative one.

Automating LinkedIn violates LinkedIn's User Agreement. Restrictions and permanent closures happen.
This checklist reduces risk; it does not remove it.

## A. Account and identity

- [ ] LinkedIn account age known. Under 12 months or dormant ⇒ use the ramp in section D, not
      the established-account numbers.
- [ ] Profile is complete (photo, headline, About, experience): a bare profile plus outbound
      volume is the strongest restriction signal.
- [ ] No other automation tool touching this account.
- [ ] Chrome audited for LinkedIn automation extensions: LinkedIn detects them even when unused.
- [ ] The account will not be run from two machines at once.
- [ ] No manual LinkedIn browsing (desktop or mobile) while a campaign is running.

## B. Network and proxy

Only if the setup needs one (VPS abroad, multi-country, or operating someone else's account).

- [ ] Type: IPv4 HTTP/HTTPS or SOCKS5. ISP, residential or mobile. Dedicated, not shared.
- [ ] Fraud score **≤75**; no bot / VPN / crawler flags.
- [ ] Real egress IP verified in a browser: the provider's dashboard may show a gateway, not the exit.
- [ ] Proxy country matches the LinkedIn account's country; time zone matched.
- [ ] `Proxies` menu validation run; anything marked **Bad** replaced before starting.
- [ ] Credentials entered by the account owner directly into the app. Never shared in chat, never
      stored in a plan document, never handled by an assistant.

## C. Limits: `Settings` → `Limits`

- [ ] `Max actions per 24 hours` = **150** (app default), or lower for a young account.
- [ ] Decided which volume standard you are holding to, because the vendor publishes two:
      the app defaults (50 invites/day, 150 messages/day) **or** its own Safety Kit guidance
      (**25–30 invites/day**, **~150/week**, **50–60 messages/day**, **max 6 invites/hour**).
      `CONFLICT`: one restriction-trigger article calls more than 25 invites/day a trigger.
      For anything client-facing or on an account you cannot afford to lose, use the Safety Kit numbers.
- [ ] Advanced per-activity limits set explicitly, not left implicit:
      invites **50**, endorsements **60**, messaging / follow / extract **150**,
      `Boost post` **100**, `Load LinkedIn profile via URL` **40**, search **100 pages/day**
      (`CONFLICT`: the help center says 200, and 100 is the app default and the conservative figure).
- [ ] `Max actions per 24 hours` is at or above the sum of the per-activity limits you actually
      want. (The docs contradict themselves on which wins: satisfy both readings.)
- [ ] Smart Daily Limit Adjustment on, **−10%** (it sends 90–100% of your limit and never exceeds it).
- [ ] Standard licence: aware that 8 activity types are capped at **20 / 24 h** regardless of
      these settings (event/group/org invites, event/group messages, image messages, post liking,
      mention in comment). See `references/limits-safety.md`.

## D. Ramp: new or dormant account only

- [ ] Days 1–14: feed scrolling, follows, ~**5 invites/day** from recommendations only.
- [ ] Then **10–15 invites/day**.
- [ ] Increase by **+5–10 every 10 days**.
- [ ] ~**35/day** by month 1, ~**50/day** by month 2. Do not skip steps to catch up.
- [ ] Pacing set to `SAFE` (not `FAST`) while ramping.

## E. Pacing: `Settings` → `Working Hours` and action `Delay settings`

- [ ] Working hours set to plausible local business hours, not 24/7.
- [ ] `Start time randomization` raised above the minimum.
- [ ] `Bunch size` and `Timeout between bunches` used to spread volume across the day
      (defaults 10 / 1 min are a burst pattern at scale: raise the timeout).
- [ ] Text input method = `Random` (default).
- [ ] Understood that the 24-hour counter is **rolling**, not a midnight reset: spending the whole
      allowance in one hour idles the account for ~24 h and is the most bot-like pattern available.

## F. Campaign structure

- [ ] Warm-up before inviting: Follow → Like/comment → `Delay between actions` → Invite.
- [ ] 2nd/3rd-degree actions placed before 1st-connection actions.
- [ ] `Check for replies` between every pair of messaging steps.
- [ ] `Failed` handling understood: `Failed` is terminal for that profile.
- [ ] Exclusions applied before launch, including a "Global Exclude" list
      (`Functions` → `List Manager` → `Add unique`): LH2 has **no** native global blacklist.
- [ ] Already-invited profiles not re-collected; withdrawn invites not re-sent
      (LinkedIn blocks re-invites for up to 3 weeks).

## G. Copy

- [ ] ≥2 variants or spintax per step: identical text at volume is detectable.
- [ ] Every variable has a fallback (IF-THEN-ELSE presence branch, or a `cs_*` default).
- [ ] Previewed against a real profile from the actual queue.
- [ ] Inside the character limits (invite note 200–300 on a paid account; 0 on free beyond the
      monthly personalized-invite quota).
- [ ] No links in the invitation note. No pitch in the connection request.

## H. Ongoing hygiene: recheck weekly

- [ ] Pending invites kept in the low hundreds (**200–500**); stale ones withdrawn every 2–4 weeks
      via `Sent invites canceller` (auto at 30 days).
      LH's own docs give four incompatible pending-invite ceilings: manage by hygiene, not by ceiling.
- [ ] No LinkedIn security prompts, email-verification-on-every-invite, or "unusual activity"
      warnings. Any of these ⇒ **stop all campaigns immediately** and read the restriction ladder
      in `references/limits-safety.md`.
- [ ] Acceptance and reply rates tracked: a collapsing acceptance rate is an early warning.
- [ ] Backups current (`references/plans-and-platform.md` §Data management).

## I. Stop conditions: halt everything if any of these appear

- Email verification demanded on every invitation.
- "Your account has been restricted" on login.
- A prompt to verify that you performed certain actions.
- Invites failing with 429 or 400 in a cluster.
- Repeated logouts or a login loop.

Do not "wait and see" and do not restart campaigns to test. Stop, then follow the recovery
playbook in `references/limits-safety.md`.
