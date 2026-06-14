# Travelport GraphQL Schema

## Overview

Travelport operates a global travel commerce platform that connects travel providers (airlines, hotels, car rental companies, rail operators) with online and offline travel agencies. Its core systems — Galileo, Apollo, and Worldspan — collectively form one of the largest Global Distribution Systems (GDS) in the world. The TripServices REST/JSON API (v11+) exposes end-to-end travel workflows covering air, stays, car, rail, and payments.

This conceptual GraphQL schema models the Travelport TripServices API surface across all major travel verticals: air (search, price, book, ticket, cancel, exchange), stays (search, availability, reserve, modify), payments (authorization, 3D Secure, reversal), and agency/profile management. It reflects both GDS and NDC content from 400+ airlines and 180+ countries of hotel coverage.

## Schema Source

- Developer Portal: https://developer.travelport.com/
- Flights API: https://developer.travelport.com/apis/flights
- Stays API: https://developer.travelport.com/apis/stays/12.1.2
- Pay API: https://developer.travelport.com/apis/pay
- Getting Started: https://developer.travelport.com/getting-started
- Downloads / DevKits: https://developer.travelport.com/downloads
- Support: https://developer.travelport.com/support
- LLMs.txt: https://developer.travelport.com/llms.txt

## Core Verticals

### Air (Flights)
Search, price, book, ticket, cancel, and exchange air travel across GDS and NDC content. The workbench-based booking flow separates availability search, offer pricing, passenger data collection, payment, and ticketing into discrete steps. Single-payload booking is also supported for simpler integrations.

### Stays (Hotels)
Search hotel availability by coordinates, address, airport/city code, or property ID. Retrieve room offers, rate plans, rules, and policies. Create, retrieve, modify, and cancel hotel reservations. Supports passive segment bookings for external/non-GDS suppliers.

### Pay (Payments)
Credit card authorizations, address validations, 3D Secure (3DS) transactions, and reversals against designated merchant vendors. Handles PCI-compliant payment processing integrated into the booking flow.

## Key Concepts

- **Session / Token**: OAuth 2.0 bearer tokens authenticate API calls. Sessions maintain stateful workbench contexts for multi-step booking flows.
- **Workbench**: A server-side booking workspace that accumulates offers, passengers, payments, and remarks before committing a booking.
- **Offer**: A priced, bookable travel product (air offer, hotel offer) combining segments, fares, taxes, and fees.
- **Booking / PNR**: The confirmed reservation record stored in the GDS, identified by a locator/PNR code.
- **Fare Basis / NDC**: GDS fares use IATA fare basis codes; NDC fares are sourced directly from airline distribution systems and may include additional branded fare attributes.
- **Loyalty**: Frequent flyer / hotel loyalty programme numbers stored on passenger profiles or passed per-booking.

## Types Summary

| Category | Types |
|---|---|
| Booking | Booking, BookingDetails, BookingStatus |
| Air | Air, AirDetails, AirOffer, AirSegment, SegmentDetails, Availability, Connection, Stopover |
| Fare | Fare, FareDetails, FareBasis, FareRules, FareBreakdown, Fee, Tax |
| Passenger | Passenger, PassengerDetails, PassengerType, ContactDetails, Document, DocumentDetails |
| Hotel | Hotel, HotelDetails, HotelProperty, HotelOffer, RoomDetails, Rate, RatePlan |
| Car | Car, CarDetails, CarSupplier, CarRates |
| Rail | Rail, RailDetails, RailSegment, Journey, JourneyDetails |
| Ticket | Ticket, TicketDetails |
| Payment | Payment, PaymentDetails, PaymentCard, CreditCard |
| Search | SearchResult, SearchCriteria |
| Content | Content, ContentDetails |
| Profile | Profile, ProfileDetails, Loyalty, LoyaltyDetails |
| Agency | Agency, AgencyDetails |
| System | Queue, Notification, APIKey, Token, Session |

## Queries

- `searchAir(criteria: SearchCriteria!)`: Search for available air offers.
- `getAirOffer(offerId: ID!)`: Retrieve a specific priced air offer.
- `searchHotel(criteria: SearchCriteria!)`: Search for hotel availability.
- `getHotelOffer(offerId: ID!)`: Retrieve a specific hotel room offer.
- `getBooking(locator: String!)`: Retrieve a booking by PNR locator.
- `getTicket(ticketNumber: String!)`: Retrieve ticket details.
- `getProfile(profileId: ID!)`: Retrieve a traveller profile.
- `getAgency(agencyId: ID!)`: Retrieve agency details.
- `listQueues(agencyId: ID!)`: List agent work queues.

## Mutations

- `createBooking(input: BookingInput!)`: Create a new booking/PNR.
- `cancelBooking(locator: String!)`: Cancel a booking.
- `ticketBooking(locator: String!)`: Issue tickets for a booked itinerary.
- `authorizePayment(input: PaymentInput!)`: Authorize a payment card.
- `reserveHotel(input: HotelInput!)`: Create a hotel reservation.
- `cancelHotelReservation(locator: String!)`: Cancel a hotel reservation.
- `createProfile(input: ProfileInput!)`: Create a traveller profile.
- `updateProfile(profileId: ID!, input: ProfileInput!)`: Update a traveller profile.
