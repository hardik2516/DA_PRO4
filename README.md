# DA_PRO4
# Amazon Price Tracker with WhatsApp Alerts

## Overview
This Jupyter Notebook tracks prices of Amazon products, logs price history, and sends WhatsApp alerts when price changes are detected. It's designed to run in Google Colab but can be adapted for local execution.

## Features
- **Price Tracking**: Scrapes Amazon product pages for current prices
- **Price History Logging**: Maintains a CSV log of price history for all tracked products
- **WhatsApp Alerts**: Sends notifications via Twilio's WhatsApp API for:
  - Price drops
  - Price increases
  - Price stability
  - Scraping errors
- **Data Visualization**: Generates price trend charts for each product

## Setup Instructions

### 1. Prerequisites
- Google Colab account (or local Jupyter environment)
- Twilio account with WhatsApp sandbox activated
- Amazon product URLs to track

### 2. Installation
Run the first cell to install required packages:
```python
pip install twilio pandas beautifulsoup4 requests
```

### 3. Configuration
1. **Twilio Credentials**:
   - Store these in Google Colab's userdata (Secrets):
     - `TWILIO_ACCOUNT_SID`
     - `TWILIO_AUTH_TOKEN`
     - `TWILIO_PHONE_NUMBER` (your Twilio WhatsApp number)
     - `RECIPIENT_PHONE_NUMBER` (your personal WhatsApp number in E.164 format)

2. **Product List**:
   - Create a CSV file named `product_urls.csv` with columns:
     - `Name`: Product name (fallback if scraping fails)
     - `URL`: Amazon product URL
   - Upload via the provided file uploader cell

## Usage
1. Run all cells sequentially
2. The script will:
   - Scrape current prices for all products
   - Update the price log (`price_log.csv`)
   - Compare with previous prices
   - Send WhatsApp alerts for significant changes
   - Generate price trend visualizations

## File Structure
- `product_urls.csv`: Input file with products to track
- `price_log.csv`: Generated log file with price history
- Output includes:
  - Console logs of scraping results
  - WhatsApp notifications
  - Price trend charts

## Customization Options
1. **Alert Thresholds**: Modify `compare_with_previous()` to change what triggers alerts
2. **Notification Content**: Edit the WhatsApp message templates in the same function
3. **Visualization**: Adjust chart parameters in the last cell

## Troubleshooting
- If scraping fails, check:
  - Amazon's robots.txt restrictions
  - Your User-Agent in the headers
  - Network connectivity (if running locally)
- For WhatsApp issues:
  - Verify Twilio credentials
  - Check sandbox activation
  - Ensure phone numbers are in E.164 format

## Notes
- The script handles various edge cases (missing prices, first-time runs)
- All date handling is timezone-naive (uses system time)
- For production use, consider adding:
  - Error handling for Twilio API limits
  - Rate limiting for Amazon requests
  - More sophisticated price change detection
