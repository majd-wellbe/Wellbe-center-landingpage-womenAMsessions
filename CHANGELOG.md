# Landing page change log

Use this file to compare results between versions. Only measured numbers go in the results tables. Leave a cell empty until it is measured.

## v1: "Fill the form" (file: `index-v1.html`)

- In the repo from 13 Oct 2026. Last change 19 Oct 2026 (commit 1534da7).
- The ad "Majd yapping women over40" (campaign "Women over 40 | Bsalim | 1 Mile | 12 october") started delivering on 16 Oct 2026.
- Flow: button > name, phone, email > 3 questions (trained before, goal, injuries) > pick day and time > booked.
- Meta Pixel `Lead` fired when name + phone were sent, before the questions and before a time was picked.

### v1 baseline: 16 to 27 Oct 2026 (27 Oct is a partial day)

| Metric | Value | Source |
|---|---|---|
| Ad spend | $109.24 | Meta Ads Manager, account Center 2025, ad level, daily rows summed |
| Landing page views | 311 | Meta Ads Manager |
| Meta leads (Pixel `Lead`) | 13 | Meta Ads Manager, attribution 1 day view / 7 day click |
| Landing page view to Meta lead | 4.2% | 13 / 311 |
| Leads from the ad in LEADS W40 (source fb or ig) | 14 | Operations sheet, read 27 Oct 2026 |
| Booked a trial | 4 | LEADS W40, Status Confirmed |
| Attended the trial | 3 | SESSIONS 1:3 attendance (1 early cancel) |
| Bought a paid package | 1 ($200) | PACKAGES |
| Leads that cancelled because the center is far | 6 | LEADS W40 Notes |

## v2: time first booking (file: `index.html`)

- Live date: ____ (the date this version is merged to main and goes live. Fill in on that day.)
- Flow: pick day and time on the page > name + WhatsApp number (+ optional injury, optional email) > booked.
- Removed questions: "Have you trained before?" and "What do you want most?". Injury is now one optional line. Email is optional, behind "+ Add email".
- Backend, sheet columns and booking rules are unchanged.
- Calendar check on 27 Oct 2026, 20:20 Beirut: the 18 time slots the live backend offered for 28 Oct to 3 Nov matched Joe's sessions and Pending trials in the Operations sheet, slot by slot (0 mismatches). The page displayed them with the right days and times in Beirut, Los Angeles and Auckland time zones, and sent the chosen date and hour unchanged.
- Meta Pixel `Lead` now fires after a time is picked and the contact details are sent. This is a different moment than in v1, so Meta lead counts are not directly comparable between versions. Compare booked trials per landing page view instead.

### v2 results (fill in after the same number of days as the v1 baseline)

| Metric | Value | Source |
|---|---|---|
| Period | | |
| Ad spend | | Meta Ads Manager |
| Landing page views | | Meta Ads Manager |
| Booked trials (Pixel `Schedule`) | | Meta Ads Manager |
| Leads from the ad in LEADS W40 | | Operations sheet |
| Booked a trial | | LEADS W40 |
| Attended the trial | | SESSIONS 1:3 |
| Bought a paid package | | PACKAGES |

## How to compare fairly

1. Use the same length of period for both versions.
2. Main metric: booked trials divided by landing page views. Second: paid packages divided by ad spend.
3. Note anything else that changed in the same period (ad creative, budget, targeting). If the ad or targeting changed too, the difference cannot be credited to the page alone.
