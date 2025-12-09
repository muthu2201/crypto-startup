# LedgerFlow

**Real-time On-Chain Financial Visibility for Web3 Teams**

LedgerFlow is a production-ready SaaS platform that provides comprehensive financial visibility for Web3 teams, DAOs, crypto freelancers, and small funds. Track balances, transactions, token movements, and generate financial reports across multiple crypto wallets.

## 🎯 Features

- **Multi-Wallet Support**: Connect up to 3 wallets (Free tier) or unlimited (Treasury tier)
- **Multi-Chain Support**: Ethereum, Polygon, BSC, Base
- **Transaction Tracking**: Real-time indexing of all transactions, token transfers, and gas fees
- **Classification**: Classify transactions as Income, Expense, or Internal Transfer
- **Tagging System**: Organize transactions with custom tags
- **Financial Reports**: Generate monthly summaries, CSV, and JSON exports
- **Shared Links**: Create read-only shareable links for investors, auditors, and team members
- **Secure**: Read-only access, no private keys, no transaction signing

## 🛠️ Tech Stack

### Backend
- **Framework**: NestJS (Node.js)
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: JWT + OAuth (Google, GitHub)
- **Blockchain**: ethers.js with Alchemy/QuickNode RPC
- **Security**: Helmet, CORS, Rate Limiting, Audit Logging

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: TailwindCSS + ShadCN UI
- **State Management**: React Context + Server Components

## 📦 Installation

### Quick Start

See [SETUP_GUIDE.md](./SETUP_GUIDE.md) for detailed step-by-step instructions.

### Prerequisites
- Node.js 18+ and npm/yarn
- PostgreSQL database (local or cloud: Supabase/Neon)
- ✅ Alchemy API key already configured for all chains (see ALCHEMY_SETUP.md)

### Backend Setup

```bash
cd backend
npm install

# Copy and configure environment variables
cp .env.example .env

# Generate JWT secrets
node scripts/generate-secrets.js
# Copy the generated secrets to .env

# Edit .env with your configuration:
# - DATABASE_URL (from Supabase/Neon or local PostgreSQL)
# - JWT_SECRET and JWT_REFRESH_SECRET (from generate:secrets)
# - RPC URLs are already configured with Alchemy API key!
# - OAuth credentials (optional)

# Set up database
npx prisma generate
npx prisma migrate dev

# Start development server
npm run start:dev
```

### Frontend Setup

```bash
cd frontend
npm install

# Create .env.local
echo "NEXT_PUBLIC_API_URL=http://localhost:3001" > .env.local

# Start development server
npm run dev
```

### Getting API Keys

**Blockchain RPC:** ✅ **Already Configured!**
- Alchemy API key `r4tABc1OmdxjSvueba7OL` is set up for Ethereum, Polygon, and Base
- See [ALCHEMY_SETUP.md](./ALCHEMY_SETUP.md) for details
- BSC uses public RPC (no key needed)

**OAuth (Optional):**
- **Google**: https://console.cloud.google.com/apis/credentials
- **GitHub**: https://github.com/settings/developers

**Database (Required):**
- **Supabase**: https://supabase.com - Free tier available
- **Neon**: https://neon.tech - Free tier available
- **Local PostgreSQL**: Install locally

## 🚀 Deployment

### Backend (Railway/Render)

1. Connect your GitHub repository
2. Set environment variables in the platform dashboard
3. Deploy

### Frontend (Vercel)

1. Import your GitHub repository
2. Set environment variables
3. Deploy

### Database (Supabase/Neon)

1. Create a new PostgreSQL database
2. Get connection string
3. Update `DATABASE_URL` in backend environment variables
4. Run migrations: `npx prisma migrate deploy`

## 🚀 Quick Test URLs

Once servers are running:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3001/api/v1
- **API Docs (Swagger)**: http://localhost:3001/api/docs

See [TESTING_URLS.md](./TESTING_URLS.md) for complete testing guide.

## 📚 API Documentation

Once the backend is running, visit:
- Swagger UI: `http://localhost:3001/api/docs`

## 🔐 Security

- **No Private Keys**: System never stores or handles private keys
- **Read-Only Access**: All blockchain interactions are read-only
- **Rate Limiting**: 100 requests per minute per user
- **Input Validation**: All inputs validated and sanitized
- **Audit Logging**: All sensitive operations logged
- **Encrypted Storage**: Sensitive data encrypted at rest

## 📊 Database Schema

See `prisma/schema.prisma` for the complete database schema.

Key models:
- User, Wallet, Transaction, Token, Tag
- Report, SharedReadOnlyLink, Subscription
- APIKey, AuditLog

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test

# E2E tests
npm run test:e2e
```

## 📝 License

MIT

## 🤝 Contributing

This is a production MVP. For production use, ensure:
1. All environment variables are properly configured
2. Database migrations are run
3. Security best practices are followed
4. Monitoring and logging are set up

## 📧 Support

For issues and questions, please open a GitHub issue.

