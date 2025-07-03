# SilverApp Backend - China Edition

A comprehensive social media backend application built with Node.js, Express, and MySQL, specifically designed for the Chinese market with full integration of China-compatible services.

## 🌟 Overview

SilverApp is a Facebook-like social media platform backend that provides a complete set of APIs for user management, social interactions, real-time messaging, payments, and more. The application is specifically optimized for deployment in China with support for local cloud services, payment providers, and push notification systems.

## 🏗️ Architecture

### Core Technologies
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MySQL with Sequelize ORM
- **Cache**: Redis
- **Real-time**: Socket.IO
- **Authentication**: JWT with refresh tokens
- **File Storage**: Tencent Cloud COS + Alibaba Cloud OSS
- **SMS**: Alibaba Cloud SMS + Tencent Cloud SMS
- **Payments**: WeChat Pay + Alipay
- **Push Notifications**: Xiaomi, Huawei, OPPO, Vivo, APNs
- **Analytics**: Baidu Analytics + Tencent Analytics

### Project Structure
```
backend/
├── app.js                      # Express application setup
├── server.js                   # Server entry point
├── package.json                # Dependencies and scripts
├── secret_rotation.js          # JWT secret rotation system
├── config/                     # Configuration files
│   ├── env.js                  # Environment configuration
│   ├── db.js                   # Database configuration
│   └── logger.js               # Winston logger setup
├── controllers/                # Route controllers
│   ├── authController.js       # Authentication logic
│   ├── chatController.js       # Messaging functionality
│   ├── friendController.js     # Friend management
│   ├── notificationController.js # Notification system
│   └── postController.js       # Post management
├── middleware/                 # Express middleware
│   ├── auth.js                 # Authentication middleware
│   ├── rateLimiting.js         # Rate limiting
│   ├── sqlInjectionFilter.js   # SQL injection protection
│   └── validator.js            # Request validation
├── models/                     # Sequelize models
│   ├── User.js                 # User model
│   ├── Post.js                 # Post model
│   ├── Message.js              # Message model
│   ├── Friend.js               # Friend relationship model
│   ├── Notification.js         # Notification model
│   ├── PaymentOrder.js         # Payment order model
│   ├── Gift.js                 # Gift model
│   └── CurrencyTransaction.js  # Virtual currency model
├── routes/                     # API routes
│   ├── authRoutes.js           # Authentication endpoints
│   ├── chatRoutes.js           # Chat endpoints
│   ├── friendRoutes.js         # Friend management endpoints
│   ├── notificationRoutes.js   # Notification endpoints
│   ├── postRoutes.js           # Post endpoints
│   ├── paymentRoutes.js        # Payment endpoints
│   ├── pushRoutes.js           # Push notification endpoints
│   └── uploadRoutes.js         # File upload endpoints
├── services/                   # Business logic services
│   ├── analytics.js            # Analytics service
│   ├── payment.js              # Payment processing
│   ├── paymentProcessor.js     # Payment business logic
│   ├── push.js                 # Push notifications
│   ├── redis.js                # Redis client
│   ├── sms.js                  # SMS service
│   ├── socket.js               # Socket.IO service
│   └── storage.js              # Cloud storage service
├── utils/                      # Utility functions
│   ├── asyncHandler.js         # Async error handling
│   ├── helpers.js              # Common utilities
│   └── security.js             # Security utilities
└── errors/                     # Error handling
    ├── AppError.js             # Custom error classes
    └── errorHandler.js         # Global error handler
```

## 🚀 Features

### 1. User Management & Authentication
- **Registration**: Phone-based registration with SMS verification
- **Login**: Multiple login methods (username/password, phone/OTP)
- **JWT Authentication**: Access and refresh token system
- **Security**: Account locking, rate limiting, password strength validation
- **Profile Management**: Complete user profile with privacy settings
- **Premium Subscriptions**: Paid premium features

### 2. Social Features
- **Posts**: Create, edit, delete posts with media support
- **Comments**: Nested commenting system
- **Likes & Reactions**: Post interaction system
- **Sharing**: Post sharing functionality
- **Privacy Controls**: Public, friends-only, private posts
- **Hashtags**: Hashtag support and trending topics

### 3. Friend System
- **Friend Requests**: Send, accept, decline friend requests
- **Friend Management**: Add, remove, block users
- **Close Friends**: Special friend categories
- **Mutual Friends**: Find common connections
- **Friend Suggestions**: AI-powered friend recommendations
- **Privacy**: Private profiles and friend list visibility

### 4. Real-time Messaging
- **Direct Messages**: One-on-one messaging
- **Message Types**: Text, images, videos, audio, files, location, contacts
- **Real-time Delivery**: Socket.IO powered real-time messaging
- **Read Receipts**: Message delivery and read status
- **Typing Indicators**: Real-time typing status
- **Message Reactions**: Emoji reactions to messages
- **Message Forwarding**: Forward messages to multiple users
- **Message Search**: Search through message history

### 5. Notification System
- **Real-time Notifications**: Socket.IO powered notifications
- **Push Notifications**: Multi-platform push support
- **Notification Types**: Likes, comments, friend requests, messages
- **Notification Settings**: Granular notification preferences
- **Notification Categories**: Social, system, promotional, security
- **Notification History**: Complete notification management

### 6. Payment System
- **WeChat Pay Integration**: Native WeChat Pay support
- **Alipay Integration**: Alipay payment processing
- **Premium Subscriptions**: Monthly, biannual, yearly plans
- **Virtual Currency**: In-app coin system
- **Gifts**: Send virtual gifts to friends
- **Post Boosting**: Paid post promotion
- **Refund System**: Automated refund processing

### 7. File Upload & Storage
- **Multi-cloud Storage**: Tencent COS + Alibaba OSS
- **File Types**: Images, videos, audio, documents
- **Avatar & Cover**: Profile picture management
- **Post Media**: Multiple media attachments
- **Message Media**: File sharing in messages
- **CDN Integration**: Fast global content delivery

### 8. Push Notifications
- **Android Support**: Xiaomi, Huawei, OPPO, Vivo push services
- **iOS Support**: Apple Push Notification Service (APNs)
- **Device Management**: Multi-device token management
- **Notification Targeting**: User-specific notifications
- **Bulk Notifications**: Mass notification system

### 9. Analytics & Monitoring
- **Baidu Analytics**: User behavior tracking
- **Tencent Analytics**: Advanced analytics
- **Event Tracking**: Custom event monitoring
- **Performance Metrics**: API performance tracking
- **Error Tracking**: Comprehensive error logging

### 10. Security Features
- **SQL Injection Protection**: Advanced SQL injection filtering
- **Rate Limiting**: Comprehensive rate limiting system
- **JWT Security**: Token rotation and blacklisting
- **Input Validation**: Joi-based request validation
- **CORS Protection**: Cross-origin request security
- **Helmet Security**: Security headers
- **XSS Protection**: Cross-site scripting prevention

## 📋 API Endpoints

### Authentication (`/api/v1/auth`)
```
POST   /register              # User registration
POST   /login                 # User login
POST   /login-otp             # OTP-based login
POST   /send-login-code       # Send login verification code
POST   /verify-phone          # Verify phone number
POST   /send-verification-code # Send verification code
POST   /refresh-token         # Refresh access token
POST   /forgot-password       # Initiate password reset
POST   /reset-password        # Reset password with code
POST   /change-password       # Change password (authenticated)
GET    /me                    # Get current user profile
POST   /logout                # Logout user
POST   /logout-all            # Logout from all devices
```

### Posts (`/api/v1/posts`)
```
POST   /                      # Create new post
GET    /feed                  # Get user feed
GET    /search                # Search posts
GET    /trending-hashtags     # Get trending hashtags
GET    /user/:userId          # Get user posts
GET    /:id                   # Get single post
PUT    /:id                   # Update post
DELETE /:id                   # Delete post
POST   /:id/like              # Like/unlike post
POST   /:id/comments          # Create comment
GET    /:id/comments          # Get post comments
POST   /:id/share             # Share post
POST   /:id/report            # Report post
```

### Chat (`/api/v1/chat`)
```
POST   /messages              # Send message
GET    /conversations         # Get conversations list
GET    /conversations/:id/messages # Get conversation messages
GET    /search                # Search messages
GET    /unread-count          # Get unread count
PUT    /messages/:id/read     # Mark message as read
DELETE /messages/:id          # Delete message
POST   /messages/:id/reactions # Add reaction
DELETE /messages/:id/reactions/:emoji # Remove reaction
POST   /messages/:id/forward  # Forward message
GET    /messages/:id/status   # Get message status
```

### Friends (`/api/v1/friends`)
```
POST   /request               # Send friend request
PUT    /request/:friendId     # Respond to friend request
GET    /                      # Get friends list
GET    /requests              # Get friend requests
GET    /suggestions           # Get friend suggestions
GET    /blocked               # Get blocked users
GET    /search                # Search users
GET    /:userId/mutual        # Get mutual friends
DELETE /:friendId             # Remove friend
POST   /block                 # Block user
POST   /unblock               # Unblock user
PUT    /:friendId/close-friend # Toggle close friend
```

### Notifications (`/api/v1/notifications`)
```
GET    /                      # Get notifications
GET    /counts                # Get notification counts
GET    /settings              # Get notification settings
GET    /stats                 # Get notification statistics
GET    /:id                   # Get specific notification
PUT    /settings              # Update notification settings
PUT    /:id/read              # Mark as read
PUT    /read-all              # Mark all as read
PUT    /:id/clicked           # Mark as clicked
PUT    /:id/snooze            # Snooze notification
DELETE /:id                   # Delete notification
DELETE /all                   # Delete all notifications
POST   /test                  # Send test notification
```

### Payments (`/api/v1/payment`)
```
POST   /create-order          # Create payment order
POST   /callback/wechat       # WeChat Pay callback
POST   /callback/alipay       # Alipay callback
GET    /query/:outTradeNo     # Query order status
POST   /refund                # Process refund
GET    /orders                # Get user orders
```

### File Upload (`/api/v1/upload`)
```
POST   /avatar                # Upload avatar
POST   /cover                 # Upload cover picture
POST   /post-media            # Upload post media
POST   /message-media         # Upload message media
POST   /presigned-url         # Generate presigned URL
DELETE /:key                  # Delete file
GET    /info/:key             # Get file info
```

### Push Notifications (`/api/v1/push`)
```
POST   /register-token        # Register device token
DELETE /remove-token          # Remove device token
GET    /tokens                # Get user tokens
POST   /send                  # Send notification (admin)
POST   /test                  # Test notification
GET    /stats                 # Get push statistics
GET    /health                # Check service health
```

## 🛠️ Installation & Setup

### Prerequisites
- Node.js 16+ 
- MySQL 8.0+
- Redis 6.0+
- China cloud service accounts (Tencent, Alibaba)

### Environment Variables
Create a `.env` file in the root directory:

```env
# Application
NODE_ENV=development
PORT=3000
API_VERSION=v1

# Database
DB_HOST=localhost
DB_PORT=3306
DB_NAME=silverapp
DB_USER=root
DB_PASSWORD=your_password

# JWT
JWT_SECRET=your_jwt_secret_min_32_chars
JWT_REFRESH_SECRET=your_refresh_secret_min_32_chars
JWT_EXPIRE=15m
JWT_REFRESH_EXPIRE=7d

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
REDIS_DB=0

# Alibaba Cloud SMS
ALIBABA_ACCESS_KEY_ID=your_access_key
ALIBABA_ACCESS_KEY_SECRET=your_secret_key
ALIBABA_SMS_SIGN_NAME=your_sign_name
ALIBABA_SMS_TEMPLATE_CODE=your_template_code

# Tencent Cloud SMS
TENCENT_SECRET_ID=your_secret_id
TENCENT_SECRET_KEY=your_secret_key
TENCENT_SMS_APP_ID=your_app_id
TENCENT_SMS_SIGN=your_sign
TENCENT_SMS_TEMPLATE_ID=your_template_id

# Tencent Cloud COS
TENCENT_COS_SECRET_ID=your_secret_id
TENCENT_COS_SECRET_KEY=your_secret_key
TENCENT_COS_BUCKET=your_bucket
TENCENT_COS_REGION=ap-beijing

# Alibaba Cloud OSS
ALIBABA_OSS_ACCESS_KEY_ID=your_access_key
ALIBABA_OSS_ACCESS_KEY_SECRET=your_secret_key
ALIBABA_OSS_BUCKET=your_bucket
ALIBABA_OSS_REGION=oss-cn-hangzhou

# WeChat Pay
WECHAT_APP_ID=your_app_id
WECHAT_APP_SECRET=your_app_secret
WECHAT_MCH_ID=your_merchant_id
WECHAT_API_KEY=your_api_key

# Alipay
ALIPAY_APP_ID=your_app_id
ALIPAY_PRIVATE_KEY_PATH=path_to_private_key
ALIPAY_PUBLIC_KEY_PATH=path_to_public_key

# Push Notifications
XIAOMI_PUSH_APP_SECRET=your_app_secret
XIAOMI_PUSH_PACKAGE_NAME=your_package_name
HUAWEI_PUSH_APP_ID=your_app_id
HUAWEI_PUSH_APP_SECRET=your_app_secret
OPPO_PUSH_APP_KEY=your_app_key
OPPO_PUSH_MASTER_SECRET=your_master_secret
VIVO_PUSH_APP_ID=your_app_id
VIVO_PUSH_APP_KEY=your_app_key
VIVO_PUSH_APP_SECRET=your_app_secret
APNS_KEY_PATH=path_to_p8_key
APNS_KEY_ID=your_key_id
APNS_TEAM_ID=your_team_id
APNS_BUNDLE_ID=your_bundle_id

# Analytics
BAIDU_ANALYTICS_SITE_ID=your_site_id
BAIDU_ANALYTICS_TOKEN=your_token
TENCENT_ANALYTICS_APP_ID=your_app_id
TENCENT_ANALYTICS_SECRET_KEY=your_secret_key
```

### Installation Steps

1. **Clone the repository**
```bash
git clone <repository-url>
cd silverapp-backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up database**
```bash
# Create MySQL database
mysql -u root -p
CREATE DATABASE silverapp;
```

4. **Configure environment**
```bash
cp .env.example .env
# Edit .env with your configuration
```

5. **Start Redis server**
```bash
redis-server
```

6. **Run the application**
```bash
# Development
npm run dev

# Production
npm start
```

## 📁 Detailed File Documentation

### Core Application Files

#### `app.js` - Express Application Setup
- **Purpose**: Main Express application configuration
- **Features**:
  - Security middleware (Helmet, CORS, XSS protection)
  - Rate limiting configuration
  - Body parsing and cookie handling
  - SQL injection protection
  - Request logging
  - Health check endpoints
  - API route mounting
  - Global error handling
  - Graceful shutdown handlers

#### `server.js` - Server Entry Point
- **Purpose**: Application bootstrap and service initialization
- **Features**:
  - Database connection and initialization
  - Redis service startup
  - Socket.IO initialization
  - Service availability checks
  - Secret rotation system
  - Graceful shutdown handling
  - Process error handlers

#### `secret_rotation.js` - JWT Security System
- **Purpose**: Automated JWT secret rotation for enhanced security
- **Features**:
  - Automatic secret generation
  - 24-hour rotation cycle
  - Grace period for token validation
  - Rotation history tracking
  - Redis integration for distributed systems
  - Manual rotation triggers

### Configuration Files

#### `config/env.js` - Environment Configuration
- **Purpose**: Centralized configuration management
- **Features**:
  - Environment variable validation
  - Secure secret loading from files
  - Database connection settings
  - JWT configuration
  - Redis settings
  - Cloud service configurations
  - Security settings
  - File upload settings
  - Push notification settings
  - Analytics configuration

#### `config/db.js` - Database Configuration
- **Purpose**: Sequelize ORM setup and database management
- **Features**:
  - MySQL connection configuration
  - Connection pooling
  - Model associations
  - Database synchronization
  - Connection testing
  - Error handling and retry logic

#### `config/logger.js` - Logging Configuration
- **Purpose**: Winston logger setup for comprehensive logging
- **Features**:
  - Multiple log levels
  - File and console transports
  - Log rotation
  - Structured logging
  - Error tracking
  - Request logging utilities

### Controllers

#### `controllers/authController.js` - Authentication Logic
- **Purpose**: User authentication and authorization
- **Features**:
  - User registration with phone verification
  - Multiple login methods (password, OTP)
  - JWT token management
  - Password reset functionality
  - Account security (locking, rate limiting)
  - Session management
  - Security event logging

#### `controllers/postController.js` - Post Management
- **Purpose**: Social media post functionality
- **Features**:
  - Post creation with media support
  - Feed generation with privacy controls
  - Comment system
  - Like/reaction system
  - Post sharing
  - Hashtag extraction
  - Content moderation
  - Search functionality

#### `controllers/chatController.js` - Messaging System
- **Purpose**: Real-time messaging functionality
- **Features**:
  - Direct messaging
  - Message types (text, media, location, contact)
  - Real-time delivery via Socket.IO
  - Read receipts and delivery status
  - Message reactions
  - Message forwarding
  - Conversation management
  - Message search

#### `controllers/friendController.js` - Social Connections
- **Purpose**: Friend relationship management
- **Features**:
  - Friend request system
  - Friend management (add, remove, block)
  - Close friend categories
  - Mutual friend discovery
  - Friend suggestions
  - User search
  - Privacy controls

#### `controllers/notificationController.js` - Notification System
- **Purpose**: User notification management
- **Features**:
  - Real-time notifications
  - Notification categories
  - Push notification integration
  - Notification preferences
  - Notification history
  - Bulk operations
  - Analytics tracking

### Middleware

#### `middleware/auth.js` - Authentication Middleware
- **Purpose**: Request authentication and authorization
- **Features**:
  - JWT token verification
  - Token blacklisting
  - Role-based access control
  - Device authentication
  - Rate limiting for auth endpoints
  - Security logging
  - Session management

#### `middleware/rateLimiting.js` - Rate Limiting
- **Purpose**: API rate limiting and abuse prevention
- **Features**:
  - Multiple rate limiting strategies
  - Redis-based storage
  - Endpoint-specific limits
  - User-based limiting
  - Dynamic rate limits
  - Comprehensive logging

#### `middleware/sqlInjectionFilter.js` - SQL Injection Protection
- **Purpose**: Advanced SQL injection attack prevention
- **Features**:
  - Pattern-based detection
  - Context-aware filtering
  - Input sanitization
  - Severity assessment
  - Comprehensive logging
  - Configurable responses

#### `middleware/validator.js` - Request Validation
- **Purpose**: Comprehensive request validation using Joi
- **Features**:
  - Schema-based validation
  - Custom validation rules
  - Input sanitization
  - Error formatting
  - Security validation
  - File upload validation

### Models

#### `models/User.js` - User Model
- **Purpose**: User data management and authentication
- **Features**:
  - Comprehensive user profile
  - Password hashing and verification
  - Phone/email verification
  - Premium subscription management
  - Security features (account locking)
  - Privacy settings
  - Virtual currency system
  - Activity tracking

#### `models/Post.js` - Post Model
- **Purpose**: Social media post management
- **Features**:
  - Post content and media
  - Privacy controls
  - Interaction counters
  - Hashtag support
  - Comment threading
  - Sharing functionality
  - Content moderation

#### `models/Message.js` - Message Model
- **Purpose**: Chat message management
- **Features**:
  - Multiple message types
  - Conversation threading
  - Delivery and read status
  - Message reactions
  - File attachments
  - Message forwarding
  - Encryption support

#### `models/Friend.js` - Friend Relationship Model
- **Purpose**: Social connection management
- **Features**:
  - Friend request workflow
  - Relationship status tracking
  - Blocking functionality
  - Close friend categories
  - Interaction tracking
  - Mutual friend discovery

#### `models/Notification.js` - Notification Model
- **Purpose**: User notification management
- **Features**:
  - Multiple notification types
  - Delivery tracking
  - Read/seen status
  - Priority levels
  - Categories
  - Expiration handling
  - Analytics data

#### `models/PaymentOrder.js` - Payment Order Model
- **Purpose**: Payment transaction management
- **Features**:
  - Order tracking
  - Payment provider integration
  - Refund management
  - Order status tracking
  - Payment metadata

### Services

#### `services/sms.js` - SMS Service
- **Purpose**: SMS sending via Chinese providers
- **Features**:
  - Alibaba Cloud SMS integration
  - Tencent Cloud SMS integration
  - Fallback mechanism
  - Rate limiting
  - Template management
  - Delivery tracking

#### `services/storage.js` - Cloud Storage Service
- **Purpose**: File storage via Chinese cloud providers
- **Features**:
  - Tencent Cloud COS integration
  - Alibaba Cloud OSS integration
  - Multi-cloud fallback
  - File type validation
  - CDN integration
  - Presigned URL generation

#### `services/payment.js` - Payment Service
- **Purpose**: Payment processing for Chinese market
- **Features**:
  - WeChat Pay integration
  - Alipay integration
  - Order management
  - Callback verification
  - Refund processing
  - Security validation

#### `services/push.js` - Push Notification Service
- **Purpose**: Multi-platform push notifications
- **Features**:
  - Android push (Xiaomi, Huawei, OPPO, Vivo)
  - iOS push (APNs)
  - Device token management
  - Bulk notifications
  - Delivery tracking
  - Platform-specific optimization

#### `services/socket.js` - Real-time Communication
- **Purpose**: Socket.IO based real-time features
- **Features**:
  - Real-time messaging
  - Presence tracking
  - Typing indicators
  - Live notifications
  - Connection management
  - Room management

#### `services/redis.js` - Redis Client
- **Purpose**: Redis cache and session management
- **Features**:
  - Connection management
  - Data serialization
  - Error handling
  - Reconnection logic
  - Performance optimization

#### `services/analytics.js` - Analytics Service
- **Purpose**: User behavior and performance tracking
- **Features**:
  - Baidu Analytics integration
  - Tencent Analytics integration
  - Event tracking
  - Performance metrics
  - Error tracking
  - Custom analytics

### Routes

#### `routes/authRoutes.js` - Authentication Routes
- **Endpoints**: User registration, login, verification, password management
- **Security**: Rate limiting, input validation, SQL injection protection

#### `routes/postRoutes.js` - Post Routes
- **Endpoints**: Post CRUD, feed, comments, likes, sharing
- **Features**: Privacy controls, media handling, search

#### `routes/chatRoutes.js` - Chat Routes
- **Endpoints**: Messaging, conversations, reactions, forwarding
- **Features**: Real-time integration, media support

#### `routes/friendRoutes.js` - Friend Routes
- **Endpoints**: Friend management, requests, blocking, suggestions
- **Features**: Privacy controls, mutual friends

#### `routes/notificationRoutes.js` - Notification Routes
- **Endpoints**: Notification management, settings, analytics
- **Features**: Push integration, preferences

#### `routes/paymentRoutes.js` - Payment Routes
- **Endpoints**: Order creation, callbacks, refunds, history
- **Features**: Multi-provider support, security

#### `routes/uploadRoutes.js` - Upload Routes
- **Endpoints**: File upload, management, presigned URLs
- **Features**: Multi-cloud support, validation

#### `routes/pushRoutes.js` - Push Notification Routes
- **Endpoints**: Token management, notification sending, testing
- **Features**: Multi-platform support, analytics

### Utilities

#### `utils/security.js` - Security Utilities
- **Purpose**: Security-related helper functions
- **Features**:
  - JWT token management
  - Encryption/decryption
  - Input validation
  - Rate limiting utilities
  - Security headers
  - CSRF protection

#### `utils/helpers.js` - Common Utilities
- **Purpose**: General-purpose helper functions
- **Features**:
  - String manipulation
  - Data validation
  - Date formatting
  - File handling
  - Pagination
  - Performance utilities

#### `utils/asyncHandler.js` - Async Error Handling
- **Purpose**: Async function error handling
- **Features**:
  - Promise error catching
  - Retry mechanisms
  - Timeout handling
  - Parallel execution
  - Sequential execution

### Error Handling

#### `errors/AppError.js` - Custom Error Classes
- **Purpose**: Standardized error definitions
- **Features**:
  - Custom error types
  - HTTP status codes
  - Error categorization
  - Operational vs programming errors

#### `errors/errorHandler.js` - Global Error Handler
- **Purpose**: Centralized error processing
- **Features**:
  - Environment-specific handling
  - Error logging
  - Security-focused responses
  - Database error handling
  - JWT error handling
  - Rate limit error handling

## 🔒 Security Features

### Authentication & Authorization
- JWT-based authentication with refresh tokens
- Automatic token rotation every 24 hours
- Token blacklisting for logout
- Role-based access control
- Device-specific authentication
- Account locking after failed attempts

### Input Validation & Sanitization
- Joi-based request validation
- SQL injection protection with pattern detection
- XSS prevention
- Input sanitization
- File type validation
- Rate limiting on all endpoints

### Data Protection
- Password hashing with bcrypt
- Sensitive data encryption
- Secure secret management
- HTTPS enforcement
- CORS protection
- Security headers (Helmet)

### Monitoring & Logging
- Comprehensive security event logging
- Failed authentication tracking
- Rate limit monitoring
- Error tracking and alerting
- Performance monitoring

## 🚀 Deployment

### Production Considerations
1. **Environment Setup**
   - Use production-grade MySQL and Redis instances
   - Configure proper SSL certificates
   - Set up load balancing
   - Configure CDN for static assets

2. **Security Hardening**
   - Enable all security middleware
   - Configure proper CORS origins
   - Set up rate limiting
   - Enable request logging

3. **Monitoring**
   - Set up application monitoring
   - Configure error tracking
   - Enable performance monitoring
   - Set up alerting

4. **Scaling**
   - Use Redis for session storage
   - Configure database read replicas
   - Set up horizontal scaling
   - Optimize database queries

## 📊 Performance Optimization

### Database Optimization
- Proper indexing on frequently queried fields
- Connection pooling
- Query optimization
- Read replicas for scaling

### Caching Strategy
- Redis for session storage
- API response caching
- Database query caching
- Static asset caching

### Real-time Performance
- Socket.IO optimization
- Connection management
- Room-based messaging
- Presence tracking optimization

## 🧪 Testing

### Available Scripts
```bash
npm test              # Run all tests
npm run test:watch    # Run tests in watch mode
npm run test:coverage # Run tests with coverage
npm run test:unit     # Run unit tests only
npm run test:integration # Run integration tests only
```

### Test Structure
- Unit tests for individual functions
- Integration tests for API endpoints
- Database tests for model operations
- Security tests for authentication

## 📈 Monitoring & Analytics

### Application Metrics
- API response times
- Error rates
- User activity
- Database performance
- Cache hit rates

### Business Metrics
- User registration rates
- Message volume
- Post engagement
- Payment transactions
- Push notification delivery

### Chinese Analytics Integration
- Baidu Analytics for web tracking
- Tencent Analytics for mobile tracking
- Custom event tracking
- Performance monitoring

## 🔧 Development

### Code Style
- ESLint configuration
- Prettier formatting
- Consistent naming conventions
- Comprehensive commenting

### Git Workflow
- Feature branch development
- Pull request reviews
- Automated testing
- Continuous integration

### Development Tools
- Nodemon for auto-restart
- Winston for logging
- Jest for testing
- Sequelize CLI for migrations

## 📞 Support

### Documentation
- API documentation
- Code comments
- README files
- Deployment guides

### Troubleshooting
- Common issues and solutions
- Error code references
- Performance optimization guides
- Security best practices

## 🔄 Updates & Maintenance

### Regular Maintenance
- Security updates
- Dependency updates
- Performance optimization
- Bug fixes

### Feature Development
- New feature planning
- API versioning
- Backward compatibility
- Migration strategies

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new features
5. Ensure all tests pass
6. Submit a pull request

## 📞 Contact

For questions, issues, or contributions, please contact the development team.

---

**SilverApp Backend** - A comprehensive social media platform built for the Chinese market with enterprise-grade security, scalability, and performance.