# Magistery Bot

Telegram trading bot for the [Magistery](https://magistery.org) prediction market protocol. Deploy your own instance — users trade prediction markets via chat commands.

## One-Click Deploy

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/sRGred)

## Self-Host with Docker Compose

```bash
git clone https://github.com/0xMagistery/bot.git
cd bot
cp .env.example .env
# Edit .env with your values
docker compose up -d
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `TELEGRAM_BOT_TOKEN` | Yes | From [@BotFather](https://t.me/BotFather) |
| `OPERATOR_SEED` | Yes | BIP-39 mnemonic (12 words). All user wallets derive from this. |
| `RPC_URL` | Yes | Polygon RPC endpoint (Alchemy, Infura, etc.) |
| `LAYERSWAP_API_KEY` | Yes | From [LayerSwap](https://layerswap.io) — for TON deposits/withdrawals |
| `OPERATOR_TELEGRAM_ID` | Yes | Your Telegram user ID — enables operator commands (`/resolve`, `/newmarket`) |

The bot auto-creates a Postgres database via the included `docker-compose.yml`. If self-hosting Postgres separately, set `DATABASE_URL`.

## First Run

1. Deploy the bot
2. Open your bot in Telegram and send `/setup`
3. Configure: bot name, fee %, categories, copy trading, group commands
4. Done — users can start trading

## What It Does

- Mirrors Polymarket markets on-chain via Magistery protocol
- Users deposit USDT (TON) → auto-bridges to Polygon USDC → trades on Magistery OrderBook
- Copy trading: users follow addresses and auto-mirror trades
- Operator sets optional fee % (collected automatically)
- Background keeper: order matching, resolution polling, settlement pipeline
- Full withdrawal pipeline back to TON

## Links

- [Protocol Documentation](https://magistery.org/docs)
- [SDK](https://www.npmjs.com/package/@magistery/sdk)
