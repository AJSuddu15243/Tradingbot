# Tradingbot

# ML Sentiment-Based Trading Bot

## Overview
This is an automated trading bot that uses machine learning sentiment analysis on financial news to make trading decisions. The bot analyzes recent news headlines for a specified stock, determines sentiment (positive or negative), and executes buy or sell orders accordingly.

## Features
- Uses Natural Language Processing (NLP) to analyze stock-related news sentiment
- Connects to Alpaca for paper trading or live trading
- Includes backtesting capabilities via Yahoo Finance data
- Implements bracket orders with take profit and stop loss points
- Trades on a 3-hour interval

## Requirements
- Python 3.6+
- lumibot
- alpaca-trade-api
- Custom `finbertutils` module

## Installation
1. Clone this repository
2. Install required packages:
```
pip install lumibot alpaca-trade-api finbertutils
```
3. Update your API credentials in the code

## Configuration
The script uses the following configurations:
- Default trading symbol: AAPL
- Default risk per trade: 25% of available cash
- Default trading interval: 3 hours
- Take profit target: 20% above entry price (for buys)
- Stop loss: 5% below entry price (for buys)
- Short take profit: 20% below entry price (for sells)
- Short stop loss: 5% above entry price (for sells)

## How It Works

### Trading Logic
1. The bot retrieves news headlines for the specified stock from the past 3 days
2. It analyzes these headlines using a sentiment analysis model (from `finbertutils`)
3. If sentiment is positive with high probability (>99.9%), the bot creates a buy order
4. If sentiment is negative with high probability (>99.9%), the bot creates a sell order
5. Each order includes take profit and stop loss levels
6. The bot will close existing positions if sentiment changes direction

### Position Sizing
The bot determines position size based on:
- Available cash
- Current stock price
- Cash-at-risk parameter (defaults to 25% of account)

### Backtesting
The script includes code to backtest the strategy using historical data from Yahoo Finance, from January 1, 2025 to April 25, 2025.

## Usage

### Paper Trading
The default configuration uses Alpaca's paper trading API. To run the bot:
```python
python tradingbot.py
```

### Live Trading
To use live trading, modify the `PAPER` parameter to `False` in the `ALPACA_CREDS` dictionary. Be sure to update the API credentials to your live trading credentials.

### Customization
You can modify the following parameters to customize the trading behavior:
- `symbol`: The stock ticker to trade (default: "AAPL")
- `cash_at_risk`: Percentage of available cash to risk per trade (default: 0.25)
- `sleeptime`: Time between trading iterations (default: "3H")

## Security Note
This code contains API credentials. In a production environment, it's recommended to:
1. Store credentials in environment variables or a secure configuration file
2. Never commit API credentials to version control

## Warning
Trading involves risk of financial loss. This code is provided for educational purposes only. Always test thoroughly on paper trading before deploying with real funds.

## Dependencies
- [lumibot](https://github.com/Lumiwealth/lumibot) - Trading framework
- [Alpaca](https://alpaca.markets/) - Brokerage API
- finbertutils - Custom module for sentiment analysis (requires separate installation)
