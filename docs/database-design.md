# 🗄️ AI ARTISAN HUB — Database Design

## 1. Overview

AI ARTISAN HUB uses a cloud-based backend architecture designed to support:

- Artisan marketplace operations
- Buyer shopping
- Delivery management
- Admin operations
- Social commerce
- Real-time chat
- AI-powered services
- Notifications
- Payments and orders
- Analytics and audit logging

The suggested backend storage architecture uses Firebase Firestore, Cloud Storage, Cloud Functions, Firebase Authentication, Firebase Cloud Messaging, and secure backend services.

---

## 2. Core Collections

The major database entities are:

- users
- artisanProfiles
- products
- stories
- posts
- follows
- conversations
- messages
- orders
- payments
- deliveries
- notifications
- reports
- auditLogs

---

## 3. Users Collection

### Collection

`users/{userId}`

### Purpose

Stores the core account information for every application user.

### Fields

- userId
- name
- email
- phone
- profileImage
- role
- language
- isActive
- createdAt
- updatedAt
- lastLoginAt

### Roles

- artisan
- buyer
- delivery
- admin

The user role must be validated by the backend and must not be trusted only from the Android client.

---

## 4. Artisan Profiles

### Collection

`artisanProfiles/{artisanId}`

### Purpose

Stores artisan-specific business and storefront information.

### Fields

- artisanId
- userId
- businessName
- description
- profileImage
- coverImage
- location
- categories
- verificationStatus
- rating
- totalSales
- followersCount
- createdAt
- updatedAt

---

## 5. Products

### Collection

`products/{productId}`

### Purpose

Stores marketplace product information.

### Fields

- productId
- artisanId
- name
- description
- category
- images
- price
- discountPrice
- stockQuantity
- sku
- materials
- dimensions
- weight
- status
- isPublished
- createdAt
- updatedAt

### Product Status

- draft
- published
- outOfStock
- archived

AI-generated product descriptions and catalog information should be reviewed and confirmed by the artisan before publication.

---

## 6. Stories

### Collection

`stories/{storyId}`

### Purpose

Stores temporary social content created by artisans and other permitted users.

### Fields

- storyId
- userId
- mediaUrl
- mediaType
- caption
- mentions
- createdAt
- expiresAt
- views

---

## 7. Posts

### Collection

`posts/{postId}`

### Purpose

Stores social feed posts.

### Fields

- postId
- userId
- caption
- media
- mediaType
- productIds
- hashtags
- mentions
- likesCount
- commentsCount
- sharesCount
- createdAt
- updatedAt

Product references allow social content to connect directly with marketplace products.

---

## 8. Follows

### Collection

`follows/{followId}`

### Fields

- followId
- followerId
- followingId
- createdAt

This supports the social discovery and personalized feed system.

---

## 9. Conversations

### Collection

`conversations/{conversationId}`

### Purpose

Stores buyer-artisan and support conversations.

### Fields

- conversationId
- participantIds
- orderId
- lastMessage
- lastMessageAt
- createdAt
- updatedAt

Order-linked conversations allow communication to remain connected with a specific purchase.

---

## 10. Messages

### Collection

`conversations/{conversationId}/messages/{messageId}`

### Fields

- messageId
- senderId
- receiverId
- messageType
- text
- mediaUrl
- productId
- orderId
- replyToMessageId
- mentions
- reaction
- isDelivered
- isRead
- createdAt

### Supported Message Types

- text
- image
- product
- voice
- system

---

## 11. Orders

### Collection

`orders/{orderId}`

### Purpose

Stores the complete lifecycle of marketplace orders.

### Fields

- orderId
- buyerId
- artisanId
- items
- subtotal
- discount
- deliveryFee
- tax
- totalAmount
- paymentId
- deliveryId
- shippingAddress
- status
- createdAt
- updatedAt

---

## 12. Order Lifecycle

The main order lifecycle is:

Created  
↓  
Payment Pending  
↓  
Paid  
↓  
Confirmed  
↓  
Preparing  
↓  
Ready for Pickup  
↓  
Picked Up  
↓  
In Transit  
↓  
Delivered

### Exception States

- Payment Failed
- Cancelled
- Return Requested
- Return Approved
- Returned
- Refunded

Order state transitions should be validated by secure backend logic.

---

## 13. Payments

### Collection

`payments/{paymentId}`

### Fields

- paymentId
- orderId
- buyerId
- amount
- currency
- provider
- providerTransactionId
- status
- paymentMethod
- createdAt
- updatedAt
- verifiedAt

Payment verification must happen through secure backend services and provider webhooks.

---

## 14. Deliveries

### Collection

`deliveries/{deliveryId}`

### Fields

- deliveryId
- orderId
- deliveryPartnerId
- pickupLocation
- deliveryLocation
- status
- currentLocation
- estimatedArrival
- pickupTime
- deliveryTime
- proofOfDelivery
- exceptionReason
- createdAt
- updatedAt
- ---

## 15. Notifications

### Collection

`notifications/{notificationId}`

### Fields

- notificationId
- userId
- type
- title
- body
- data
- isRead
- createdAt

Notifications can be generated for:

- Orders
- Payments
- Delivery updates
- Messages
- Follows
- Mentions
- Stories
- Promotions
- AI tasks
- Administrative events

---

## 16. Reports

### Collection

`reports/{reportId}`

### Purpose

Supports moderation, safety, and abuse reporting.

### Fields

- reportId
- reporterId
- targetType
- targetId
- reason
- description
- status
- reviewedBy
- resolution
- createdAt
- updatedAt

### Status Values

- open
- under_review
- resolved
- dismissed

---

## 17. Audit Logs

### Collection

`auditLogs/{logId}`

### Purpose

Records important backend and administrative actions.

### Fields

- logId
- actorId
- actorRole
- action
- targetType
- targetId
- metadata
- timestamp

Audit logging is important for security, administration, AI actions, payment operations, and sensitive workflow changes.

---

## 18. Firebase Storage

Large media files should not be stored directly inside Firestore documents.

Firebase Cloud Storage can be used for:

- Profile images
- Product images
- Story media
- Post media
- Reels and videos
- Chat images
- Voice messages
- Proof-of-delivery media
- Documents

Firestore should store the appropriate secure media references or URLs.

---

## 19. Authentication

Firebase Authentication can manage account authentication.

Supported authentication methods may include:

- Email / Password
- Phone Authentication
- Google
- Facebook

The authenticated identity should be connected to the corresponding `users` document.

---

## 20. Role-Based Authorization

The backend must enforce role-based authorization.

### Buyer

- Browse products
- Create orders
- Send messages
- Track own orders

### Artisan

- Manage products
- Manage orders
- View earnings
- Communicate with customers

### Delivery

- View assigned jobs
- Update delivery status
- Upload proof of delivery
- Manage delivery workflow

### Admin

- Manage users
- Moderate content
- Manage operations
- View analytics
- Review audit information

Authorization must be enforced on the server/backend layer.

---

## 21. AI Data Access

AI services must not receive unrestricted database access.

The recommended flow is:

User  
↓  
Android Application  
↓  
Backend API / Cloud Function  
↓  
Authentication + Role Check  
↓  
Permission Check  
↓  
Authorized Data Retrieval  
↓  
AI Service  
↓  
Response / Draft  
↓  
User Confirmation  
↓  
Backend Action

AI tools should access only the information required for the current task.

---

## 22. Security Principles

The database architecture should follow these principles:

- Server-side authorization
- Least-privilege access
- Secure authentication
- Firestore security rules
- Media validation
- Rate limiting
- Audit logging
- Sensitive-data protection
- Secure payment verification
- No secret API keys in the Android application
- No privileged database credentials inside the mobile client

---

## 23. Data Relationships

Simplified relationship model:

```text
users
 ├── artisanProfiles
 ├── products
 ├── stories
 ├── posts
 ├── follows
 ├── conversations
 ├── orders
 ├── notifications
 └── reports

products
 └── orders

orders
 ├── payments
 ├── deliveries
 └── conversations

conversations
 └── messages

users
 └── auditLogs

The database design should support future expansion including:

AI-powered personalization
Advanced analytics
Live shopping
Wholesale/B2B
Custom orders
Digital certificates
Smart bundles
Fraud detection
Offline-first artisan drafts
Web-based administration
Deep links


The database architecture is designed to provide a secure and scalable foundation for the four connected AI ARTISAN HUB products:
Artisan Business Platform
          +
Buyer Social Commerce
          +
Delivery Operations
          +
Admin Control Center
