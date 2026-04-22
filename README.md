# StockIQ — Real-Time Stock Market Intelligence Platform

> Live stock data from Apple, Tesla, Microsoft, Amazon, NVIDIA and more — with ML price predictions, sentiment analysis, and a professional trading dashboard.

---

## What This Project Does

StockIQ is a full-stack stock market intelligence platform that pulls **real, live data** from Yahoo Finance (no API key needed) and serves it through a professional financial dashboard with:

- **Live stock quotes** for Apple, Tesla, Microsoft, Amazon, Alphabet, NVIDIA, Meta
- **Interactive price charts** with 1M / 3M / 6M / 1Y history
- **Volume bars** and **RSI indicator** (14-day)
- **ML price predictions** — 7-day forecast with confidence bands using Linear Regression trained on real historical data
- **News sentiment analysis** — real headlines from Yahoo Finance scored for bullish/bearish tone
- **Market indices** — S&P 500, NASDAQ, DOW Jones in the top bar
- **Watchlist** — side-by-side performance comparison of all 7 stocks
- **Price alerts** — set custom triggers (price above/below threshold)

---

## Quick Start

### 1. Create virtual environment
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 2. Install dependencies
```powershell
pip install fastapi "uvicorn[standard]" yfinance numpy pandas pydantic python-dotenv loguru
```

### 3. Start the server
```powershell
python -m uvicorn src.api.main:app --reload --port 8000
```

### 4. Open the dashboard
**http://localhost:8000**

API docs: **http://localhost:8000/api/docs**

> No API key needed. yfinance pulls real data from Yahoo Finance for free.

---

## Project Structure

```
stock-intelligence/
├── src/
│   └── api/
│       ├── main.py              ← FastAPI app entry point
│       └── routes/
│           ├── stock.py         ← /api/stock/quote + /history
│           ├── predict.py       ← /api/predict  (ML forecast)
│           ├── sentiment.py     ← /api/sentiment (news scoring)
│           └── indices.py       ← /api/indices  (S&P, NASDAQ, DOW)
├── dashboard/
│   ├── templates/index.html     ← Single-page dashboard
│   └── static/
│       ├── css/main.css         ← Luxury financial dark theme
│       └── js/app.js            ← Chart.js + live API calls
├── requirements.txt
└── README.md
```

---

## API Endpoints

| Method | Endpoint | Description |
|--------|---------|-------------|
| GET | `/api/stock/quote?symbol=AAPL` | Real-time quote for any stock |
| GET | `/api/stock/history?symbol=AAPL&period=1mo` | Price history (1mo/3mo/6mo/1y) |
| GET | `/api/predict?symbol=AAPL` | 7-day ML price forecast |
| GET | `/api/sentiment?symbol=AAPL` | News sentiment analysis |
| GET | `/api/indices` | S&P 500, NASDAQ, DOW Jones |

---

## How the ML Prediction Works

1. Downloads 6 months of real historical prices via yfinance
2. Engineers 12 features: Moving Averages (5/10/20 day), Standard Deviation, Returns (1/5/10 day), Price-to-MA ratios, RSI
3. Trains a Linear Regression model (pure NumPy, no scikit-learn needed)
4. Predicts the next 7 trading days with a 90% confidence band
5. Outputs a BUY / HOLD / SELL signal based on expected % move

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | FastAPI + Uvicorn |
| Real-time Data | yfinance (Yahoo Finance) |
| ML | NumPy Linear Regression |
| Data Processing | NumPy + Pandas |
| Dashboard | HTML5 + CSS3 + Chart.js |
| Theme | DM Serif Display + DM Mono fonts |
