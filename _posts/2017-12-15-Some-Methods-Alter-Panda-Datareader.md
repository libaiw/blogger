---
title: Alternative methods for Datareader of Panda 
---
Since Google change the policy of data queries, "datareader" of panda for Python doesn't work well. Here are some alternative ways for workaround.

> Get a CSV file: sample URL: https://finance.google.com/finance/historical?q=SPY&startdate=2017/01/01&enddate=2017/05/22&output=csv

> pandas_datareader snippet 

...
<p>
import pandas_datareader.data as web
import datetime

start = datetime.datetime(2017, 1, 1)
end = datetime.date.today()

google = False

if google:
    f = web.DataReader("ETR:SIE", 'google', start, end)
else:
    f = web.DataReader("SIE.DE", 'yahoo', start, end)

print(f.Close)
</p>
...

>>

import datetime
import requests
from io import StringIO
# This is just a wrapper importing the compatible version of
#     urllib's urlencode--see pandas docs
from pandas.io.common import urlencode
import pandas as pd

BASE = 'http://finance.google.com/finance/historical'


# There seems to be confusion over whether the date api has changed.
# https://github.com/pydata/pandas-datareader/pull/425
# Both formats seem to work, but I'll use the "newer" one here to be safe
def get_params(symbol, start, end):
    params = {
        'q': symbol,
        'startdate': start.strftime('%Y/%m/%d'),
        'enddate': end.strftime('%Y/%m/%d'),
        'output': "csv"
    }
    return params


def build_url(symbol, start, end):
    params = get_params(symbol, start, end)
    return BASE + '?' + urlencode(params)


start = datetime.datetime(2010, 1, 1)
end = datetime.datetime.today()   # made around 10:30 am EST
sym = 'SPY'
url = build_url(sym, start, end)

data = requests.get(url).text
data = pd.read_csv(StringIO(data), index_col='Date', parse_dates=True)

print(data.head())


>>
import datetime

from pandas.compat import StringIO, bytes_to_str
from pandas.io.common import urlencode
import requests


BASE = 'http://finance.google.com/finance/historical'


def _get_params(symbol, start, end):
    params = {
        'q': symbol,
        'startdate': start.strftime('%Y/%m/%d'),
        'enddate': end.strftime('%Y/%m/%d'),
        'output': "csv"
    }
    return params


def build_url(symbol, start, end, form='new'):
    params = _get_params(symbol, start, end)
    return BASE + '?' + urlencode(params)


sym = 'AAPL'
start = date(2010, 1, 1)
end = date.today()

url = build_url(sym, start, end)
# http://finance.google.com/finance/historical?q=AAPL&startdate=Jan+01%2C+2010&enddate=Dec+05%2C+2017&output=csv


session = requests.Session()
byts = session.get(url).content
out = StringIO()
out.write(bytes_to_str(byts))
out.seek(0)
data = pd.read_csv(out, index_col=0, parse_dates=True).sort_index()

data 
              Open    High     Low   Close     Volume
# Date                                                 
# 2010-01-04   30.49   30.64   30.34   30.57  123432050
# 2010-01-05   30.66   30.80   30.46   30.63  150476004
# 2010-01-06   30.63   30.75   30.11   30.14  138039594
# 2010-01-07   30.25   30.29   29.86   30.08  119282324
# 2010-01-08   30.04   30.29   29.87   30.28  111969081
# 2010-01-11   30.40   30.43   29.78   30.02  115557365
# 2010-01-12   29.88   29.97   29.49   29.67  148614774
# 2010-01-13   29.70   30.13   29.16   30.09  151472335
# 2010-01-14   30.02   30.07   29.86   29.92  108288411
# 2010-01-15   30.13   30.23   29.41   29.42  148584065
# 2010-01-19   29.76   30.74   29.61   30.72  182501620
# 2010-01-20   30.70   30.79   29.93   30.25  153037892
#            ...     ...     ...     ...        ...
# 2017-11-16  171.18  171.87  170.30  171.10   23637484
# 2017-11-17  171.04  171.39  169.64  170.15   21899544
# 2017-11-20  170.29  170.56  169.56  169.98   16262447
# 2017-11-21  170.78  173.70  170.78  173.14   25131295
# 2017-11-22  173.36  175.00  173.05  174.96   25588925
# 2017-11-24  175.10  175.50  174.65  174.97   14026673
# 2017-11-27  175.05  175.08  173.34  174.09   20716802
# 2017-11-28  174.30  174.87  171.86  173.07   26428802
# 2017-11-29  172.63  172.92  167.16  169.48   41666364
# 2017-11-30  170.43  172.14  168.44  171.85   41527218
# 2017-12-01  169.95  171.67  168.50  171.05   39759288
# 2017-12-04  172.48  172.62  169.63  169.80   32542385

