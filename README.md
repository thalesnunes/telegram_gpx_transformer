# telegram_gpx_transformer

Telegram bot that smooths GPS gaps in Samsung Health GPX files.

Samsung watches often lose GPS signal during workouts, creating gaps where
Strava treats the activity as stopped. This bot interpolates those gaps with
1-second interval trackpoints so Strava shows a more accurate elapsed time.

## How it works

1. You send a `.gpx` file exported from Samsung Health to the bot
2. The bot finds all time gaps > 5 seconds between trackpoints
3. It adds interpolated points at 1-second intervals (linear lat/lon/elevation)
4. Heart rate is carried forward from the last known real point
5. The smoothed `.gpx` is sent back to you

## Setup

### 1. Create a Telegram bot

1. Open Telegram and message [@BotFather](https://t.me/BotFather)
2. Send `/newbot` and follow the prompts
3. Copy the bot token you receive

### 2. Configure

```bash
cp .env.example .env
# Edit .env and paste your bot token
```

### 3. Run with Docker Compose

```bash
docker compose up -d
```

### Or run locally

```bash
uv sync
uv run python main.py
```

## Usage

1. Open your bot in Telegram
2. Send `/start` for a welcome message
3. Send any `.gpx` file
4. Receive the smoothed file back

## Development

```bash
uv sync
uv run python -m gpx_transformer  # test against data/ sample
```
