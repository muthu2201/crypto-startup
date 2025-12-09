# 🚀 Start Here - LedgerFlow Quick Start

## Test Your Web App - URLs

### Main Application URLs:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3001/api/v1  
- **API Documentation**: http://localhost:3001/api/docs

## Quick Start (3 Steps)

### 1️⃣ Start Backend
```bash
cd backend
npm install
npm run start:dev
```
✅ Wait for: `🚀 LedgerFlow API running on port 3001`

### 2️⃣ Start Frontend  
```bash
cd frontend
npm install
npm run dev
```
✅ Wait for: `Ready on http://localhost:3000`

### 3️⃣ Open Browser
👉 **Go to: http://localhost:3000**

## First Time Setup

Before starting, you need to configure:

1. **Copy environment template:**
   ```bash
   cd backend
   cp env-template.txt .env
   ```

2. **Generate JWT secrets:**
   ```bash
   npm run generate:secrets
   ```
   Copy the output to your `.env` file.

3. **Set database URL:**
   - Local: `postgresql://postgres:postgres@localhost:5432/ledgerflow`
   - Cloud: Get from Supabase/Neon dashboard

4. **Run database migrations:**
   ```bash
   npx prisma generate
   npx prisma migrate dev
   ```

## What You'll See

1. **Login/Register Page** - Create your account
2. **Dashboard** - Overview of wallets and transactions
3. **Add Wallet** - Connect your crypto wallets
4. **Transactions** - View and classify transactions
5. **Reports** - Generate financial reports

## Need Help?

- **Setup Issues**: See [SETUP_GUIDE.md](./SETUP_GUIDE.md)
- **Testing**: See [TESTING_URLS.md](./TESTING_URLS.md)
- **API Docs**: http://localhost:3001/api/docs
- **Configuration**: See [backend/CONFIG.md](./backend/CONFIG.md)

## Troubleshooting

**Port in use?**
- Change `PORT=3002` in `backend/.env`

**Database error?**
- Check `DATABASE_URL` in `backend/.env`
- Ensure PostgreSQL is running

**Can't connect?**
- Verify both servers are running
- Check console for errors

---

**Ready?** Start with step 1 above! 🎉

