---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - curl

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://gameper.io'>Documentation Powered by Gameper</a>

includes:
  - errors

search: true
---

# Introduction

Gameper API 문서에 오신 것을 환영합니다.

REST 형식의 Gameper API를 통해서 겜퍼 시스템에서 자산을 발행하고 전송할 수 있습니다.

본 문서는 겜퍼 API를 어떻게 사용하는지에 관한 정보를 제공합니다.

# API KEY

> To check available apis with your api key, use this code:


```curl
# With every request, you can just pass the correct header with each request
curl "https://api.gameper.io/"
  -H "GP-ACCESS-KEY: gamepergameper" \
  -H "Content-Type: application/json"
```

겜퍼 API를 사용하기 위해서는 API 키가 필요합니다. API KEY는 [겜퍼](http://gameper.io)에 연락하면 받으실 수 있습니다.

API KEY를 사용하는 모든 요청은 다음의 헤더 값과 시그니쳐를 포함해야 합니다.

- GP-ACCESS-KEY API 키
- GP-ACCESS-SIGN 시그니쳐
- GP-ACCESS-TIMESTAMP 타임스탬프

API 헤더 값은 다음의 조건들을 만족해야 합니다.

1. 모든 요청은 <code>content-type: application/json</code> 헤더를 가져아하고 데이터는 유효한 JSON 스타일이어야 합니다..
2. <code>GP-ACCESS-SIGN</code> 헤더는 <code>sha256(timestamp + method + request-path + body(string concatenation))</code>을 secret key로 사인한 값입니다.
3. <code>timestamp</code>값은 헤더의 <code>CP-ACCESS-TIMESTAMP</code>와 같아야 합니다.
4. body는 요청 값들을 공백을 제외하고 단순히 붙인 값입니다. GET 요청의 경우 생략됩니다.
5. 요청 메소드는 대문자여야 합니다(<code>GET</code>, <code>POST</code>).
6. <code>GP-ACCESS-TIMESTAMP</code> 헤더는 Unix timestamp의 second 단위 입니다.
7. <code>GP-ACCESS-TIMESTAMP</code>값은 실제 요청 시각과 10초 이상 차이가 나면 거절됩니다. 

<aside class="notice">
베타 버전 Gameper API는 GP-ACCESS-KEY 헤더만 필요합니다.
</aside>

# Assets

## Get Balance

```curl
curl "http://api.gameper.io/v1/fabric/jp/balanceOf/GPToken/0x9d6d492bD500DA5B33cf95A5d610a73360FcaAa0" \
  -H "GP-ACCESS-KEY: gamepergameper" \
  -H "Content-Type: application/json" \
  -H "type: Org1"
```

> The above command returns JSON structured like this:

```json
{
  "asset_id": "GPToken",
  "uri": "Gameper Token",
  "balance": "10000",
  "value": "100"
}
```

유저의 현재 잔고를 가져옵니다.

### HTTP Request

`GET http://api.gameper.io/v1/fabric/jp/balanceOf/<ASSET_ID>/<USER_ADDRESS>`

### URL Parameters

Parameter | Description
--------- | -----------
ASSET_ID | 자산 ID
USER_ADDRESS | 유저 주소(식별값)

## Mint

```curl
curl "http://api.gameper.io/v1/fabric/jp/mint" \
  -X POST \
  -H "GP-ACCESS-KEY: gamepergameper" \
  -H "Content-Type" application/json"
  -H "type: Org1" \
  -d '{
    "asset_id":"GPToken",
    "from_account":"john",
    "to_account":"kevin",
    "amount":"2000",
    "name":"GPToken",
    "value":"100",
    "uri":"This is GP Token",      
  }'
```

> The above command returns JSON structured like this:

```json
{
  "asset_id": "GPToken",
  "uri": "This is GP Token",
  "total_supply": "10000",
  "value": "100",
  "tx_id":"0x9da6878671c45d7e5f4c43688565ff3fb334ce7ba22bebb28df272a35265e7bf"
}
```
자산을 발행합니다. 권한이 있는 유저만 자산을 발행 또는 추가 발행 할 수 있습니다. `tx_id`를 이용하여 블록 익스플로러에서 tx를 확인 할 수 있습니다.

### HTTP Request

`POST http://api.gameper.io/v1/fabric/jp/mint`

### BODY Parameters

Parameter | Description
--------- | -----------
asset_id | 자산 ID
from_account | 발행하는 유저 주소
to_account | 자산을 받는 유저 주소
amount | 발행량
name | 자산 이름
value | 자산 가치
uri | 추가 정보

<aside class="warning">
권한이 있는 유저만이 자산을 발행 할 수 있습니다.
</aside>

## Transfer

```curl
curl "http://api.gameper.io/v1/fabric/jp/transfer" \
  -X POST \
  -H "GP-ACCESS-KEY: gamepergameper" \
  -H "Content-Type" application/json"
  -H "type: Org1" \
  -d '{
    "asset_id":"GPToken",
    "from_account":"john",
    "to_account":"kevin",
    "amount":"2000",
  }'
```

> The above command returns JSON structured like this:

```json
{
  "tx_id":"0x9da6878671c45d7e5f4c43688565ff3fb334ce7ba22bebb28df272a35265e7bf"
}
```
자산을 전송합니다. `tx_id`를 이용하여 블록 익스플로러에서 tx를 확인 할 수 있습니다.

### HTTP Request

`POST http://api.gameper.io/v1/fabric/jp/transfer`

### BODY Parameters

Parameter | Description
--------- | -----------
asset_id | 자산 ID
from_account | 자산을 보내는 유저 주소
to_account | 자산을 받는 유저 주소
amount | 발행량

<aside class="warning">
잔고가 충분해야 자산을 전송할 수 있습니다.
</aside>

## Total Supply

To be continued.

## Swap

To be continued.

## Approve

To be continued.