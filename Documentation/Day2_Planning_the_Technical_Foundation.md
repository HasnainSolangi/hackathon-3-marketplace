**Day 2 - Planning the Technical Foundation**
# Solangi Woods -  E-commerce Marketplace Builder Hackathon.

## Objectives

### 1. Define Technical Requirements
- **Frontend Requirements**: The necessary frontend components have been outlined, including setting up the Next.js project structure and implementing a responsive design system.
- **Sanity CMS as Backend**: Sanity CMS has been integrated to manage product data, customer details, and order records, which serves as the backend for the marketplace.
- **Third-Party APIs**: API endpoints have been defined for product listing, order processing, authentication, and shipping tracking, ensuring that all technical requirements are met.

### 2. Design System Architecture
- **System Architecture Diagram**: A clear system architecture diagram has been included, showcasing the interaction between the frontend, Sanity CMS, and third-party APIs.
- **Data Flow and User Workflows**: Diagrams illustrating the data flow for product browsing, order placement, user registration, and order processing have been created to map out the user journey and system processes.

### 3. Plan API Requirements
- **API Endpoints**: Key API endpoints have been documented, such as:
  - Product-related endpoints (`GET /products`, `POST /products`)
  - Order management endpoints (`POST /orders`, `GET /orders/{id}/status`)
  - Authentication and certificate verification endpoints.
- **Parameter Descriptions**: Detailed descriptions of parameters (e.g., `category`, `woodType`, `priceRange`) are provided for each endpoint, ensuring clarity in API usage.

### 4. Write Technical Documentation
- A comprehensive technical specification, with clear descriptions of endpoints, examples, and authentication details.
- **API Consistency Guidelines**: Guidelines for maintaining consistency in API naming conventions and error responses have been included to ensure the documentation is structured and easy to follow.



### 5. Key Outcome of Day 2
- The technical plan is fully aligned with the business goals established on Day 1, ensuring that the marketplace will meet both business and technical needs.
- System architecture and API documentation are well-documented, providing a clear understanding of how the marketplace will be built.
- The feedback loop, including API consistency guidelines, has been incorporated to enhance collaboration and refine the plan further.

### Conclusion
With the completion of Day 2 tasks, this README now meets the objectives outlined in the **Day 2 - Planning the Technical Foundation**. Alhamdulillah! Now I am well-prepared to transition to the implementation phase on Day 3!

**INSHA'ALLAH**



----------------------------------------
----------------------------------------
----------------------------------------
    
1 - **Basic system architecture showing the relationship between frontend, Sanity CMS, and third-party APIs**


![Basic System Architect](https://github.com/user-attachments/assets/62db28c0-0505-4f75-a21a-9fcb7247bc10)
---

2 - **Data flow for product browsing and order placement**

![data-work-flow](https://github.com/user-attachments/assets/ea9f4376-8e8a-4983-a401-4224f9fc5e81)
---

3 - **User registration workflow**

![user-registration](https://github.com/user-attachments/assets/8f2b4451-b1b2-4119-94f4-512886813f41)
---

4 - **Order processing workflow with shipping integration**


![order-flow](https://github.com/user-attachments/assets/839508bf-6860-49d5-b102-2546db93745a)
-------
![Basic-work-flow](https://github.com/user-attachments/assets/fcacae1d-11f3-4218-bc8e-bf0693bc2b19)

-------
### API Documentation - Solangi Woods

#### Key API Endpoints

1. Product Endpoints

- GET /api/products - List all furniture products
- GET /api/products/{id} - Get specific product details
- GET /api/products/wood-types - List available wood types
- POST /api/products/custom-request - Submit customization request


2. Authentication Endpoints

- GET /api/auth/certificate/{id} - Verify wood authentication
- POST /api/auth/verify-craftsman - Verify craftsman credentials


3. Order Management

- POST /api/orders - Create new order
- GET /api/orders/{id}/status - Check order status
- GET /api/orders/{id}/tracking - Get shipping updates

#### Base URL

```
https://api.solangiwoods.com/v1
```

#### Authentication
All API requests require a Bearer token in the Authorization header:
```
Authorization: Bearer <your_token>
```

## Endpoints

### Products

#### 1. Get All Products
```
GET /products
```
Query Parameters:
- category (string): Filter by furniture category
- woodType (string): Filter by wood type
- isPureWood (boolean): Filter for 100% wooden items
- priceRange (object): Min and max price range

Response Example:
```json
{
  "products": [
    {
      "id": "prod_123",
      "name": "Mahogany Dining Table",
      "category": "dining",
      "woodType": "mahogany",
      "isPureWood": true,
      "price": 1299.99,
      "dimensions": "72x36x30",
      "authenticityCertificate": "AUTH_123",
      "stockQuantity": 5,
      "images": ["url1", "url2"],
      "craftsmanId": "CRAFT_456",
      "warranty": "5 years"
    }
  ],
  "total": 1,
  "page": 1
}
```

#### 2. Create Order
```
POST /orders
```
Request Body:
```json
{
  "customerId": "cust_123",
  "products": [
    {
      "productId": "prod_123",
      "quantity": 1,
      "customizations": {
        "finish": "natural",
        "specifications": "custom size 80x40x30"
      }
    }
  ],
  "shippingAddress": {
    "street": "123 Main St",
    "city": "Springfield",
    "state": "IL",
    "zip": "62701"
  },
  "specialInstructions": "Please handle with care"
}
```

### Authentication & Certificates

#### 1. Verify Product Authenticity
```
GET /certificates/{certificateId}
```
Response Example:
```json
{
  "certificateId": "AUTH_123",
  "productId": "prod_123",
  "woodType": "mahogany",
  "originLocation": "Sustainable Forest XYZ",
  "craftsmanDetails": {
    "id": "CRAFT_456",
    "name": "Hasnain Ahmed",
    "expertise": "Master Woodworker",
    "yearsExperience": 15
  },
  "certificationDate": "2025-01-16",
  "verificationStatus": "verified"
}
```

### Shipping & Tracking

#### 1. Get Shipping Estimate
```
POST /shipping/estimate
```
Request Body:
```json
{
  "products": ["prod_123"],
  "destination": {
    "zip": "62701",
    "country": "USA"
  }
}
```

#### 2. Track Order
```
GET /orders/{orderId}/tracking
```
Response Example:
```json
{
  "orderId": "order_789",
  "status": "in_transit",
  "estimatedDelivery": "2025-01-20",
  "currentLocation": "Springfield Hub",
  "specialHandling": true,
  "deliveryNotes": "Large item delivery"
}
```
### API Consistency Guidelines

#### Endpoint Naming Convention:
- Use the pattern `/api/[resource]` for each endpoint. For example:
  - `GET /api/products` to retrieve all products.
  - `POST /api/products` to add a new product.

#### Parameter Naming:
- Use **camelCase** for request body fields: `productId`, `orderId`, `customizations`.
- Use **snake_case** for query parameters: `wood_type`, `price_range`.

#### Error Responses:
- Always return the appropriate HTTP status codes:
  - `404 Not Found`: If the resource does not exist.
  - `400 Bad Request`: If the request is missing required fields.
  - `500 Internal Server Error`: For server-related issues.


### Implementation Plan
**Technical Priorities**

1. Frontend Development

- Set up Next.js project structure
- Implement responsive design system
- Create reusable components for furniture display

2. Sanity CMS Integration

- Configure Sanity Studio
- Implement content schemas
- Set up API endpoints


3. Third-Party Integrations

- Payment gateway setup
- Shipping tracking integration
- Wood authentication system



4. Security Considerations

- Implement authentication
- Secure API endpoints
- Encrypt sensitive data
- Set up CORS policies

5. Next Steps

- Begin frontend development
- Set up Sanity Studio
- Integrate authentication system
- Implement payment processing
- Create wood verification system

