# PennyPal Backend

PennyPal is a personal finance management application that helps users track expenses, manage savings, and share costs with friends. This backend provides APIs for all PennyPal application features.

## 🚀 Tech Stack

### Core Technologies
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - MongoDB ODM

### Authentication & Security
- **Passport.js** - Authentication middleware
- **Google OAuth 2.0** - Social login
- **JWT** - Token-based authentication
- **bcrypt** - Password hashing
- **Helmet** - Security headers

### AI & OCR Services
- **Tesseract.js** - OCR for receipt scanning
- **Elice API** - AI assistant for categorization
- **Google Cloud Vision** - Advanced OCR

### External APIs
- **Open Exchange Rates** - Currency conversion
- **Nodemailer** - Email service
- **Brevo SMTP** - Email delivery

### Development Tools
- **Nodemon** - Development server
- **Morgan** - HTTP request logger
- **CORS** - Cross-origin resource sharing
- **Docker** - Containerization

## 📁 Project Structure

```
PennyPal-Backend/
├── controllers/          # Business logic
├── database/            # Database connection
├── docs/               # API documentation
├── middlewares/        # Custom middleware
├── models/             # MongoDB schemas
├── passport/           # Authentication strategies
├── routes/             # API endpoints
├── services/           # External services
├── utils/              # Helper functions
├── .env                # Environment variables
├── server.js           # Main server file
├── package.json        # Dependencies
├── dockerfile          # Docker configuration
└── docker-compose.yml  # Docker compose setup
```

## 🛠️ Installation & Setup

### Prerequisites
- Node.js (v18 or higher)
- MongoDB (local or cloud)
- npm or yarn

### 1. Clone Repository
```bash
git clone <repository-url>
cd PennyPal-Backend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Configuration
Create `.env` file based on `.env.backend.example`:

```bash
cp .env.backend.example .env
```

### 4. Start Development Server
```bash
# Development mode with auto-reload
npm run serve

# Production mode
npm start
```

Server will run at `http://localhost:3000`

## 🐳 Docker Deployment

### 1. Build and Run with Docker Compose
```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### 2. Manual Docker Build
```bash
# Build image
docker build -t pennypal-backend .

# Run container
docker run -p 3000:3000 --env-file .env pennypal-backend
```

## 📚 API Endpoints

### Authentication
- `POST /auth/register` - User registration
- `POST /auth/login` - User login
- `GET /auth/google` - Google OAuth login
- `POST /auth/logout` - User logout

### Transactions
- `GET /transaction` - Get user transactions
- `POST /transaction` - Create new transaction
- `PUT /transaction/:id` - Update transaction
- `DELETE /transaction/:id` - Delete transaction

### OCR (Receipt Scanning)
- `POST /ocr/scan` - Scan receipt image
- `POST /ocr/process` - Process OCR results

### Currency
- `GET /currency/rates` - Get exchange rates
- `POST /currency/convert` - Convert currency

### Savings
- `GET /savings` - Get savings goals
- `POST /savings` - Create savings goal
- `PUT /savings/:id` - Update savings goal

### Bills
- `GET /bills` - Get bills and reminders
- `POST /bills` - Create bill reminder
- `PUT /bills/:id` - Update bill

### Groups
- `GET /groups` - Get user groups
- `POST /groups` - Create new group
- `POST /groups/:id/expenses` - Add group expense

### Friends
- `GET /friends` - Get friends list
- `POST /friends/request` - Send friend request
- `PUT /friends/:id/accept` - Accept friend request

### AI Assistant
- `POST /ai/categorize` - Auto-categorize transaction
- `POST /ai/advice` - Get financial advice

### Dashboard
- `GET /dashboard/summary` - Get financial summary
- `GET /dashboard/analytics` - Get spending analytics

## 🔧 Configuration

### MongoDB Setup
1. **Local MongoDB:**
   ```bash
   # Install MongoDB
   # Windows: Download from mongodb.com
   # macOS: brew install mongodb-community
   # Linux: sudo apt install mongodb
   
   # Start MongoDB service
   mongod
   ```

2. **MongoDB Atlas (Cloud):**
   - Create account at [MongoDB Atlas](https://www.mongodb.com/atlas)
   - Create new cluster
   - Get connection string
   - Update `MONGO` in `.env` file

### Google OAuth Setup
1. Open [Google Cloud Console](https://console.cloud.google.com/)
2. Create new project or select existing project
3. Enable Google+ API
4. Create OAuth 2.0 credentials
5. Add authorized redirect URIs:
   - `http://localhost:3000/auth/google/callback` (development)
   - `https://yourdomain.com/auth/google/callback` (production)

### Email Configuration (Brevo)
1. Register at [Brevo](https://www.brevo.com/)
2. Create SMTP credentials
3. Update email configuration in `.env`

## 🚀 Production Deployment

### 1. Server Requirements
- Node.js v18+
- MongoDB
- Minimum 1GB RAM
- SSL Certificate (for HTTPS)

### 2. Environment Setup
```bash
# Set production environment
export NODE_ENV=production

# Install PM2 for process management
npm install -g pm2

# Start application with PM2
pm2 start server.js --name pennypal-backend

# Setup PM2 startup
pm2 startup
pm2 save
```

### 3. Nginx Configuration (Optional)
```nginx
server {
    listen 80;
    server_name yourdomain.com;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }
}
```

## 🧪 Testing

### Health Check
```bash
curl http://localhost:3000/health
```

### API Testing
```bash
# Test authentication
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password"}'

# Test OCR
curl -X POST http://localhost:3000/ocr/scan \
  -H "Content-Type: multipart/form-data" \
  -F "image=@receipt.jpg"
```

## 📝 Scripts

```bash
# Development
npm run serve          # Start with nodemon

# Production
npm start             # Start server

# Testing
npm test              # Run tests (if available)
```

## 🔒 Security Features

- **Helmet.js** - Security headers
- **CORS** - Cross-origin protection
- **Rate limiting** - API rate limiting
- **Input validation** - Request validation
- **JWT tokens** - Secure authentication
- **Password hashing** - bcrypt encryption
- **Session security** - Secure session configuration

## 🐛 Troubleshooting

### Common Issues

1. **Port already in use:**
   ```bash
   # Change port in .env
   PORT=3001
   ```

2. **MongoDB connection error:**
   ```bash
   # Make sure MongoDB is running
   mongod
   
   # Or check connection string in .env
   ```

3. **OCR not working:**
   ```bash
   # Install Tesseract
   # Windows: Download from GitHub
   # macOS: brew install tesseract
   # Linux: sudo apt install tesseract-ocr
   ```

4. **Google OAuth error:**
   - Make sure redirect URI is correct in Google Console
   - Check GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET

## 📞 Support

If you encounter issues:
1. Check logs in console
2. Make sure all environment variables are set
3. Verify database connection
4. Check API documentation at `/api` endpoint

## 📄 License

This project is licensed under the ISC License.

---

**PennyPal Backend** - Manage your finances easily and smartly! 💰✨