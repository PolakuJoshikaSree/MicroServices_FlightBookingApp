# Flight Booking Microservices System

A scalable microservices-based flight booking application supporting One-Way and Round-Trip bookings.
Built using Spring Boot WebFlux (Reactive), MongoDB, Eureka Discovery, API-Gateway, Feign Client and Resilience4J.

---

## Project Architecture

📦 MicroServices_FlightBookingApp  
│  
├── flight-service       (8081)  
├── booking-service      (8082)  
├── api-gateway          (8080)  
└── eureka-server        (8761)  

---

## Technologies Used

| Component | Technology |
|---------|------------|
| Framework | Spring Boot WebFlux |
| Database | MongoDB |
| Discovery | Eureka Server |
| Communication | Feign Client |
| Routing | API Gateway |
| Resilience | Resilience4J Circuit Breaker |

---

## How to Run

1. Start `eureka-server` (http://localhost:8761)  
2. Start `flight-service`  
3. Start `booking-service`  
4. Start `api-gateway`  
5. Send all requests via Gateway → `http://localhost:8080/...`

---

## API Gateway Routing

| Gateway URL | Target Service |
|-------------|----------------|
| /flights/** | flight-service |
| /booking/** | booking-service |

---

# Flight Service APIs

### Add Flight  
POST → `http://localhost:8080/flights/add`
```json
{
  "flightName": "Air India Express",
  "fromCity": "HYD",
  "toCity": "DEL",
  "date": "2025-12-25",
  "totalSeats": 50,
  "availableSeats": 50,
  "tripType": "ONE_WAY"
}
```

### Search Flights  
GET → `http://localhost:8080/flights/search?from=HYD&to=DEL&date=2025-12-25`

---

# Booking Service APIs

### ONE-WAY Booking  
POST → `http://localhost:8080/booking/book`
```json
{
  "tripType": "ONE_WAY",
  "flightIdOnward": "FL001",
  "seatNumbersOnward": ["A1","A2"],
  "userName": "Joshika",
  "email": "joshika@mail.com",
  "passengers":[
    {"name":"Neha","age":21,"gender":"F"},
    {"name":"Riya","age":20,"gender":"F"}
  ],
  "meal": true,
  "journeyDate": "2025-12-25"
}
```

### ROUND-TRIP Booking  
```json
{
  "tripType": "ROUND_TRIP",
  "flightIdOnward": "FL001",
  "flightIdReturn": "FL002",
  "seatNumbersOnward": ["A1","A2"],
  "seatNumbersReturn": ["B1","B2"],
  "userName": "Joshika",
  "email": "joshika@mail.com",
  "passengers":[{"name":"Neha","age":21,"gender":"F"}],
  "meal": true,
  "journeyDate": "2025-12-25",
  "returnDate": "2026-01-02"
}
```

### Get Booking by PNR  
GET → `http://localhost:8080/booking/pnr/{pnr}`

### Booking History  
GET → `http://localhost:8080/booking/history/{email}`

### Cancel Ticket  
DELETE → `http://localhost:8080/booking/cancel/{pnr}`

---

## MongoDB Collections

| Service | Collection |
|--------|------------|
| flight-service | flights |
| booking-service | bookings |

---

## Features

- One-Way and Round-Trip support  
- PNR Generation  
- Seat Locking while booking  
- Cancel booking + seat restore  
- History search by email  
- Centralized gateway routing  
- Circuit-breaker resilience

---

## Author

Joshika Sree Polaku  
Microservices Flight Booking System (Backend)
