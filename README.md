# Payment Service API - README

## Overview
The **Payment Service API** is part of a movie reservation system that allows users to make payments for their reservations. This API provides an endpoint for processing payments securely by taking in payment details such as card number, expiration date, and CVV.

## Assignment Objectives
This assignment is focused on designing an OpenAPI specification for a payment service within a movie ticket booking system. The goal is to define the process of interacting with the API for handling payments, including the required request and response data structures.

## API Specifications

### OpenAPI Version
- **Version**: 3.0.0

### Basic Information
- **Title**: Payment Service API
- **Version**: 1.0.0
- **Description**: API for making a payment for a movie reservation.

## Endpoints

### 1. Make Payment for Reservation
- **Endpoint**: `/reservations/{reservationId}/payment`
- **Method**: `POST`
- **Summary**: Allows a user to make a payment for an existing movie reservation.

#### Parameters
- **Path Parameter**:
  - `reservationId` (string): The ID of the reservation for which payment needs to be made.
  
  **Example**: `reservationId: 12345`

#### Request Body
- **Required**: Yes
- **Content Type**: `application/json`
- **Schema**:
  - **paymentDetails** (object): Contains the payment details:
    - `cardNumber` (string): The card number for payment.
    - `expiryDate` (string): The expiration date of the card.
    - `cvv` (string): The CVV code of the card.
  
  **Example**:
  ```json
  {
    "paymentDetails": {
      "cardNumber": "4111111111111111",
      "expiryDate": "12/24",
      "cvv": "123"
    }
  }
  ```

#### Responses
- **200 OK**: Payment has been successfully processed.
  - **Content Type**: `application/json`
  - **Schema**:
    - `bookingId` (string): The ID of the confirmed booking.
    - `eTicket` (string): The e-ticket for the booking.
  
  **Example**:
  ```json
  {
    "bookingId": "abc123",
    "eTicket": "ETICKET-123456789"
  }
  ```

- **400 Bad Request**: Payment failed or invalid details were provided.

  **Example**:
  ```json
  {
    "error": "Invalid card details. Please check and try again."
  }
  ```

- **404 Not Found**: The reservation was not found.

  **Example**:
  ```json
  {
    "error": "Reservation with ID 12345 not found."
  }
  ```

## How to Use
To use the Payment Service API:
1. Send a `POST` request to `/reservations/{reservationId}/payment`.
2. Provide the `reservationId` in the URL path and include the necessary payment details in the request body.
3. Handle responses according to the status code returned.

### Example Request
```http
POST /reservations/12345/payment
Content-Type: application/json

{
  "paymentDetails": {
    "cardNumber": "4111111111111111",
    "expiryDate": "12/24",
    "cvv": "123"
  }
}
```

### Example Successful Response
```json
{
  "bookingId": "abc123",
  "eTicket": "ETICKET-123456789"
}
```

## Additional Notes
- Ensure that the `reservationId` is valid and corresponds to an existing reservation.
- All payment details must be accurate, and card information must be handled securely.
- It is recommended to use encryption for sensitive data like card numbers and CVV to ensure security.
