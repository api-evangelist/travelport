# Travelport (travelport)

A global travel technology company connecting travel providers with online and offline travel agencies. Operates a commerce platform facilitating airline, hotel, and car rental bookings through its Galileo, Apollo, and Worldspan systems.

**URL:** [https://www.travelport.com/](https://www.travelport.com/)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=travelport-api-evangelist&utm_content=repo)

## Tags:

 - Travel, Travel Technology, Reservations, GDS, NDC, Flights, Hotels, Payments

## Timestamps

- **Created:** 2026-05-05
- **Modified:** 2026-05-16

## APIs

Travelport publishes its modern REST/JSON API suite at the **TripServices** developer portal: https://developer.travelport.com/

- **TripServices Flights API** — End-to-end air workflows (search, price, book, ticket, cancel, exchange) across GDS and NDC content. https://developer.travelport.com/apis/flights
- **TripServices Stays API** — Hotel search, availability, booking, and modification across 180+ countries. https://developer.travelport.com/apis/stays/12.1.2
- **TripServices Pay API** — Credit-card authorizations, address validation, 3D Secure transactions, and reversals (v11.33.0). https://developer.travelport.com/apis/pay

### Servers

- **Production:** `https://api.travelport.net/11`
- **Sandbox:** `https://api.pp.travelport.net/11`

### Authentication

All TripServices APIs use bearer token (JWT) authentication via the `Authorization: Bearer <token>` header.

### Access

Developers can request a trial via the developer portal or contact Travelport sales for enterprise access. A legacy developer portal remains available for existing integrations.

