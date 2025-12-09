# LedgerFlow Setup Guide

Complete step-by-step guide to get LedgerFlow running.

## Prerequisites

- Node.js 18+ installed
- PostgreSQL database (local or cloud)
- Git installed

## Step 1: Clone and Install

```bash
# Clone the repository
git clone <your-repo-url>
cd crypto

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

## Step 2: Set Up Database

### Option A: Local PostgreSQL

```bash
# Install PostgreSQL (if not installed)
# macOS: brew install postgresql
# Ubuntu: sudo apt-get install postgresql
# Windows: Download from postgresql.org

# Create database
createdb ledgerflow

# Or using psql:
psql -U postgres
CREATE DATABASE ledgerflow;
\q
```

### Option B: Cloud Database (Recommended)

1. **Supabase** (Free tier available)
   - Go to https://supabase.com
   - Create new project
   - Copy connection string from Settings > Database

2. **Neon** (Free tier available)
   - Go to https://neon.tech
   - Create new project
   - Copy connection string

## Step 3: Configure Environment Variables

### Backend Configuration

```bash
cd backend

# Copy example file
cp .env.example .env

# Generate JWT secrets
node scripts/generate-secrets.js

# Edit .env file with your values
nano .env  # or use your preferred editor
```

**Required values to fill:**

1. **DATABASE_URL**
   ```
   DATABASE_URL=postgresql://user:password@host:port/database
   ```

2. **JWT Secrets** (generated above)
   ```
   JWT_SECRET=<generated-secret>
   JWT_REFRESH_SECRET=<generated-secret>
   ```

3. **Blockchain RPC URLs** ✅ **Already Configured!**

   Your Alchemy API key is already set up for all chains:
   ```
   ETHEREUM_RPC_URL=https://eth-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
   POLYGON_RPC_URL=https://polygon-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
   BASE_RPC_URL=https://base-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
   BSC_RPC_URL=https://bsc-dataseed.binance.org/
   ```
   
   These are already in the `.env.example` file - just copy them to your `.env` file.

4. **OAuth (Optional but recommended)**

   **Google OAuth:**
   - Go to https://console.cloud.google.com/apis/credentials
   - Create OAuth 2.0 Client ID
   - Add redirect URI: `http://localhost:3001/api/v1/auth/google/callback`
   - Copy Client ID and Secret

   **GitHub OAuth:**
   - Go to https://github.com/settings/developers
   - Create new OAuth App
   - Set callback URL: `http://localhost:3001/api/v1/auth/github/callback`
   - Copy Client ID and Secret

### Frontend Configuration

```bash
cd frontend

# Create .env.local file
cat > .env.local << EOF
NEXT_PUBLIC_API_URL=http://localhost:3001
EOF
```

## Step 4: Set Up Database Schema

```bash
cd backend

# Generate Prisma Client
npx prisma generate

# Run migrations
npx prisma migrate dev --name init

# (Optional) Open Prisma Studio to view database
npx prisma studio
```

## Step 5: Start Development Servers

### Terminal 1: Backend

```bash
cd backend
npm run start:dev
```

Backend will run on http://localhost:3001
API docs available at http://localhost:3001/api/docs

### Terminal 2: Frontend

```bash
cd frontend
npm run dev
```

Frontend will run on http://localhost:3000

## Step 6: Verify Installation

1. **Check Backend:**
   - Visit http://localhost:3001/api/docs
   - You should see Swagger API documentation

2. **Check Frontend:**
   - Visit http://localhost:3000
   - Should redirect to login page

3. **Test API:**
   ```bash
   # Register a test user
   curl -X POST http://localhost:3001/api/v1/auth/register \
     -H "Content-Type: application/json" \
     -d '{"email":"test@example.com","password":"Test123!@#","name":"Test User"}'
   ```

## Step 7: Add Your First Wallet

1. Log in to the frontend
2. Click "Add Wallet"
3. Enter a wallet address (e.g., `0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb`)
4. Select chain (Ethereum, Polygon, BSC, or Base)
5. The indexer will start fetching transactions

## Troubleshooting

### Database Connection Error

```bash
# Check if PostgreSQL is running
# macOS/Linux:
pg_isready

# Check connection string format
# Should be: postgresql://user:password@host:port/database
```

### RPC Connection Error

- Verify RPC URLs are correct
- Check if API keys are valid
- For Alchemy, ensure you're using the correct network (mainnet vs testnet)
- Try using public RPC for testing

### JWT Secret Error

```bash
# Generate new secrets
cd backend
node scripts/generate-secrets.js
# Copy to .env file
```

### Port Already in Use

```bash
# Change port in .env
PORT=3002  # or any available port
```

## Production Deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md) for production deployment instructions.

## Next Steps

- Complete frontend UI pages
- Set up monitoring (Sentry)
- Configure backups
- Set up CI/CD
- Review security checklist

## Getting Help

- Check [README.md](./README.md) for overview
- See [API_ROUTES.md](./API_ROUTES.md) for API documentation
- Review [PRODUCTION_CHECKLIST.md](./PRODUCTION_CHECKLIST.md) before going live

