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
  -H "Authorization: gamepergameper"
```

> `gamepergameper` 부분을 고객님의 API키로 바꾸어주세요.

겜퍼 API를 사용하기 위해서는 API 키가 필요합니다. API KEY는 [겜퍼](http://gameper.io)에 연락하면 받으실 수 있습니다.

API KEY를 사용하는 모든 요청은 다음의 헤더 값과 시그니쳐를 포함해야 합니다.

- GP-ACCESS-KEY API 키
- GP-ACCESS-SIGN 시그니쳐
- GP-ACCESS-TIMESTAMP 타임스탬프

모든 요청은 content type: application/json 헤더를 가져아하고 데이터는 유효한 JSON 스타일이어야 합니다..

GP-ACCESS-SIGN 헤더는 sha256(timestamp + method + request-path + body(string concatenation))을 secret key로 사인한 값입니다. timestamp 값은 헤더의 timestamp와 같아야 합니다.

body는 요청 값들을 공백을 제외하고 단순히 붙인 값입니다. GET 요청의 경우 생략됩니다.

요청 메소드는 대문자여야 합니다(GET, POST).

GP-ACCESS-TIMESTAMP 헤더는 Unix timestamp의 second 단위 입니다.

Timestamp 값은 실제 요청 시각과 10초 이상 차이가 나면 거절됩니다. 


`GP-ACCESS-KEY: gamepergameper`

<aside class="notice">
<code>gamepergameper</code> 부분을 고객님의 API 키로 바꾸셔야 합니다..
베타 버전 Gameper API는 GP-ACCESS-KEY 헤더만 필요합니다.
</aside>

# Assets

## Get Balance

```curl
curl "http://api.gameper.io/v1/assets/balance/GPToken/0x9d6d492bD500DA5B33cf95A5d610a73360FcaAa0"
  -H "GP-ACCESS-KEY: gamepergameper"
```

> The above command returns JSON structured like this:

```json
{
  "asset_id": "GPToken",
  "uri": "Gameper Token",
  "balance": "10000",
  "value": 100
}
```

유저의 현재 잔고를 가져옵니다.

### HTTP Request

`GET http://api.gameper.io/v1/assets/balance/<ASSET_ID>/<USER_ADDRESS>`

### URL Parameters

Parameter | Description
--------- | -----------
ASSET_ID | 자산 ID
USER_ADDRESS | 유저 주소(식별값)

## Mint

## Transfer

## Total Supply

## Swap

## Approve


## Get All Kittens



> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```curl
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
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

```curl
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
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

