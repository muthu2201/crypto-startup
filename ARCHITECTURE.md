# LedgerFlow - System Architecture

## Product Overview
**LedgerFlow** - Real-time On-Chain Financial Visibility for Web3 Teams

A read-only SaaS dashboard for Web3 teams to track balances, transactions, and generate financial reports across multiple crypto wallets.

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  Next.js 14 Frontend (Vercel)                            │  │
│  │  - App Router, TypeScript, TailwindCSS, ShadCN UI        │  │
│  │  - Dashboard, Wallets, Transactions, Reports             │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ HTTPS / REST API
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API GATEWAY LAYER                           │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  NestJS Backend (Railway/Render)                         │  │
│  │  - REST API                                               │  │
│  │  - JWT Authentication + OAuth (Google, GitHub)           │  │
│  │  - Rate Limiting, DDoS Protection                        │  │
│  │  - Request Validation, CSRF/XSS Protection               │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────┴─────────┐
                    │                   │
                    ▼                   ▼
┌──────────────────────────┐  ┌──────────────────────────┐
│   BUSINESS LOGIC LAYER    │  │   BLOCKCHAIN INDEXER     │
│  - Wallet Management      │  │  - Multi-chain Support   │
│  - Transaction Processing │  │  - Reorg-safe Indexing   │
│  - Tagging System         │  │  - Event Parsing         │
│  - Export Generation      │  │  - Gas Fee Calculation   │
│  - Shared Links           │  │  - Token Price Fetching   │
│  - Subscription Logic     │  │  - Cron Jobs + Queue     │
└──────────────────────────┘  └──────────────────────────┘
                    │                   │
                    └─────────┬─────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      DATA LAYER                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  PostgreSQL (Supabase/Neon)                              │  │
│  │  - Prisma ORM                                             │  │
│  │  - User, Wallet, Transaction, Token, Tag, Report         │  │
│  │  - Subscription, SharedLink, AuditLog                     │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                   EXTERNAL SERVICES                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │  Alchemy/    │  │  Stripe      │  │  OAuth       │         │
│  │  QuickNode   │  │  (Billing)   │  │  Providers   │         │
│  │  RPC Nodes   │  │              │  │  (Google,    │         │
│  │              │  │              │  │   GitHub)    │         │
│  └──────────────┘  └──────────────┘  └──────────────┘         │
└─────────────────────────────────────────────────────────────────┘
```

## Component Details

### Frontend (Next.js 14)
- **Framework**: Next.js 14 with App Router
- **Language**: TypeScript
- **Styling**: TailwindCSS + ShadCN UI
- **State Management**: React Context + Server Components
- **Authentication**: Client-side JWT handling
- **Deployment**: Vercel

### Backend (NestJS)
- **Framework**: NestJS (Node.js)
- **API Style**: REST
- **Authentication**: JWT + Refresh Tokens
- **Validation**: class-validator, class-transformer
- **Security**: Helmet, CORS, Rate Limiting
- **Deployment**: Railway / Render

### Database (PostgreSQL)
- **Provider**: Supabase / Neon
- **ORM**: Prisma
- **Features**: 
  - Connection pooling
  - Automatic backups
  - Read replicas (for scaling)

### Blockchain Indexer
- **RPC Providers**: Alchemy / QuickNode
- **Supported Chains**: Ethereum, Polygon, BSC, Base
- **Features**:
  - Reorg-safe indexing
  - Event parsing (ERC-20, swaps, contracts)
  - Gas fee calculation
  - Token price fetching (CoinGecko API)
  - Queue-based processing
  - Error recovery and retry logic

### Security Architecture
- **Authentication**: JWT with refresh tokens
- **Authorization**: Role-based access control
- **Rate Limiting**: Per-user and per-IP
- **Input Validation**: All inputs validated and sanitized
- **SQL Injection**: Prisma ORM parameterized queries
- **XSS/CSRF**: Helmet.js + SameSite cookies
- **Audit Logging**: All sensitive operations logged
- **Encryption**: Environment variables encrypted at rest

## Data Flow

### Wallet Connection Flow
1. User enters public wallet address
2. Backend validates address format
3. Indexer starts fetching historical transactions
4. Transactions stored in database
5. Real-time updates via cron jobs

### Transaction Indexing Flow
1. Cron job triggers indexer
2. Indexer queries RPC for new blocks
3. Filters transactions for tracked wallets
4. Parses events (transfers, swaps, contracts)
5. Calculates gas fees and USD values
6. Stores normalized data in PostgreSQL
7. Updates wallet balances

### Export Flow
1. User requests export (CSV/JSON)
2. Backend queries transactions with filters
3. Formats data according to export type
4. Generates file
5. Returns download link
6. Logs export in audit log

### Shared Link Flow
1. User creates read-only share link
2. Backend generates secure token
3. Sets expiration date
4. Stores link metadata
5. Link provides read-only dashboard access
6. User can revoke link anytime

## Scalability Considerations

### Database
- Indexed queries for fast lookups
- Pagination for large result sets
- Partitioning for transaction tables (by date)
- Read replicas for reporting queries

### API
- Rate limiting per user tier
- Caching for frequently accessed data
- Background job processing
- Horizontal scaling via load balancer

### Indexer
- Queue-based processing
- Parallel chain indexing
- Incremental sync (only new blocks)
- Batch processing for efficiency

## Security Measures

1. **No Private Keys**: System never stores or handles private keys
2. **Read-Only Access**: All blockchain interactions are read-only
3. **Input Validation**: All user inputs validated and sanitized
4. **Rate Limiting**: Prevents abuse and DDoS
5. **Audit Logging**: All sensitive operations logged
6. **Encrypted Storage**: Sensitive data encrypted at rest
7. **Secure Headers**: Helmet.js for security headers
8. **CORS**: Strict CORS policy
9. **SQL Injection**: Prisma ORM prevents SQL injection
10. **XSS Protection**: Input sanitization and CSP headers

## Deployment Architecture

### Frontend (Vercel)
- Automatic deployments from Git
- Edge network for global CDN
- Environment variables via Vercel dashboard

### Backend (Railway/Render)
- Docker container deployment
- Environment variables via platform dashboard
- Auto-scaling based on traffic
- Health check endpoints

### Database (Supabase/Neon)
- Managed PostgreSQL
- Automatic backups
- Connection pooling
- Point-in-time recovery

## Monitoring & Observability

- **Error Tracking**: Sentry or similar
- **Logging**: Structured logging (Winston/Pino)
- **Metrics**: API response times, error rates
- **Uptime Monitoring**: Health check endpoints
- **Database Monitoring**: Query performance, connection pool

## Future Enhancements

- Multi-chain expansion (Solana, Cosmos, etc.)
- Real-time WebSocket updates
- Advanced analytics and charts
- Custom report builder
- API access for integrations
- Mobile app (React Native)

