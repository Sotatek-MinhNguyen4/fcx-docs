# BASE URL: https://api.fcx.velo.org
#1. LIST ORDER API
### 1.1 Api create order
#### Workflow create bsc order:
- Send coin to host wallet via metamask
- Get value from metamask for parameter of create order api
- Order with pending status created success response
- BE check and update order status to active
- Order listed and can match
#### POST /api/v1/order
ID | param | type | description | example |
--- | --- | --- | --- | --- |
1 | user_id | number | user id of account, can be assigned again at backend but required before | 1 
2 | pair_id | number | id of pair trading | 1
3 | type | number | type of order, market order or limit order. Type = 1 is limit order, type = 2 is market order | 1
4 | side | number | order is buy or sell, side = 1 is buy order and 2 is sell order | 1
5 | price | string | price want to buy or sell per coin | "1"
6 | amount (optional) | string | amount of coin want to buy or sell (If input amount parameter, so total will not required, total will be calculated by amount * price) | "2"
7 | total (optional) | string | total of coin want to get or spend (If input total parameter, so amount will not required, amount will be calculated by total / price) | 3.00000000
8 | method | number | used for define network of order, method = 1 is stellar network, method = 2 is bsc network | 2
9 | maker_token | string | address of token that want to exchange, get from metamask | 
10 | taker_token | string | address of token want to take | 
11 | maker_amounts | string | amount of token that want to exchange (need to times with token decimal), get from metamask | "198500"
12 | taker_amounts | string | amount of token want to take (need to times with token decimal) | 199980.00000000
13 | maker | string | owner wallet address, get from metamask | 
13 | taker | string | get from metamask | 
14 | fee_recipient | string | host wallet address, required and checked if create order on bsc network, stellar will not required. Get it from metamask | 
15 | salt | string | get from metamask | 
16 | expiry | string | time of order expire | 4105098000000 
17 | fee_rate | string | get from metamask | 4105098000000 
18 | signature | json | required when create order on bsc network, stellar network not required ```(use Signature of @0x/protocol-utils, JSON.stringify(bscOrderWithSignature.signature)```  | 
19 | stellar_id | string | required when create order on stellar network, bsc network not required | 
20 | order_hash | string | data create order hashed required when create order on bsc network, stellar not required ```(use LimitOrder of @0x/protocol-utils, function getHash())```  | 
21 | sender | string | get from metamask  | 

```Note: sender, fee_recipient get from metamask when connected with our website```
![Alt text](./metamask.png?raw=true "Metamask")

#### Example of create limit buy order on bsc network
```bash 
curl 'http://localhost:3000/api/v1/order' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="90", "Google Chrome";v="90"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjE0OSwiaWF0IjoxNjQyMjYyMjk3LCJleHAiOjE2NDIyNjI4OTd9.EUaT4hAwNBgpkM2Chm1TRTwxyiym_Y2RB4ymOtZnPzs' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36' \
  -H 'Content-Type: application/json' \
  -H 'Origin: http://localhost:3001' \
  -H 'Sec-Fetch-Site: same-site' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: http://localhost:3001/' \
  -H 'Accept-Language: en-US,en;q=0.9,vi;q=0.8' \
  --data-raw '{"maker_token":"0x364c348c88cf73a3bf83b4aeafcddcdcc0758a74","taker_token":"0xad561d38f93c5f6b391e89be958a18ba7c973267","maker_amounts":"198500","taker_amounts":"198500","price":"1","amount":"2","sender":"0x0e01164A64daCB3811a3E61e74B3ebf9ebA8410E","maker":"0x7ed3ed81af7e2622762ece82f1ee2240079299ec","taker":"0x0000000000000000000000000000000000000000","taker_token_fee_amounts":"1500","fee_recipient":"0x2D4159A016fD5318da2057a2173d48Dc11af314e","pool":"0x0000000000000000000000000000000000000000000000000000000000000000","expiry":"4105098000","salt":"5958798523602954416002924332320155705279085706701420024498823625238961912584","type":1,"signature":"{\"r\":\"0xa7afcbee942f035edee385d36535d492986cc977afd38b06b8aa443f8bd5a03b\",\"s\":\"0x52d76b7a71f6aaa659e65cc45d723352dd9d6d5601f483e8bf714329ae7d3616\",\"v\":28,\"signatureType\":2}","pair_id":1,"side":1,"order_hash":"0x9e0102c13f58b463c25f40a4945e957db1f3762994f4856772114156db647ff2","method":2}' \
  --compressed
```
#### Success response
```json 
{
    "code":0,
    "data":{
        "maker_token":"0x364c348c88cf73a3bf83b4aeafcddcdcc0758a74",
        "taker_token":"0xad561d38f93c5f6b391e89be958a18ba7c973267",
        "maker_amounts":"198500",
        "taker_amounts":"198500",
        "price":"1",
        "amount":"2",
        "sender":"0x0e01164A64daCB3811a3E61e74B3ebf9ebA8410E",
        "maker":"0x7ed3ed81af7e2622762ece82f1ee2240079299ec",
        "taker":"0x0000000000000000000000000000000000000000",
        "taker_token_fee_amounts":"1500",
        "fee_recipient":"0x2D4159A016fD5318da2057a2173d48Dc11af314e",
        "pool":"0x0000000000000000000000000000000000000000000000000000000000000000",
        "expiry":"4105098000",
        "salt":"79012298893516645825601943828471925744555987808523384181075828635400212917506",
        "type":1,
        "signature":"{\"r\":\"0xcd9c469f2a7bdc021c776dac831d27a9fe9699ace6031a823ffbf3b117d4f3b8\",\"s\":\"0x4a338e271fd750ccf431aa36396934dd498f3a3b907ea23b7123364fa66564f6\",\"v\":28,\"signatureType\":2}",
        "pair_id":1,
        "side":1,
        "order_hash":"0xade7b2c2ce342683361c5b98dc2f7aadc656c3c100f5880818d43ae86d7c7d33",
        "method":2,
        "user_id":149,
        "fee_rate":"0.00750000",
        "filled_amount":"0",
        "remaining_amount":"1.985",
        "status":0,"id":53
    },
    "metadata":{
        "timestamp":"2022-01-15T15:21:27.144Z"
    }
}
```

### 1.2 Api cancel order
#### PUT /api/v1/order/:id/cancel
ID | param | type | description | example |
--- | --- | --- | --- | --- |
1 | id | number | id of order want to cancel | 1 |

#### Example
```bash
curl 'http://localhost:3000/api/v1/order/52/cancel' \
  -X 'PUT' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 0' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="90", "Google Chrome";v="90"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjE0OSwiaWF0IjoxNjQyMjYyMjk3LCJleHAiOjE2NDIyNjI4OTd9.EUaT4hAwNBgpkM2Chm1TRTwxyiym_Y2RB4ymOtZnPzs' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36' \
  -H 'Origin: http://localhost:3001' \
  -H 'Sec-Fetch-Site: same-site' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: http://localhost:3001/' \
  -H 'Accept-Language: en-US,en;q=0.9,vi;q=0.8' \
  --compressed
```

#### Success response
```json
{
    "code":0,
    "data":{
        "id":52,
        "user_id":149,
        "pair_id":1,
        "type":1,
        "side":1,
        "price":"1.00000000",
        "average":null,
        "amount":"2.00000000",
        "filled_amount":"0.00000000",
        "remaining_amount":"1.98500000",
        "total":null,
        "status":-1,
        "method":2,
        "fee_rate":"0.00750000",
        "maker_token":"0x364c348c88cf73a3bf83b4aeafcddcdcc0758a74",
        "taker_token":"0xad561d38f93c5f6b391e89be958a18ba7c973267",
        "maker_amounts":"198500.00000000",
        "taker_amounts":"198500.00000000",
        "sender":"0x0e01164A64daCB3811a3E61e74B3ebf9ebA8410E",
        "maker":"0x7ed3ed81af7e2622762ece82f1ee2240079299ec",
        "taker":"0x0000000000000000000000000000000000000000",
        "taker_token_fee_amounts":"1500.00000000",
        "fee_recipient":"0x2D4159A016fD5318da2057a2173d48Dc11af314e",
        "signature":"{\"r\": \"0x6e7f0906871fced0781f90cddb77e8c66a4d40f9b1a5b8ea2438e46d7aec1ea9\", \"s\": \"0x7ecdbb0f07508ebafbe980bb2041c79f65061808bfd226d53f2d1903a0cb20f0\", \"v\": 27, \"signatureType\": 2}",
        "salt":"44280389984292706666356042711083545075914898498415566171132947110988651370682",
        "order_hash":"0xace0158a2532f2f89ece20b00dda3ed67c4b8b1c07405f3360f80dfea4018efa",
        "stellar_id":null,
        "pool_id":null,
        "expiry":4105098000,
        "created_at":"2022-01-15T08:20:52.000Z",
        "updated_at":"2022-01-15T15:58:40.325Z"
    },
    "metadata":{
        "timestamp":"2022-01-15T15:58:40.338Z"
    }
}
```

### 1.3 Api list orders
#### GET /api/v1/order/list
ID | param | type | description | example |
--- | --- | --- | --- | --- |
1 | page | number | page | 1 |
2 | limit | number | number of order in page | 10 |
3 | pair (optional) | number | id of pair | 1 |
4 | method (optional) | number | id of order method | 1 |
5 | wallet (optional) | string | owner wallet address used for create order |  |
6 | status (optional) | number[] | order status, Invalid = -2, Pending = 0, Canceled = -1, Fillable = 1,Filling = 2, Fulfill = 3, PartiallyFilled = 4, | [0] |

#### Example request
```bash
curl 'http://localhost:3000/api/v1/order/list?page=1&limit=8&method\[\]=1&method\[\]=2&method\[\]=4&method\[\]=8&status\[\]=1&status\[\]=2&status\[\]=0' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="90", "Google Chrome";v="90"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjE0OSwiaWF0IjoxNjQyMzE0NjQyLCJleHAiOjE2NDIzMTUyNDJ9.w2WY2xMQlJoCbOLwlojjzDpOqUHDt1o9SAMWA7kCxn4' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36' \
  -H 'Origin: http://localhost:3001' \
  -H 'Sec-Fetch-Site: same-site' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: http://localhost:3001/' \
  -H 'Accept-Language: en-US,en;q=0.9,vi;q=0.8' \
  -H 'If-None-Match: W/"3ac-tg+Y3lYVZ70RsRez6iVWjsTCp28"' \
  --compressed
```

#### Success response
```json
{
  "code":0,
  "data":[
    {
      "id":54,
      "user_id":149,
      "pair_id":1,
      "type":1,
      "side":1,
      "price":"1.00000000",
      "average":null,
      "amount":"2.00000000",
      "filled_amount":"0.00000000",
      "total":null,
      "status":0,
      "method":2,
      "maker_amounts":"198500.00000000",
      "taker_amounts":"198500.00000000",
      "address":"0x7ed3ed81af7e2622762ece82f1ee2240079299ec",
      "stellar_id":null,
      "pool_id":null,
      "created_at":"2022-01-15T09:01:56.000Z",
      "base_name":"vEUR","quote_name":"vUSD"
    },
    {
      "id":51,
      "user_id":149,
      "pair_id":1,
      "type":1,
      "side":1,
      "price":"1.00000000",
      "average":null,
      "amount":"2.00000000",
      "filled_amount":"0.00000000",
      "total":null,"status":0,
      "method":2,
      "maker_amounts":"198500.00000000",
      "taker_amounts":"198500.00000000",
      "address":"0x7ed3ed81af7e2622762ece82f1ee2240079299ec",
      "stellar_id":null,
      "pool_id":null,
      "created_at":"2022-01-15T08:15:12.000Z",
      "base_name":"vEUR","quote_name":"vUSD"
    }
  ],
  "metadata":{
    "page":1,
    "limit":8,
    "totalItem":2,
    "totalPage":1,
    "timestamp":"2022-01-16T06:30:43.291Z"
  }
}
```

#2. PAIR API
### 2.1 Api list pair support
#### GET /api/v1/pair/list
#### Example request
```bash
curl 'http://localhost:3000/api/v1/pair/list' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="90", "Google Chrome";v="90"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjE0OSwiaWF0IjoxNjQyMzE0NjQyLCJleHAiOjE2NDIzMTUyNDJ9.w2WY2xMQlJoCbOLwlojjzDpOqUHDt1o9SAMWA7kCxn4' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36' \
  -H 'Origin: http://localhost:3001' \
  -H 'Sec-Fetch-Site: same-site' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: http://localhost:3001/' \
  -H 'Accept-Language: en-US,en;q=0.9,vi;q=0.8' \
  -H 'If-None-Match: W/"1a74-pLJO5QVYVCeL77orgE87FiQ4lIc"' \
  --compressed
```
#### Success response 
```json
{
  "code":0,
  "data":[
    {
      "pairs_id":1,
      "price_precision":"0.00001",
      "amount_precision":"0.01",
      "minimum_amount":"1",
      "minimum_total":"1",
      "group_count":5,
      "quote_name":"vUSD",
      "base_warp_type_id":4,
      "base_name":"vEUR",
      "base_symbol":"vEUR",
      "base_type":2,
      "base_stellar_issuer":"GAXXMQMTDUQ4YEPXJMKFBGN3GETPJNEXEUHFCQJKGJDVI3XQCNBU3OZI",
      "base_bsc_address":"0xad561d38f93c5f6b391e89be958a18ba7c973267",
      "base_decimal":5,
      "quote_warp_type_id":2,
      "quote_symbol":"vUSD",
      "quote_type":2,
      "quote_stellar_issuer":"GAXXMQMTDUQ4YEPXJMKFBGN3GETPJNEXEUHFCQJKGJDVI3XQCNBU3OZI",
      "quote_bsc_address":"0x364c348c88cf73a3bf83b4aeafcddcdcc0758a74",
      "quote_decimal":5
    },
    {
      "pairs_id":2,
      "price_precision":"0.0001",
      "amount_precision":"0.01",
      "minimum_amount":"1",
      "minimum_total":"1",
      "group_count":4,
      "quote_name":"vTHB",
      "base_warp_type_id":4,
      "base_name":"vEUR",
      "base_symbol":"vEUR",
      "base_type":2,
      "base_stellar_issuer":"GAXXMQMTDUQ4YEPXJMKFBGN3GETPJNEXEUHFCQJKGJDVI3XQCNBU3OZI",
      "base_bsc_address":"0xad561d38f93c5f6b391e89be958a18ba7c973267",
      "base_decimal":5,
      "quote_warp_type_id":3,
      "quote_symbol":"vTHB",
      "quote_type":2,
      "quote_stellar_issuer":"GAXXMQMTDUQ4YEPXJMKFBGN3GETPJNEXEUHFCQJKGJDVI3XQCNBU3OZI",
      "quote_bsc_address":"0x5417ef6c5638d8d8a5630e14f17a75d5d32ab476",
      "quote_decimal":5
    }
  ],
  "metadata":{
    "timestamp":"2022-01-16T06:34:11.484Z"
  }
}
```
#3. TRADE API
### 3.1 Api list trade history
#### GET /api/v1/trades/list
ID | param | type | description | example |
--- | --- | --- | --- | --- |
1 | page | number | page | 1 |
2 | limit | number | number of order in page | 10 |
2 | limit | number | number of order in page | 10 |
3 | pair (optional) | number | id of pair | 1 |
4 | method (optional) | number | id of order method | 1 |
5 | wallet (optional) | string | owner wallet address used for create order |  |
6 | tradeMethodTab (optional) | number[] | pancake = 8, stellar = 1, bsc order book = 2, bsc pool = 4 | [1] |
7 | orderId (optional) | number | id of order | 1 |
8 | pool (optional) | string | pool address |  |
9 | type (optional) | number | type |  |
10 | coinId (optional) | number | type |  |
11 | startDate (optional) | date | start date |  |
12 | endDate (optional) | date | end date |  |
