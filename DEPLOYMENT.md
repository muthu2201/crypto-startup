# LedgerFlow Deployment Guide

## Production Deployment Checklist

### 1. Environment Variables

Ensure all environment variables are set in your deployment platform:

**Backend (Railway/Render)**
- `DATABASE_URL` - PostgreSQL connection string
- `JWT_SECRET` - Strong random secret (min 32 chars)
- `JWT_REFRESH_SECRET` - Strong random secret (min 32 chars)
- `FRONTEND_URL` - Your frontend URL
- RPC URLs for all supported chains
- OAuth credentials (Google, GitHub)
- Stripe keys (if enabling billing)

**Frontend (Vercel)**
- `NEXT_PUBLIC_API_URL` - Your backend API URL

### 2. Database Setup

1. Create PostgreSQL database (Supabase/Neon)
2. Run migrations:
   ```bash
   npx prisma migrate deploy
   ```
3. Verify connection

### 3. Backend Deployment

**Railway:**
1. Connect GitHub repository
2. Set root directory to `backend`
3. Set build command: `npm install && npm run build`
4. Set start command: `npm run start:prod`
5. Add all environment variables
6. Deploy

**Render:**
1. Create new Web Service
2. Connect GitHub repository
3. Set root directory to `backend`
4. Set build command: `npm install && npm run build`
5. Set start command: `npm run start:prod`
6. Add all environment variables
7. Deploy

### 4. Frontend Deployment

**Vercel:**
1. Import GitHub repository
2. Set root directory to `frontend`
3. Framework preset: Next.js
4. Add environment variables
5. Deploy

### 5. Post-Deployment

1. Verify API is accessible
2. Test authentication flow
3. Test wallet addition
4. Verify indexing works
5. Check error logs
6. Set up monitoring (Sentry, etc.)

### 6. Monitoring

- Set up error tracking (Sentry)
- Monitor API response times
- Set up database monitoring
- Configure alerts for critical errors

### 7. Security Hardening

- Enable HTTPS only
- Set secure cookie flags
- Configure CORS properly
- Enable rate limiting
- Set up DDoS protection (Cloudflare)
- Regular security audits

### 8. Scaling Considerations

- Database connection pooling
- Read replicas for reporting
- CDN for static assets
- Horizontal scaling for API
- Queue workers for indexing
- Caching layer (Redis)

## Production Checklist

- [ ] All environment variables configured
- [ ] Database migrations run
- [ ] SSL certificates installed
- [ ] CORS configured correctly
- [ ] Rate limiting enabled
- [ ] Error tracking set up
- [ ] Monitoring configured
- [ ] Backup strategy in place
- [ ] Security audit completed
- [ ] Performance testing done
- [ ] Documentation updated

