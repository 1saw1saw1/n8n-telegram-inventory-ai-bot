# n8n Telegram Inventory AI Bot

AI-powered warehouse assistant built with **n8n**, **Telegram Bot API**, **Supabase** and CRM integration.

The system automates inventory analytics, stock monitoring and product search through a Telegram interface.

## Features

* 🔄 Automatic CRM synchronization every hour
* 📊 Product analytics calculation
* 📦 Stock level monitoring
* 🚨 Critical inventory alerts
* 📉 Outsider product detection
* 🔍 Product search through Telegram
* 🤖 AI assistant for warehouse analytics
* 🗄 Supabase database integration

## Architecture

```
                Schedule Trigger
                       |
                       ↓
                    CRM API
                       |
                       ↓
              n8n Data Processing
                       |
                       ↓
                  Supabase
                       |
                       |
                       ↓
Telegram Bot  ←→  n8n Workflow  ←→  AI Assistant
```

## Workflows

### 1. CRM Inventory Sync

Runs automatically every hour.

Flow:

```
Schedule Trigger
        |
        ↓
CRM API
        |
        ↓
Data Processing
        |
        ↓
Supabase UPSERT
```

The workflow updates product analytics without creating duplicates.

Database table:

`predict_product_analytics`

Contains:

* SKU
* Product name
* Current stock
* Cost price
* Sales volume
* Average sales interval
* Days remaining

### 2. Telegram Inventory Assistant

Users interact with the bot through Telegram.

Available actions:

```
🚨 Critical stock
📉 Outsiders
📦 Create order
🔍 Product search
```

The bot uses session states to understand user actions:

Example:

```
User presses:
🔍 Product search

Session:
state = search_product

User:
"product name"

Bot:
searches inventory database
```

## Technologies

* n8n Self-hosted
* Telegram Bot API
* Supabase REST API
* PostgreSQL
* JavaScript Code nodes
* CRM API integration
* AI models

## Database

### predict_product_analytics

Stores calculated inventory metrics.

### bot_sessions

Stores user interaction states.

Example:

```
chat_id
state
query
created_at
updated_at
```

## Deployment

Requirements:

* Self-hosted n8n instance
* Telegram Bot Token
* Supabase project
* CRM API credentials

## Future Improvements

* Fuzzy product search
* AI recommendations for purchasing
* Automatic order generation
* Sales forecasting
* Dashboard visualization
* Role-based access

## License

MIT
