# 02 · What a booking actually is

*Roughly 25 minutes. The single most important module here.*

---

If you take one thing from this repository, take this: **"booking" means at
least four different things, and conflating them is the most common
architectural mistake in travel software.**

An engineer hears "booking" and models one table called `bookings`. Six months
later the client asks a question that table cannot answer, and the answer is a
rewrite.

## The four things

### 1. The enquiry

Somebody has expressed interest. Nothing is reserved, nothing is owed, no
supplier knows this person exists. There may be no dates, no names, no firm
destination.

Lifespan: hours to months. Most die.

### 2. The quote

The operator has priced something specific. It has an expiry, because the prices
underneath it move. There may be several quotes for one enquiry — three hotel
options, two date ranges — and the customer may accept one, none, or ask for a
fifth.

Lifespan: days to weeks. Expires by design.

### 3. The reservation

A supplier has held inventory. A hotel has blocked a room; an airline holds
seats under a PNR. This has a **deadline**, and the deadline is not negotiable —
miss it and the hold silently evaporates.

Critically: a reservation may exist **with no money taken**, and money may have
been taken **with no reservation confirmed**. Both happen constantly.

### 4. The booking

The customer is committed, money has moved, and the operator has an obligation
to deliver. This is the thing with legal consequences, the thing that appears in
accounts, and the thing regulation cares about.

---

## Why one table cannot hold all four

The relationships are not one-to-one in any direction:

- One enquiry → many quotes
- One quote → one booking, or none
- **One booking → many reservations.** A two-week trip might be four flights,
  three hotels, two transfers and an excursion, each with its own supplier, own
  confirmation reference, own cancellation deadline and own cancellation penalty.
- **One reservation → many passengers**, who may not all be on the same segments

And the state transitions are not linear. A booking can be confirmed, then have
one hotel cancelled and replaced, while the flights are untouched and the
customer has paid a deposit but not the balance.

Ask yourself: *what is the status of that booking?* There is no single correct
answer, which tells you a single `status` column on a single table is the wrong
model.

## The shape that works

```
enquiry
  └── quote (many, each versioned, each with an expiry)
        └── booking (0 or 1)
              ├── traveller (many)
              ├── component (many)  ← flight, hotel, transfer, excursion
              │     └── reservation (supplier ref, deadline, cancellation policy)
              └── payment (many: deposit, balance, refund, supplement)
```

**The component is the unit that matters.** Status lives on components, not on
the booking. The booking's status is *derived* — a booking is confirmed when all
its components are confirmed, partially confirmed when some are, at risk when a
reservation deadline is approaching and the customer has not paid.

Deriving it is more work. It is also the only version that can answer "which
bookings have a supplier deadline in the next 48 hours and no balance payment?",
which is the question that actually keeps operators awake.

## Versioning quotes, and why

A quote is a **statement of price at a point in time**. When the customer comes
back after ten days and the hotel has gone up, you need to show them a new quote
without destroying the old one — because they will say "you told me £1,400" and
you need to be able to say "on the 3rd, yes, and here is what changed."

Never update a quote in place. Supersede it.

The same applies to bookings after amendment. The customer changed their return
flight; you need both the original and the amended version, with a record of who
changed what and when. Immutability is not architectural purism here — it is how
you win an argument with a customer, and how you satisfy a regulator.

## The mistakes, ranked by how much they cost

**1. One `bookings` table with a `status` enum.** Cannot represent a partially
confirmed trip. Discovered in month four.

**2. Storing a price as a single number.** A price is a net cost, a markup, taxes,
fees, a currency, and an exchange rate at a moment. Store the components — you
will need to answer "what did we actually make on this?" and "why is this
different from last time?"

**3. No supplier reference on components.** When a hotel says "we have no record
of this", the supplier's own reference is the only thing that resolves it.

**4. Treating cancellation policy as text.** "Free cancellation until 14 days
before arrival" is a *rule* with a date and a penalty. Stored as prose, no system
can warn anyone. Stored as a date and an amount, you can build the alert that
saves the operator thousands.

**5. Assuming passengers equal payers.** The person paying is frequently not
travelling. A parent books for adult children; a company books for staff. Model
the payer separately or the invoicing will be wrong.

---

## Go and find out

For an operator you know, or one whose website you can read:

1. When they say "booking", which of the four do they mean? Ask them to walk you
   through one from first contact to departure and count the state changes.
2. What is the longest gap between deposit and balance? That gap is where their
   cash sits and where their risk lives.
3. What happens when a customer changes one flight on a six-component trip? Who
   does what, in what order, and where is it recorded?
4. Ask what happens when a supplier deadline is missed. If the answer involves a
   spreadsheet or someone's memory, you have found your first project.

**Next:** [03 · Where the money is](03-money-flows.md)
