# Payflow Payment API Documentation
A REST API for processing and managing online payments.
## Overview
This API allows developers to securely create and manage payments transactions programmatically.
This API is designed for :
- Accepting customer payments
- Tracking payment status
- Managing transactions records
## Base URL
https://api.payflow.com/v1
## Authentication
All endpoints require a Bearer token in the request header. Include your API key as shown below:
### Authorization
Authorization: Bearer YOUR_API_KEY
Keep your API key secure. See Best Practices for more details
## Headers
| Key          | Value             |
|--------------|-------------------|
|Content-Type  |application/json   |
|Authorization | Bearer {token}    |
## Endpoints
### Create Payments
Endpoint: /payments
Method: POST
Description: Creates a new payment transaction
#### Example Request
**HTTPS Request**: POST/payments
**cURL Example**
```bash
curl -X POST \
https://api.payflow.com/v1/payments/ \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "content-Type: application/json" \
-d '{
     "amount": 5000,
     "currency": "NGN",
     "customer_id": "001"
     }

```
#### Response (201 Created)
```json
{
    "id": "pay_001",
    "amount": 5000,
    "currency" : "NGN",
    "createdAt": "2026-03-29T10:00:00Z"
}
```
### Get Payment Status
Endpoint: /payments/{id}
Method: GET
Description: Retrieves the status of a payment.
#### Example Request
**HTTPS Request**: GET /payments/pay_001
**cURL Example**
```bash
curl -X GET
https://api.payflow.com/v1/payments/pay_001/ \
-H "Authorization: Bearer YOUR_API_KEY" 
```
#### Response (200 OK)
```json
{
    "id": "pay_001",
    "amount": 5000,
    "currency": "NGN",
    "status": "successful"
}
```
### Refund Payment
Endpoint:/payments/{id}/refund
Method: POST
Description: Refunds a completed payment.
#### Example Request
**HTTPS Request**: POST/payments/{id}/refund
cURL Example
```bash
curl -X POST
https://api.payflow.com/v1/payments/pay_001/refund/ \
-H "Authorization: Bearer YOUR_API_KEY"
```
#### Response (200 OK)
```json
{
    "id": "pay_001",
    "status": "refunded"
}
```
## Error Responses
| Status Code  | Meaning       | Cause                          | Fix
|------------- |---------------|--------------------------------|----------------------
| 400          | Bad Request   | Missing fields              | Validate request body
| 401          | Unauthorized  | Invalid Api key             | Check authorization header
| 404          | Not found     | Invalid endpoint            | Confirm URL path
| 500          | Server error  | Server issue                | Retry or contact support
## Best Practices
- Never expose your API key in frontend code
- Always validate request data before sending
- Use HTTPS for all API requests
- Implement proper error handling
- Log API responses for debugging 

    
