---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the XRPL.to API
---

# Introduction

Welcome to the XRPL.to API! You can use our API to access XRPL.to API endpoints, which can get information on various tokens' metrics in our database.

We have language bindings in Shell and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Tokens

## Get All Tokens

```shell
#!/bin/bash

response=$(curl -sS "https://api.xrpl.to/api/tokens?start=0&limit=100&sortBy=vol24hxrp&sortType=desc&filter=")
echo $response

```

```ruby
require 'net/http'
require 'json'

uri = URI('https://api.xrpl.to/api/tokens')
params = {
  "start" => "0",
  "limit" => "100",
  "sortBy" => "vol24hxrp",
  "sortType" => "desc",
  "filter" => ""
}

uri.query = URI.encode_www_form(params)

res = Net::HTTP.get_response(uri)
tokens = JSON.parse(res.body)
```

```python
import requests

url = "https://api.xrpl.to/api/tokens"
params = {
    "start": "0",
    "limit": "100",
    "sortBy": "vol24hxrp",
    "sortType": "desc",
    "filter": ""
}

response = requests.get(url, params=params)
tokens = response.json()
```

```javascript
const axios = require('axios');

const res = await axios.get(`https://api.xrpl.to/api/tokens?start=0&limit=100&sortBy=vol24hxrp&sortType=desc&filter=`);

const tokens = res.data;
```

> The above command returns JSON structured like this:

```json
{
  "result": "success",
  "took": "18.70",
  "exch": {
    "USD": 2.559408291448575,
    "EUR": 2.6770493364433525,
    "JPY": 0.045246821410082315,
    "CNY": 0.3705075954057058
  },
  "H24": {
    "_id": "METRICS_24H",
    "activeAddresses24H": 12290,
    "tradedTokens24H": 447,
    "tradedXRP24H": 3565973.664622,
    "transactions24H": 15546
  },
  "global": {
    "_id": "METRICS_GLOBAL",
    "gDexVolume": 3565973.664622,
    "gDexVolumePro": -18.842402030897333,
    "gMarketcap": 120827548.02265854,
    "gMarketcapPro": 0.12402123412199728,
    "gScamVolume": 87.23683099999998,
    "gScamVolumePro": 0.002446367786320914,
    "gStableVolume": 490506.24331000005,
    "gStableVolumePro": 13.755184121977937,
    "gXRPdominance": 0,
    "gXRPdominancePro": 0
  },
  "total": 8416,
  "count": 8416,
  "tagName": "",
  "start": 0,
  "limit": 1,
  "sortBy": "vol24hxrp",
  "sortType": "desc",
  "filter": "",
  "tokens": [
    {
      "_id": "0413ca7cfc258dfaf698c02fe304e607",
      "md5": "0413ca7cfc258dfaf698c02fe304e607",
      "amount": "399211088.84308900115",
      "currency": "534F4C4F00000000000000000000000000000000",
      "date": "2019-12-07",
      "dateon": 1654094361537,
      "domain": "sologenic.com",
      "holders": 237778,
      "issuer": "rsoLo2S1kiGeCcn6hCUXVrCpGMWLrRrLZz",
      "kyc": false,
      "offers": 5913,
      "social": {
        "twitter": "realSologenic",
        "facebook": "realsologenic",
        "linkedin": "realsologenic",
        "instagram": "realsologenic",
        "telegram": "CoinFieldCHAT",
        "discord": "uSdE6tS67B",
        "youtube": "c/GoSOLOTV",
        "medium": "@sologenic",
        "tiktok": "@sologenic.official",
        "reddit": "r/Sologenic"
      },
      "trustlines": 288429,
      "urlSlug": "sologenic-solo",
      "user": "Sologenic",
      "verified": true,
      "imgExt": "jpg",
      "name": "SOLO",
      "tags": [
        "Payment",
        "Market",
        "Collectables & NFTs",
        "Tokenized Stocks"
      ],
      "whitepaper": "https://www.sologenic.com/downloads/sologenic-whitepaper.pdf",
      "exch": 0.41949763333333334,
      "marketcap": 68304369.66850857,
      "maxMin24h": [
        0.19057847838771405,
        0.15721754517708283
      ],
      "p24h": -0.02042820490359476,
      "p7d": -0.02816231645870154,
      "pro24h": -12.463507027255588,
      "pro7d": -17.182186625955396,
      "vol24h": 3358118.9322646316,
      "vol24htx": 4123,
      "vol24hx": 3345545.1935411547,
      "vol24hxrp": 1454435.640453,
      "id": 1,
      "supply": "399211088.84308900115",
      "usd": "0.16390414719486037532",
      "time": 1678372110000,
      "lines": 288434
    }
    ...
  ]
}
```

This endpoint retrieves tokens.

### HTTP Request

`GET https://api.xrpl.to/api/tokens?start=0&limit=20&sortBy=vol24hxrp&sortType=desc&filter=`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
start | 0 | start value for pagination.
limit | 100 | limit count value for pagination.(limit<100)
sortBy | vol24hxrp | Can be one of these values: name, exch, pro24h, pro7d, vol24hxrp, vol24htx, marketcap, trustlines, supply
sortType | desc | asc, desc

<aside class="success">
The parameter amount in JSON object is Total Supply value, supply is Circulating Supply Value.
</aside>

## Get a Specific Token Info

```shell
#!/bin/bash

slug="your_slug_here"
token=$(curl -sS "https://api.xrpl.to/api/token/${slug}?desc=no" | jq -r '.token')
echo $token

```

```ruby
require 'net/http'
require 'json'

url = URI("https://api.xrpl.to/api/token/#{slug}?desc=no")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

response = http.get(url)
data = JSON.parse(response.body)
token = data['token']
```

```python
import requests

response = requests.get('https://api.xrpl.to/api/token/' + slug + '?desc=no')
data = response.json()
token = data['token']

```

```javascript
const axios = require('axios');

const res = await axios.get(`https://api.xrpl.to/api/token/${slug}?desc=no`);

const token = res.data.token;
```

> The above command returns JSON structured like this:

```json
{
  "res": "success",
  "took": "6.94",
  "total": 8471,
  "exch": {
    "USD": 2.771922536854558,
    "EUR": 2.8985507231384062,
    "JPY": 0.045246821410082315,
    "CNY": 0.38774718883288095
  },
  "H24": {
    "_id": "METRICS_24H",
    "activeAddresses24H": 11174,
    "tradedTokens24H": 421,
    "tradedXRP24H": 3949753.145774,
    "transactions24H": 15611
  },
  "global": {
    "_id": "METRICS_GLOBAL",
    "gDexVolume": 3949753.145774,
    "gDexVolumePro": -1.9996575118499607,
    "gMarketcap": 83849829.0436422,
    "gMarketcapPro": -41.82340299541073,
    "gScamVolume": 160.08653499999994,
    "gScamVolumePro": 0.004053076966880398,
    "gStableVolume": 1628773.854211,
    "gStableVolumePro": 41.237358237278464,
    "gXRPdominance": 0,
    "gXRPdominancePro": 0
  },
  "token": {
    "_id": "0413ca7cfc258dfaf698c02fe304e607",
    "md5": "0413ca7cfc258dfaf698c02fe304e607",
    "amount": "399210377.26909844428",
    "currency": "534F4C4F00000000000000000000000000000000",
    "date": "2019-12-07",
    "dateon": 1654094361537,
    "domain": "sologenic.com",
    "holders": 237780,
    "issuer": "rsoLo2S1kiGeCcn6hCUXVrCpGMWLrRrLZz",
    "kyc": false,
    "offers": 5941,
    "social": {
      "twitter": "realSologenic",
      "facebook": "realsologenic",
      "linkedin": "realsologenic",
      "instagram": "realsologenic",
      "telegram": "CoinFieldCHAT",
      "discord": "uSdE6tS67B",
      "youtube": "c/GoSOLOTV",
      "medium": "@sologenic",
      "tiktok": "@sologenic.official",
      "reddit": "r/Sologenic"
    },
    "trustlines": 288451,
    "urlSlug": "sologenic-solo",
    "user": "Sologenic",
    "verified": true,
    "imgExt": "jpg",
    "name": "SOLO",
    "tags": [
      "Payment",
      "Market",
      "Collectables & NFTs",
      "Tokenized Stocks"
    ],
    "whitepaper": "https://www.sologenic.com/downloads/sologenic-whitepaper.pdf",
    "exch": 0.41431412813356644,
    "marketcap": 34606143.17186692,
    "maxMin24h": [
      0.16806045503009803,
      0.148757450059567
    ],
    "p24h": -0.01203137327349643,
    "p7d": -0.06888010268404397,
    "pro24h": -8.04945630899725,
    "pro7d": -46.08346566188192,
    "vol24h": 1986560.5475786927,
    "vol24htx": 3582,
    "vol24hx": 1978817.4465349228,
    "vol24hxrp": 826402.436249,
    "id": 3,
    "supply": "399210377.26909844428",
    "usd": "0.14946814805427781923",
    "time": 1678454362000,
    "lines": 288462
  }
}
```

This endpoint retrieves a specific token.

### HTTP Request

`GET https://api.xrpl.to/api/token/<slug>?desc=yes`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
slug |   | The URL slug of the token to retrieve or md5 value of the token, use the below method to get md5 value.
desc | no | yes or no, if yes, returns the description of the token in markdown language.

## Get Sparkline of a token

### HTTP Request

`https://api.xrpl.to/api/sparkline/<md5>`

Parameter | Default | Description
--------- | ------- | -----------
md5 |   | md5 value of the token

### Example

`https://api.xrpl.to/api/sparkline/0413ca7cfc258dfaf698c02fe304e607`

## Get MD5 value of the token

### Node

const CryptoJS = require('crypto-js');

const md5 = CryptoJS.MD5(issuer + '_' + currency).toString();

## Get Rich List of a Token

```shell
#!/bin/bash

md5="your_md5_here"
response=$(curl -sS "https://api.xrpl.to/api/richlist/${md5}?start=0&limit=20")
echo $response

```

```ruby
require 'net/http'
require 'json'

md5 = 'your_md5_here'

url = URI("https://api.xrpl.to/api/richlist/#{md5}?start=0&limit=20")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

response = http.get(url)
richlist = JSON.parse(response.body)
puts richlist

```

```python
import requests
import hashlib

md5 = hashlib.md5(b"your_md5_here").hexdigest()

response = requests.get(f"https://api.xrpl.to/api/richlist/{md5}", params={
    'start': '0',
    'limit': '20'
})
richlist = response.json()
print(richlist)

```

```javascript
const axios = require('axios');

const res = await axios.get(`https://api.xrpl.to/api/richlist/${md5}?start=0&limit=20`);

const richlist = res.data.richList;
```

> The above command returns JSON structured like this:

```json
{
  "result": "success",
  "took": "0.03",
  "length": 288450,
  "richList": [
    {
      "account": "rU7UKpxEYrXpbD5C5JGcqdSf3TxHxwKof5",
      "balance": 113652483.001849,
      "id": 1,
      "holding": 28.46
    }
    ...
  ]
}
```

This endpoint retrieves rich list of the specific token.

### HTTP Request

`GET https://api.xrpl.to/api/richlist/<md5>?start=0&limit=20`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
md5 |   | md5 value of the token
start | 0 | start value for pagination.
limit | 100 | limit count value for pagination.(limit<100)

<aside class="success">
You can see the example of Richlist here; https://xrpl.to/token/sologenic-solo/trustlines
</aside>

## Get Exchange history of a Token

```shell
#!/bin/bash

md5="your_md5_value"

url="https://api.xrpl.to/api/history?md5=$md5&page=0&limit=10"

response=$(curl -s "$url")

exchangeList=$(echo "$response" | jq -r '.data.hists')

echo "$exchangeList"

```

```ruby
require 'httparty'

url = "https://api.xrpl.to/api/history?md5=#{md5}&page=0&limit=10"
res = HTTParty.get(url)
exchangeList = res.parsed_response["hists"]

```

```python
import requests

url = f"https://api.xrpl.to/api/history?md5={md5}&page=0&limit=10"
res = requests.get(url)
exchangeList = res.json()["hists"]

```

```javascript
const axios = require('axios');

const res = await axios.get(`https://api.xrpl.to/api/history?md5=${md5}&page=0&limit=10`);

const exchangeList = res.data.hists;
```

> The above command returns JSON structured like this:

```json
{
  "result": "success",
  "took": "1.20ms",
  "count": 5493809,
  "hists": [
    {
      "_id": "78323565_2",
      "dir": "buy",
      "account": "rMGN8dELwKaDCJTmhSmdrPEKZJxv81qdC6",
      "maker": "rBTwLga3i2gz3doX6Gva3MgEV8ZCD8jjah",
      "taker": "rMGN8dELwKaDCJTmhSmdrPEKZJxv81qdC6",
      "seq": 85195314,
      "pair": "21e8e9b61d766f6187cb9009fda56e9e",
      "takerPaid": {
        "currency": "USD",
        "issuer": "rvYAfWj5gh67oV6fW32ZzP3Aw4Eubs59B",
        "value": "1459.65139676366"
      },
      "takerGot": {
        "currency": "XRP",
        "issuer": "XRPL",
        "value": "3941.286822"
      },
      "ledger": 78323565,
      "hash": "0D030F7AAB8EB756887916EEC6B9C3D73E0331F574D40F992C5E53E9AAE43D98",
      "time": 1678457291000
    },
    ...
  ]
}
```

This endpoint retrieves exchange history of the specific token.

### HTTP Request

`GET https://api.xrpl.to/api/history?md5=<md5>&page=0&limit=10`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
md5 |   | md5 value of the token
start | 0 | start value for pagination.
limit | 100 | limit count value for pagination.(limit<100)

<aside class="success">
You can see the example of Exchange History here; https://xrpl.to/token/sologenic-solo/historical-data
</aside>

## Get the current status

```shell
#!/bin/bash
url="https://api.xrpl.to/api/status"
response=$(curl -s "$url")
status=$(echo $response | jq -r '.data')
echo $status

```

```ruby
require 'net/http'
require 'json'

url = URI("https://api.xrpl.to/api/status")
response = Net::HTTP.get(url)
status = JSON.parse(response)['data']
puts status

```

```python
import requests

url = "https://api.xrpl.to/api/status"
response = requests.get(url)
status = response.json()['data']
print(status)

```

```javascript
const axios = require('axios');

const res = await axios.get(`https://api.xrpl.to/api/status`);

const status = res.data;
```

> The above command returns JSON structured like this:

```json
{
  "res": "success",
  "took": "5.586383819580078ms",
  "total": 8474,
  "exch": {
    "USD": 2.7015362105177005,
    "EUR": 2.8433162165697095,
    "JPY": 0.045246821410082315,
    "CNY": 0.3847633748967508
  },
  "H24": {
    "_id": "METRICS_24H",
    "activeAddresses24H": 11142,
    "tradedTokens24H": 418,
    "tradedXRP24H": 4027180.35343,
    "transactions24H": 15637
  },
  "global": {
    "_id": "METRICS_GLOBAL",
    "gDexVolume": 4026677.251987,
    "gDexVolumePro": 10.71157432777575,
    "gMarketcap": 84997204.17146377,
    "gMarketcapPro": -42.81452373297125,
    "gScamVolume": 160.06901199999996,
    "gScamVolumePro": 0.003975213357887386,
    "gStableVolume": 1613455.8129330003,
    "gStableVolumePro": 40.06916154347424,
    "gXRPdominance": 0,
    "gXRPdominancePro": 0
  }
}
```

This endpoint retrieves the current status of the platform, or XRPL.
It returns the metrics of 24 hours and Global, and the current exchange rates compared to XRP.

### HTTP Request

`GET https://api.xrpl.to/api/status`

