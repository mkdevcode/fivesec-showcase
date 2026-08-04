# Fivesec — User Guide

A practical guide to how clients book, and how a specialist runs their day
— no technical jargon, just what actually happens on each screen.

> Fivesec is an online booking service for solo specialists and small teams
> who work with clients by appointment — barbers, cosmetologists, trainers,
> and similar service professionals.

---

## Roles

**Client** — uses the public booking page. No account needed. Picks a
service, sees available dates and open slots, confirms contact details,
gets a confirmation page.

**Master (specialist)** — works from their own cabinet: today's bookings,
all bookings, booking actions, services, client base, schedule, profile
settings, push notifications.

**Admin / Owner** — manages access, salon settings, and specialists
according to their permission level.

---

## Public Booking Flow

Every specialist has their own personal booking link.

**Step 1 — Choose a service.** The client sees the specialist's available
services, each showing name, duration, price, currency, and a short
description. A long description opens in a separate detail view instead of
cluttering the card.

**Step 2 — Choose date & time.** Only genuinely available dates and slots
are shown, calculated from the specialist's working schedule, the selected
service's duration, existing bookings, schedule exceptions, blocked
personal time, and the specialist's timezone.

**Step 3 — Confirm.** The client enters contact details (name, phone,
email, comment) and accepts the privacy policy, depending on what's
configured. Once confirmed, the booking is created and immediately visible
in the specialist's cabinet.

**Step 4 — Result page.** The client sees a confirmation with the service,
date, time, contact details, and a success message.

---

## The Specialist's Cabinet

Built mobile-first — usable from a phone, tablet, or desktop equally well.

### Bookings

**Today's bookings** — start time, client name, service, duration, price,
status, contact details, and quick actions, all for the current day.

**All bookings** — the full list with filters, for finding an old booking,
checking upcoming history, reviewing completed visits, or finding
cancellations.

**Booking actions** — confirm, complete the visit, mark a no-show, cancel,
reschedule, view client details, or contact the client directly through
whatever channel is available.

**Statuses** matter beyond just labeling — a booking's status feeds
directly into the client's visit history, cancellation stats, and no-show
tracking, so keeping them current isn't just bookkeeping, it's what makes
the client profile trustworthy later.

### Manual booking creation

Useful when a client messaged, called, or booked in person instead of
through the public link: open the create-booking flow, pick a service,
pick date & time, find or add the client, confirm. Starting from a
client's profile pre-fills that client and can suggest their previous
service — faster for repeat visits.

### Services

For each service: name, duration, price, currency, active/inactive, and a
client-facing description (kept short and specific — no need to repeat the
service name, and it's worth checking how it renders on mobile before
publishing). A temporarily unavailable service should be deactivated
rather than deleted — deleting a service that's already tied to booking
history isn't the intended path.

### Clients

Active and archived client lists, search by name or phone, a client
profile with visit history, visit/cancellation/no-show counts, a
reliability indicator, notes, and quick contact actions.

**Contact channels** per client can include phone call, SMS, WhatsApp,
Viber, Telegram, Instagram, Facebook, or email — quick-contact buttons only
work once the relevant field is actually filled in correctly.

**Archived clients** stay out of the normal booking flow while their
history is preserved — for clients the specialist no longer actively works
with, but doesn't want to lose the record of.

### Schedule

Weekly rules define baseline availability (e.g. working Mon/Tue/Thu/Fri,
off Wed/Sun, Saturday as-needed). **Exceptions** handle one-off days — a day
off, a shortened day, an extra open day, part of a day blocked. **Personal
time** blocks a specific window (lunch, a break between clients, personal
errands) — once blocked, clients simply don't see that slot as available.

### Timezone

Booking logic runs on the specialist's timezone — relevant if they work
from a different country than their clients, or relocate. After changing
timezone, it's worth double-checking upcoming bookings and the schedule
display.

---

## PWA Mode

Fivesec installs like a native app — an icon on the home screen, faster
access, and (where permitted) web push notifications for new bookings and
daily summaries.

**Android:** open in Chrome → install prompt or browser menu → add to home
screen → confirm.
**iPhone:** open in Safari → Share button → "Add to Home Screen" → confirm.

---

## Push Notifications

Used for new bookings, important booking changes, and end-of-day summaries.
Requires: opening the app in a supported browser, allowing notifications,
and not blocking them at either the phone's system level or the browser/PWA
level. If notifications stop arriving, that's usually where to look first.

---

## A Specialist's Typical Day

**Morning:** open the cabinet, check today's bookings, review new requests,
check personal time/breaks, reach out to clients if needed.

**During the day:** keep booking statuses current, mark completed visits,
log no-shows/cancellations, add client notes, create manual bookings for
anyone who reached out directly.

**End of day:** confirm completed bookings, make sure statuses are current,
preview tomorrow's bookings, block personal time if needed, check for new
requests.

---

## Good Habits

- Don't leave a booking with a stale status.
- Don't create duplicate client records with different phone numbers
  unless there's a real reason to.
- Only fill contact channels with data that's actually correct.
- Use notes for anything important about a client worth remembering.
- Don't delete a service that already has booking history — deactivate it.
- Re-check the schedule after changing working hours.
- Test the public booking link after any meaningful change to services or
  schedule.
- Use PWA mode for faster day-to-day phone use.

---

## Troubleshooting

**Client doesn't see any open time** — check: is the service active? is
its duration set correctly? is there a working day in the schedule? is
there an exception blocking that date? is personal time blocking it? is
the slot already taken by another booking?

**Date/time displays incorrectly** — check the specialist's timezone, the
booking date, schedule settings, and whether timezone changed after
bookings were already created.

**Quick-contact button doesn't work** — check that the relevant field is
filled in, the phone number is valid, the username/link is correct, and
the corresponding messenger app is actually installed on the device.

**Push notifications aren't arriving** — check browser notification
permission, phone system-level permissions, whether notifications are
disabled for the installed PWA, whether the browser supports web push, and
whether the app is open in a mode where push isn't supported.

**A form isn't saving changes** — check that all required fields are
filled, there are no validation errors, the connection is stable, and the
page wasn't refreshed before saving.

---

## Quick Reference

**Booking** — a client's confirmed request for a specific service, date,
and time.
**Slot** — an open block of time available for booking.
**Service** — a specialist's offering: name, duration, price, description.
**Archived client** — kept in history, excluded from the active booking flow.
**Personal time** — a window the specialist has blocked on their schedule.
**Schedule exception** — a one-off rule overriding the standard weekly
schedule for a specific date.

---

## Getting Started (First-Time Setup)

1. Set up your profile.
2. Add your services.
3. Set up your schedule.
4. Check your public booking link.
5. Create a test booking.
6. Install the app on your phone.
7. Enable push notifications.
8. Start accepting real bookings.

---

## Worked Example

A specialist wants to start taking manicure bookings:

1. Creates a "Manicure" service.
2. Sets duration — say, 90 minutes.
3. Sets price and currency.
4. Adds a short client-facing description.
5. Opens their working days and hours in the schedule.
6. Copies their public booking link.
7. Shares it with clients, or adds it to their Instagram bio.
8. A client picks the service, date, and time themselves.
9. The booking appears in the specialist's cabinet.
10. The specialist gets notified and sees it on their schedule.

---

## The Core Idea

Fivesec exists to cut down the back-and-forth messaging and chaotic manual
scheduling that solo service professionals deal with. The client picks a
convenient time on their own; the specialist gets a structured booking,
client history, quick contact options, a schedule, and notifications — all
in one place.
