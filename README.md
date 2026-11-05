# AI Events Finder – Switzerland

**A curated, AI-assisted list of AI events in Switzerland, kept in an Airtable table. The scan finds and checks events, and I verify them every week.**

I built it for [European Women in AI (EWAI)](https://europeanwomeninai.com) and it's open to anyone in Switzerland who is learning AI and wants to find events worth their time. The focus is events where no technical background is assumed and where you get to talk with people, not just listen.

- **See the events and how the table works:** <https://l00kw.github.io/AI-events-finder-ch/>
- **What changed and why:** [`RELEASE_NOTES.md`](RELEASE_NOTES.md)
- **Spotted a mistake or know an event we missed?** Use the form on the landing page, or [open an issue](https://github.com/l00kw/AI-events-finder-ch/issues/new/choose).

Maintained by [Wendy Look](https://www.linkedin.com/in/wendylook/).

## How it works

1. **Scan.** Twice a week, an AI assistant (Claude, run as a scheduled task) checks Swiss event calendars and Meetup groups. It follows a written rulebook: [`skill/ewai-event-scan/SKILL.md`](skill/ewai-event-scan/SKILL.md).
2. **Verify.** For each candidate, it opens the organiser's own page and records the date, venue, price and registration link. When a fact isn't published, it writes "TBC" instead of guessing, and it re-checks links on events coming up soon.
3. **Publish.** New rows go public straight away, labelled *Not verified*, so people hear about events early. Rejected rows are hidden.
4. **Review.** Every Monday a reminder lists the unverified rows, date and link problems first. I mark each one *Verified* or *Rejected*. The assistant never verifies anything.

What gets in today: in-person events in Switzerland where AI is the main theme, run in English, with a page where you can register for that specific event (events listed only on calendars or aggregator sites are left out). Pitch nights, investor events, job fairs and trade shows are left out. The full criteria are in §6 of the rulebook.

## What's next

These are planned and not yet live. See the release notes for status.

- **Selected virtual events.** Learning opportunities that are skills-focused and not built around selling one product.
- **German-language events.**
- **A feedback form** that writes straight to the table.

## Repository contents

| Path | What it is |
|---|---|
| `index.html` | The landing page (GitHub Pages) |
| `skill/ewai-event-scan/SKILL.md` | The rulebook: sources, criteria, tagging, verification and write rules |
| `RELEASE_NOTES.md` | Changes to the table, the rules and the scan, with the reason for each |
| `CONTRIBUTING.md` | How to suggest events, sources or rule changes |
| `.github/ISSUE_TEMPLATE/` | Templates for reporting a mistake or suggesting an event |
| `.release-notes/airtable-setup.md` | Snapshot of the table's fields and views, used by the weekly release-notes check |
| `LICENSE` | MIT |

## Copy this for your country

1. **Table.** Create an Airtable base with the fields in §1 of `SKILL.md`. Make a public view that either shows only `Status = Verified`, or (like this one) shows everything except `Rejected` with Status visible. Hide the internal fields (Table Creator Action Required, Added by). In the share settings, turn off "allow viewers to copy data / download CSV".
2. **Config.** In `SKILL.md`, replace `<BASE_ID>`, `<TABLE_ID>` and the field IDs with your own (Airtable shows them in the API docs for your base).
3. **Rules.** Change the country, cities, sources, language rule and audience to fit your community.
4. **Run.** Connect Airtable to Claude and create a scheduled task that runs the skill (or uses `SKILL.md` as its prompt).
5. **Review.** Approve or reject rows yourself. Plan the time for it: the scan finds more than you'd expect.

Never commit API tokens. The base and table IDs aren't secret on their own, but this repo uses placeholders so copies don't point at this table by mistake.

## Setting up GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)`.
