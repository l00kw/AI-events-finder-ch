# Scheduled scan snapshot

Used by the weekly release-notes check to spot changes to the scheduled scan. Generated, don't edit by hand. Airtable IDs are replaced with placeholders.

Taken: 2026-11-05

- **Name:** EWAI event scan (Mon & Fri)
- **Schedule:** `0 5 * * 1,5` (UTC): Monday and Friday at 05:00 UTC, which is 06:00 in Zurich in winter and 07:00 in summer
- **Enabled:** yes
- **Model:** claude-opus-5-5
- **Notifications:** push, email

## Prompt

```
Use the ewai-event-scan skill and run it exactly as written. It is the single source of truth for the run mode, sources, verification rules, what may be written to Airtable, and when to notify.

Airtable IDs for this run: use base `<BASE_ID>` wherever the skill says `<BASE_ID>`, and table `<TABLE_ID>` wherever it says `<TABLE_ID>`. The field IDs in the skill are correct as written.

Label names are being renamed (Nov 2026), and the skill may still use the old names. Before writing, read the current options of the Status field (fldS4AueH2OjCNYis) and the Registration field (fldKR6Rt6A3oplo4H, formerly "Link Status"), and write whichever name exists: "Not verified" (old: "To review"), "Verified" (old: "Approved"), "Open" (old: "Confirmed"), "Closed" (old: "Confirmed - closed"). Never create an option to get either name. Never write "Generic listing page — no direct event URL found" or "Pattern-matched, not verified": if an event has no registration page of its own, don't add it, and list it in the summary under "Skipped: no registration page" with name, date and where you saw it.

If the ewai-event-scan skill is not available in this session, change nothing in Airtable and send one push notification inside <routine_summary> tags saying: "EWAI event scan didn't run: the ewai-event-scan skill wasn't available."

Otherwise finish exactly as the skill's §8 (Finish) says. Do not create any other pages, files or artifacts.
```
