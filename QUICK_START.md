# Quick Start Guide

Get LedgerFlow running in 5 minutes.

## 1. Install Dependencies

```bash
# Backend
cd backend && npm install

# Frontend  
cd ../frontend && npm install
```

## 2. Set Up Database

**Option A: Supabase (Easiest)**
1. Go to https://supabase.com
2. Create free account
3. Create new project
4. Copy connection string from Settings > Database

**Option B: Local PostgreSQL**
```bash
createdb ledgerflow
```

## 3. Configure Backend

```bash
cd backend

# Copy environment template
cp .env.example .env

# Generate JWT secrets
npm run generate:secrets

# Edit .env file - minimum required:
# - DATABASE_URL (from step 2)
# - JWT_SECRET (from generate:secrets)
# - JWT_REFRESH_SECRET (from generate:secrets)
# - RPC URLs are already configured with Alchemy API key!
#   Just copy from .env.example to .env
```

## 4. Set Up Database Schema

```bash
cd backend
npx prisma generate
npx prisma migrate dev --name init
```

## 5. Configure Frontend

```bash
cd frontend
echo "NEXT_PUBLIC_API_URL=http://localhost:3001" > .env.local
```

## 6. Start Servers

**Terminal 1 - Backend:**
```bash
cd backend
npm run start:dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

## 7. Access Application

- Frontend: http://localhost:3000
- API Docs: http://localhost:3001/api/docs

## Next Steps

- Register a user account
- Add your first wallet
- See transactions being indexed

## Need Help?

See [SETUP_GUIDE.md](./SETUP_GUIDE.md) for detailed instructions.

