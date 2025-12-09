# Alchemy API Configuration

## ✅ API Key Configured

Your Alchemy API key `r4tABc1OmdxjSvueba7OL` is already configured for all supported blockchain networks.

## Configured Networks

| Network | RPC URL |
|---------|---------|
| **Ethereum** | `https://eth-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL` |
| **Polygon** | `https://polygon-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL` |
| **Base** | `https://base-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL` |
| **BSC** | `https://bsc-dataseed.binance.org/` (Public RPC) |

## Usage in Environment File

Copy these to your `backend/.env` file:

```env
ETHEREUM_RPC_URL=https://eth-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
POLYGON_RPC_URL=https://polygon-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
BASE_RPC_URL=https://base-mainnet.g.alchemy.com/v2/r4tABc1OmdxjSvueba7OL
BSC_RPC_URL=https://bsc-dataseed.binance.org/
```

## Alchemy Dashboard

- View your API usage: https://dashboard.alchemy.com/
- Monitor requests and compute units
- Free tier: 300M compute units/month

## Security Notes

⚠️ **Important:**
- Never commit your `.env` file to version control
- For production, use environment variables in your hosting platform
- Consider rotating API keys periodically
- Monitor usage to prevent unexpected charges

## Testing the Connection

Once your backend is running, the indexer will automatically use these RPC endpoints when:
- Adding a new wallet
- Syncing transactions
- Fetching balances

No additional configuration needed - just ensure the RPC URLs are in your `.env` file!

