# FixMate — Server (API)

Express + MongoDB + JWT + Stripe backend for **FixMate**, an on-demand device & home appliance repair service booking platform.

## Purpose
Serves the 4 core collections (`user` via BetterAuth, `services`, `bookings`, `payments`), enforces role-based access (customer / technician / admin), the server-side job status pipeline, and Stripe pay-after-service checkout.

## Stack
- Node.js · Express 4 · TypeScript
- MongoDB (native driver)
- JWT role middlewares (`verifyToken` · `verifyCustomer` · `verifyTechnician` · `verifyAdmin`)
- Stripe Checkout + Webhook (test mode) · ImgBB upload proxy
- multer, cors, dotenv

## Env (`.env` — see `.env.example`)
| Key | Where to get it |
|---|---|
| `MONGODB_URI` | [MongoDB Atlas](https://cloud.mongodb.com) free cluster |
| `JWT_SECRET` | must **match** `JWT_SECRET` in client `.env.local` |
| `CORS_ORIGINS` | your client origin(s), comma separated |
| `STRIPE_SECRET_KEY` | Stripe dashboard → Developers → API keys (test) |
| `STRIPE_WEBHOOK_SECRET` | Stripe dashboard → Webhooks (test mode) |
| `IMGBB_API_KEY` | https://api.imgbb.com/ |

## Run
```bash
npm install
cp .env.example .env   # fill values
npm run dev            # http://localhost:5000/api/health
```
Production: `npm run build && npm start`

## API
`GET /api/services` (search/filter/sort/paginate) · service CRUD · bookings + status pipeline · payments (checkout/verify/webhook) · admin moderation · profile · `/api/upload/imgbb` — full table in `../FIXMATE-PAGES-AND-PROTOTYPE.md`.
