# GeoDB

REST API for city and geographic data. Returns city name, state, country, coordinates, population, and capital status.

## Features

- Single endpoint for city lookups worldwide
- Returns structured JSON with full location data
- Filter by city name and/or country code
- 5,000 requests/month on free tier
- Example Response:
```json
[
  {
    "city_name": "New York",
    "state": "New York",
    "country_code": "US",
    "is_capital": false,
    "coordinates": {
      "latitude": 40.6943,
      "longitude": -73.9249
    },
    "population": 18713220
  }
]
```

## Authentication

1. Create account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up)

![Sign Up](https://raw.githubusercontent.com/omkarcloud/assets/master/images/signup.png)

2. Get API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key)

![Copy API Key](https://raw.githubusercontent.com/omkarcloud/assets/master/images/enrichment-key-omkar.png)

3. Include `API-Key` header in requests

## Quick Start

```bash
curl -X GET "https://city-api.omkar.cloud/city?name=New%20York" \
  -H "API-Key: YOUR_API_KEY"
```

```json
[
  {
    "city_name": "New York",
    "state": "New York",
    "country_code": "US",
    "is_capital": false,
    "coordinates": {
      "latitude": 40.6943,
      "longitude": -73.9249
    },
    "population": 18713220
  }
]
```

## Installation

### Python

```bash
pip install requests
```

```python
import requests

response = requests.get(
    "https://city-api.omkar.cloud/city",
    params={"name": "New York"},
    headers={"API-Key": "YOUR_API_KEY"}
)

cities = response.json()
```

### Node.js

```bash
npm install axios
```

```javascript
import axios from "axios";

const response = await axios.get("https://city-api.omkar.cloud/city", {
    params: { name: "New York" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

const cities = response.data;
```

## API Reference

### Endpoint

```
GET https://city-api.omkar.cloud/city
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `API-Key` | Yes | API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key) |

### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `name` | No | — | City name (e.g., "New York", "Tokyo") |
| `country_code` | No | — | Two-letter ISO country code (e.g., "US", "JP") |

### Response

```json
[
  {
    "city_name": "string",
    "state": "string",
    "country_code": "string",
    "is_capital": "boolean",
    "coordinates": {
      "latitude": "number",
      "longitude": "number"
    },
    "population": "number"
  }
]
```

| Field | Type | Description |
|-------|------|-------------|
| `city_name` | string | City name |
| `state` | string | State or province |
| `country_code` | string | Two-letter ISO code |
| `is_capital` | boolean | Whether it's the country's capital |
| `coordinates.latitude` | number | Latitude coordinate |
| `coordinates.longitude` | number | Longitude coordinate |
| `population` | number | City population |

## Examples

### Search by city name

```python
response = requests.get(
    "https://city-api.omkar.cloud/city",
    params={"name": "Tokyo"},
    headers={"API-Key": "YOUR_API_KEY"}
)

for city in response.json():
    print(f"{city['city_name']}, {city['country_code']}: {city['population']}")
```

### Filter by country

```python
response = requests.get(
    "https://city-api.omkar.cloud/city",
    params={"name": "London", "country_code": "GB"},
    headers={"API-Key": "YOUR_API_KEY"}
)

london_uk = response.json()[0]
```

### Get coordinates

```javascript
const { data } = await axios.get("https://city-api.omkar.cloud/city", {
    params: { name: "Paris" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

const { latitude, longitude } = data[0].coordinates;
```

## Error Handling

```python
response = requests.get(
    "https://city-api.omkar.cloud/city",
    params={"name": "InvalidCity123"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
    if not data:
        # No cities found
        pass
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Support

[![Contact Us on WhatsApp about GeoDB](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20GeoDB.)

[![Contact Us on Email about GeoDB](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=GeoDB%20Question)
