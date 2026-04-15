# ShopVerse - Flipkart Inspired E-commerce Platform

A full-stack e-commerce application inspired by Flipkart's shopping flow and layout patterns, with product listing, product detail, cart, checkout, and order success pages.

## Tech Stack

- Frontend: React, React Router, Axios, TailwindCSS
- Backend: Node.js, Express
- Database: PostgreSQL

## Features Implemented

- Flipkart-style sticky top navigation with category menu and search
- Product grid with pricing, discount badges, and delivery highlights
- Product detail page with key buying signals and CTA flow
- Cart page with quantity updates, remove item, and price summary
- Checkout page with structured delivery form and payment method
- Order placement with persistent order and order item records
- Built-in authentication (signup/login) without external auth providers
- Product images loaded from backend `image_url` values (remote URLs)

## Project Structure

- `frontend/` - React UI application
- `backend/` - Express API and PostgreSQL integration

## API Endpoints

- `POST /api/auth/signup` - create account
- `POST /api/auth/login` - login and receive signed token
- `GET /api/auth/me` - fetch current profile (requires token)
- `GET /api/products` - list products (supports `q`, `category`, `sort`)
- `GET /api/products/:id` - get product details
- `GET /api/cart` - get current default user's cart
- `POST /api/cart` - add product to cart
- `PATCH /api/cart/:id` - update cart item quantity
- `DELETE /api/cart/:id` - remove cart item
- `POST /api/order` - place order from cart

## Database Schema (Custom Design)

### `users`
- `id` (PK)
- `full_name`
- `email` (unique)
- `created_at`

### `products`
- `id` (PK)
- `name`
- `description`
- `price`
- `category`
- `stock`
- `image_url`
- `rating`
- `review_count`
- `created_at`

### `cart`
- `id` (PK)
- `user_id` (FK -> users.id)
- `product_id` (FK -> products.id)
- `quantity`
- unique constraint on (`user_id`, `product_id`)

### `orders`
- `id` (PK)
- `user_id` (FK -> users.id)
- `address` (JSONB)
- `total_amount`
- `payment_method`
- `status`
- `created_at`

### `order_items`
- `id` (PK)
- `order_id` (FK -> orders.id)
- `product_id` (FK -> products.id)
- `quantity`
- `price_at_purchase`

## Setup Instructions

### 1) Clone and install dependencies

Backend:

```bash
cd backend
npm install
```

Frontend:

```bash
cd frontend
npm install
```

### 2) Configure environment variables

Create `backend/.env`:

```env
PORT=5000
DB_USER=your_postgres_user
DB_HOST=localhost
DB_NAME=your_db_name
DB_PASSWORD=your_postgres_password
DB_PORT=5432
```

Optional frontend env (`frontend/.env`):

```env
REACT_APP_API_BASE_URL=http://localhost:5000/api
```

### 3) Seed sample data

```bash
cd backend
node seed.js
```

This creates schema and inserts sample catalog data across categories like Mobiles, Fashion, Electronics, Home, Appliances, Travel, and Grocery.

### 4) Run backend

```bash
cd backend
npm start
```

### 5) Run frontend

```bash
cd frontend
npm start
```

Open `http://localhost:3000`.

## Assumptions

- Signed auth token is generated and verified using Node.js native `crypto`.
- No external authentication service/package is used.
- Focus is on e-commerce UX flow, data modeling, and backend integration.
- External image URLs are used for product images.

## Demo Credentials (after seed)

- Email: `default@shopverse.local`
- Password: `password123`

## Original Work Note

This implementation is custom-built for this project requirement and not copied from public repository boilerplates beyond standard library/framework starters.
# Ecommerce_web_app
# Ecommerce_app
