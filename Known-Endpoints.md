# Known Endpoints

(host: app.snapchat.com unless otherwise specified)

## /loq/register_exp

Registers Device ID with Snapchat. Appears to only be on iOS.

### iOS example:

Request form:

```
device_unique_id: some random 40 char hex string
req_token: static token and timestamp using req_token formula
timestamp: current millis timestamp
```

## /loq/device_id

Gets a dtoken1i/dtoken1v pair. Use to create new Device IDs. Don't do this too often, but do this enough that you do not get banned. Only run upon initial app opening, reset after reinstall.

### Android example:

Headers:
```
Accept-Locale: en_US
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Accept-Encoding: gzip
Accept-Language: en-US;q=1
Accept: application/json
Content-Length: 98
Connection: keep-alive
User-Agent: Snapchat/10.25.5.3 (HTC One M8; Android 5.1; gzip)
```

Body:
```
req_token: 930a6150aad1fd386edf5cebf5a64ef4b9e94d8d19515a8139b4c314d7c513cb
timestamp: 1517762512144
```

Response:
```json
{"dtoken1i":"<insert dtoken1i here>","dtoken1v":"<insert dtoken1v here>"}
```
dtoken1i and dtoken1v are used in the login process. dtoken1v is used in the HMAC for the DSIG in login. dtoken1i is sent with it.

### iOS:

Add a X-Snapchat-Client-Auth-Token and a UUID to headers, and change User-Agent to an iOS one.

## /bq/ping_network

Seems to be iOS exclusive. No known use, except to keep the API as authentic as possible and not to tip off Snap's backend.

### iOS example:

```
Host: app.snapchat.com
Accept-Locale: en_US
Accept-Encoding: gzip
Accept: */*
Accept-Language: en-us
Connection: keep-alive
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
```

## /loq/suggest_username_v2

This endpoint seems to be used to suggest usernames in the registration section.

### iOS example:

Headers:

```
Accept-Locale: en_US
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Snapchat-UUID: B3A77EC1-AEA2-458E-8775-B6E48520F318
Accept-Encoding: gzip
Accept-Language: en-US;q=1
X-Snapchat-Client-Auth-Token: v8:EB624DDA75B9D4221DC35EE69852A5D3:8BC365C959C252CA0F66C2A1C9A0E539BF2C68C829FDAFB9AA626A8BA2B66997875130827662F2DED724CDE06754DACA2DE2DC1F115DC057470C73FB70DCC5E25D331B0675A94EA98B17F3A7A5E7BEC7600B12282B80A3EF34285D36097E302F9D87E7CD4C0767AE5763DC9C8F863B9B3261C67B7719F6A82436A68D6352F682FD9B8136197740499393EB9393A39E7621E8EB2D1919FB4ACCFA5D1161FD7D17BB3359178E1CF08105B3439584B34B363ADB4B23DD84819D4C89D91C0D51C08A3E9C42EA8427BF43BDAD038DD04E216B3AE72FBA8A5439F1AA5143D66A93751A
Accept: application/json
Content-Length: 133
Connection: keep-alive
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
```

Body:

```
first_name: Snapchat
last_name: Test
req_token: 930a6150aad1fd386edf5cebf5a64ef4b9e94d8d19515a8139b4c314d7c513cb
timestamp: 1517762512144
```

Response:

```
//success:
{"requested_username":"snaptest","suggestions":["snaptest1", "snaptest2", "snaptest3", "snaptest4"]}
//fail:
{"error_message":"snaptest is already taken!","requested_username":"snaptest","suggestions":["snaptest1", "snaptest2", "snaptest3", "snaptest4"]}
```

## /loq/register_v2

This endpoint is used to register a user.

### iOS Example

Headers:

```
Host: app.snapchat.com
Accept-Locale: en_US
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Snapchat-UUID: F27B4634-7D90-4286-A187-3C9948E24E4C
Accept-Encoding: gzip
Accept-Language: en-US;q=1
X-Snapchat-Client-Auth-Token: v8:8EA4360D44572E8305BABE437DC11B5C:E2607C37EE0483EE5036EA1DB81FE2957150EAE0751FF91ED9900D1C85B4438CC47D650EFA66811A68A5A8D2E49AA6C09184E28EC31A9943F00104CB2E8FDBC045E66B26A103149A4002C8DF8868966056CF916F0D98DFB1172C2355C8E93DAA925A924B74533500AE4FACCA02E2FA665ECB72B3F5D273B867EBD1E70A078EBB76D3F86E531FFD1FF7537B4B81535917E12F5F2F0B4C3CB048C47B93E5412E3FFD611A4A053D51B1DB509AA6A266230C56DEF7C940C7E4CF97BC07B250AA49E6B295A487487DF1384625D953BE934EA95A0E01A76A93751A
Accept: application/json
Content-Length: 841
Connection: keep-alive
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
```

Body:
```
birthday	: 1970-01-01
dsig: 8937C32E60239490D6F9
dtoken1i	: 00001:C/BvukRrSriLbpnQyN1EUkZspeN1Hm8Zl9fHUFT7S7qmEaU3x2ujPAZfx+0utKNY
fidelius_client_init: {"new_out_beta":"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEHcKJhBv5xlDa6URejcOqAsX+b1myWwUJY/JOjEst+UEjvxZUHMG89vN9En/1r6GS4gUUa9PEiI39AKuTDEqpiw==","new_hashed_out_beta":"6rxrin9gRqYgOlc5SFPzYToowruejs+sC11ZnY6DqnE=","hashed_out_betas":["6rxrin9gRqYgOlc5SFPzYToowruejs+sC11ZnY6DqnE="],"new_iwek":"AYagnop7NzvmOocc2XRObiDaJgC3rvvcQMpQZN16h9U=","new_fidelius_version":9}
first_name: Snapchat
from_deeplink: false
last_name: Test
password	: [REDACTED]
req_token: 930ae7507a413e686e2826eaf2a4def4aaed4d8e19c26a8a79b44714dcc5145b
study_settings: {}
time_zone: America/New_York
timestamp: 1517764298239
username	: [REDACTED]
```

Response: Check login response Wiki page.

## /bq/get_captcha and /bq/solve_captcha

### /bq/get_captcha

iOS:

headers:

```
Accept: */*
Accept-Locale: en_US
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
Accept-Language: en-US;q=1
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Snapchat-UUID: 9BC2D857-AB43-42C8-9E8A-C48C077B17B7
X-Snapchat-Client-Auth-Token: v8:8D3B280493F1BEC8677915B51633D918:C98BC7B480CCDAB62F4DCA1A12E779ED4A498B6A1E3F7FED0813E6A654C900ADC67A431D664BF9419B84A0B31E26A7363C90A231FAA4B95A405250E185905B391083F3B8E42C2BEF47496BF3976515B7696C44ADE4129112A3B1082E61F56A66B39A9FC13CFA5379A4C48C690F4962DF4C3257AAF1D3245F65D9F1FE8DD8BE5700DE15FAA98326FB0A874A640951549D44469F202BA2A5C8EE750A92913EC888F3E9BD30FF8F2398538804261C33DF80D7D20CA1893E38C00B052478CD48CED23A1B1375E6CCF6DA84150A7BB593E9908654017B5548F31AB2241A09B45A0C15B13DED80AC197C6387D69B4C4F45247E430B349D4DE5D6F20010D2683DA3DCA11BBE599BC96562796A93751A
Connection: keep-alive
From: snapchat@snapchat.com
Content-Length: 120
Accept-Encoding: gzip
```

body:
```
req_token: 2b0d5f35fcc57a63aa9a5dd6f973836bd3c9e85eb470062af2b6e9c295160265
timestamp: 1517764386735
username	: [REDACTED]
```

response:

headers:
```
X-Snapchat-Request-Id: 5a773f2200ff0bea8d5b51ef620001737e6665656c696e736f6e6963652d68726400016d61737465723733383731300001020153
Content-Type: application/zip;charset=utf-8
Cache-Control: no-cache, no-store
X-Snapchat-Notice: Snapchat Private APIs - Unauthorized use is prohibited.
Content-Disposition: attachment;filename=username~1517764387243.zip
X-Captcha-Task-Description: U2VsZWN0IGFsbCBpbWFnZXMgY29udGFpbmluZyBhIGdob3N0Lg==
X-Cloud-Trace-Context: 02461a04210c1c0096186b3732501ea6
Date: Sun, 04 Feb 2018 17:13:07 GMT
Server: Google Frontend
Content-Length: 69157
Alt-Svc: hq=":443"; ma=2592000; quic=51303431; quic=51303339; quic=51303338; quic=51303337; quic=51303335,quic=":443"; ma=2592000; v="41,39,38,37,35"
Connection: Keep-alive
```

body: a gzip of 9 pictures

### /bq/solve_captcha

iOS:

headers:
```
Accept: application/json
Accept-Locale: en_US
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
Accept-Language: en-US;q=1
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Snapchat-UUID: 86D75C6C-F07A-4E27-82B9-681CDA3B4A1C
X-Snapchat-Client-Auth-Token: v8:B755DF4BE2EBE5657DB0335B478F93C5:50FD52ADCF2A776102A0B44FC00B96A428F7CB75CC56C913214B0644135313CE73A31BEB007047F809A56D032F426DAD3020AF9BE384886DE793E4CCA164FBA46C7269DAE63FEF935B0C8C122342A2E7E75C847C2516D2BE156135CFF1C6AEED9EDE14752495128B5CFFDBF98D9839EB9801560D0C7EFA6EA21127D89DA350D2031BA6C1C4F6F7F1BB5DE638B3792795E4B6A5FA3903A0F45A401048E583A9FB8C0AFA84041129EF3C369FF55F258AE18D30BE7EC66A1D88A6262C09B83034A74DEDE772C7CDDB7BDCB5F141A9F48A4D865B37A80BAF27C8C5787416D1F8487D13F2CEBFEB5AE6C3F69797E5744E104C1D6229F31445B39D0536E28064D002E3498F4DD3515BBD76275460F66A93751A
Connection: keep-alive
From: snapchat@snapchat.com
Content-Length: 185
Accept-Encoding: gzip
```

body:
```
captcha_id: [the filename from get_captcha]
captcha_solution: [011101110] 3x3, as in 0 for not a ghost and 1 for ghost. row then next row etc...
req_token: request token
timestamp: timestamp
username: username
```

response:
```
{"find_friends_enabled":true,"is_reset_password":false}
```

## https://auth.snapchat.com/scauth/login

This is the endpoint used to login to Snapchat.

### iOS

Headers:
```
X-Snapchat-Client-Token: v8:0B09C33E534EEEB79966B3B9CF5A6E3D:79D593A546295A3BEE50CAB13DDC4303A96A6F0328D4FA495CECE3B6783D4C21E085C727BFFCCD4A7AA8B9237D7BBB5A5F39D0EA2E26A9825C3A954691C656D18FF8C069C905101B760FC741C773EEA2E119C69C5BF524DBBF36110258C9DE4F6533BF89973E2749BDA6641BF1B199F27CC031F2D03037986F3105368A7C623AD7F3351871EDC7E43679B7237E08B917F366C79D995823A7110805CA5EF19AD851A66A5FAB00174F6A93751A
Accept-Locale: en_US
Accept: application/json
User-Agent: Snapchat/10.24.5.3 (iPhone5,3; iOS 10.3.3; gzip)
Accept-Language: en-US;q=1
Content-Type: application/x-www-form-urlencoded; charset=utf-8
X-Snapchat-UUID: A3191A2A-07EE-4F3E-849D-534B5CFAA03C
X-Snapchat-Client-Auth-Token: v8:38EA8947246505967D231DF2394951C8:4C8CB2CD74FE49CA6EBB855ADA921FF0AFA309BFF007A772EFE59C66238ED4AE14BF7D968A80D175EBA0B7AE06062F3564C05E8ADAF49F6FD2A7DEA3B9537772DCA0E6122FA71CB19682F0248EDFCE316EB1CF480A3479D862CD8A3974646372FFD267B89FFEF2873AA21567F46143B1BC0B39AA00D3C605C8650D53329716F583EA769195079AE17084E1204FDD26E125F8AFFD0F3F887A350A6F6566DAF3332C13A5986A91326997C32BEDE34AF3896CFC9A11A73FAFD9F0C9A565AF70A62FE09B529A89E667F29CD80ABCC944717213779709A4C13FD989C5F7586A93751A
Connection: keep-alive
Content-Length: 960
Accept-Encoding: gzip
```

more data to come