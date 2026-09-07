# Travel tech: a learning path

How travel booking and operations systems actually work, written for engineers
who are about to build one.

Not a tutorial series and not a framework. It is the map of the domain — the
concepts, the vocabulary, and the specific things that go wrong — that nobody
hands you and that takes about three years to assemble by breaking things in
production.

---

## Who this is for

- An engineer who has just been handed a travel client and does not know what
  ATOL, NDC, PNR or TOMS mean
- A developer building a booking system for the first time, who has correctly
  sensed that this is harder than it looks
- Someone choosing a specialism and considering travel

It assumes you can already build a web application with a database. It does not
assume you know anything about travel.

## Who it is not for

If you want a tutorial that ends with a deployed app, this is the wrong
repository. There is very little code here. The hard part of travel software is
not the code — it is knowing which of the fourteen things a "booking" can mean
is the one your client means.

---

## The path

Work through in order. Each module is a single file, twenty to forty minutes of
reading, and ends with things to go and find out about your own client's
business.

### Part 1 — The shape of the industry

| | Module | What you will understand afterwards |
|---|---|---|
| 01 | [Who is who](modules/01-who-is-who.md) | Suppliers, aggregators, OTAs, DMCs, tour operators, TMCs and agents — and why the distinction changes everything about what you build |
| 02 | [What a booking actually is](modules/02-what-a-booking-is.md) | Why "booking" means at least four different things, and why conflating them is the most common architectural mistake in travel software |
| 03 | [Where the money is](modules/03-money-flows.md) | Commission, markup, net rates, merchant vs agency model, and why the answer determines your data model |

### Part 2 — The systems you will connect to

| | Module | What you will understand afterwards |
|---|---|---|
| 04 | [GDS, NDC and direct connects](modules/04-supply-and-apis.md) | How inventory reaches you, the vocabulary of each channel, and what to expect from their APIs |
| 05 | [Search, availability and caching](modules/05-search-and-caching.md) | Why travel search is a genuinely hard distributed systems problem, and the caching strategies that make it survivable |
| 06 | [Pricing and the disappearing fare](modules/06-pricing.md) | Why the price changes between search and book, what to do about it, and how to talk to customers about it |

### Part 3 — Building the thing

| | Module | What you will understand afterwards |
|---|---|---|
| 07 | [Modelling an itinerary](modules/07-itinerary-modelling.md) | A data model that survives a multi-city trip, a changed date and a partial cancellation |
| 08 | [The enquiry-to-quote gap](modules/08-enquiry-to-quote.md) | Where small operators actually lose money, and the highest-value system you can build for one |
| 09 | [Payments in travel](modules/09-payments.md) | Deposits, balance dates, chargebacks, virtual cards, and why travel is a high-risk merchant category |
| 10 | [Failure modes](modules/10-failure-modes.md) | The specific things that break at 2am in month nine, catalogued so you can design against them |

### Part 4 — The parts that are not code

| | Module | What you will understand afterwards |
|---|---|---|
| 11 | [Regulation you cannot ignore](modules/11-regulation.md) | ATOL, package travel rules, IATA, TOMS, and what happens if the system you built loses the evidence |
| 12 | [Working with operators](modules/12-working-with-operators.md) | How travel businesses actually run, why staff abandon the CRM you built, and what to ask in a first meeting |

### Appendix

- [Glossary](GLOSSARY.md) — every acronym, defined plainly
- [Further reading](FURTHER-READING.md) — where to go for authoritative detail
- [Practice projects](PRACTICE.md) — four builds, in increasing order of difficulty

---

## How to use it

**If you have a client waiting:** read 01, 02 and 08 today, then 12 before your
first meeting. Those four will stop you from designing the wrong thing.

**If you are learning the domain properly:** work through in order over two or
three weeks. Do the questions at the end of each module against a real
operator's website — they are answerable from outside, and answering them is
most of the skill.

**If you are stuck on something specific:** the [glossary](GLOSSARY.md) and
module 10 are the two most useful standalone documents.

---

## A note on where this comes from

This is written from building booking platforms and operations systems for
travel companies since 2019, and from co-owning a UK travel company — which
means having been on the receiving end of systems that made a Tuesday
impossible.

That second part matters more than the first. Most travel software is built by
people who have never watched a consultant fight the tool at 6pm with a customer
on hold. Several modules exist because of specific things that went wrong on our
side of the desk.

Corrections from people who work in travel are especially welcome. If something
here is wrong, or true in the UK and false in the Gulf, [open an issue](../../issues).

## Contributing

Genuinely useful contributions:

- **Regional differences.** This is UK and Gulf weighted. How things work in the
  US, EU, India or Southeast Asia would improve it considerably.
- **Corrections from operators.** If you run a travel business and a module
  misdescribes your reality, say so.
- **Worked examples.** Anonymised, real, with the numbers.

Please do not submit AI-generated module drafts. The value here is specificity
from experience, and that does not survive being generated.

## Licence

[CC BY 4.0](LICENSE) — use it, teach from it, translate it, build on it.
Attribution appreciated.

Written by [Codic Systems](https://codicsystems.com) — booking and operations
software for travel companies, Islamabad.
