# Glossary

Every acronym you will meet in a travel project, defined plainly.

## Industry structure

| Term | Meaning |
|---|---|
| **OTA** | Online Travel Agency. Sells to consumers online — Booking.com, Expedia. |
| **TMC** | Travel Management Company. Handles corporate travel, with policy enforcement and reporting. |
| **DMC** | Destination Management Company. In-country specialist providing ground services to operators selling into that destination. |
| **Tour operator** | Assembles components into a package and sells it as one product, taking on the obligation to deliver it. Legally distinct from an agent. |
| **Travel agent** | Sells someone else's product for commission. Different legal obligations from an operator — this distinction matters and clients confuse it. |
| **Consolidator** | Buys airline capacity in bulk and resells to agents at net rates. |
| **Bedbank** | Wholesaler of hotel inventory to the trade — Hotelbeds, WebBeds. |

## Supply and distribution

| Term | Meaning |
|---|---|
| **GDS** | Global Distribution System. Amadeus, Sabre, Travelport. The legacy backbone of airline and hotel distribution. Powerful, expensive, and older than most of your stack. |
| **NDC** | New Distribution Capability. IATA's XML standard letting airlines distribute richer content directly, bypassing GDS limitations. Adoption is uneven and "NDC-enabled" means different things to different airlines. |
| **PNR** | Passenger Name Record. The reservation record in a GDS, identified by a six-character locator. |
| **Direct connect** | An API straight to a supplier, bypassing intermediaries. Better margins, more integrations to maintain. |
| **Allocation** | Inventory a supplier has pre-assigned to you, typically with a release deadline. |
| **Free sale** | Inventory you may sell without checking, up to agreed limits. |
| **Stop sale** | A supplier instruction to stop selling immediately. If your system cannot honour one quickly, you will oversell. |

## Money

| Term | Meaning |
|---|---|
| **Net rate** | What you pay the supplier. Your selling price is net plus markup. |
| **Commission model** | You sell at the supplier's price and receive a percentage back. |
| **Merchant model** | You take the customer's money and pay the supplier. More cash flow, more risk, more regulation. |
| **Markup** | What you add to net. May be percentage, fixed, tiered, or per component — model it as a rule, not a number. |
| **TOMS** | Tour Operators' Margin Scheme. A special UK VAT treatment taxing the margin rather than the full sale. Materially affects whether VAT on your invoice is recoverable by the operator. |

## Regulation

| Term | Meaning |
|---|---|
| **ATOL** | Air Travel Organiser's Licence. UK financial protection for flight-inclusive packages. An ATOL certificate must be issued to the customer, and the system that fails to produce one creates a compliance problem, not just a missing PDF. |
| **PTR** | Package Travel Regulations. Define what counts as a package and what the organiser owes the traveller. Combining two components can inadvertently create a package with obligations attached. |
| **IATA** | International Air Transport Association. Sets standards; accredits agents to issue tickets. |
| **BSP** | Billing and Settlement Plan. IATA's mechanism for settling between agents and airlines. |

## Operations

| Term | Meaning |
|---|---|
| **Itinerary** | The customer-facing sequence of what happens when. Distinct from the booking, which is the commercial record. |
| **Component** | One bookable element — a flight, a hotel stay, a transfer. The right unit for status and cancellation policy. |
| **Amendment** | A change after confirmation. Usually incurs supplier fees and always needs an audit trail. |
| **No-show** | The customer did not arrive. Typically fully chargeable, and needs to be distinguishable from a cancellation in your data. |
| **Rooming list** | Who is in which room. Sent to hotels ahead of arrival for group bookings, and a common source of manual work worth automating. |
| **Manifest** | The list of travellers on a departure. |
