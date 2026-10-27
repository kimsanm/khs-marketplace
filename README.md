# KHS Market — Multi-vendor Digital Marketplace

A full-stack starter for an original multi-vendor marketplace with React + Vite + Tailwind, Express, MongoDB Atlas, JWT authentication, USD/KHR display, seller tools, admin moderation, and payment-verified automatic delivery.

## Requirements
- Node.js 20+
- MongoDB Atlas database (or local MongoDB)
- A payment provider account for production payment verification

## Quick start

### 1) Configure backend
```bash
cd server
cp .env.example .env
# Edit .env and set MONGODB_URI, JWT_SECRET, CLIENT_URL, and payment provider values
npm install
npm run dev
```

### 2) Configure frontend
In another terminal:
```bash
cd client
cp .env.example .env
npm install
npm run dev
```
Open the Vite URL (normally http://localhost:5173).

### 3) Create the first admin
Register a normal user in the app, then promote that user in MongoDB:
```javascript
db.users.updateOne({ email: "you@example.com" }, { $set: { role: "admin" } })
```
Do not expose database credentials or JWT secrets in the frontend.

## Important payment note
The included payment integration is a **safe provider adapter/demo stub**. It does not pretend a payment is real. Orders remain `pending_payment` until a verified server-side provider webhook confirms payment. Automatic delivery runs only after that verified event. Before production, implement the selected provider's signature verification and status lookup in `server/src/services/paymentProvider.js`, and configure the provider webhook URL to `/api/payments/webhook`.

## Main features
- Email/password registration and login with bcrypt + JWT
- Customer, seller, and admin roles
- Seller application / seller profile basics
- Product create, edit, publish, and moderation status
- Product listing, category/search filters, and product details
- Cart and checkout order creation
- USD and KHR price display using configurable exchange rate
- Server-side order total calculation
- Payment webhook endpoint with signature-verification placeholder
- Automatic digital delivery after verified payment
- Admin overview, product moderation, and order list
- Rate limiting, Helmet, CORS, validation, and role middleware

## Production checklist
- Implement provider-specific webhook signature verification and server-side payment status checks.
- Use HTTPS and secure cookies or short-lived access tokens with refresh-token rotation.
- Configure transactional email, logging, backups, monitoring, and abuse protection.
- Set real product file storage (S3-compatible object storage); never store private download links in public product JSON.
- Add tax, consumer-protection, seller verification, dispute, refund, and privacy policies.
- Keep products/services authorized and compliant with each platform's terms.
