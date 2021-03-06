# Falcon Stats
[![Build Status](https://travis-ci.org/dmuhs/falcon-stats.svg?branch=master)](https://travis-ci.org/dmuhs/falcon-stats)
[![PyPI](https://img.shields.io/pypi/status/falcon-stats.svg)](https://pypi.python.org/pypi/falcon-stats)
[![PyPI](https://img.shields.io/pypi/v/falcon-stats.svg)](https://pypi.python.org/pypi/falcon-stats)
[![PyPI](https://img.shields.io/pypi/format/falcon-stats.svg)](https://pypi.python.org/pypi/falcon-stats)


`falcon-stats` is a simple usage statistics middleware for the [Falcon REST framework](https://falconframework.org/). It should primarily enable later analysis that separately gets relevant data from the DB.

## Data Collection
*Falcon Stats* gathers data on incoming requests and their processed responses. Currently the following features are saved:

- Response Timestamp
- Processing Time between Request and Response
- Request Method
- User Agent
- Request URI (domain, endpoint and query string)
- Remote IP (closest to the server)
- Request Content-Type
- Response Status
- Request Content Length

Note that logging and database access add overhead to the processing time. Furthermore it will add a few milliseconds on every response.

## Installation
... is as easy as

```
pip install git+https://github.com/sycured/falcon-stats.git
```

Installation assumes you have the packages found in *requirements.txt* installed.

## Usage
In your main falcon file import the `FalconStatsMiddleware` and add it to the middleware list of your API instance. That's it.

```python
from falconstats import FalconStatsMiddleware
...
fsm = FalconStatsMiddleware(
    db_engine="mysql+pymysql",
    db_user="root",
    db_pass="my-secret-pw",
    db_addr="localhost",
    db_port="3306",
    db_name="stats"
)
app = falcon.API(middleware=[fsm])
```

## Compatibility
The middleware is tested with Python 3.6, 3.7 and 3.8. I don't plan on supporting older version.
