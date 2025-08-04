# RuralConnect Backend API

A comprehensive Node.js backend for the RuralConnect platform - connecting rural communities with essential services and products.

## 🚀 Features

### Authentication & Authorization
- User registration and login
- JWT-based authentication
- Password hashing with bcrypt
- Protected routes with middleware

### Core Functionality
- **Services Management** - CRUD operations for services
- **Products Catalog** - Product listing with search and filtering
- **News & Updates** - Dynamic news content management  
- **Contact System** - Contact form submissions and management
- **Booking System** - Shopping cart and order management
- **User Profiles** - Profile management and updates

### Technical Features
- RESTful API design
- MongoDB with Mongoose ODM
- Input validation and sanitization
- Error handling and logging
- CORS configuration
- Rate limiting (ready to implement)
- File upload support (ready to implement)

## 🛠 Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB with Mongoose
- **Authentication:** JWT (JSON Web Tokens)
- **Password Hashing:** bcryptjs
- **Environment:** dotenv
- **Security:** CORS, Helmet (ready to implement)

## 📦 Installation & Setup

### Prerequisites
- Node.js (v16+)
- MongoDB (local or Atlas)
- npm or yarn

### 1. Clone Repository
```bash
git clone <repository-url>
cd ruralconnect-backend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Setup
```bash
# Copy environment template
cp .env.example .env

# Edit .env with your configurations
nano .env
```

### 4. Database Setup
```bash
# Start MongoDB locally (if using local installation)
mongod

# Or use MongoDB Atlas connection string in .env
```

### 5. Start Development Server
```bash
# Development mode with auto-reload
npm run dev

# Production mode
npm start
```

The server will start on `http://localhost:5000`

## 🔌 API Endpoints

### Authentication
```
POST /api/register     # User registration
POST /api/login        # User login
```

### Services
```
GET  /api/services     # Get all services
POST /api/services     # Create service (protected)
```

### Products
```
GET  /api/products     # Get products (with search/filter)
POST /api/products     # Create product (protected)
```

### News
```
GET  /api/news         # Get published news
POST /api/news         # Create news (protected)
```

### Contact
```
POST /api/contact      # Submit contact form
GET  /api/contact      # Get all contacts (protected)
```

### Bookings
```
POST /api/bookings     # Create booking (protected)
GET  /api/bookings     # Get user bookings (protected)
GET  /api/bookings/:id # Get specific booking (protected)
PATCH /api/bookings/:id # Update booking (protected)
```

### User Profile
```
GET  /api/profile      # Get user profile (protected)
PATCH /api/profile     # Update profile (protected)
```

### Health Check
```
GET  /api/health       # API health status
```

## 📝 API Usage Examples

### User Registration
```javascript
POST /api/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "+1234567890"
}
```

### User Login
```javascript
POST /api/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

### Create Booking
```javascript
POST /api/bookings
Authorization: Bearer <jwt-token>
Content-Type: application/json

{
  "items": [
    {
      "productId": "64f8a1b2c3d4e5f6g7h8i9j0",
      "quantity": 2
    }
  ],
  "deliveryAddress": "Village Main Road, District",
  "notes": "Please deliver in the evening"
}
```

### Search Products
```javascript
GET /api/products?search=rice&category=Groceries
```

## 🗃 Database Schema

### User Model
```javascript
{
  name: String (required),
  email: String (required, unique),
  password: String (required, hashed),
  phone: String,
  role: String (user/admin),
  createdAt: Date
}
```

### Product Model
```javascript
{
  name: String (required),
  price: Number (required),
  icon: String (required),
  category: String (required),
  description: String,
  inStock: Boolean,
  createdAt: Date
}
```

### Booking Model
```javascript
{
  user: ObjectId (ref: User),
  items: [{
    product: ObjectId (ref: Product),
    quantity: Number,
    price: Number
  }],
  totalAmount: Number,
  status: String (pending/confirmed/delivered),
  deliveryAddress: String,
  notes: String,
  createdAt: Date
}
```

## 🔒 Authentication

The API uses JWT (JSON Web Tokens) for authentication:

1. **Register/Login** - Receive JWT token
2. **Include Token** - Add to Authorization header: `Bearer <token>`
3. **Protected Routes** - Automatically validated

## 🌱 Data Seeding

The server automatically seeds initial data:
- 5 essential services
- 6 grocery products  
- 3 news articles

Manual seeding:
```bash
npm run seed
```

## 🚀 Deployment

### Heroku Deployment
```bash
# Create Heroku app
heroku create ruralconnect-api

# Set environment variables
heroku config:set MONGODB_URI=<your-mongodb-atlas-url>
heroku config:set JWT_SECRET=<your-secret>

# Deploy
git push heroku main
```

### Railway Deployment
```bash
# Install Railway CLI