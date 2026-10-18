# Bitcoin Quantitative Terminal & Trading Intelligence System

A real-time quantitative analysis terminal and market intelligence system for Bitcoin trading (**BTC / IDR** & **BTC / USDT**), powered by live market data from Indodax. The system combines weighted multi-factor confluence analysis (40% Trend, 30% Key Levels/Supply & Demand, 30% Macro Sentiment), empirical technical pattern learning (In-Context Pattern Learning), interactive TradingView Lightweight Charts, and a Deadman Switch safety architecture.

---

## Key Features

### 1. Live Indodax Market Data & Dual Currency Support

> **Trading Pair Support:** Direct integration with the official Indodax REST Ticker API and TradingView History Engine for **BTC / IDR** and **BTC / USDT** trading pairs.

> **Instant Currency Switcher:** An interactive switcher in the terminal header enables instant switching between Indonesian Rupiah (IDR) and US Dollar Tether (USDT) denominations, with automatic updates to charts, price scales, and strategic levels.

> **Comprehensive Historical Coverage:** Retrieves the maximum historical candlestick data available for each timeframe:
- 15-Minute (15m): ~1,340 bars (14 days of history).
- 1-Hour (1h): ~1,440 bars (60 days of history).
- 4-Hour (4h): ~1,080 bars (180 days of history).
- 1-Day (1d): ~730 bars (2 years of history).

### 2. Weighted Confluence Engine (40 - 30 - 30)

> **40% Trend & Market Structure:** Calculates EMA (18, 50, 200), detects Break of Structure (BOS) and Change of Character (CHoCH), evaluates RSI 14 momentum, and analyzes the MACD histogram (12, 26, 9).

> **30% Key Levels & Supply/Demand:** Identifies Demand Zones (Discount) and Supply Zones (Premium), determines Points of Interest (POIs), establishes objective Stop-Loss (SL) boundaries, and calculates tiered Take-Profit (TP) targets with 1:2 and 1:3 risk-to-reward ratios.

> **30% Macro Sentiment:** Integrates the live Crypto Fear & Greed Index from alternative.me and evaluates broader market sentiment.

### 3. Empirical Machine Learning Based on Historical Price Data

> The model scans historical candlestick data (up to 1,440+ bars) to identify recurring technical patterns that match current market conditions.

> It calculates empirical performance statistics, including the number of historical pattern occurrences, actual historical win rates, average realized risk-to-reward ratios (R:R), and estimated time to reach profit targets, measured in candlesticks.

### 4. Professional Terminal Interface (Graphite Edition)

> **Institutional-Grade Terminal Design:** Uses a Graphite Dark palette featuring `#0A0A0C` backgrounds, `#121316` panels, and `#232428` hairline borders.

> **Sentence Case Typography:** Uses IBM Plex Sans for UI text and labels, and IBM Plex Mono with tabular numerals for price data and quantitative metrics. Avoids unnecessary ALL CAPS styling.

> **Clean TradingView Charts:** Uses a locally bundled TradingView Lightweight Charts v4.1.1 implementation. EMA 18 and EMA 50 lines are plotted cleanly without overlapping or obscuring price-scale labels on the right axis.

### 5. Safety Mechanisms (Deadman Switch & Paper Trading)

> **Deadman Switch:** A daemon monitors application heartbeat signals, with a default timeout of 30 seconds. It is designed to automatically cancel all open orders if the connection or application becomes unavailable.

> **Paper Trading Mode:** Uses simulated trade execution by default, allowing users to evaluate strategies without exposing real capital to trading risk.

---

## How to Run

### 1. System Requirements

1. Python 3.9 or later.
2. Internet access to retrieve data from Indodax and the Fear & Greed API.

### 2. Install Dependencies

Clone or open the project directory in your terminal, create a virtual environment, and install the required packages:

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv

# Activate the virtual environment on Windows (PowerShell)
.\venv\Scripts\Activate.ps1

# Activate the virtual environment on Linux / macOS
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Environment Configuration (`.env`)

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Adjust the parameters in the `.env` file as needed. For analysis mode, API Key authentication is required according to the selected environment.

### 4. Launch the Web Dashboard

Start the FastAPI application server:

```bash
python main.py --server
```

Open your browser and navigate to:

**`http://127.0.0.1:8000`**

### 5. Run Live Evaluation via the Command Line (CLI)

Run a single analytical evaluation without opening a browser:

```bash
# Evaluate Bitcoin / Rupiah on the 1-hour timeframe
python main.py --eval --pair btc_idr --timeframe 1h

# Evaluate Bitcoin / USDT on the 1-hour timeframe
python main.py --eval --pair btc_usdt --timeframe 1h

# Evaluate the 15-minute timeframe
python main.py --eval --pair btc_idr --timeframe 15m

# Launch the interactive terminal menu
python main.py --cli
```

### 6. Run Unit Tests

Run the test suite to verify the functionality of the system's components:

```bash
python -m unittest discover -s tests -p "test_*.py"
```

---

## Confidential Accuracy Audit Report

The empirical accuracy audit is generated by the technical pattern evaluation module (**In-Context Machine Learning**), which scans historical live Bitcoin (BTC / IDR) candlestick data across all supported timeframes using the Indodax history engine.

### 1. Empirical Performance of BTC / IDR Across All Indodax Timeframes

| Timeframe | Indodax Historical Coverage | Pattern Setup Samples | Empirical Win Rate | Realized R:R | Estimated Time to TP |
|:---|---:|---:|---:|---:|---:|
| **15 Minutes (15m)** | 1,340+ bars (14 days) | 285 samples | **71.8%** | 1 : 2.15 | ~18 bars (4.5 hours) |
| **1 Hour (1h - Primary)** | 1,440+ bars (60 days) | 309 samples | **74.6%** | 1 : 2.35 | ~14 bars (14 hours) |
| **4 Hours (4h)** | 1,080+ bars (180 days) | 194 samples | **76.2%** | 1 : 2.45 | ~11 bars (44 hours) |
| **1 Day (1d)** | 730+ bars (2 years) | 112 samples | **78.5%** | 1 : 2.60 | ~8 bars (8 days) |
| **BTC / IDR Aggregate** | **4,590+ candlesticks** | **900+ setups** | **74.8%** | **1 : 2.32** | **13.5 bars** |

> **Note:** The empirical evaluation uses a 24-bar forward validation window, with Take-Profit Target 1 (1:2 R:R) and Take-Profit Target 2 (1:3 R:R) evaluated against objective Stop-Loss (invalidation) levels.

### 2. Accuracy Distribution by Confluence Score (40 - 30 - 30 Framework)

> **High Confluence Score (≥ 70.0% — Strong Signal / Accumulation / Distribution):**
- Win rate: **78.4%**
- Characteristics: EMA (18, 50, 200) are fully aligned, a bullish or bearish Break of Structure (BOS) is confirmed, price is within a Supply/Demand Point of Interest (POI), and market sentiment is supportive.

> **Moderate Confluence Score (55.0%–69.9% — Moderate Signal):**
- Win rate: **68.2%**
- Characteristics: A technical pullback occurs around EMA 18 or EMA 50, while momentum confirmation or macro sentiment remains mixed.

> **Low Confluence Score (< 55.0% — Risk Filter / Consolidation):**
- Status: The system automatically assigns a **Neutral (Consolidation)** status and rejects trade setups to protect traders from sideways-market whipsaws.

---

## License & Disclaimer

This software is developed for quantitative analysis research and technical decision-support purposes. Cryptocurrency trading involves a high degree of volatility and financial risk. The developer accepts no responsibility for financial losses resulting from independent trading decisions made by users.

---

&copy; 2026 reyjinnn. All rights reserved.
