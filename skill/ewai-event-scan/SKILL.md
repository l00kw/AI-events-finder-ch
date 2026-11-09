---
name: ewai-event-scan
description: Scan Swiss AI event sources and maintain the EWAI Airtable events table — find new in-person, English-language AI events in Switzerland, verify dates and registration links, re-check existing rows, and write them as "Not verified". Use when asked to run the EWAI event scan (full or light), re-check event links, or add events to the EWAI table.
---

# EWAI event scan

You maintain an Airtable table of AI events in Switzerland for EWAI, a Swiss peer community for professional women aged 30–55 navigating AI without a technical background. Members read this table and register for events from it, so every fact must be true and every link must work. A missing event costs little; a wrong date or dead link costs a member's trust. When in doubt, leave a field honest ("TBC", "not stated") rather than complete.

## 0. Setup (do this first)

1. Run `TZ=Europe/Zurich date +"%Y-%m-%d %u"` and write the result at the top of your notes as TODAY and WEEKDAY (1 = Monday). Use TODAY for "Added on", "Last checked" and all "checked YYYY-MM-DD" notes. TODAY is never an event date.
2. Run mode: WEEKDAY = 1 (Monday) or any day other than Friday → FULL. WEEKDAY = 5 (Friday) → LIGHT. LIGHT = Tier 1 sources + recurring-series check + link check only.
3. Window: events physically in Switzerland, dated TODAY through TODAY + 90 days in FULL mode, or TODAY through TODAY + 14 days in LIGHT mode (new events only; the link check in §3 is unchanged). Exception: in FULL mode, recurring-series sessions use a 30-day window (§4).

## 1. Airtable reference (use these IDs; don't rediscover the schema)

Base `<BASE_ID>`, table `<TABLE_ID>`. (Copying this setup? Replace these and the field IDs below with your own.)

| Field | ID | Allowed values / format |
|---|---|---|
| Date | fldt449C5JIYbjbeJ | YYYY-MM-DD (first day if multi-day) |
| Event Name | fldyZMsVLLYhiH3up | organiser's title |
| Type | fldJGu7f1puugB89t | Connect · Learn |
| For | fld5hwAawrQIn9VYL | Everyone · Founders · Product & UX · Developers · Researchers · Business leaders · Healthcare professionals · Security professionals |
| Domain | fldNXv7VH4z9Cg423 | see §6 |
| Category | fldO5S7gDJWFYMFQO | Meetup · Panel + Apéro · Small Group · Networking · Large Conference · Hackathon · Workshop · Talk · Public & Community |
| Approx Size | fldtuU4VN1LIA6gtu | Small · Medium · Large (only these three) |
| Location | fldchXksj2JXEX2Jl | venue, city |
| Cost | fldhkHcHlKFRDqAsR | "CHF n" · "Free" · "Invite-only" · "TBC" |
| Registration Link | fldeLthNufDpgbz2n | URL |
| Registration | fldKR6Rt6A3oplo4H | Open · Closed (definitions in §5; field formerly named Link Status) |
| Source | fldKpEsm6agO54S0N | ai-weeks.ch · hackevents.net · Luma · Meetup · Eventbrite · Eventfrog · Organiser site · Deep Tech Nation · Women's network · Zurich AI Festival (if the Eventfrog option doesn't exist yet, leave Source blank and write "Found on Eventfrog" in Table Creator Action Required — never create the option) |
| Why | fldcCHCiRgvjTEJG0 | one member-facing sentence |
| Notes | fld23KV0dbAWW6FSq | member-facing practical facts |
| Table Creator Action Required | fldLoFcgPsZbY4cfg | internal: what the owner must check |
| Last checked | fldPTzkNo1Q86tgCW | YYYY-MM-DD |
| Status | fldS4AueH2OjCNYis | Not verified (you only ever write this). Others: Verified (checked by the owner), Rejected |
| Added by | fld6g73JRrJInHL8a | Agent |
| Added on | fldmhXlBgIw1RKaTd | TODAY |

Rules: never create, rename or delete fields or select options; never write retired options (For: Healthcare, Finance, Cybersecurity, Legal, Robotics, Engineers & Researchers; Domain: Security; Size: Small-Medium, Large (600); Registration: From official programme, Pattern-matched, not verified, Generic listing page — no direct event URL found). Never modify a row whose Status is Verified or Rejected. When reading, request only the fields you need. Write in batches of up to 50 records.

Label names are being renamed. Before writing, read the current options of Status and Registration and use whichever name exists: "Not verified" (old name "To review"), "Verified" (old name "Approved"), "Open" (old name "Confirmed"), "Closed" (old name "Confirmed - closed"). Never create an option to get the new name.

Rows whose Table Creator Action Required starts with "Exception kept by table owner" were added by the owner despite a rule; don't treat them as a precedent for adding similar events.

## 2. Read the table

One read of all rows with fields: Event Name, Date, Status, Registration Link, Registration, Last checked, Domain. Build:
- a dedupe list (all statuses — Rejected means "already turned down, never re-add");
- a link-check list (§3).

## 3. Link check on existing rows (both modes)

Re-check an upcoming Not verified row only if at least one is true: its Date is within 14 days of TODAY; Registration is not "Open"; Last checked is empty or more than 7 days before TODAY. Skip all others — they were verified recently.

For each row you re-check, open its Registration Link and:
- broken (404, error, homepage, a different event or year) or an aggregator page → find the direct registration page (§5), update Registration Link + Registration, explain in Table Creator Action Required. If no registration page for this event exists, write "recommend reject: no registration page for this event (checked YYYY-MM-DD)" in Table Creator Action Required — never delete rows;
- registration closed or sold out → Registration "Closed", update Notes;
- different date or venue on the page → correct it, explain in Table Creator Action Required;
- Domain empty → fill it (§6);
- always set Last checked = TODAY.

Upcoming Verified rows: in FULL mode, open the link of those within 30 days; never edit them; list any problem in the summary.

## 4. Find candidates

### Sources

Tier 1 — every run:
- https://ai-weeks.ch/events — primary calendar. Each event has its own page at ai-weeks.ch/events/<title-slug>-<YYYY-MM-DD> with a Register link to the organiser. Reach it via the listing's links, a "site:ai-weeks.ch <title>" search, or the slug-plus-date pattern (use only if it loads the right event). Don't conclude an ai-weeks.ch event has no registration until you've opened its event page.
- https://www.hackevents.net/ch/cities/zurich, /basel, /geneva, /lausanne, /bern (city main pages; the per-tab pages often come back empty)
- Luma — NEVER skipped, in either mode and whatever the budget: https://luma.com/discover/zurich/ai, https://luma.com/discover/geneva/ai, https://luma.com/zurich, https://luma.com/geneva, https://luma.com/lausanne. Luma listings and event pages usually show no date: for every AI-themed, in-window-looking item, open the event page and look for an allowed fallback date source (§5); list items whose date can't be verified in the summary rather than dropping them silently.
- https://app.sprintd.org/series/hack-apertus — the authority on which Hack Apertus stops exist; each stop's sprintd page is its Registration Link. Don't add a stop that appears only on an aggregator.
- https://techface.ch/events — the readable source for TechFace / women-in-tech events (use this instead of womentechswitzerland.com).
- Meetup group iCal feeds — fetch `https://www.meetup.com/<group>/events/ical/` for each group: mindstone-zurich-ai-meetup, mindstone-geneva-ai-meetup, language-ai-meetup, ibmpoweraizurich, Zurich-Women-in-Machine-Learning-and-Data-Science, swiss-ai-group, PyData-Zurich, artifical-intelligence-zurich. An empty feed means no upcoming events, not a failure. The feed gives title, date/time and event URL but NO venue: open the event page (meetup.com/<group>/events/<id>/) for venue, cost and format. For Mindstone events, the community.mindstone.com/events/<slug> page loads without login and carries the Register button; it often shows no date, so take the date from the iCal feed and say so in Table Creator Action Required. If the iCal feed and the event page disagree on venue, use the event page and note the conflict.

Tier 2 — FULL mode only:
- https://www.startupticker.ch/en/events, https://deeptechnation.ch/events/, https://dev.events/EU/CH, https://www.greaterzuricharea.com/en/events
- https://ai-startup-center.com/news-events-technopark/ (often times out: one retry, then mark unreachable)
- Eventfrog: https://eventfrog.ch/en/events.html?searchTerm=AI and https://eventfrog.ch/en/events.html?searchTerm=artificial%20intelligence. Noisy ("AI" also matches Appenzell Innerrhoden, Ai Weiwei, kids' camps) and mostly German or online, so apply the cheap filter hard. Individual pages (eventfrog.ch/en/p/…) show the full date with year, venue, organiser and ticket status ("Sale open – ends …"); the Eventfrog event page counts as a ticket shop and can be the Registration Link.
- https://www.womenintechswitzerland.com/events
- https://www.eventbrite.ch/b/switzerland--zurich/science-and-tech/ — low priority and noisy; dates on the listing have no year. Keep only titles containing AI / KI / artificial intelligence / machine learning / LLM / agent, then confirm date, year and venue on the individual eventbrite.ch/e/ page. Skip it if the run budget is tight.
- Web searches (one each): "AI event Zurich [month year]", "AI event Geneva [month year]", "AI event Basel [month year]", "AI event Lausanne [month year]", "AI event Bern [month year]", "AI workshop Zurich", "AI hackathon Switzerland", "AI healthcare conference Switzerland", "AI fintech Switzerland", "AI legal Switzerland"

Tier 3 — FULL mode, first Monday of the month only:
- https://swissfintechladies.com/events-2026/, WiDS Zurich (search for its current Luma/Meetup page)
- https://www.zurichaifestival.ch/program — August to early October only
- One web search `site:meetup.com AI Zurich` (and `site:meetup.com AI Geneva`) to spot new AI Meetup groups. Don't add groups to the iCal list yourself; list new candidates in the summary for the owner.
- Once a year (when a run falls in the 8 weeks before it): search for the #wetechtogether conference and add it if it passes the criteria — its own site can't be fetched.

Recurring series — every run (both modes):
- From the table read (§2), list the recurring series: the same normalised event name on two or more rows, or a name with a session number or month (e.g. "#7", "November AI Meetup"), with at least one session dated in the last 60 days or later. Ignore series whose rows are all Rejected.
- For each series, open its organiser's own calendar once: the organiser's events page if one exists (find it via the link on an existing row's Luma/Meetup page, e.g. ai-society.ch/events for AI Society Coffee Chats), otherwise the Luma calendar page (luma.com/calendar/…) or the Meetup group's iCal feed. Add every session not already in the table that falls in this step's window (FULL mode: TODAY through TODAY + 30 days; LIGHT mode: TODAY through TODAY + 14 days), one row per session, each with its own registration link, opened and verified as in §5.
- Luma calendar pages usually list sessions without dates; a session's date must still come from an allowed source (§5) — the organiser's events page counts as the organiser's site.
- FULL mode: no cap — check every series, add only sessions dated within the next 30 days (later sessions are picked up by later runs), and this step is never skipped or cut short for budget. LIGHT mode: about 8 page fetches for this step; if you hit that, list the series you didn't check in the summary.

Known dead ends — don't spend calls on them: womentechswitzerland.com and wetechtogether.ch (block fetching — never work around a block), Eventbrite city search pages (/d/…), Meetup's /find search, Impact Hub Zurich's events page (JavaScript calendar, no events in the text — its events show up on Luma/ai-weeks.ch instead), luma.com/basel (unrelated calendar), Eventfrog category pages such as /en/events/ch/digital-ai.html (silently fall back to the generic list) and api.eventfrog.net.

If a source fails, note it and move on.

### Cheap filter before opening any event page

From the listing text alone, drop anything that: is already in the dedupe list (same normalised name, date within 1 day) or Rejected; is dated outside the window; is titled or described only in German/French/Italian; says online/webinar/livestream; is a pitch night, investor event or job fair; is clearly not about AI. Only open event pages for what remains.

### Budget

Luma sources (and, in FULL mode, the recurring-series check) are never skipped for budget — if the budget is tight, drop Tier 2 non-Luma sources first. At most 4 parallel subagents. Each gets: this full prompt, its assigned sources, the dedupe list, and a cap of 40 page fetches. Whole run: stop discovering at ~200 page fetches total (~80 in LIGHT mode), write what you've verified, and list what you skipped in the summary.

### What subagents return

A compact list, one entry per candidate, no prose:

```
name | date | date_source_url | date_quote | venue_city | venue_source_url | language (+quote, or "not stated") | cost (+quote, or "not stated") | audience_quote (or "not stated") | format | registration_url | registration_url_opened (yes/no) | registration_status | doubts
```

Every factual field needs the URL it was read on and a short verbatim quote. A field without a source is "not stated", never a guess. Subagents never write to Airtable.

## 5. Verify (main agent, before writing)

You — not the subagents — are responsible for what goes into the table.
- Re-open every registration_url you will write and check it shows this event's name (and date, where the page shows one). If it doesn't load or shows something else, it is not a registration page.
- Drop or flag any field whose quote is missing or doesn't support the value.

Dates:
- Take dates and venues from the individual event page, never a listing summary (listings scramble dates and cities).
- Check the year and that the weekday matches; women's-network and aggregator calendars often show last year's edition.
- Many Luma and Mindstone pages hide the date. Allowed fallback sources, in order: the organiser's own site, the Meetup event page or the group's Meetup iCal feed, the ai-weeks.ch event page, the hackevents.net event page. If the date comes only from ai-weeks.ch, hackevents.net or an iCal feed, add the event but say so in Table Creator Action Required. Not allowed as date sources: nomad.watch or other mirrors, Luma's internal API, search-result snippets.
- Conflicting sources → organiser page > Luma/Eventbrite/Meetup page > aggregator; describe the conflict in Table Creator Action Required.

Registration links:
- Must be opened and must load this exact event. No 404s, homepages, other years, login walls (use the public event page instead), or URLs you constructed and didn't open.
- Prefer the event's own Luma/Eventbrite/Meetup page, ticket shop, or the organiser's page that carries the booking button.
- Aggregators (ai-weeks.ch, hackevents.net, swissdataevents.ch, startupticker.ch, dev.events, women's-network listings, GitHub) are discovery sources, not registration links. Follow them to the organiser.
- No registration page for this specific event (only a listing, a calendar, or an aggregator page about the event) → don't add it. List it in the summary under "Skipped: no registration page" with name, date and the page where you saw it, so the owner can add it by hand.
- An organiser page with a visible register / join / sign-up button or clear sign-up instructions counts as a registration page, even if the form behind it won't open for you. Add the event and write "registration button not opened — check it" in Table Creator Action Required.

Registration:
Registration says whether people can register for THIS event through the Registration Link, as of Last checked. The organiser's own page counts as a registration page.
- Open — you opened the link, it shows this event, and people can register or request a place now (approval required and request-to-join count as open).
- Closed — same page, but registration is closed, sold out or waiting-list only. Put the detail in Notes ("Sold out, waiting list open, checked YYYY-MM-DD").
- Open never means the event is happening; it means the link goes to this event's registration page. If only some ticket types are sold out, stay Open and name the sold-out ones in Notes.
- Update Registration on every check, in both directions: sold out → Closed; reopened → Open.
- If the page can't be read (JavaScript-only page, login wall, error): a new row is not added (list it in the summary); on an existing row leave Registration as it is, write "link not verifiable (checked YYYY-MM-DD)" in Table Creator Action Required, and set Last checked.

Never infer:
- Language: an English web page doesn't mean an English event. If the event language isn't stated, flag "language not stated" in Table Creator Action Required.
- Cost: if no price is published, Cost = "TBC". Never "likely free".
- Size: if no capacity or attendance is stated, estimate from venue/format and add "size estimated" to Table Creator Action Required.
- People and numbers in Why: only names, companies and figures that appear on a page you opened.

## 6. Criteria and tagging

Add an event only if all are true:
1. Physically in Switzerland.
2. AI is the main theme — in the title, or most of the programme. One AI panel/track inside a broader conference doesn't count. Networking events with no AI theme don't count.
3. Run in English (bilingual counts).
4. In person (no online-only, no webinars).
5. Not a recruiting fair, trade show or student-only event. Vendor-run events with practical content (hands-on labs, workshops, masterclasses) are welcome — name the company in Why. Exclude pure sales pitches and booth expos.
6. Not an investor, pitch or fundraising event (pitch nights, investor summits/days, VC nights, investor/executive dinners, founder–investor matchmaking) — these are investor-community discussions, not practical AI knowledge for members.
7. Not a templated or low-quality listing (copied text mentioning another country, "TBD" venue with many identical dates, "AI SaaS / prompt to profit" lead-gen series).
8. Has a registration page for this specific event (§5).
9. Not already in the table (any status).

Technical events (developer meetups, hackathons, research talks) are allowed; tag For accurately so members can filter.

Borderline (probably passes, something uncertain) → add as Not verified and explain in Table Creator Action Required in one or two plain sentences; if you think it likely fails, write "recommend reject" and the rule. Clearly failing → don't add; mention in the summary only if it was close.

Type:
- Connect — people talk to each other and no technical background is assumed: panel with apéro/networking, meetup, breakfast/lunch roundtable, community night, networking evening, small conference under ~150. Never for conferences over ~300 people or over CHF 400.
- Learn — content-first or hands-on: conferences, summits, hackathons, workshops, talks. For hackathons, say in Why whether non-developers are explicitly invited.
- Fits both → Connect. Unsure → Learn, and say so in Table Creator Action Required.

For (who it's for — roles only, from the page's own audience wording such as "who should attend", "designed for", ticket categories, speakers):
- Everyone — only when the organiser explicitly opens it to a general audience and no role/domain expertise is assumed. Never a fallback: if no audience is stated, pick the roles the content and speakers point to and note "audience not stated".
- Founders — founders, entrepreneurs. Product & UX — PMs, designers, UX researchers. Developers — people who write code or build software (incl. AI in software engineering, MLOps, hackathons). Researchers — academic/scientific audiences, incl. life-science researchers. Business leaders — executives, managers, decision-makers and business-function professionals (compliance, legal, finance, HR), incl. hospital executives and CISOs/CIOs when strategic. Healthcare professionals — clinicians, hospital/health-system staff and clinical leads. Security professionals — CISOs, security engineers, IT security/risk managers, ethical hackers.

Domain (what it's about — pick 1–3, most specific first; always include the industry if the event is AI-in-an-industry):
Generative AI & LLMs · AI Agents · AI at Work & Productivity · AI Strategy & Business · AI Governance, Ethics & Law · AI Safety & Alignment · Cybersecurity · MLOps & AI Engineering · Data & Analytics · Machine Learning Research · Robotics & Physical AI · Healthcare & Life Sciences · Finance & Fintech · Product & Design · Open-Source & Sovereign AI · Sustainability & Society · Language AI · Startups & Innovation. Never "AI" on its own.

Category: Meetup (recurring, informal) · Panel + Apéro (talk then networking) · Small Group (<40) · Networking (connection is the purpose) · Large Conference (150+) · Hackathon · Workshop (hands-on, leave with a skill) · Talk (no networking window) · Public & Community (open to the public, tours/demos/culture). Approx Size: Small <40 · Medium 40–150 · Large 150+.

Dedupe: same event = names match after removing punctuation and case, and dates within 1 day. Same name but dates more than a day apart → open the existing row's Registration Link before deciding: if the existing Not verified row's date is wrong, correct it (no new row) and explain; if the row is Verified/Rejected, don't touch it and report it; add a new row only when the pages show genuinely separate sessions (e.g. different URL per session). Recurring series (e.g. monthly Mindstone meetups): one row per dated session.

## 7. Write

For each new event fill every field in §1. Field content rules:
- Why — one sentence for members: what it is plus useful facts from the page (named speakers, who runs it, discount code, women-only, non-developers welcome, bring a laptop, multi-day range). No doubts, no internal commentary.
- Notes — practical facts with the date checked (approval required, waitlist, "2 spots left, checked YYYY-MM-DD", apply-by date, unusual way to register, venue outside the centre). Blank if none. No doubts.
- Table Creator Action Required — blank if the event passed every rule cleanly; otherwise what the owner should check. All doubts go here and only here.
- Last checked = TODAY; Status = Not verified; Added by = Agent; Added on = TODAY.

## 8. Finish

Write the summary:
- run mode; events added by Type and by Source; how many have something in Table Creator Action Required
- existing rows fixed (link, date, venue, registration status)
- Verified rows with problems (not modified)
- Skipped: no registration page — one line each: name, date, where you saw it
- close calls excluded, one line each with the rule
- sources that failed, were empty or were skipped for budget
- recurring series checked, new sessions added from them, and any series not checked (LIGHT mode)
- new Meetup groups spotted (Tier 3 months only)
- months in the window with zero Connect events

Then notify: send exactly one push notification with the summary inside <routine_summary> tags (most important sentence first) — but only if at least one is true: events were added; an existing row was fixed; a Verified row has a problem; a Tier 1 source failed; the run couldn't complete. Otherwise send nothing. Post nowhere else and message no one else.
