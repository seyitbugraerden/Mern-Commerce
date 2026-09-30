<div align="center">

# 🛍️ MERN E-Commerce App

### Full-stack e-commerce application built with MongoDB, Express, React and Node.js

A complete MERN-based commerce project featuring **product management, authentication, shopping cart, categories, coupons, admin operations and REST API integration**.

<br />

![MongoDB](https://img.shields.io/badge/MongoDB-8-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?style=for-the-badge&logo=express&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Ant Design](https://img.shields.io/badge/Ant_Design-5-0170FE?style=for-the-badge&logo=antdesign&logoColor=white)

</div>

---

## About the Project

**MERN E-Commerce App** is a full-stack e-commerce application developed with the MERN stack:

```text
MongoDB
Express.js
React
Node.js
```

The project includes both:

- Customer-facing storefront
- Administrative management interface

The backend exposes REST endpoints for users, products, categories and coupons, while the React frontend consumes those endpoints to provide shopping and administration workflows.

---

## Main Features

### Storefront

- Home page
- Shop page
- Product listing
- Product detail pages
- Product gallery
- Product colors and sizes
- Product reviews UI
- Shopping cart
- Coupon interaction
- Product search
- Blog pages
- Contact page
- Authentication page
- Promotional dialog
- Responsive header and footer

### Admin

- Admin-only interface
- Product management
- Product creation
- Product editing
- Product deletion
- Category management
- Coupon management
- User listing
- User deletion
- Role-based admin access

### Backend

- Express REST API
- MongoDB / Mongoose
- User registration
- User login
- bcrypt password hashing
- Product CRUD
- Category CRUD
- Coupon CRUD
- Product search
- User deletion
- CORS
- Morgan request logging

---

## Application Architecture

```text
┌──────────────────────────────┐
│        React Frontend        │
│                              │
│ Storefront                   │
│ Admin Panel                  │
│ Cart                         │
│ Authentication               │
└───────────────┬──────────────┘
                │
                │ HTTP / REST
                ▼
┌──────────────────────────────┐
│       Express Backend        │
│                              │
│ /api/auth                    │
│ /api/products                │
│ /api/categories              │
│ /api/coupons                 │
└───────────────┬──────────────┘
                │
                ▼
┌──────────────────────────────┐
│           MongoDB            │
│                              │
│ Users                        │
│ Products                     │
│ Categories                   │
│ Coupons                      │
└──────────────────────────────┘
```

---

## Tech Stack

### Frontend

| Technology | Purpose |
| --- | --- |
| **React 18** | UI architecture |
| **Vite 5** | Frontend development/build |
| **React Router 6** | Client-side routing |
| **Ant Design 5** | Admin UI and feedback components |
| **Axios** | HTTP client |
| **React Slick** | Slider/carousel components |
| **React Quill** | Rich-text product editor |
| **Stripe JS** | Payment integration dependency |
| **CSS** | Component-level styling |

### Backend

| Technology | Purpose |
| --- | --- |
| **Node.js** | Server runtime |
| **Express 4** | REST API |
| **MongoDB** | Database |
| **Mongoose 8** | ODM |
| **bcryptjs** | Password hashing |
| **CORS** | Cross-origin requests |
| **Morgan** | HTTP request logging |
| **dotenv** | Environment configuration |
| **Nodemon** | Development server reload |
| **Stripe** | Payment integration dependency |

---

## Frontend Routes

The application uses React Router.

```text
/
├── /shop
├── /blog
├── /blog/:id
├── /contact
├── /cart
├── /auth
├── /product/:id
│
└── /admin
    ├── /users
    ├── /categories
    ├── /categories/create
    ├── /categories/update/:id
    ├── /products
    ├── /products/create
    ├── /products/update/:id
    ├── /coupons
    ├── /coupons/create
    └── /coupons/update/:id
```

---

## Authentication

The application implements registration and login through the Express API.

### Register

```text
POST /api/auth/register
```

Registration includes:

- Name
- Email
- Password
- Random avatar
- Default `user` role

Before storing a password, the backend hashes it using:

```js
bcrypt.hash(password, 10)
```

The user model supports:

```text
user
admin
```

roles.

---

## Login

```text
POST /api/auth/login
```

The backend:

1. Looks up the user by email
2. Compares the submitted password with the stored hash
3. Returns user information and role

The frontend stores the returned user state in:

```text
localStorage
```

Admin users are redirected into the admin area.

---

## Role-Based Admin Interface

The admin layout checks:

```js
user.role
```

from local storage.

If the user role is:

```text
admin
```

the administration interface becomes available.

The admin menu contains:

```text
Dashboard
Categories
Products
Coupons
Users
Orders
```

> The navigation includes an Orders entry, but a completed order-management route is not present in the current router configuration.

---

## Product Management

Products are backed by a Mongoose schema containing:

```text
name
images
reviews
description
colors
sizes
price
category
timestamps
```

Price data contains:

```js
price: {
  current,
  discount
}
```

---

## Product API

### Get All Products

```http
GET /api/products
```

### Get Product

```http
GET /api/products/:productId
```

### Create Product

```http
POST /api/products
```

### Update Product

```http
PUT /api/products/:productId
```

### Delete Product

```http
DELETE /api/products/:productId
```

### Search Products

```http
GET /api/products/search/:productName
```

Product search uses a MongoDB regular expression:

```js
{
  name: {
    $regex: productName,
    $options: "i"
  }
}
```

This provides case-insensitive product-name search.

---

## Product Creation

The admin product creation form supports:

- Product name
- Price
- Discount percentage
- Category
- Multiple image URLs
- Multiple colors
- Multiple sizes
- Rich-text description

Rich-text content is entered using:

```text
React Quill
```

The image, color and size inputs are converted from multiline text into arrays before sending them to the API.

---

## Categories

Categories have their own dedicated CRUD API.

### Endpoints

```http
GET    /api/categories
GET    /api/categories/:categoryId
POST   /api/categories
PUT    /api/categories/:categoryId
DELETE /api/categories/:categoryId
```

The admin UI supports:

- Category list
- Category creation
- Category update
- Category deletion

---

## Coupons

Coupons are persisted in MongoDB and managed through the REST API.

### Endpoints

```http
GET    /api/coupons
GET    /api/coupons/:couponId
GET    /api/coupons/code/:couponCode
POST   /api/coupons
PUT    /api/coupons/:couponId
DELETE /api/coupons/:couponId
```

The admin panel supports:

- Coupon list
- Coupon creation
- Coupon editing
- Coupon deletion

Coupon information includes:

```text
Code
Discount percentage
```

---

## Shopping Cart

The cart uses React Context.

```text
CartProvider
```

provides:

```text
addToCart()
removeFromCart()
cartItems
```

Cart items are persisted in:

```text
localStorage
```

This allows cart state to survive page refreshes.

---

## Cart Flow

```text
Product
   │
   ▼
Add to Cart
   │
   ▼
CartContext
   │
   ├── cartItems
   │
   └── localStorage
   │
   ▼
Cart Page
   │
   ├── Cart Table
   ├── Coupon
   └── Cart Totals
```

---

## Product Details

The product detail area contains several dedicated components:

```text
ProductDetails
├── Breadcrumb
├── Gallery
├── Info
└── Tabs
```

The page architecture supports:

- Product images
- Product information
- Price
- Discount
- Product options
- Description
- Reviews
- Tabbed content

---

## Reviews

The product model contains an embedded review schema:

```js
{
  text,
  rating,
  user
}
```

The frontend includes:

```text
Reviews
ReviewItem
ReviewForm
```

components.

This provides a foundation for product review functionality.

---

## Admin Product Table

Admin products are displayed using Ant Design's:

```text
Table
```

component.

The table combines product data with category data fetched from the API.

Displayed information includes:

- Product image
- Name
- Category
- Current price
- Discount percentage
- Edit action
- Delete action

---

## User Management

Admin users can retrieve all registered users through:

```http
GET /api/auth/register
```

The admin user table displays:

```text
Avatar
Name
Email
Role
```

Users can also be deleted by email:

```http
DELETE /api/auth/:email
```

---

## MongoDB Models

The backend currently contains models for:

```text
User
Product
Category
Coupon
```

### User

```text
name
email
password
role
avatar
timestamps
```

### Product

```text
name
images
description
colors
sizes
price
category
reviews
timestamps
```

---

## Backend Route Structure

```text
/api
│
├── /auth
│   ├── register
│   ├── login
│   └── delete user
│
├── /products
│   ├── CRUD
│   └── search
│
├── /categories
│   └── CRUD
│
└── /coupons
    └── CRUD
```

---

## Project Structure

```text
MERN-E-CommerceApp/
│
├── backend/
│   ├── modals/
│   │   ├── Category.js
│   │   ├── Coupon.js
│   │   ├── Product.js
│   │   └── User.js
│   │
│   ├── routes/
│   │   ├── auth.js
│   │   ├── categories.js
│   │   ├── coupons.js
│   │   ├── index.js
│   │   └── products.js
│   │
│   ├── package.json
│   └── server.js
│
├── frontend/
│   ├── public/
│   │   └── img/
│   │
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/
│   │   │   ├── Blogs/
│   │   │   ├── Cart/
│   │   │   ├── Categories/
│   │   │   ├── Layouts/
│   │   │   ├── Modals/
│   │   │   ├── ProductDetails/
│   │   │   ├── Products/
│   │   │   ├── Reviews/
│   │   │   └── Slider/
│   │   │
│   │   ├── context/
│   │   │   └── CartProvider.jsx
│   │   │
│   │   ├── layouts/
│   │   │   ├── AdminLayout.jsx
│   │   │   ├── Layout.jsx
│   │   │   └── MainLayout.jsx
│   │   │
│   │   ├── pages/
│   │   │   ├── admin/
│   │   │   ├── AuthPage.jsx
│   │   │   ├── BlogPage.jsx
│   │   │   ├── CartPage.jsx
│   │   │   ├── ContactPage.jsx
│   │   │   ├── HomePage.jsx
│   │   │   ├── ProductDetailsPage.jsx
│   │   │   └── ShopPage.jsx
│   │   │
│   │   ├── App.jsx
│   │   └── main.jsx
│   │
│   ├── package.json
│   └── vite.config.js
│
└── LICENSE
```

---

## Getting Started

Clone the repository:

```bash
git clone https://github.com/seyitbugraerden/MERN-E-CommerceApp.git
```

Navigate to the project:

```bash
cd MERN-E-CommerceApp
```

---

## Backend Setup

Navigate to the backend:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Create your environment configuration:

```env
MONGO_URI=your_mongodb_connection_string
```

Start the backend:

```bash
npm start
```

The API runs on:

```text
http://localhost:5000
```

---

## Frontend Setup

Open another terminal and navigate to:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start Vite:

```bash
npm run dev
```

The frontend will be available on the local Vite development URL.

---

## API Summary

| Resource | Method | Endpoint |
| --- | --- | --- |
| Register | POST | `/api/auth/register` |
| Login | POST | `/api/auth/login` |
| Users | GET | `/api/auth/register` |
| Delete User | DELETE | `/api/auth/:email` |
| Products | GET | `/api/products` |
| Product | GET | `/api/products/:productId` |
| Create Product | POST | `/api/products` |
| Update Product | PUT | `/api/products/:productId` |
| Delete Product | DELETE | `/api/products/:productId` |
| Product Search | GET | `/api/products/search/:productName` |
| Categories | GET | `/api/categories` |
| Create Category | POST | `/api/categories` |
| Update Category | PUT | `/api/categories/:categoryId` |
| Delete Category | DELETE | `/api/categories/:categoryId` |
| Coupons | GET | `/api/coupons` |
| Create Coupon | POST | `/api/coupons` |
| Update Coupon | PUT | `/api/coupons/:couponId` |
| Delete Coupon | DELETE | `/api/coupons/:couponId` |

---

## Current Development Status

The project already contains a substantial end-to-end MERN architecture.

### Implemented

- React storefront
- Express API
- MongoDB persistence
- Product CRUD
- Category CRUD
- Coupon CRUD
- Registration
- Login
- Password hashing
- Role-based admin interface
- User management
- Cart Context
- Cart persistence
- Product search
- Product details
- Blog routes
- Admin UI

### Areas for Further Development

- Token-based authentication
- Protected backend admin routes
- Order model and order API
- Checkout workflow
- Fully integrated Stripe checkout
- Review API persistence
- Server-side cart persistence
- Inventory management
- Image upload service
- Pagination
- Better validation
- Automated tests

---

## Security Improvements

For a production environment, the authentication architecture should be extended with:

- JWT or session authentication
- HTTP-only cookies
- Protected backend admin routes
- Authorization middleware
- Request validation
- Rate limiting
- Helmet
- Input sanitization
- CSRF protection where applicable
- Secure secret management

The current admin frontend checks the role from `localStorage`, so production authorization should also be enforced by the backend.

---

## Environment Security

Environment files should not be committed to source control.

Recommended setup:

```text
backend/.env
frontend/.env
```

should remain local and be covered by `.gitignore`.

If committed environment files contain active credentials, those credentials should be rotated.

---

## Development Roadmap

Potential next steps include:

- JWT authentication
- Refresh token flow
- Checkout page
- Stripe payment flow
- Order creation
- Order history
- Admin order management
- Product stock tracking
- Review persistence
- Wishlist functionality
- Image uploads
- Cloud storage
- Product pagination
- Category filters
- Price filters
- Search debouncing
- API validation
- Unit tests
- Integration tests
- End-to-end tests
- Docker support

---

## Developer

<div align="center">

### Seyit Buğra Erden

**Full Stack Developer · Software Engineer**

[GitHub](https://github.com/seyitbugraerden) ·
[LinkedIn](https://www.linkedin.com/in/sbugraerden/)

<br />

Built with **MongoDB · Express · React · Node.js**

</div>
