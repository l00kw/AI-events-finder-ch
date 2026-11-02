# AI-events-finder-ch

**EWAI AI Events – Switzerland**

A hand-checked list of in-person, English-language AI events in Switzerland, curated for [EWAI](#), a peer community for professional women navigating AI without a technical background.

- **Browse events:** the landing page (`index.html`, served with GitHub Pages) embeds the public table.
- **How it works:** an AI assistant (Claude) scans event calendars on a schedule, following the rulebook in [`skill/ewai-event-scan/SKILL.md`](skill/ewai-event-scan/SKILL.md). It adds candidates to an Airtable table as *To review*. A person approves or rejects every row before members see it.
- **What changed and why:** [`RELEASE_NOTES.md`](RELEASE_NOTES.md).

## Repository contents

| Path | What it is |
|---|---|
| `index.html` | The landing page for members (GitHub Pages) |
| `skill/ewai-event-scan/SKILL.md` | The rulebook: sources, inclusion criteria, tagging, verification and write rules |
| `RELEASE_NOTES.md` | Changes to the table, the rules and the scan, with the reason for each |
| `CONTRIBUTING.md` | How to suggest events, sources or rule changes |
| `LICENSE` | MIT |

## Copy this for your country

1. **Table.** Create an Airtable base with the fields in §1 of `SKILL.md`. Make a public view filtered to `Status = Approved`, and hide the internal fields (Table Creator Action Required, Status, Added by). In the share settings, turn off "allow viewers to copy data / download CSV".
2. **Config.** In `SKILL.md`, replace `<BASE_ID>`, `<TABLE_ID>` and the field IDs with your own (Airtable shows them in the API docs for your base).
3. **Rules.** Change the country, cities, sources, language rule and audience to fit your community.
4. **Run.** Connect Airtable to Claude and create a scheduled task that uses the contents of `SKILL.md` as its prompt (or add it as a skill and have the task run the skill).
5. **Review.** Approve or reject rows yourself. The assistant never approves anything.

Never commit API tokens. The base and table IDs are not secret on their own, but this repo uses placeholders so copies don't point at EWAI's table by mistake.

## Setting up GitHub Pages

Settings → Pages → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)`.
