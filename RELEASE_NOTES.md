# Release notes

What changed in the events table, its rules and the scan, and why. Newest first.

Each entry says **what** changed, **why**, and **who it affects** (people browsing events, the reviewer, or people copying the setup).

**How this history was rebuilt.** The repo started on 2 Nov 2026, but the table is two months older. Earlier entries come from three places: the dates rows were added to the table and who added them, the scan's schedule history, and the project's working notes. Where a date or reason wasn't recorded, the entry says so instead of guessing.

---

## v1.1 · 5 Nov 2026 · Clearer about what this is and who it's for

- **What:**
  - Rewrote the README and the landing page. They now explain what the table is, how a row gets in, what each column means and what's planned next.
  - Added a feedback form to the landing page, alongside GitHub issues.
  - Fixed a landing-page bug: the "table will appear here" placeholder showed even after the table loaded.
- **Why:** People who found the table didn't know what it was or how to read it. The project has also grown past "EWAI's internal list". It's Wendy's project, built for EWAI and open to anyone in Switzerland learning AI.
- **Affects:** Everyone. No change to the table or the scan.

---

## v1.0 · 2 Nov 2026 · Open-sourced the setup

- **What:**
  - Created this public repo (MIT): the landing page on GitHub Pages, the scan rulebook (`skill/ewai-event-scan/SKILL.md`), these notes, a contributing guide and issue templates.
  - Turned the scan's instructions into a reusable skill. The scheduled task now just says "run the skill", so the rules live in one place that can be published and versioned.
  - Kept the scan's behaviour unchanged on purpose.
- **Why:** So people can see how events are chosen, report mistakes, and copy the setup for another country.
- **Affects:** Everyone, and especially people copying the setup. The public rulebook uses placeholders instead of the real Airtable IDs.

---

## v0.4 · 27 Oct 2026 · Reviewed what the scan misses (no change yet)

- **What:** Compared the scan's results with a by-hand search for small, discussion-style events in Zurich. The scan had already found some good ones (HerImpact, a Coffee Meetup) but missed two of the best: a German-language discussion at Paulus Akademie and the Aipéro.
- **Found:**
  - The English-only rule causes the biggest misses.
  - The sources lean towards tech-community calendars and miss civic and academic ones, such as kinewsletter.ch, Paulus Akademie and UZH's Digital Society Initiative.
  - "Connect" is too broad to single out small, conversation-first events.
- **Decided:** The table is meant to be public. A capacity limit for "Connect" events is wanted. Changes to the scan were held back to be discussed first.
- **Affects:** Nobody yet. These feed into the roadmap below.

---

## v0.3 · Oct 2026 · Rules and tags tightened

Between the first scan and 2 Nov, the rulebook was refined into the version published in this repo. Individual changes weren't dated, so they're grouped here.

- **Exclusions made explicit:**
  - Investor and pitch events are out: pitch nights, investor summits, VC nights and founder–investor matchmaking. They're investor-community discussions, not practical AI knowledge.
  - AI must be the main theme. One AI panel inside a broader conference doesn't count.
  - Vendor-run events with hands-on content (labs, workshops, masterclasses) stay in, with the company named in Why.
- **Verification rules:**
  - Dates and venues come from the event's own page, never a listing summary.
  - The year and weekday are checked.
  - The registration link must be opened and must show this exact event.
  - Unknown facts are written as "TBC" or flagged for the reviewer, never guessed.
- **New and changed fields:**
  - **Domain** (what the event is about) was added. Many September rows don't have one yet.
  - **Link Status** and **Last checked** track whether the registration link still works. The scan re-checks events coming up within 14 days.
  - **Table Creator Action Required** collects every doubt in one internal column, so the public Why and Notes stay clean.
  - **Approx Size** settled on three bands: Small (<40), Medium (40–150) and Large (150+).
  - **For** (who it's for) was re-cut into roles. Details are under "Retired options" below.
- **Sources:**
  - Added Meetup group calendar feeds and techface.ch.
  - Sources were split into tiers by how often they're checked.
  - Sites that block automated reading are listed as dead ends, and the scan doesn't work around blocks.
- **Run modes:** Monday is a full run. Friday is a light run: main sources plus a link check.
- **Affects:** Reviewer and people copying the setup. Older rows may still carry retired values.

---

## v0.2 · 21 Sep – 2 Oct 2026 · The scan starts adding events

- **What:**
  - Set up a scheduled scan on 21 Sep. It runs Monday and Friday mornings and writes new events into the table as *To review*, rather than publishing them directly.
  - Review happens in Airtable through the **Status** field (To review / Approved / Rejected). **Added by** (Agent / Manual) and **Added on** show where each row came from.
  - Only approved rows are shown publicly.
  - The first rows from the scan arrived on 30 Sep (12 events), followed by 30 more on 2 Oct.
- **Why:** Finding events by hand every month didn't scale. Keeping review as a human step in Airtable means nothing reaches members unchecked.
- **Affects:** Reviewer.

---

## v0.1 · 3–21 Sep 2026 · The table is created

- **What:**
  - Started the Airtable table on 3 Sep with 14 events added by hand.
  - On 21 Sep, imported a further 65 hand-curated events covering September to December.
  - Each event is tagged **Connect** (people talk to each other, no technical background assumed) or **Learn** (content first: talks, conferences, workshops, hackathons). A size estimate shows whether real conversation is realistic.
- **Why:** To give EWAI members one place to find AI events that suit professionals without a technical background, with enough detail to judge whether an event is worth an evening.
- **Affects:** Everyone.

---

## Retired options

These select options were replaced. The scan is told never to write them again. Some older rows still carry them.

| Field | Retired option | Replaced by | Why |
|---|---|---|---|
| For | Engineers & Researchers | Developers · Researchers (inferred) | Not recorded. Likely to separate people who write code from academic audiences. |
| For | Healthcare | Healthcare professionals (inferred) | Not recorded. Likely to name a role rather than an industry. |
| For | Cybersecurity | Security professionals (inferred) | Not recorded. Same likely reason. |
| For | Finance, Legal, Robotics | Domain field (inferred) | Not recorded. These describe topics, which now go in Domain. |
| Domain | Security | Cybersecurity (inferred) | Not recorded. |
| Approx Size | Small-Medium, Large (600) | Small · Medium · Large | Not recorded. Three bands are easier to filter. |
| Link Status | From official programme | Not recorded | Not recorded. |

"Inferred" means the replacement exists in the table today, but the reason for the change wasn't written down.

---

## Known issues

- **Review backlog.** As of 5 Nov, 106 of the scan's 134 rows are still *To review*, and they aren't public until someone checks them. This is the main reason for the planned "Not verified" status and weekly reminder.
- **Rulebook and table disagree on one Link Status option.** The rulebook uses "Generic listing page — no direct event URL found". The table has "Pattern-matched, not verified" instead. One of the two needs renaming so the scan doesn't create a stray option.

---

## Planned

Agreed in principle and not live yet.

- **Virtual events, selected.** Rule to settle first: is a vendor-hosted programme acceptable when the skills carry over to other tools? Do recordings count as events?
- **German-language events,** and broader civic and academic sources.
- **Status "To review" → "Not verified",** so it's visible when nobody has checked a row. This also needs the rulebook and scheduled task updated.
- **A weekly review reminder** that lists new unverified rows with links.
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
