# 08 · The enquiry-to-quote gap

*Roughly 30 minutes. The highest-value system you can build for a small operator.*

---

Ask a tour operator where they lose money and they will say marketing costs, or
supplier margins, or a competitor undercutting them.

Watch them work for a day and you will see something different: **enquiries
arriving faster than quotes go out.** Not lost to price — lost to latency.

## The economics

A small operator receives an enquiry through a web form, WhatsApp, Instagram, a
phone call and email — five channels, no shared inbox. A consultant picks it up,
reads it, works out what is missing, replies asking, waits, receives an answer,
opens a supplier portal, checks three options, copies prices into a spreadsheet,
applies markup, writes a quote in Word, converts to PDF, emails it.

Elapsed: often a day, sometimes three over a weekend.

Meanwhile the customer messaged four operators. The one who replied in two hours
has already had the conversation.

The numbers most operators do not track but will recognise:

- **Enquiry-to-first-response time** — the single strongest predictor of
  conversion in the segment
- **Enquiries per consultant per day** — usually far below what they think
- **Quotes per enquiry** — how many die before anyone priced anything
- **Time per quote** — often 25–45 minutes of skilled labour

Twenty-five minutes at, say, £22 an hour of loaded cost, on a quote that
converts one time in five, is roughly £45 of labour per booking spent on
assembling documents. That is before anyone sells anything.

## What to build, in order of return

### 1. One inbox

Before anything clever. Every channel lands in one place, with a status and an
owner. Most operators do not have this, and it is the reason enquiries are
missed rather than lost.

This is unglamorous, takes days rather than weeks, and is frequently the highest
return work you will ever do for them.

### 2. Structured capture

Turn free text into fields: destination, dates, passengers, budget, trip type.
This is where a language model genuinely earns its place — extraction is a task
models are reliable at.

Two rules. **Never guess a missing field** — null is a fine answer and a
fabricated destination is not. And **never let the model quote**; extraction and
pricing are different jobs, and only one of them can create a legal obligation.

### 3. The gap-filling reply

Most enquiries are missing something. An automated reply that asks *only* for
what is actually missing — not a generic form — recovers hours per week and
markedly improves response time metrics.

The template matters more than the technology. "To put some options together I
just need to know roughly when you'd like to travel and how many of you there
are" converts far better than a link to a form.

### 4. Quote assembly

Not automated pricing — **assisted** pricing. The consultant picks components;
the system applies the markup rules, calculates totals, generates the document
and sends it. Twenty-five minutes becomes four.

Resist the urge to automate the choosing. Which hotel suits a family with a
four-year-old is judgement, and it is the part of the job the consultant is
actually good at. Automate the typing, not the thinking.

### 5. Follow-up

Quotes expire. Most operators never chase. A scheduled sequence — day 2, day 5,
day 12, each with a reason to make contact rather than "just following up" —
recovers a meaningful share of quotes that would otherwise die silently.

## What not to build

**Full self-service booking for a complex-itinerary operator.** They exist
precisely because their product does not fit a booking engine. Building them one
is building the thing that put them out of business.

**A price comparison across suppliers**, unless they already have API access to
all of them. Screen-scraping supplier portals breaks constantly and usually
violates the terms they signed.

**An AI agent that talks to customers unsupervised.** In travel, an invented
price or availability claim is a consumer-law problem, not an embarrassing
screenshot.

---

## How to sell this

This is the easiest engagement to sell in travel software, because the pain is
felt daily and the arithmetic is arguable in one sentence.

The move that works: go through their public enquiry form *as a customer*, note
one specific thing — nine of eleven UK operators ask for a phone number before
telling you anything about price — and open with that observation rather than a
pitch. It proves you looked, and it starts the conversation on their problem
rather than your service.

Then scope it as a **paid discovery sprint** before quoting a build. Anyone
unwilling to pay to have the problem properly mapped was never going to sign the
build.

---

## Go and find out

1. Time your own enquiry. Send one to three operators on a Friday evening and
   record when each replies. That is your opening line for all three.
2. Count the fields on their enquiry form. More than six and they are losing
   people at the form.
3. Ask an operator how many enquiries they received last month. If they cannot
   answer, that is the project.
4. Ask what happens to a quote nobody replies to. If the answer is "nothing",
   there is money on the floor.

**Next:** [09 · Payments in travel](09-payments.md)
