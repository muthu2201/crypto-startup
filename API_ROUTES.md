# LedgerFlow API Routes

Complete list of all API endpoints.

Base URL: `/api/v1`

## Authentication

### Register
- **POST** `/auth/register`
- Body: `{ email, password, name? }`
- Returns: `{ user, accessToken, refreshToken }`

### Login
- **POST** `/auth/login`
- Body: `{ email, password }`
- Returns: `{ user, accessToken, refreshToken }`

### Refresh Token
- **POST** `/auth/refresh`
- Body: `{ refreshToken }`
- Returns: `{ accessToken, refreshToken? }`

### Logout
- **POST** `/auth/logout`
- Headers: `Authorization: Bearer <token>`
- Body: `{ refreshToken? }`
- Returns: `{ message }`

### OAuth - Google
- **GET** `/auth/google` - Initiate OAuth
- **GET** `/auth/google/callback` - OAuth callback

### OAuth - GitHub
- **GET** `/auth/github` - Initiate OAuth
- **GET** `/auth/github/callback` - OAuth callback

### Get Current User
- **GET** `/auth/me`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ user }`

## Users

### Get Profile
- **GET** `/users/me`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ user }`

### Update Profile
- **PATCH** `/users/me`
- Headers: `Authorization: Bearer <token>`
- Body: `{ name?, avatar? }`
- Returns: `{ user }`

## Wallets

### Add Wallet
- **POST** `/wallets`
- Headers: `Authorization: Bearer <token>`
- Body: `{ address, chain, label? }`
- Returns: `{ wallet }`

### List Wallets
- **GET** `/wallets`
- Headers: `Authorization: Bearer <token>`
- Returns: `[{ wallet }]`

### Get Wallet
- **GET** `/wallets/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ wallet }`

### Get Wallet Balance
- **GET** `/wallets/:id/balance`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ native, tokens, totalUSD }`

### Update Wallet
- **PATCH** `/wallets/:id`
- Headers: `Authorization: Bearer <token>`
- Body: `{ label? }`
- Returns: `{ wallet }`

### Delete Wallet
- **DELETE** `/wallets/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ message }`

## Transactions

### List Transactions
- **GET** `/transactions`
- Headers: `Authorization: Bearer <token>`
- Query params:
  - `walletIds?` - Comma-separated wallet IDs
  - `chain?` - Chain filter
  - `type?` - Transaction type
  - `classification?` - Classification filter
  - `startDate?` - ISO date string
  - `endDate?` - ISO date string
  - `tokenId?` - Token ID filter
  - `page?` - Page number (default: 1)
  - `limit?` - Items per page (default: 50, max: 100)
- Returns: `{ data: [{ transaction }], pagination }`

### Get Transaction
- **GET** `/transactions/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ transaction }`

### Monthly Summary
- **GET** `/transactions/monthly-summary`
- Headers: `Authorization: Bearer <token>`
- Query params:
  - `year` - Year (required)
  - `month` - Month 1-12 (required)
- Returns: `{ period, summary, transactions }`

### Classify Transaction
- **PATCH** `/transactions/:id/classify`
- Headers: `Authorization: Bearer <token>`
- Body: `{ classification }`
- Returns: `{ transaction }`

### Tag Transaction
- **PATCH** `/transactions/:id/tag`
- Headers: `Authorization: Bearer <token>`
- Body: `{ tagId }` (or null to remove)
- Returns: `{ transaction }`

### Add Notes
- **PATCH** `/transactions/:id/notes`
- Headers: `Authorization: Bearer <token>`
- Body: `{ notes }`
- Returns: `{ transaction }`

## Tags

### Create Tag
- **POST** `/tags`
- Headers: `Authorization: Bearer <token>`
- Body: `{ name, color?, description? }`
- Returns: `{ tag }`

### List Tags
- **GET** `/tags`
- Headers: `Authorization: Bearer <token>`
- Returns: `[{ tag }]`

### Get Tag
- **GET** `/tags/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ tag }`

### Update Tag
- **PATCH** `/tags/:id`
- Headers: `Authorization: Bearer <token>`
- Body: `{ name?, color?, description? }`
- Returns: `{ tag }`

### Delete Tag
- **DELETE** `/tags/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ message }`

## Reports

### Generate Report
- **POST** `/reports`
- Headers: `Authorization: Bearer <token>`
- Body: `{ type, format, startDate?, endDate?, walletIds?, tokenIds?, classifications? }`
- Returns: `{ report }`

### List Reports
- **GET** `/reports`
- Headers: `Authorization: Bearer <token>`
- Returns: `[{ report }]`

### Get Report
- **GET** `/reports/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ report }`

### Download Report
- **GET** `/reports/:id/download`
- Headers: `Authorization: Bearer <token>`
- Returns: File download (CSV or JSON)

## Shared Links

### Create Shared Link
- **POST** `/shared-links`
- Headers: `Authorization: Bearer <token>`
- Body: `{ name?, walletIds, expiresInDays? }`
- Returns: `{ link }`

### List Shared Links
- **GET** `/shared-links`
- Headers: `Authorization: Bearer <token>`
- Returns: `[{ link }]`

### Access Shared Link (Public)
- **GET** `/shared-links/public/:token`
- No authentication required
- Returns: `{ link, wallets }`

### Revoke Shared Link
- **DELETE** `/shared-links/:id`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ message }`

## Subscriptions

### Get Plans
- **GET** `/subscriptions/plans`
- No authentication required
- Returns: `[{ plan }]`

### Get User Subscription
- **GET** `/subscriptions/me`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ status, plan, subscription }`

### Update Subscription
- **PATCH** `/subscriptions/me`
- Headers: `Authorization: Bearer <token>`
- Body: `{ plan }`
- Returns: `{ subscription }`

## Indexer (Internal/Admin)

### Index Wallet
- **POST** `/indexer/wallet/:walletId`
- Headers: `Authorization: Bearer <token>`
- Returns: `{ message }`

## Error Responses

All endpoints may return:
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `429` - Too Many Requests (Rate Limited)
- `500` - Internal Server Error

Error format:
```json
{
  "statusCode": 400,
  "message": "Error message",
  "error": "Bad Request"
}
```

