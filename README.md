python-bittrex-aio  
==============


Asynchronous python bindings for bittrex using aiohttp. Modified from bittrex-python by erocsomdahl


Installation
-------------

### for most recent stable release
`pip install python-bittrex-aio`

### for bleeding edge development
`pip install git+https://github.com/BlockHub/python-bittrex-aio.git`

API Documentation
-------------
**API 1.1 is considered stable**

[Official API Documentation](https://bittrex.com/Home/Api)

**API 2.0 is BETA, use at your own risk**

[Unofficial 2.0 API Documentation](https://github.com/thebotguys/golang-bittrex-api/wiki/Bittrex-API-Reference-(Unofficial)) - The golang guys have been diligently following the rapid changes to the 2.0 Beta, but use at your own risk.


Example Usage for Bittrex API
-------------

```python
from aiobittrex.bittrex import Bittrex, API_V1_1
import asyncio

my_bittrex = Bittrex(None, None, api_version=API_V1_1)  # or defaulting to v1.1 as Bittrex(None, None)
tasks = [my_bittrex.get_markets()]

loop = asyncio.get_event_loop()
res = loop.run_until_complete(asyncio.gather(*tasks))[0]
```

This call to get_markets returns an object such as the following:

```python
{'success': True, 'message': '', 'result': [{'MarketCurrency': 'LTC', ...
```

API_V2_0 and API_V1_1 are constants that can be imported from Bittrex.

To access account methods, an API key for your account is required and can be
generated on the `Settings` then `API Keys` page.
Make sure you save the secret, as it will not be visible
after navigating away from the page.

```python
from aiobittrex.bittrex import *

my_bittrex = Bittrex("<my_api_key>", "<my_api_secret>", api_version="<API_V1_1> or <API_V2_0>")

tasks = [my_bittrex.get_balance('ETH')]

loop = asyncio.get_event_loop()
res = loop.run_until_complete(asyncio.gather(*tasks))[0]


```

This call to get_balance returns an object such as the following:

```python
{'success': True,
 'message': '',
 'result': {'Currency': 'ETH', 'Balance': 0.0, 'Available': 0.0,
            'Pending': 0.0, 'CryptoAddress': None}
}
```

v1.1 constants of interest:
---
```
BUY_ORDERBOOK = 'buy'
SELL_ORDERBOOK = 'sell'
BOTH_ORDERBOOK = 'both'
```

v2.0 constants of interest
---
These are used by get_candles()
```
TICKINTERVAL_ONEMIN = 'oneMin'
TICKINTERVAL_FIVEMIN = 'fiveMin'
TICKINTERVAL_HOUR = 'hour'
TICKINTERVAL_THIRTYMIN = 'thirtyMin'
TICKINTERVAL_DAY = 'Day'
```
these are used by trade_sell() and trade_buy()
```
ORDERTYPE_LIMIT = 'LIMIT'
ORDERTYPE_MARKET = 'MARKET'

TIMEINEFFECT_GOOD_TIL_CANCELLED = 'GOOD_TIL_CANCELLED'
TIMEINEFFECT_IMMEDIATE_OR_CANCEL = 'IMMEDIATE_OR_CANCEL'
TIMEINEFFECT_FILL_OR_KILL = 'FILL_OR_KILL'

CONDITIONTYPE_NONE = 'NONE'
CONDITIONTYPE_GREATER_THAN = 'GREATER_THAN'
CONDITIONTYPE_LESS_THAN = 'LESS_THAN'
CONDITIONTYPE_STOP_LOSS_FIXED = 'STOP_LOSS_FIXED'
CONDITIONTYPE_STOP_LOSS_PERCENTAGE = 'STOP_LOSS_PERCENTAGE'
```

Testing
-------


In order to run the integration tests, a file called "secrets.json" must be added to the test folder.
Structure it as follows, adding your API keys:

```json
{
  "key": "mykey",
  "secret": "mysecret"
}
```
