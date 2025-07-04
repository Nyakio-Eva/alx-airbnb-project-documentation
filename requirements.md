
# Backend Feature Specifications – Airbnb Clone

This document outlines the detailed specifications for three core backend features: User Authentication, Property Management, and Booking System.

## 1.User Authentication

### Features
- User registration (guest or host)
- Login/logout
- JWT-based authentication
- Password hashing and validation

### API Endpoints

#### POST /auth/register
- **Description**: Register a new user (guest or host)
- **Input**:
```json
{
  "email": "user@example.com",
  "first_name": "Evaly",
  "last_name": "Nyaks",
  "phone_number": "72987890",
  "password": "securePassword123",
  "role": "guest",  // or "host"
  "created_at": "12:0001-07-2025"
}
```
- **Output**:
```json
{
  "message": "User created successfully",
  "user_id": "uuid",
  "token": "jwt_token_here"
}
```
- **Validation**:
  - Email must be unique and valid format
  - Password must be at least 8 characters

---

#### POST /auth/login
- **Description**: Authenticate a user
- **Input**:
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```
- **Output**:
```json
{
  "token": "jwt_token_here"
}
```
- **Validation**:
  - Credentials must match
  - Return 401 on failure

---

## 2. Property Management

### Features
- Create property listing (host only)
- View property listings
- Update or delete own listings

### API Endpoints

#### POST /properties/
- **Description**: Add a new property listing
- **Input**:
```json
{
  "name": "Beach House",
  "description": "Cozy beachfront stay.",
  "location": "Mombasa, Kenya",
  "price_per_night": 45.00,
  "amenities": ["WiFi", "AC", "Kitchen"],
  "created_at":"12:3002-08-2024"
}
```
- **Output**:
```json
{
  "property_id": "uuid",
  "message": "Property listed successfully"
}
```
- **Validation**:
  - Host must be authenticated
  - Fields required: name, location, price

---

#### GET /properties/
- **Description**: Retrieve all listings (with filters)
- **Query Params**: location, price range, amenities
- **Output**:
```json
[
  {
    "id": "uuid",
    "name": "Beach House",
    "price": 45.00
  }
]
```

---

## 3. Booking System

### Features
- Book available properties for specific dates
- Cancel bookings
- Track booking status

### API Endpoints

#### POST /bookings/
- **Description**: Create a booking
- **Input**:
```json
{
  "property_id": "uuid",
  "start_date": "2025-08-01",
  "end_date": "2025-08-03",
  
}
```
- **Output**:
```json
{
  "booking_id": "uuid",
  "status": "confirmed",
  "total_price": 90.00
}
```
- **Validation**:
  - Property must be available
  - Date range must be valid (start < end)

---

#### GET /bookings/status
- **Description**: View user’s booking history/status
- **Output**:
```json
[
  {
    "booking_id": "uuid",
    "property_id": "uuid",
    "status": "confirmed",
    "date": "2025-08-01"
  }
]
```

## Performance Criteria
- API response time ≤ 200ms for read operations
- Handle at least 100 concurrent users
- Cache frequent GET requests (e.g., /properties)
- Paginate results for large datasets



