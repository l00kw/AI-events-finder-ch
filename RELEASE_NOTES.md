# Release notes

What changed in the events table, its rules and the scan, and why. Newest first.

Each entry says **what** changed, **why**, and **who it affects** (people browsing events, the reviewer, or people copying the setup).

**How this history was rebuilt.** The repo started on 2 Nov 2026, but the table is two months older. Earlier entries combine:
- the table's own record timestamps (when rows were created, and whether by hand or by the scan);
- the scheduled scan's settings;
- the working chats from September, 27 Oct and 2 Nov.

**The gap:** no working notes survive for late September to October, when the rulebook changed most. Those changes are grouped and marked "date not recorded". Where a reason wasn't written down, the entry says so instead of guessing.

---

## v1.4.1 · 10 Nov 2026 · Online events: time window replaces the Europe-host test

- **What:**
  - An online event no longer needs a Swiss or European host, or a page saying it's for Europe. It needs to **start between 08:00 and 21:00 Zurich time**, be interactive, and not be tied to one vendor's product.
  - The vendor rule is now stricter online: if taking part requires one company's product (for example "download X to hack along"), the event is out, even when it's hands-on.
  - The AI Collective's Luma calendar is now an online source. The scan keeps only its virtual sessions.
  - Maven's free lessons are not a source, because each one promotes a paid course. The owner can add one by hand.
- **Why:** A test run of the rule against real listings showed the host's location was the wrong test. A US-run session at 20:00 Zurich time works fine for people here, while the rule rejected it. What matters is whether someone in Switzerland can join live and take part.
- **Affects:** People browsing may see more online sessions run from outside Europe, all at workable hours. Reviewer: slightly more online rows to check.

---

## v1.4 · 10 Nov 2026 · Online events, on trial

- **What:**
  - **New Format column:** In-person, Online or Hybrid. All 223 existing rows were set to In-person. Format shows in the public view and in "Older events". Online rows say "Online (platform)" in Location.
  - **Online events can now be added, if they pass the online rule:**
    - run by a Swiss or European host, **or** the page explicitly says it's for people in European time zones (for example an "EU edition");
    - interactive: at least live Q&A, discussion or hands-on work, not a broadcast-only livestream;
    - starts between 08:00 and 21:00 Zurich time;
    - not a product sales webinar, and not tied to one vendor's tool.
  - The usual rules still apply: AI is the main theme, run in English, and it has its own registration page. Recordings aren't added by the scan. The table owner adds them by hand.
  - The scan looks for online events in its existing sources and through a few extra searches on full (Monday) runs, capped at about 20 page loads.
  - Online events appear in the main public list alongside in-person ones.
  - Two recent examples were added by hand to try the format: the VCM Demo Night 07 (EU Edition, with European Women in AI) and the University of St.Gallen webinar "AI Agents in Management". Both are past events.
- **Why:** Good learning events happen online too, and some are aimed specifically at Europe. Two recent ones didn't appear because the rulebook excluded anything online. The Europe-host-or-audience rule keeps the list relevant to people in Switzerland without listing every webinar worldwide. It's a trial so online events can be counted against in-person ones before deciding whether they need their own table.
- **Affects:** People browsing will see some Online rows. Filter on Format if you only want in-person events. Reviewer: online rows have their own checks (host, audience wording, start time). People copying the setup need to add the Format field.

---

## v1.3 · 4–5 Nov 2026 · Recurring series checked at the source, and shorter look-ahead windows

- **What:**
  - **Recurring series are checked every run.** The scan lists the series already in the table: the same event name on two or more rows, or a name with a session number or month (for example "#7" or "November AI Meetup"). It ignores series that are all Rejected or that last ran more than 60 days ago. For each series it opens the organiser's own events page once, or else the Luma calendar or the Meetup group feed, and adds upcoming sessions that aren't in the table yet, one row per session. A session's date still has to come from an allowed source. Luma calendars usually list sessions without dates, so they're not enough on their own.
  - **Full runs (Monday):** the series check has no page limit and is never cut for budget, but only adds sessions dated in the next 30 days. Later sessions are picked up as they come into range.
  - **Light runs (Friday):** only add events dated in the next 14 days, for both the main sources and recurring series. The series check stops after about 8 page loads, and the run summary lists any series it didn't reach. Re-checking links on rows already in the table works as before.
  - Full runs still look 90 days ahead for one-off events.
- **Why:**
  - An AI Society Coffee Chat in Zurich on Fri 6 Nov was missing from the table. Its Luma page shows no date and it wasn't listed on hackevents.net or ai-weeks.ch, which is where the earlier sessions had been found. The date was only on the organiser's own page (ai-society.ch/events). Series like this tend to show up once on an aggregator and then drop off.
  - The 30-day and 14-day windows: not recorded.
- **Affects:** People browsing should see more sessions of regular meetups, closer to the date. Reviewers will see fewer far-off series sessions, and fewer new rows from Friday runs.

---

## v1.2 · 5 Nov 2026 · Unreviewed events are public, and labelled as such

- **What:**
  - **The public table shows every event except rejected ones**, with **Status** now visible. It reads *Not verified* (only the scan has checked it) or *Verified* (a person has checked it). This was already how the view was filtered. Status was just hidden, so nobody could tell the difference.
  - **Labels renamed.** Status: To review → **Not verified**, Approved → **Verified**. The field "Link Status" was renamed **Registration**: Confirmed → **Open**, Confirmed - closed → **Closed**. The Registration column is now visible in the public view too.
  - **Events without their own registration page are no longer added.** Before, an event with only a calendar, listing or aggregator page could be added with the "Generic listing page" label. Now the scan skips it and lists it in its run summary so it can be added by hand. An organiser page with a visible register or join button still counts, even if the scan can't open the form.
  - Removed the unused Registration option "Pattern-matched, not verified". No rows used it.
  - Added short descriptions to the **Status** and **Registration** fields explaining each value, so they show when hovering over the column header in Airtable.
  - Added **Eventfrog** as a Source option.
  - **The public view shows "Day & Date" (with the weekday, e.g. "Tue, Nov 10 2026") instead of Date**, and Status moved to the last column. Sorting and filtering still use Date.
  - **Past events marked Verified in bulk.** The 53 unreviewed events dated before 5 Nov (3 Oct – 4 Nov) were set to *Verified* in one batch, to clear them out of the review queue. They were **not** individually reviewed. They're past, so they don't appear in the public view, and the record IDs were kept so the change can be undone.
  - **Scheduled scan instructions** now tell the scan to check which label names exist before writing (old or new), and never to write the retired "Generic listing page" or "Pattern-matched" options. This was a safeguard while the labels were being renamed. The schedule is unchanged: Monday and Friday at 05:00 UTC.
  - **Weekly review reminder** every Monday evening. It lists unverified upcoming events, with date conflicts and link problems first.
- **Why:**
  - Reviewing every row before publishing didn't keep up with the scan. 106 rows were waiting on 5 Nov. Showing them labelled means people hear about events early and can see what's been checked.
  - Rows linking to aggregator pages caused the most mistakes. Of the rows that relied on one, three turned out to be last year's events, and five were labelled "Confirmed" while linking only to an aggregator page.
- **Affects:** Everyone. Treat *Not verified* events as leads and double-check them on the organiser's page. Reviewer: the weekly reminder replaces the ad-hoc review.

---

## v1.1 · 5 Nov 2026 · Clearer about what this is and who it's for

- **What:**
  - Rewrote the README and the landing page. They now explain what the table is, how a row gets in, what each column means and what's planned next.
  - Added a feedback form to the landing page, alongside GitHub issues.
  - Fixed a landing-page bug: the "table will appear here" placeholder showed even after the table loaded.
  - Synced the public rulebook with the version the scan actually runs (see v1.0.1).
- **Why:** People who found the table didn't know what it was or how to read it. The project has also grown past "EWAI's internal list". It's Wendy's project, built for EWAI and open to anyone in Switzerland learning AI.
- **Affects:** Everyone. No change to the table or to how the scan behaves.

---

## v1.0.1 · 2–5 Nov 2026 · More Luma, plus Eventfrog

The exact date wasn't recorded, but the change came after the repo was published.

- **What:**
  - Luma calendars (Zurich, Geneva, Lausanne and the AI discovery pages) are now never skipped, in either run mode or when the run budget is tight.
  - Luma event pages often hide the date. In that case the scan looks for an allowed fallback source, and it lists events it couldn't date instead of silently dropping them.
  - Added Eventfrog AI searches as a source, filtered hard because "AI" also matches unrelated listings.
- **Why:** Not recorded. The new rule says Luma is never skipped "whatever the budget", which suggests Luma events were being missed when runs hit their limit.
- **Affects:** People browsing should see more small events. Reviewers will see more rows to check.

---

## v1.0 · 2 Nov 2026 · Open-sourced the setup

- **What:**
  - Created this public repo (MIT): the landing page on GitHub Pages, the scan rulebook (`skill/ewai-event-scan/SKILL.md`), these notes, a contributing guide and issue templates.
  - Turned the scan's instructions into a reusable skill. The scheduled task now just runs the skill, so the rules live in one place that can be published and versioned.
  - Kept the scan's behaviour unchanged on purpose.
- **Why:** So people can see how events are chosen, report mistakes, and copy the setup for another country.
- **Affects:** Everyone, and especially people copying the setup. The public rulebook uses placeholders instead of the real Airtable IDs.

---

## v0.4 · 27 Oct 2026 · Reviewed what the scan misses (no change yet)

- **What:** Compared the scan's results with a by-hand search for small, discussion-style events in Zurich. The scan had already found good ones (HerImpact, a Coffee Meetup), but it missed a German-language discussion at Paulus Akademie and the Aipéro.
- **Found:**
  - The English-only rule causes the biggest misses.
  - The sources lean towards tech-community calendars and miss civic and academic ones, such as kinewsletter.ch, Paulus Akademie and UZH's Digital Society Initiative.
  - "Connect" is too broad to single out small, conversation-first events.
- **Decided:** The table is meant to be public. A capacity limit for "Connect" events is wanted. Changes to the scan were held back to be discussed first.
- **Affects:** Nobody yet. These feed into the "Planned" section below.

---

## v0.3 · Late Sep – Oct 2026 · Rules reshaped: some loosened, some tightened

Individual dates weren't recorded. This entry compares the first scan prompt (mid-September) with the rulebook published on 2 Nov.

**Loosened.** This is why the table now holds technical events.
- **Hackathons:** went from excluded to allowed. Why says whether non-developers are welcome.
- **Technical background:** "no technical background assumed" was a requirement and was dropped. Technical events are allowed and tagged by audience in **For**, so people can filter.
- **Big or expensive conferences:** events over ~300 people or CHF 400 were excluded. Now they're allowed but can't be tagged Connect.
- **Vendor events:** vendor showcases were excluded. Now hands-on vendor events (labs, workshops, masterclasses) are welcome, with the company named. Pure sales pitches and booth expos stay out.
- **Format:** "must let people talk to each other" became the Connect/Learn split, so talk-first events can be listed and labelled honestly.
- Why each rule was loosened wasn't recorded. For vendor events, the reason given was that they offer practical workshops members should get exposure to.

**Tightened.**
- Investor and pitch events are out: pitch nights, investor summits, VC nights and founder–investor matchmaking. They're investor-community discussions, not practical AI knowledge.
- AI must be the main theme. One AI panel inside a broader conference doesn't count.

**Verification.**
- Dates and venues come from the event's own page, never a listing summary.
- The year and weekday are checked.
- Registration links must be opened and must show this exact event.
- Unknown facts are written as "TBC" or flagged for the reviewer, never guessed.

**Fields.**
- Added **Domain** (what the event is about). Many September rows don't have one yet.
- Added **Table Creator Action Required**. It collects every doubt in one internal column, so the public Why and Notes stay clean.
- Added **Last checked**. The scan re-checks events coming up within 14 days.
- **Link Status** settled on Confirmed / Confirmed - closed. "Unverified", used in the first scan prompt, is no longer written. Whether it was renamed or retired wasn't recorded.
- **For** was re-cut from a mix of audiences and industries into roles. See "Retired options".

**Sources.**
- Added Meetup group calendar feeds and techface.ch.
- Sources were split into three tiers by how often they're checked.
- Sites that block automated reading are listed as dead ends, and the scan doesn't work around blocks.
- Dropped PWN, PWG and luma.com/basel. Luma Basel turned out to be an unrelated calendar; reasons for the others weren't recorded.

**Schedule.** The scan moved from the planned weekly Monday run to Monday (full run) and Friday (light run: main sources plus a link check).

**Affects:** Everyone. Expect more technical and larger events than in September, labelled so you can filter them out.

---

## v0.2 · ~17 Sep – 2 Oct 2026 · The scan is designed and starts adding events

- **First scan prompt (~17–18 Sep):**
  - Sources: ai-weeks.ch, Women in Tech Switzerland, Swiss Fintech Ladies, PWN, PWG, Greater Zurich Area, startupticker, dev.events, Luma (including Basel), Meetup, Eventbrite and web searches. hackevents.net, Deep Tech Nation, WiDS, TechFace and a deep-tech search were added soon after.
  - Excluded: hackathons, conferences over ~300 people or CHF 400, trade shows and vendor showcases, job fairs and student-only events. Events had to assume no technical background.
  - Approx Size used three bands from the start: Small (<40), Medium (40–150) and Large (150+).
  - Link Status: Confirmed / Unverified.
  - Rule added: take the venue from the event's own page, not the listing. **Why:** listing pages gave wrong venues, for example for a legal hackathon and an HSLU Rotkreuz event.
- **Scheduled task created on 21 Sep.** It was first planned as a weekly Monday run. New rows arrive as *To review*, review happens in Airtable through **Status** (To review / Approved / Rejected), and only approved rows are shown publicly. **Added by** (Agent / Manual) and **Added on** show where each row came from.
- **First rows from the scan:** 12 on 30 Sep and 30 on 2 Oct, according to the table's record timestamps.
- **Why:** Finding events by hand every month didn't scale. Keeping review as a human step means nothing is published unchecked.
- **Affects:** Reviewer.

---

## v0.1 · 3–21 Sep 2026 · The table is created

- **What:**
  - The table's timestamps show 14 rows created by hand on 3 Sep and 65 more on 21 Sep, imported from a hand-curated CSV covering September to December.
  - The working notes mention 25 rows at the time the scan was designed and a final CSV of 58 rows. Why these counts differ from the timestamps (duplicates, deletions or later edits) wasn't recorded.
- **First rules (exact dates not recorded):**
  - English only (bilingual counts).
  - Switzerland only, even if an event abroad is livestreamed.
  - In person only, for members to connect with one another. Online events and hackathons were excluded.
  - Hackathons were later brought back (see v0.3).
- **Fields:**
  - Added **Type** (Connect / Learn) and **For** (originally a mix of audiences and industries).
  - Tried and then dropped: Circle, Format, Time, Time Status and Link Verified.
  - Created **Link Status** with three options: "Pattern-matched, not verified", "Generic listing page — no direct event URL found" and "CONFIRMED live". **Why:** registration links built from ai-weeks.ch's URL pattern kept failing, so each link needed a label saying how far it had been checked.
- **Why:** To give EWAI members one place to find AI events where they can connect with each other and that suit professionals without a technical background.
- **Affects:** Everyone.

---

## Retired options

These select options were replaced. The scan is told never to write them again. Some older rows still carry them. The table owner added the reasons on 5 Nov.

| Field | Retired option | Replaced by | Why |
|---|---|---|---|
| For | Engineers & Researchers | Developers · Researchers (inferred) | Some labeled events were only for Researchers or Developers, not both. Separate to make clearer target audience (i.e. "For" column) for events. |
| For | Healthcare, Cybersecurity | Healthcare professionals · Security professionals (inferred) | Populates "For" column for Healthcare and Cybersecurity events. |
| For | Finance, Legal, Robotics | Domain field (inferred) | Event audience is everyone, these three (Finance, Legal, Robotics) explain domain, not audience |
| Domain | Security | Cybersecurity (inferred) | Same reason as the row above. |
| Approx Size | Small-Medium, Large (600) | Small · Medium · Large | Not recorded. The three bands date from the first scan prompt, so these two were one-off values added to the table later. |
| Registration (was Link Status) | Pattern-matched, not verified · Generic listing page — no direct event URL found | Nothing: events without their own registration page are no longer added | See v1.2. |
| Link Status | From official programme, Unverified | Not recorded | Easier to understand, "Review state. New events from the weekly scan arrive as To review." |

"Inferred" means the replacement exists in the table today, but the change itself wasn't written down.

---

## Known issues

- **Review backlog.** As of 5 Nov, 53 upcoming events haven't been reviewed by a person. They're public and labelled *Not verified*. The weekly reminder is there to bring this down.
- **"Verified" on past events isn't always a real review.** The 53 past events bulk-marked on 5 Nov (see v1.2) weren't checked one by one.
- **The scan's doubts aren't public.** Its notes on each row (for example "date differs between sources") are in an internal column. *Not verified* rows can look more certain than they are.

---

## Planned

Agreed in principle and not live yet.

- **Virtual events, selected.** Rule to settle first: is a vendor-hosted programme acceptable when the skills carry over to other tools? Do recordings count as events?
- **German-language events,** and broader civic and academic sources.
- **A public "Check before you go" note** for *Not verified* rows, showing the scan's main doubt in plain words.
- **A capacity limit** to pick out small, conversation-first events within Connect.
- **A feedback form** that writes straight to the table instead of email.

---

## Template

```
## vX.Y · YYYY-MM-DD · Short title

- **What:**
- **Why:**
- **Affects:**
```
