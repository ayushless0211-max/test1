# Trdautotokenbot — Railway deployment

This package runs the Telegram bot as a Railway worker using long polling.

## Deploy

1. Create a new Railway project and deploy this folder from the ZIP or GitHub.
2. Add the environment variable `TELEGRAM_BOT_TOKEN` in Railway. Never put the token in the code or ZIP.
3. Deploy the service and check the deployment logs for `started`.

## Environment variables

Required:

- `TELEGRAM_BOT_TOKEN` — the replacement token from BotFather

Optional:

- `BOT_DATA_FILE` — defaults to `bot_data.json`; use `/data/bot_data.json` when a Railway Volume is mounted at `/data`
- `BOT_OPEN_ACCESS` — defaults to `true`, allowing all users except banned users
- `BOT_OWNER` — display name, defaults to `@Trdcoderz`
- `BOT_CREDITS` — display credit, defaults to `@Trdcoderz`
- `BOT_USERNAME` — dashboard metadata only
- `BOT_CHANNEL` — dashboard metadata only, defaults to `@trdkings`

## Persistent data

The bot uses `bot_data.json` for Firebase/device/user configuration. Railway's local filesystem is not durable across all redeployments, so create a Railway Volume mounted at `/data` and set:

```
BOT_DATA_FILE=/data/bot_data.json
```

Do not upload a data file containing Firebase API keys or other private data into a public repository.

## Access behavior

All non-banned users can open and use the bot by default. Admin-only and owner-only tools remain restricted by Telegram numeric IDs in the bot data/configuration.