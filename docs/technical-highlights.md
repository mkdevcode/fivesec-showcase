# Fivesec — Technical Highlights

A production booking SaaS for solo service professionals and small teams —
a public-facing booking flow paired with a mobile-first specialist cabinet,
running as an installable PWA with push notifications.

> Fivesec has real active users across Europe today.
> See also: [User Guide](business-guide.md) — how a specialist actually
> runs their booking flow day to day.

---

## Tech Stack

Next.js 16 (App Router) · React 19 · TypeScript · Prisma 6 · PostgreSQL ·
NextAuth v5 · next-intl · Tailwind CSS 4 · Radix UI primitives · Web Push
API · Cloudinary · Resend · Vercel Analytics

---

## System Overview

Two halves, one codebase: a **public booking flow** reachable through each
specialist's personal link, and a **specialist cabinet** — role-gated,
mobile-first, installable as a PWA.

```
/book/[slug]/services   → public: pick a service
/book/[slug]/schedule   → public: pick date & time
/book/[slug]/confirm    → public: contact details + confirmation

/master                        → specialist cabinet home
/master/bookings               → today's bookings
/master/bookings/all           → all bookings, filterable
/master/services               → manual booking creation
/master/clients                → client list, search, archive
/master/clients/[clientId]     → client profile, history, notes
/master/schedule                → weekly rules, exceptions, personal time
/master/settings/setup_services → service management
/superadmin                     → access requests, salon provisioning
```

Role-based zones exist for specialists, admins, owners, and
super-admins — each sees a different slice of the system matched to what
they're actually responsible for.

---

## Availability Logic

The hardest part of a booking system isn't the calendar UI — it's
correctly answering "what slots are actually open right now" given several
independent constraints layered together:

- the specialist's weekly working-hours rules
- one-off **schedule exceptions** (a shortened day, an extra open day, a
  day off)
- blocked **personal time** windows (breaks, lunch, errands)
- the selected service's duration
- bookings that already exist in that window
- the specialist's timezone

Available slots are computed by intersecting all of these — not just
checking "is this hour free," but "is this hour free, of the right length,
on a day that's actually open, given the specialist's own clock." Getting
the timezone piece right matters specifically because specialists and
clients aren't always in the same one, and the same moment in time has to
render identically in both the booking logic and the UI regardless of
who's looking at it.

---

## Booking Snapshot Pattern

Each booking stores a **snapshot** of the service at the moment it was
made — `serviceName`, `serviceDuration`, `servicePrice`, `serviceCurrency`
— rather than a live reference to the service record. If a specialist
later renames a service, changes its price, or adjusts its duration,
bookings already made keep showing what the client actually agreed to at
booking time. This is the same reasoning e-commerce systems use for order
line items: what was purchased shouldn't silently change because the
catalog changed later.

---

## Client Model

A client isn't just a name and phone number — the profile tracks
reliability signals (visit count, cancellation count, no-show count) built
directly from booking history, multiple contact channels (phone, SMS,
WhatsApp, Viber, Telegram, Instagram, Facebook, email) with a preferred
method and language, an acquisition source, and free-form notes. Archiving
a client removes them from the active booking flow (so they don't clutter
day-to-day use) while keeping their full history intact — deletion isn't
the mechanism for "I don't work with this client anymore."

Re-booking from a client's profile pre-fills that client and can suggest
their previous service — a small detail, but it's the difference between a
30-second manual booking and a multi-step one for a specialist who's
mostly handling repeat clients.

---

## Service Descriptions

Client-facing service descriptions are capped at 300 characters, editable
from service settings, and rendered on booking cards — with longer text
opening in a separate detail dialog instead of stretching the card layout.
A small constraint, but it keeps the mobile booking flow (where most
clients actually book from) visually consistent regardless of how verbose
a given specialist's description is.

---

## PWA & Push Notifications

The cabinet installs as a home-screen app on both Android and iOS, backed
by the Web Push API for new-booking and daily-summary notifications.
Push requires the standard chain to actually work end to end: browser
support, user permission, and neither the OS nor the browser/PWA blocking
notifications at their own level — any one of those breaking silently
stops notifications, which is why it's the first thing checked when a
specialist reports missed alerts.

---

## Internationalization

The interface is fully localized via `next-intl` rather than having
translated strings bolted on — built for specialists and clients who don't
share a first language, which matters for a product used across several
European markets rather than a single domestic one.

---

## Data Integrity Notes

Migrations reflect real feature growth rather than a fixed initial schema
— contact-channel support (Viber, then a broader set of client contact
methods, then Facebook) and the service description field were each added
incrementally as the product evolved, without breaking existing booking
data. The booking snapshot pattern above is part of the same discipline:
schema changes that affect the catalog shouldn't retroactively rewrite
what already happened.

---

## Notes for Client Work

Fivesec is a working product with real specialists using it across
multiple countries today — not a demo. Adapting the underlying approach
for a different business would mean revisiting: which contact channels
matter for that market, localization for the target languages, branding
and booking-flow UX, notification channels beyond web push if the
audience needs them (SMS, email reminders), and integration needs specific
to that business (payments, calendar sync, etc.) that aren't part of the
current scope.
