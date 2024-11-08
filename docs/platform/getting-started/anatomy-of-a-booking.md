Anatomy of a Booking
====================

## Bookings

A _booking_ is the root element for a sale.
Bookings are comprised of:

* A sale currency, which determines the currency used for 
* A reference, which provides an alternate means to directly address the booking
* A status, which provides a top-level indication of the booking's current state
* An optional customer profile as the primary contact point for the booking
* Reservations which compose the services and goods which are being sold
* Transactions which record any payments made against the booking

## Customers

A _customer_ holds a persistent profile between bookings.
A customer may be either a direct consumer or a third party agent. It represents
the primary contact point for the sale.

The customer may be a passenger who is
travelling on the booking or may be a non-passenger individual, a sales agent,
or another type of partner.

## Reservations

A _booking_ is comprised of _reservations_. Each reservation represents an 
atomic line item for a specific _product_. Each has its own status and workflow,
and may have zero or more _passengers_ assigned to it.
The number of passengers which may be assigned to a reservation is determined by
the _occupancy_ range of the associated product.

Reservations often have _service dates_, these are the specific dates that the
services of the associated product will be rendered to the assigned passengers.

Reservations have a fixed workflow which represents their lifecycle.
The state transitions available on a reservation depend on its current state
as well as validity checks for it to be moved to a new state.

## Passengers

A _passenger_ represents an individual person receiving services as part of a
single booking. Passengers are specific to an individual booking, but may be
associated with a customer to create a profile across multiple bookings.

Passengers can contain detailed information relevant to the booking and the
reservations on which the passenger is assigned.

## Products

_Products_ are all things which can be bought, sold, and reserved. 
A product can be anything from a package tour, a stay in a hotel, a flight,
merchandise, or a discount. 

All "types" of product in RezKit are represented as products, which depending
on their type may have additional data or behaviours.

## Product Providers

Most products within RezKit originate from _product providers_. These are
external systems which are connected to RezKit via a standardized communication
interface.
This allows RezKit to query the provider about the products they
offer, request reservations for those products, and make further requests on
those reservations.

:::note
When a reservation is on a product which belongs to a provider, the reservation
is owned by the provider. This means that while RezKit can make _requests_ to
modify or cancel the reservation, it is the _provider_ and only the provider
which decides if the request is accepted.
:::

You can find more detail about how 
product providers work in our [detailed guide](../product-provider/introduction)


## Transactions

A _transaction_ represents a payment made in relation to the receivable account
of the booking. 

Each booking is a receivable account with a balance which is determined by the
sum of the sale prices for all reservations which are in the **confirmed** 
state.

When a payment is made towards the sale price of the booking, it is recorded as
a transaction. These transactions also include refunds and account adjustments.