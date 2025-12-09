# LedgerFlow Testing URLs

## 🚀 Quick Start URLs

### Frontend (Next.js)
- **Main App**: http://localhost:3000
- **Dashboard**: http://localhost:3000/dashboard
- **Login**: http://localhost:3000/auth/login (auto-redirects if not logged in)

### Backend API (NestJS)
- **API Base**: http://localhost:3001/api/v1
- **API Documentation (Swagger)**: http://localhost:3001/api/docs
- **Health Check**: http://localhost:3001/api/v1/health (if implemented)

## 📋 How to Start Testing

### Step 1: Start Backend
```bash
cd backend
npm run start:dev
```

Wait for: `🚀 LedgerFlow API running on port 3001`

### Step 2: Start Frontend
```bash
cd frontend
npm run dev
```

Wait for: `Ready on http://localhost:3000`

### Step 3: Access the App
1. Open browser: http://localhost:3000
2. You'll be redirected to login/register
3. Create an account or log in
4. Access the dashboard

## 🧪 Testing Endpoints

### API Testing (using curl or Postman)

**1. Register a User:**
```bash
curl -X POST http://localhost:3001/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "Test123!@#",
    "name": "Test User"
  }'
```

**2. Login:**
```bash
curl -X POST http://localhost:3001/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "Test123!@#"
  }'
```

**3. Get Wallets (with token from login):**
```bash
curl -X GET http://localhost:3001/api/v1/wallets \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

**4. Add a Wallet:**
```bash
curl -X POST http://localhost:3001/api/v1/wallets \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "address": "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb",
    "chain": "ETHEREUM",
    "label": "My Wallet"
  }'
```

## 📚 API Documentation

Visit http://localhost:3001/api/docs for interactive Swagger documentation where you can:
- See all available endpoints
- Test API calls directly in the browser
- View request/response schemas
- Try authentication flows

## 🔍 Testing Checklist

- [ ] Backend starts without errors
- [ ] Frontend loads at http://localhost:3000
- [ ] Can register a new user
- [ ] Can login with credentials
- [ ] Can access dashboard
- [ ] Can add a wallet
- [ ] Wallet indexing starts
- [ ] Transactions appear (after indexing)
- [ ] API docs accessible at http://localhost:3001/api/docs

## 🐛 Troubleshooting

### Port Already in Use
If port 3000 or 3001 is already in use:
- Change `PORT=3002` in `backend/.env`
- Or kill the process: `lsof -ti:3001 | xargs kill`

### CORS Errors
- Ensure `FRONTEND_URL` in backend `.env` matches your frontend URL
- Default: `FRONTEND_URL=http://localhost:3000`

### Database Connection Error
- Check `DATABASE_URL` in `backend/.env`
- Ensure PostgreSQL is running
- Test connection: `psql $DATABASE_URL`

### RPC Connection Error
- Verify Alchemy API key is correct
- Check RPC URLs in `.env`
- Test RPC: `curl https://eth-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL`

## 🌐 Production URLs

When deployed:
- **Frontend**: https://your-domain.vercel.app (or your domain)
- **Backend**: https://your-api.railway.app (or your domain)
- **API Docs**: https://your-api.railway.app/api/docs

## 📱 Mobile Testing

For mobile device testing on same network:
1. Find your local IP: `ipconfig` (Windows) or `ifconfig` (Mac/Linux)
2. Update `FRONTEND_URL` in backend `.env` to: `http://YOUR_IP:3000`
3. Access from mobile: `http://YOUR_IP:3000`

