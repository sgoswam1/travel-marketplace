# COPILOT_PROMPTS.md

This document contains detailed, ready-to-use code generation prompts for Cursor IDE / GitHub Copilot, organized by epic within the `sgoswam1/travel-marketplace` project.

## 1. Database Schema

### Specifications
- Design a relational database schema to support the core functionalities of the travel marketplace application.

### Prompts
```plaintext
// Prompt for generating the database schema
// Types of entities: Trip, User, Itinerary, Bid, Payment
// Relationships:
// - User can have multiple Trips
// - Trip has one Itinerary and multiple Bids
// - Bid has one Payment

CREATE TABLE Users (
    UserId INT PRIMARY KEY,
    UserName VARCHAR(255) NOT NULL,
    Email VARCHAR(255) NOT NULL,
    PasswordHash VARCHAR(255) NOT NULL
);

CREATE TABLE Trips (
    TripId INT PRIMARY KEY,
    UserId INT,
    StartDate DATE,
    EndDate DATE,
    FOREIGN KEY (UserId) REFERENCES Users(UserId)
);

CREATE TABLE Itineraries (
    ItineraryId INT PRIMARY KEY,
    TripId INT,
    Details TEXT,
    FOREIGN KEY (TripId) REFERENCES Trips(TripId)
);

CREATE TABLE Bids (
    BidId INT PRIMARY KEY,
    TripId INT,
    UserId INT,
    Amount DECIMAL(10, 2),
    FOREIGN KEY (TripId) REFERENCES Trips(TripId),
    FOREIGN KEY (UserId) REFERENCES Users(UserId)
);

CREATE TABLE Payments (
    PaymentId INT PRIMARY KEY,
    BidId INT,
    Status VARCHAR(50),
    FOREIGN KEY (BidId) REFERENCES Bids(BidId)
);
```

### Deliverables Checklist
- [ ] Complete database schema SQL scripts
- [ ] Entity-Relationship Diagram (ERD)

### Acceptance Criteria
- The schema must support all specified functionalities.
- Relationships should be accurately represented.

## 2. Backend API

### Specifications
- Design the API endpoints to handle requests for Trips, Itineraries, Bids, and Payments.

### Prompts
```plaintext
// Prompt for generating backend API for handling Trips
// Create RESTful API endpoints:
// - GET /api/trips
// - POST /api/trips

[HttpGet]
public IEnumerable<Trip> GetTrips() {
    // Implementation here
}

[HttpPost]
public IActionResult CreateTrip(Trip trip) {
    // Implementation here
    return CreatedAtAction(nameof(GetTrip), new { id = trip.TripId }, trip);
}
```

### Deliverables Checklist
- [ ] Comprehensive API specification (OpenAPI/Swagger)
- [ ] Endpoint implementation.

### Acceptance Criteria
- All API endpoints must be functioning as expected.
- Validation and error handling implemented.

## 3. React Frontend

### Specifications
- Create UI components for managing Trips, Bids, and Payments in React.

### Prompts
```plaintext
// Prompt for generating a React component for Trip List
import React from 'react';

const TripList = () => {
    const [trips, setTrips] = React.useState([]);

    React.useEffect(() => {
        // Fetch trips from API
    }, []);

    return (
        <ul>{trips.map(trip => <li key={trip.TripId}>{trip.Details}</li>)}</ul>
    );
};

export default TripList;
```

### Deliverables Checklist
- [ ] Complete set of UI components
- [ ] Integrated with backend API

### Acceptance Criteria
- All UI components should render correctly.
- Proper state management used.

## 4. Infrastructure/DevOps

### Specifications
- Set up Docker and CI/CD workflows for deployment.

### Prompts
```plaintext
// Dockerfile for .NET Core API
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
COPY . .
EXPOSE 80

// Prompt for CI/CD GitHub Actions
name: CI
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Build
        run: dotnet build
```

### Deliverables Checklist
- [ ] Docker setup completed
- [ ] CI/CD pipeline configured

### Acceptance Criteria
- Application must run smoothly in Docker.
- CI/CD should trigger on code push.

## 5. Documentation

### Specifications
- Create comprehensive documentation for developers and end-users.

### Prompts
```plaintext
// Prompt for generating documentation outline
# Travel Marketplace API Documentation

## Introduction

## API Endpoints
- [ ] Trip Management
- [ ] User Authentication

## Setup Instructions
1. Clone the repository
2. Run `docker-compose up`
```

### Deliverables Checklist
- [ ] User documentation complete
- [ ] Developer API documentation complete

### Acceptance Criteria
- All sections must be covered in detail.
- Documentation must be easy to follow and free of errors.