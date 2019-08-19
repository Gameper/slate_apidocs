# Errors

<aside class="notice">
겜퍼 API가 실패하면 다음의 코드가 반환됩니다. 음수 값은 블록체인 스마트 컨트랙트에서의 반환값입니다.
</aside>

The Gamper API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The api requested is hidden for administrators only.
404 | Not Found -- The specified api could not be found.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
