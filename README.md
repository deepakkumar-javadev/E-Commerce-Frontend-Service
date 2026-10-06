# E-Commerce Frontend

E-Commerce Frontend is a static web-based frontend for the microservices-based e-commerce application. It provides a user-friendly interface for browsing products, managing the shopping cart, placing orders, making payments, and tracking orders.

The frontend communicates with the backend microservices through the **API Gateway**.

---

## Features

* User registration and login
* JWT-based authentication
* Browse products
* Search and view product details
* Add products to cart
* Update cart items
* Remove products from cart
* Place orders
* Support for Cash on Delivery (COD)
* Support for online payments
* Razorpay payment integration
* View order details
* Track order status
* View order history
* Responsive user interface

---

## Technologies Used

* **HTML5**
* **CSS3**
* **JavaScript**
* **REST APIs**
* **JWT Authentication**
* **Razorpay**
* **API Gateway**

---

## Application Flow

```text
                         Customer
                            │
                            ▼
                  ┌──────────────────┐
                  │ E-Commerce       │
                  │    Frontend      │
                  │    :9090         │
                  └────────┬─────────┘
                           │
                           │ REST API
                           ▼
                  ┌──────────────────┐
                  │   API Gateway    │
                  │      :8080       │
                  └────────┬─────────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
        User Service  Product Service  Cart Service
             │             │             │
             └─────────────┼─────────────┘
                           │
                           ▼
                     Order Service
                           │
                    ┌──────┴──────┐
                    ▼             ▼
             Payment Service  Inventory
```

---

## Main Pages

### Authentication

```text
index.html
register.html
```

Provides:

* User login
* New user registration
* JWT token handling

---

### Products

```text
products.html
```

Provides:

* Product listing
* Product search
* Product details
* Add product to cart

---

### Cart

```text
cart.html
```

Provides:

* View cart items
* Update quantity
* Remove items
* View total amount
* Proceed to checkout

---

### Checkout

```text
place-order.html
```

Provides:

* Order details
* Shipping/customer information
* Payment method selection
* COD and online payment options

---

### Payment

```text
payment.html
```

Provides online payment processing through Razorpay.

```text
Customer
   ↓
Frontend
   ↓
API Gateway
   ↓
Payment Service
   ↓
Razorpay
```

---

### Order Details

```text
order-details.html
```

Provides:

* Order information
* Payment status
* Order status
* Order tracking
* Delivery information

---

## Authentication Flow

The frontend uses JWT-based authentication.

```text
User Login
    │
    ▼
Frontend
    │
    ▼
API Gateway
    │
    ▼
User Service
    │
    ▼
JWT Token
    │
    ▼
Browser Local Storage
```

For authenticated requests, the JWT token is sent in the `Authorization` header.

```text
Authorization: Bearer <JWT_TOKEN>
```

---

## Shopping Flow

```text
Login
  ↓
Browse Products
  ↓
Select Product
  ↓
Add to Cart
  ↓
View Cart
  ↓
Proceed to Checkout
  ↓
Select Payment Method
  ↓
 ┌───────────────┐
 │               │
 ▼               ▼
COD           Online
 │               │
 ▼               ▼
Order         Razorpay
Created       Payment
 │               │
 └───────┬───────┘
         ▼
    Order Details
         ↓
    Track Order
```

---

## Backend Integration

The frontend communicates with backend services through the API Gateway instead of directly calling individual microservices.

```text
Frontend
  :9090
    │
    ▼
API Gateway
  :8080
    │
    ├── User Service       :8082
    ├── Product Service    :8083
    ├── Inventory Service  :8084
    ├── Cart Service       :8085
    ├── Order Service      :8086
    ├── Payment Service    :8087
    └── Notification      :8088
```

This provides a single entry point for frontend-to-backend communication.

---

## API Gateway Configuration

The frontend uses the API Gateway as its backend entry point.

```text
Frontend URL:
http://localhost:9090

API Gateway:
http://localhost:8080
```

Example:

```text
Frontend
   │
   │ GET /product/...
   ▼
API Gateway :8080
   │
   ▼
Product Service :8083
```

---

## Project Structure

```text
E-Commerce-Frontend
│
├── index.html
├── register.html
├── products.html
├── cart.html
├── place-order.html
├── payment.html
├── order-details.html
│
├── css/
│   └── style.css
│
├── js/
│   ├── auth.js
│   ├── products.js
│   ├── cart.js
│   ├── order.js
│   └── payment.js
│
└── assets/
    ├── images/
    └── icons/
```

---

## Running the Frontend

Since the frontend is a static web application, it can be served using a local web server.

Example:

```text
Frontend:
http://localhost:9090
```

Make sure the backend services and API Gateway are running before using the application.

Required services include:

```text
Eureka Server       :8761
API Gateway         :8080
User Service        :8082
Product Service     :8083
Inventory Service   :8084
Cart Service        :8085
Order Service       :8086
Payment Service     :8087
Notification Service:8088
Frontend            :9090
```

---

## Payment Integration

The frontend supports both payment methods:

### Cash on Delivery

```text
Frontend
   ↓
API Gateway
   ↓
Order Service
   ↓
Payment Service
   ↓
COD Payment
```

### Online Payment

```text
Frontend
   ↓
API Gateway
   ↓
Order Service
   ↓
Payment Service
   ↓
Razorpay
   ↓
Payment Success
   ↓
Order Confirmation
```

---

## Order Tracking

Customers can view their order details and track the order status from the frontend.

Example order lifecycle:

```text
PENDING
   ↓
CONFIRMED
   ↓
SHIPPED
   ↓
DELIVERED
```

The frontend displays the latest order and payment information received from the backend services.

---

## Security

The frontend stores the JWT token received after successful login and sends it with authenticated API requests.

Sensitive backend credentials such as:

* Database passwords
* Razorpay secrets
* JWT secrets
* Email passwords

are **not stored in the frontend**.

---

## E-Commerce Architecture

```text
                    ┌──────────────────┐
                    │    Customer      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    Frontend      │
                    │      :9090       │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   API Gateway    │
                    │      :8080       │
                    └────────┬─────────┘
                             │
       ┌─────────────────────┼─────────────────────┐
       │          │          │          │          │
       ▼          ▼          ▼          ▼          ▼
     User      Product    Inventory    Cart      Order
    :8082       :8083       :8084      :8085     :8086
                                                     │
                                                     ▼
                                                  Payment
                                                   :8087
                                                     │
                                                     ▼
                                                  Razorpay
```

---

## Future Enhancements

* Product filtering and sorting
* Wishlist functionality
* Improved responsive design
* User profile management
* Product reviews and ratings
* Real-time order tracking
* Push notifications

---

## Tech Stack Used

**HTML5 | CSS3 | JavaScript | REST APIs | JWT | Razorpay | API Gateway | Microservices**
