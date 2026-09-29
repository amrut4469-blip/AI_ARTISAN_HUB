# AI ARTISAN HUB — User Roles

## Overview

AI ARTISAN HUB is designed around four connected user roles:

1. Artisan
2. Buyer
3. Delivery Partner
4. Administrator

Each role has a dedicated dashboard and role-specific workflows.

---

# 1. Artisan

## Artisan Dashboard

The Artisan dashboard includes:

- Home
- Products
- Orders
- Earnings
- Stories
- AI Studio
- Messages

## Artisan Capabilities

Artisans can:

- Manage their profile and store
- Create and manage products
- Manage inventory
- Process orders
- Track earnings
- Create stories
- Communicate with customers
- Manage promotional content
- View business insights

## Artisan AI — Artisan Copilot

The Artisan Copilot includes:

- Product Writer
- Visual Catalog AI
- Pricing Helper
- Content Creator
- Sales Insights
- Customer Reply Assistant
- Stock Forecast
- Business Coach

AI-generated factual claims should be reviewed and confirmed by the artisan.

---

# 2. Buyer

## Buyer Dashboard

The Buyer dashboard includes:

- Feed
- Explore
- Shop
- Cart
- Orders
- Chats
- Stories
- AI Shopping

## Buyer Capabilities

Buyers can:

- Discover products
- Search products
- View product details
- Add products to cart
- Manage wishlist
- Checkout
- Track orders
- Review purchases
- Follow artisans
- Save content and products
- Communicate with artisans

## Buyer AI — Smart Shopping Assistant

The Buyer AI includes:

- Visual Search
- Conversational Discovery
- Gift Assistant
- Compare Assistant
- Personalized Discovery
- Order Assistant
- Review Summarizer
- Support Assistant

---

# 3. Delivery Partner

## Delivery Dashboard

The Delivery dashboard includes:

- Jobs
- Map
- Pickup
- Delivery
- Proof
- Earnings
- AI Route

## Delivery Capabilities

Delivery partners can:

- Switch online/offline status
- View delivery jobs
- View order details
- Navigate to pickup locations
- Manage pickup
- Update delivery status
- Provide proof of delivery
- Handle delivery exceptions
- Track earnings

## Delivery AI — Route & Operations Copilot

The Delivery AI includes:

- Route Planner
- ETA Assistant
- Task Prioritizer
- Exception Assistant
- Voice Mode
- Daily Summary

---

# 4. Administrator

## Admin Dashboard

The Admin dashboard includes:

- Users
- Products
- Orders
- Delivery
- Content
- Finance
- AI
- Analytics

## Administrator Capabilities

Administrators can:

- Manage users
- Verify artisans
- Moderate products
- Manage orders
- Monitor payments and reconciliation
- Manage delivery operations
- Moderate content
- Manage notifications
- View analytics
- Review audit logs

## Admin AI — Operations Intelligence Center

The Admin AI includes:

- Anomaly Detection
- Moderation Copilot
- Business Analyst
- Support Copilot
- Forecasting
- Incident Summarizer
- AI Governance Panel

The moderation copilot is intended to assist moderation workflows rather than silently perform banning decisions.

---

# Role-Based Architecture

```text
                    AI ARTISAN HUB
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
    ARTISAN              BUYER          DELIVERY PARTNER
        │                  │                  │
 Artisan Copilot     Shopping AI       Route & Operations AI
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                           ▼
                    ADMINISTRATOR
                           │
                           ▼
              Operations Intelligence AI
