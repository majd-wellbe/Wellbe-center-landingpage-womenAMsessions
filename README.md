# Wellbe Free Trial (Women over 40)

`index.html` is the current page. `index-v1.html` is the previous version, kept for comparison (see CHANGELOG.md).

Landing page with the booking calendar on the page itself, then one short contact step (name + WhatsApp number, optional injury note and email). Static site on GitHub Pages, backend = Apps Script writing to the Operations sheet (tab `LEADS W40`).

## Booking rules (built in)
- Mon to Fri, 7 / 8 / 9 / 10 AM, 60 min, next 7 days, slot must start 12+ hours from now.
- Joe max 3 clients per hour = his clients in SESSIONS 1:1 + 1:2 + 1:3 at that hour + `Pending` rows in LEADS W40. Other trainers never count.
- Joe has room and no 1:1 / 1:2 client at that hour = **open** (booked as Instant, Status = Pending until Romy confirms). Joe at 3, or Joe has a 1:1 / 1:2 client at that hour = **Full**. The page never shows spot counts. (Checked against the live backend on 27 Oct 2026.)
- Flow: pick a day and time on the page > name + WhatsApp number (+ optional injury, optional email) > booked. The page sends `lead` then `book` back to back, so the lead row exists even if the booking fails.
- One booking per phone number (the backend matches an existing lead by phone and returns it).
- "Trained before" and "What do you want most" are no longer asked; those columns stay empty for new leads. Injuries are saved through the `lead` call.
- "None of these work?" saves name + number only (Status = No Booking) so Romy can find a time.
- Invite a friend: the confirmation page gives a WhatsApp invite link (`?d=date&h=hour&by=name`). The friend fills the same form and lands on that session preselected. Her Source column shows `by=Name`.

## Romy's workflow in LEADS W40
| Status | Meaning | Holds a seat? |
|---|---|---|
| No Booking | Filled the form, skipped booking. Call her. | No |
| Pending | Booked a time. Call within 24h. | Yes |
| Confirmed | Automation runs (below) | No (SESSIONS 1:3 counts her now) |
| Cancelled / No Answer | Seat released | No |

## Auto confirm (Romy only picks "Confirmed")
1. Client found in Sheet 1 CLIENTS by phone, then by exact name. If none, a new CXXX client is created.
2. PACKAGES row: `Trial Session - 1:3 (Free)`, 1 pass, $0, starts on the trial date, 30 day expiry, New Client = N (the Y goes on her first paid package).
3. SESSIONS 1:3: if a session already exists at that date/hour with a free spot, she is added to it. Otherwise a new row is created with Joe, same room as his last session, Status = Scheduled.
4. Client ID, Package ID and Session ID are written back to the lead row (green headers, never type there).
5. WhatsApp + email: "W40 CONFIRMED". The calendar scanner creates the event on its next run.

If anything fails (hour already full, missing date/time), Status flips back to Pending, the reason goes in Notes, and you get a "CONFIRM FAILED" alert.
For a lead who skipped booking: type Trial Date (`2026-10-15`) and Trial Time (`8:00 AM`) first, then set Confirmed.
Never add W40 leads to SESSIONS 1:3 by hand. If she cancels after confirming, mark it in SESSIONS 1:3 as usual.

## Backend setup (one time, 5 minutes)
1. Go to script.google.com > New project. Name it `Wellbe W40 Backend`. Use the Google account that can edit the Operations sheet.
2. Project Settings (gear) > Time zone = (GMT+03:00) Beirut.
3. Paste `backend/Code.gs` over everything in Code.gs. Save.
4. Run `setupW40` once, approve permissions. The `LEADS W40` tab appears in Operations and the auto confirm trigger is installed. The project needs access to both Operations and Sheet 1 (Client Portal): use the account that owns them.
5. Run `testSlots` and check the log shows days and hours. Run `testW40Alert` to check WhatsApp + email.
6. Deploy > New deployment > type Web app. Execute as: Me. Who has access: Anyone. Deploy. Copy the URL ending in `/exec`.
7. In `index.html`, find `API_URL: ''` and paste the URL between the quotes.

Any later change to Code.gs: Deploy > Manage deployments > Edit > Version: New version (keeps the same URL).

## Meta Pixel
When you have one, paste the ID in `PIXEL_ID: ''`. Events: `PageView`, `OpenForm` + `FormStep` (custom: step 1 = time picked, step 2 = contact sheet opened), `Lead` (name + phone sent, now after a time is picked), `Schedule` (time booked). Optimize the campaign for `Schedule` once you have 50 a week, `Lead` before that.

## Demo mode
With `API_URL` empty the page runs on fake slots so you can click through it. Nothing is saved.
