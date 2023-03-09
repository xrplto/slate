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
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the XRPL.to API! You can use our API to access XRPL.to API endpoints, which can get information on various tokens' metrics in our database.

We have language bindings in Shell and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Tokens

## Get All Tokens

```shell
curl "https://api.xrpl.to/api/tokens?start=0&limit=20&sortBy=vol24hxrp&sortType=desc&filter="
```

```ruby
require 'net/http'
require 'json'

uri = URI('https://api.xrpl.to/api/tokens%27')
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
limit | 100 | limit count value for pagination.(100>limit>1)
sortBy | vol24hxrp | Can be one of these values: name, exch, pro24h, pro7d, vol24hxrp, vol24htx, marketcap, trustlines, supply
sortType | desc | Ascending or Descending

<aside class="success">
The parameter amount in JSON object is Total Supply value, supply is Circulating Supply Value.
</aside>

## Get a Specific Token Info

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

