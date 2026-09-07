# 10 · Failure modes

*Roughly 30 minutes. Read before you design, not after you ship.*

---

A catalogue of the specific things that break in travel systems, why they break,
and what to do about them. Most of these are obvious in hindsight and none of
them are obvious in advance.

---

## The price changed between search and book

**What happens:** the customer sees £1,240, clicks book, and the supplier returns
£1,310. Airline and hotel inventory is priced dynamically and the fare you cached
four minutes ago is gone.

**Why it hurts:** if you take the money at the old price you eat the difference.
If you show an error you lose the sale. If you silently charge the new price you
have a chargeback and possibly a regulator.

**What to do:** re-price immediately before payment, always. Show the change
explicitly with the old and new price and make the customer confirm. Keep the
quote's expiry short enough to be honest — a 30-day quote on a dynamic fare is a
promise you cannot keep.

## The supplier deadline passed quietly

**What happens:** a hotel held a room until 14 days before arrival. Nobody paid
the balance. The hold released. Nobody noticed until the customer arrived.

**Why it hurts:** this is the single most expensive failure in tour operating.
The operator either rebooks at walk-up rates or compensates a customer standing
in a lobby.

**What to do:** store the cancellation deadline as a **date field**, not as text
in a notes column. Then the alert is trivial: anything with a deadline inside
seven days and an unpaid balance goes on a dashboard and into somebody's inbox.
Operators will pay for this feature alone.

## Timezones ate the date

**What happens:** a flight departs 23:50 on the 14th local time. Stored as UTC,
rendered in the browser's timezone, it displays as the 15th. The customer
arrives a day late.

**Why it hurts:** travel is the domain where this genuinely ruins someone's
holiday.

**What to do:** **store local times with an explicit timezone identifier**, not
UTC alone, for anything a human will act on. A flight departure is
`2026-06-14T23:50` at `Europe/London`, and that pair is the truth. Convert for
display only when you know whose timezone you are converting into. Never let a
date-only field silently become a datetime at midnight.

## Two people booked the last room

**What happens:** two consultants quote the same allocation simultaneously. Both
book. One fails.

**What to do:** hold inventory at quote time if the supplier supports it, and
treat every reservation as provisional until the supplier confirms with a
reference. Never show "confirmed" in your UI on the strength of your own database
row.

## The passenger name does not match the passport

**What happens:** booked as "Mo Khan", passport says "Mohammed Ali Khan".
Airlines refuse travel or charge a change fee that can exceed the fare.

**What to do:** capture given names and surname as separate fields, exactly as
they appear in the travel document, and say so on the form. Validate against
obvious problems — no digits, plausible length. Then make the name confirmation
step deliberate: display it and require an explicit tick. This one is cheap to
prevent and brutal to fix.

## The webhook arrived twice

**What happens:** a payment provider or messaging platform redelivers a webhook
because your endpoint was slow to acknowledge. You take payment twice, or create
two enquiries.

**What to do:** every webhook handler must be **idempotent**. Store the provider's
event ID with a unique constraint and make reprocessing a no-op. Acknowledge fast,
process asynchronously.

## The supplier API changed without telling you

**What happens:** a field that was always present becomes optional. Your parser
throws. Bookings stop.

**What to do:** validate supplier responses at the boundary and fail loudly into
a queue rather than silently into a null. Alert on parse failures. Never assume a
field exists because it always has — travel APIs are notoriously casual about
versioning, and some are SOAP services older than your career.

## The PDF is the only record

**What happens:** the invoice, the ATOL certificate and the itinerary were
generated as PDFs and emailed. The underlying data changed. Now nobody knows what
the customer was actually told.

**What to do:** **generate documents from stored data, and store the generated
artefact too**, with a hash and a timestamp. When a customer says "your invoice
said £1,400", you can produce the exact file they received. This is also what a
regulator asks for.

## Everything was fine until 40 concurrent searches

**What happens:** each search fans out to eight suppliers with 3–8 second
response times. Forty concurrent users means 320 in-flight requests, connection
pools exhaust, the site stops.

**What to do:** cap concurrency per supplier, set aggressive timeouts, return
partial results rather than waiting for the slowest, and cache aggressively with
short TTLs. Travel search is a distributed systems problem wearing a search box.

## The consultant went back to the spreadsheet

**What happens:** you built a CRM. Six weeks later everyone is using Excel again.

**Why:** the system made the common case slower than the spreadsheet did.
Fourteen fields required when six would do; four clicks where one would do; no
keyboard entry; no bulk edit.

**What to do:** watch someone do the job before designing the form. Make the
ninety-per-cent path fast and let the rare case be slow. **A system nobody uses
is worse than no system**, because it also carries the data that is now half in
two places.

## It broke at 2am in month nine

**What happens:** something you did not monitor failed while you slept and the
client found out first.

**What to do:** error monitoring and uptime alerting from day one, not after the
first incident. Telling a client "I get alerted before you notice" during the
sales conversation is worth more than any portfolio piece — and it is only true
if you set it up.

---

## The test to apply before you accept any travel engagement

> **If this goes wrong at 2am in month four, do I know what to do?**

For a booking platform where you understand the domain, the answer should be
yes. For a system you would have to research before you could scope it, the
answer is no, and the right move is to say so and sell a discovery sprint
instead.

---

## Go and find out

1. Ask an operator about the worst thing a system did to them. You will get a
   real story, and it will be on this list.
2. Look at your own current project. Which three of these are you exposed to right
   now, and what would each cost?
3. Pick the cheapest one to fix and fix it this week.

**Next:** [11 · Regulation you cannot ignore](11-regulation.md)
