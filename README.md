# Public Cryptocurrency Price API

A free, public API providing cryptocurrency prices and exchange rates. This service is available for anyone to use without restrictions.

## Overview

This API provides real-time cryptocurrency prices and exchange rates, updated regularly. It's designed to be simple to use for both non-programmers and developers alike. The API serves prices for cryptocurrencies from the top 250 by market capitalization.

The API uses a local cache to ensure fast response times and reliable service. Instead of querying external providers for every request, the API maintains an internal cache that is updated at regular intervals. This approach provides:
- Fast response times (typically under 100ms)
- Reduced load on external data providers
- Consistent availability even during external service disruptions
- Lower latency for users worldwide

## Endpoints

### Cryptocurrency Prices
- Base URL: `https://api.maslanka.io/{ticker}`
- Returns: Plain text price in USD
- Note: Ticker must be in UPPERCASE
- Example: `https://api.maslanka.io/BTC` returns the current Bitcoin price
- Check the status page for the complete list of supported cryptocurrencies

### Exchange Rates
- Base URL: `https://api.maslanka.io/{currency}`
- Returns: Plain text exchange rate against PLN
- Note: Currency must be in UPPERCASE
- Example: `https://api.maslanka.io/USD` returns the current USD/PLN rate

### Status Page
- Status page: `https://api.maslanka.io/status`
- Shows list of supported cryptocurrencies and current status

## Update Frequency
- Cryptocurrency prices: Updated every 5 minutes
- Exchange rates: Updated every hour

## Supported Exchange Rates
The API provides exchange rates for Polish Zloty (PLN) against:
- USD/PLN
- EUR/PLN
- CHF/PLN
- GBP/PLN

## Use Cases

### For Non-Programmers
This API is particularly useful for creating cryptocurrency portfolios in spreadsheet applications. The formulas below will automatically import the current price into your spreadsheet cell, which you can then use in calculations. The prices will automatically refresh every 5 minutes, keeping your portfolio up to date.

These formulas will:
- Import the current cryptocurrency price into the cell
- Allow you to use this value in other calculations (e.g., multiply by your holdings)
- Automatically update every 5 minutes
- Work with any supported cryptocurrency (just change BTC to the supported ticker)

#### Google Sheets
```excel
=IMPORTDATA("https://api.maslanka.io/BTC")
```

#### Microsoft Excel
```excel
=WEBSERVICE("https://api.maslanka.io/BTC")
```

### For Developers
This API can serve as a fallback endpoint for your applications. Even if you're using other price sources as your primary data provider, you can use this API as a backup to ensure continuous service. It's also perfect for prototyping and development purposes where you need quick access to current cryptocurrency prices without setting up complex infrastructure or dealing with API keys and rate limits.

#### Python Example
```python
import requests

def get_price(ticker: str) -> float:
    """
    Get current price for a cryptocurrency.
    
    Args:
        ticker (str): Cryptocurrency ticker in uppercase (e.g., 'BTC', 'ETH')
    
    Returns:
        float: Current price in USD
    """
    response = requests.get(f"https://api.maslanka.io/{ticker.upper()}")
    response.raise_for_status()  # Raises an exception for 4XX/5XX responses
    return float(response.text)

# Example usage
btc_price = get_price("BTC")
print(f"Current Bitcoin price: ${btc_price:,.2f}")
```

## Disclaimer

This API is provided for educational purposes only. The information is delivered "as is" without any warranties, express or implied. The author is not responsible for any financial losses, damages, or other consequences that may arise from using this API or the information it provides. Users should always verify the data independently and use it at their own risk.
