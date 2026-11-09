# Airtable setup snapshot

Used by the weekly release-notes check to spot changes to the table's setup. Generated, don't edit by hand.

Taken: 2026-11-09

## Fields (table order)

- **Day & Date** · formula (primary field) · `IF({Date}, DATETIME_FORMAT({Date}, 'ddd, MMM D YYYY'), '')`
  - description: Read-only display of the Date field with the weekday, e.g. "Sat, Oct 3 2026". Sort and filter on Date, not on this field.
- **Event Name** · singleLineText
- **Why** · richText
  - description: One line on why this passed the filter and what a member should know
- **Domain** · multipleSelects
  - description: What the event is about (topic), as opposed to For (who it's aimed at). Pick 1-3, most specific first.
  - options: Generative AI & LLMs | AI Agents | AI at Work & Productivity | AI Strategy & Business | AI Governance, Ethics & Law | AI Safety & Alignment | Security | MLOps & AI Engineering | Data & Analytics | Machine Learning Research | Robotics & Physical AI | Healthcare & Life Sciences | Finance & Fintech | Product & Design | Open-Source & Sovereign AI | Sustainability & Society | Language AI | Startups & Innovation | Cybersecurity
- **For** · multipleSelects
  - description: Who the event is aimed at, by role or industry
  - options: Everyone | Founders | Product & UX | Engineers & Researchers | Business leaders | Healthcare | Finance | Cybersecurity | Legal | Robotics | Developers | Researchers | Healthcare professionals | Security professionals
- **Registration Link** · singleLineText
- **Registration** · singleSelect
  - description: Open = the Registration Link opened this event's registration page on the Last checked date and registration was open. Closed = same page, but full, sold out or waiting list only.
  - options: Open | Closed
- **Type** · singleSelect
  - description: Connect = meeting people is the point. Learn = content-first or hands-on.
  - options: Connect | Learn
- **Cost** · singleLineText
  - description: Free, an amount, TBC, or Invite-only
- **Category** · singleSelect
  - options: Panel + Apéro | Meetup | Small Group | Large Conference | Networking | Hackathon | Workshop | Public & Community | Talk
- **Approx Size** · singleSelect
  - options: Small | Medium | Large | Small-Medium | Large (600)
- **Location** · singleLineText
- **Source** · singleSelect
  - description: Where the event was found
  - options: ai-weeks.ch | hackevents.net | Luma | Meetup | Eventbrite | Organiser site | Deep Tech Nation | Women's network | Manual | Zurich AI Festival | Eventfrog
- **Notes** · multilineText
- **Last checked** · date (ISO)
  - description: Internal: the date the scan (or the table owner) last opened this row's Registration Link and confirmed date, venue and registration status. Hide from member views.
- **Status** · singleSelect
  - description: Verified = checked by a person. Not verified = found and checked by the scan, not yet reviewed by a person (reviewed weekly). Rejected = hidden from the public view.
  - options: Not verified | Verified | Rejected | https://luma.com/ht3s8136
- **Date** · date (friendly)
  - description: The event date (first day for multi-day events). Weekday is shown in the "Day & Date" formula field.
- **Added by** · singleSelect
  - options: Agent | Manual
- **Added on** · date (ISO)
- **Table Creator Action Required** · multilineText
  - description: Internal, for the table owner: what to check or decide before approving (doubtful criteria, unconfirmed date or language, conflicting sources). Empty means the event passed every rule cleanly. Hide this field from member views.

## Views

### Grid view (public)
- filter: Date >= today (Europe/Zurich) AND Status != Rejected
- sort: Date ascending
- visible: Day & Date, Event Name, Why, Domain, For, Registration Link, Registration, Type, Cost, Category, Approx Size, Location, Source, Notes, Last checked, Status

### Older events
- filter: Date < today (GMT)
- sort: Date ascending
- visible: Day & Date, Date, Event Name, Why, For, Cost, Category, Approx Size, Location, Registration Link, Source, Notes, Type

### To Review
- filter: Date >= today (Europe/Zurich) AND Status = Not verified
- sort: Date ascending
- visible: Day & Date, Date, Event Name, Status, Registration Link, Notes, Why

### Rejected events
- filter: Status = Rejected
- sort: none
- visible: Day & Date, Date, Event Name, Status, Registration Link, For, Category, Approx Size, Location, Cost, Source, Notes, Registration, Type, Why, Added by, Added on, Table Creator Action Required, Domain, Last checked

### All columns view
- filter: none
- sort: Date ascending
- visible: Day & Date, Event Name, Registration, Registration Link, For, Status, Added by, Added on, Table Creator Action Required, Last checked
