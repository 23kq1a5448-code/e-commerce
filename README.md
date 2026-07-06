# AVI E-Commerce Website

A complete e-commerce platform with AI-powered product recommendations, featuring both user and admin accounts.

## Features

### User Account
- **Product Browsing**: Browse products with AI-powered recommendations
- **Advanced Filtering**: Filter by price range, color, size, shape, category, and more
- **Search**: Smart search functionality across products
- **Shopping Cart**: Add/remove items, quantity management
- **Checkout**: Complete checkout process with shipping address
- **Payment Processing**: Simulated payment integration
- **Reviews & Ratings**: Leave reviews and rate products
- **Order Tracking**: View order history and status
- **Wishlist**: Save favorite products
- **Profile Management**: Update personal information and address
- **Submit Requirements**: Request products or features to admin

### Admin Account
- **Dashboard**: Overview of users, products, orders, and revenue
- **Product Management**: Add, edit, delete products with full specifications
- **Order Management**: View all orders and update order status
- **Review Moderation**: View and moderate customer reviews
- **Client Requirements**: Handle and respond to customer requests
- **Analytics**: Track sales and user engagement

## Tech Stack

- **Frontend**: React 18, React Router, TailwindCSS, Lucide Icons
- **Backend**: Node.js, Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT (JSON Web Tokens)
- **State Management**: React Context API, Zustand
- **Styling**: TailwindCSS with custom components

## Prerequisites

- Node.js (v16 or higher)
- MongoDB (installed and running locally)
- npm or yarn

## Installation

1. **Clone the repository** (or navigate to the project directory)

2. **Install root dependencies**:
   ```bash
   npm install
   ```

3. **Install backend dependencies**:
   ```bash
   cd backend
   npm install
   ```

4. **Install frontend dependencies**:
   ```bash
   cd ../frontend
   npm install
   ```

5. **Set up environment variables**:
   - The backend `.env` file is already created with default values
   - For production, update `JWT_SECRET` and add your `STRIPE_SECRET_KEY`
   - Ensure MongoDB is running on `mongodb://localhost:27017`

6. **Seed the database** (creates admin/user accounts and sample products):
   ```bash
   cd backend
   npm run seed
   ```

## Running the Application

### Development Mode (Both Frontend & Backend)
From the root directory:
```bash
npm run dev
```
This starts:
- Backend on http://localhost:5000
- Frontend on http://localhost:3000

### Individual Servers

**Backend only:**
```bash
cd backend
npm run dev
```

**Frontend only:**
```bash
cd frontend
npm run dev
```

### Production Build

**Build frontend:**
```bash
cd frontend
npm run build
```

**Start backend in production:**
```bash
cd backend
npm start
```

## Default Accounts

After running the seed script, you can log in with:

- **Admin Account**:
  - Email: admin@avi.com
  - Password: admin123

- **User Account**:
  - Email: user@avi.com
  - Password: user123

## Project Structure

```
E-commerces/
├── backend/
│   ├── models/          # Database models (User, Product, Order, Review, ClientRequirement)
│   ├── routes/          # API routes
│   ├── middleware/      # Authentication middleware
│   ├── seed.js          # Database seeding script
│   ├── server.js        # Express server entry point
│   └── .env             # Environment variables
├── frontend/
│   ├── src/
│   │   ├── components/  # Reusable components (Navbar, Footer)
│   │   ├── contexts/    # React contexts (Auth, Cart)
│   │   ├── pages/       # Page components
│   │   │   ├── admin/   # Admin dashboard pages
│   │   │   ├── Home.jsx
│   │   │   ├── Products.jsx
│   │   │   ├── ProductDetail.jsx
│   │   │   ├── Cart.jsx
│   │   │   ├── Checkout.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Register.jsx
│   │   │   ├── Profile.jsx
│   │   │   ├── Orders.jsx
│   │   │   ├── Wishlist.jsx
│   │   │   └── SubmitRequirement.jsx
│   │   ├── App.jsx      # Main app component with routing
│   │   └── main.jsx     # Entry point
│   └── index.html
├── package.json         # Root package.json
└── README.md           # This file
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Products
- `GET /api/products` - Get all products (with filtering)
- `GET /api/products/:id` - Get single product
- `POST /api/products` - Create product (admin)
- `PUT /api/products/:id` - Update product (admin)
- `DELETE /api/products/:id` - Delete product (admin)

### Orders
- `POST /api/orders` - Create order
- `GET /api/orders/myorders` - Get user orders
- `GET /api/orders/:id` - Get single order
- `PUT /api/orders/:id/pay` - Mark order as paid
- `PUT /api/orders/:id/deliver` - Mark order as delivered

### Reviews
- `GET /api/reviews/product/:productId` - Get product reviews
- `POST /api/reviews` - Create review
- `PUT /api/reviews/:id/helpful` - Mark review as helpful

### Admin
- `GET /api/admin/dashboard` - Get dashboard stats
- `GET /api/admin/users` - Get all users
- `GET /api/admin/orders` - Get all orders
- `PUT /api/admin/orders/:id/status` - Update order status
- `GET /api/admin/reviews` - Get all reviews
- `DELETE /api/admin/reviews/:id` - Delete review
- `GET /api/admin/requirements` - Get client requirements
- `PUT /api/admin/requirements/:id` - Update requirement

### Recommendations
- `GET /api/recommendations/:userId` - Get AI recommendations
- `GET /api/recommendations/similar/:productId` - Get similar products

### Client Requirements
- `POST /api/client-requirements` - Submit requirement
- `GET /api/client-requirements/my` - Get user requirements

## AI Recommendation System

The AI recommendation system scores products based on:
- **Rating (40%)**: Higher rated products score better
- **Review Count (20%)**: More reviews indicate popularity
- **Featured Status (15%)**: Featured products get bonus points
- **Stock Availability (10%)**: Products in stock are preferred
- **Price Competitiveness (15%)**: Better value for money
- **Recency (5%)**: Newer products get slight preference

## Features in Detail

### Advanced Filtering
Users can filter products by:
- Price range (min/max)
- Category (Electronics, Clothing, Home & Garden, etc.)
- Color (Red, Blue, Black, White, etc.)
- Size (XS, S, M, L, XL, XXL)
- Shape (Round, Square, Rectangle, Oval)
- Sort options (Newest, Price Low-High, Price High-Low, Top Rated)

### Admin Dashboard
The admin dashboard provides:
- Real-time statistics (users, products, orders, revenue)
- Quick access to all management sections
- Recent orders overview
- Order status management

### Client Requirements
Users can submit:
- Product requests
- Feature requests
- Bug reports
- General inquiries
- Priority levels (Low, Medium, High, Urgent)

Admins can:
- View all requirements
- Update status (Open, In Progress, Resolved, Closed)
- Respond to requirements

## Troubleshooting

**MongoDB Connection Error**:
- Ensure MongoDB is running: `mongod` (or use MongoDB Compass)
- Check the MONGODB_URI in backend/.env

**Port Already in Use**:
- Change PORT in backend/.env
- Update frontend vite.config.js proxy target accordingly

**CORS Errors**:
- Ensure backend CORS is configured correctly
- Check that frontend proxy is set up in vite.config.js

## License

This project is for educational purposes.

## Support

For issues or questions, please contact the development team.
