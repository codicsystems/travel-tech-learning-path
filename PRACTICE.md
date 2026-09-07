# Practice projects

Four builds in increasing order of difficulty. Each one teaches something the
modules can only describe.

Do them against real operator websites — the information is public and reading
it carefully is most of the skill.

---

## 1 · The enquiry form audit

**Half a day. Do this one even if you do no others.**

Pick fifteen tour operators. Go through each enquiry form as a customer and
record: number of fields, whether price information appears before the form,
whether a phone number is required, how long until a human replies.

**You will produce:** a spreadsheet, and the single best cold outreach opener
available to you — a specific, accurate, non-insulting observation about that
operator's own funnel.

**You will learn:** what the industry standard actually is, rather than what you
assume it is.

## 2 · The quote document generator

**Two to three days.**

Build something that takes structured trip data — components, prices, passengers,
dates — and produces a branded quote PDF with a per-component breakdown, a total,
a deposit amount, a balance due date, and an expiry.

**Constraints that make it real:** prices must be stored as net, markup and tax
separately. The document must be regenerable from data. Store the generated file
with a hash.

**You will learn:** why storing a price as one number fails, and how documents
become evidence.

## 3 · The deadline watcher

**Three to four days.**

Model bookings with components, each with a supplier reference, a cancellation
deadline and a penalty. Model payments with a deposit and a balance due date.
Then build the dashboard and the alert: which bookings have a supplier deadline
inside seven days and an unpaid balance.

**You will learn:** the derived-status problem from module 02, and why this
single feature is one an operator will pay for on its own.

## 4 · The multi-supplier search

**One to two weeks. Genuinely hard.**

Build a search that queries three mock suppliers with deliberately awful
characteristics: one responds in 300ms, one in 6 seconds, one fails 20% of the
time. Return merged, de-duplicated, sorted results.

**Constraints:** cap concurrency per supplier. Return partial results rather than
waiting for the slowest. Cache with a short TTL and show the user how fresh the
data is. Re-price before booking and handle the price having changed.

**You will learn:** why travel search is a distributed systems problem, and why
every travel site you have used feels slightly slow.

---

## What to do with them

Numbers 1 and 3 are portfolio pieces that a travel operator will immediately
understand. Number 4 is the one that will get you hired by an agency.

Write up what you learned. A short post about what fifteen enquiry forms taught
you is more likely to start a client conversation than any amount of framework
knowledge.
