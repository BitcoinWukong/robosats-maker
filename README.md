# robosats-maker
A python script to simplify the life of robosats maker.

By default, the script creates a new order at 8AM UTC, and cancel the order at 11PM UTC. You can adjust the value by setting `--start_hour` and `--end_hour` parameters.

The script relies on blink.sv wallet API to pay for the maker bond. In the future, we may consider support other LN providers, but only Blink wallet is supported at this moment.

# Prerequisite
1. You need a Blink wallet account at blink.sv in order to use this script, and you need to create a blink API token which you can get from https://www.blink.sv/en/api
1. You also need a Robosats Robot token, which will be used to create the order
1. You need a local tor service running, the script assuming the tor service is listening at localhost:9050


# How to use

1. Install pip libs:
`pip3 install -r requirements.txt`
1. Run the script:
`robosats-maker.py [--type {0,1}] [--currency {1,2,3,4,5,6}] robosats_token blink_api_key amount payment_method premium`

For example:
`python3 robosats-maker.py --start_hour 15 --end_hour 23 --type 1 --currency 2 $$robosats_token $$blink_api_token 100 "USDT" 20`

# Notes

For more details, you can check `python3 robosats-maker.py -h`:
```
➜  python3 robosats-maker.py -h
usage: robosats-maker.py [-h] [--type {0,1}] [--currency {1,2,3,4,5,6}] [--start_hour START_HOUR] [--end_hour END_HOUR]
                         robosats_token blink_api_key amount payment_method premium

RoboSats Maker Script

positional arguments:
  robosats_token        RoboSats token
  blink_api_key         Blink API key
  amount                Amount for the order
  payment_method        Payment Method, more details:
                        https://github.com/RoboSats/robosats/blob/main/frontend/src/components/PaymentMethods/MethodList.ts
  premium               Premium for the order

optional arguments:
  -h, --help            show this help message and exit
  --type {0,1}          Order type: 0 for buy, 1 for sell (default: 0)
  --currency {1,2,3,4,5,6}
                        Currency: 1 for USD, 2 for EUR, etc. (default: 2), more details:
                        https://github.com/RoboSats/robosats/blob/main/frontend/static/assets/currencies.json
  --start_hour START_HOUR
                        Start hour in UTC
  --end_hour END_HOUR   End hour in UTC

```
