---
title: BSV ARC v1.0.0
language_tabs:
  - http: HTTP
  - javascript: JavaScript
  - java: Java
  - go: Go
  - ruby: Ruby
  - python: Python
  - shell: curl
language_clients:
  - http: ""
  - javascript: ""
  - java: ""
  - go: ""
  - ruby: ""
  - python: ""
  - shell: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="bsv-arc">BSV ARC v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

License: <a href="https://bitcoinassociation.net/open-bsv-license/">Open BSV Licence</a>

# Authentication

- HTTP Authentication, scheme: bearer Bearer authentication as defined in RFC 6750

* API Key (Api-Key)
    - Parameter Name: **Api-Key**, in: header. Please enter API key needed to access endpoints into field. Api-Key: My_API_Key

* API Key (Authorization)
    - Parameter Name: **Authorization**, in: header. Please enter the custom authorization needed to access endpoints into field. Authorization: My_Authorization_Key

<h1 id="bsv-arc-arc">Arc</h1>

## Get the policy settings

<a id="opIdGET policy"></a>

> Code samples

```http
GET /v1/policy HTTP/1.1

Accept: application/json

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('/v1/policy',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```java
URL obj = new URL("/v1/policy");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/v1/policy", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get '/v1/policy',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('/v1/policy', headers = headers)

print(r.json())

```

```shell
# You can also use wget
curl -X GET /v1/policy \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

`GET /v1/policy`

This endpoint returns the policy settings.

> Example responses

> 200 Response

```json
{
  "timestamp": "2019-08-24T14:15:22Z",
  "policy": {
    "maxscriptsizepolicy": 500000,
    "maxtxsigopscountspolicy": 4294967295,
    "maxtxsizepolicy": 10000000,
    "miningFee": {
      "satoshis": 50,
      "bytes": 1000
    }
  }
}
```

<h3 id="get-the-policy-settings-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[PolicyResponse](#schemapolicyresponse)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Security requirements failed|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
BearerAuth, Api-Key, Authorization
</aside>

## Get transaction status.

<a id="opIdGET transaction status"></a>

> Code samples

```http
GET /v1/tx/{txid} HTTP/1.1

Accept: application/json

```

```javascript

const headers = {
  'Accept':'application/json',
  'Authorization':'Bearer {access-token}'
};

fetch('/v1/tx/{txid}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```java
URL obj = new URL("/v1/tx/{txid}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/v1/tx/{txid}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.get '/v1/tx/{txid}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'Bearer {access-token}'
}

r = requests.get('/v1/tx/{txid}', headers = headers)

print(r.json())

```

```shell
# You can also use wget
curl -X GET /v1/tx/{txid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

`GET /v1/tx/{txid}`

This endpoint is used to get the current status of a previously submitted transaction.

<h3 id="get-transaction-status.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|txid|path|string|true|The transaction ID (32 byte hash) hex string|

> Example responses

> 200 Response

```json
{
  "timestamp": "2019-08-24T14:15:22Z",
  "blockHash": "00000000000000000854749b3c125d52c6943677544c8a6a885247935ba8d17d",
  "blockHeight": 782318,
  "txid": "7927233d10dacd5606cee5bf0b28668fc191e730029ace4c7fc40ede59a2825e",
  "txStatus": "MINED",
  "extraInfo": null
}
```

<h3 id="get-transaction-status.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[TransactionStatus](#schematransactionstatus)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Security requirements failed|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not found|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
BearerAuth, Api-Key, Authorization
</aside>

## Submit a transaction.

<a id="opIdPOST transaction"></a>

> Code samples

```http
POST /v1/tx HTTP/1.1

Content-Type: text/plain
Accept: application/json
X-CallbackUrl: string
X-CallbackToken: string
X-MerkleProof: string
X-WaitForStatus: 0

```

```javascript
const inputBody = '<transaction hex string>';
const headers = {
  'Content-Type':'text/plain',
  'Accept':'application/json',
  'X-CallbackUrl':'string',
  'X-CallbackToken':'string',
  'X-MerkleProof':'string',
  'X-WaitForStatus':'0',
  'Authorization':'Bearer {access-token}'
};

fetch('/v1/tx',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```java
URL obj = new URL("/v1/tx");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"text/plain"},
        "Accept": []string{"application/json"},
        "X-CallbackUrl": []string{"string"},
        "X-CallbackToken": []string{"string"},
        "X-MerkleProof": []string{"string"},
        "X-WaitForStatus": []string{"0"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "/v1/tx", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'text/plain',
  'Accept' => 'application/json',
  'X-CallbackUrl' => 'string',
  'X-CallbackToken' => 'string',
  'X-MerkleProof' => 'string',
  'X-WaitForStatus' => '0',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post '/v1/tx',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'text/plain',
  'Accept': 'application/json',
  'X-CallbackUrl': 'string',
  'X-CallbackToken': 'string',
  'X-MerkleProof': 'string',
  'X-WaitForStatus': '0',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('/v1/tx', headers = headers)

print(r.json())

```

```shell
# You can also use wget
curl -X POST /v1/tx \
  -H 'Content-Type: text/plain' \
  -H 'Accept: application/json' \
  -H 'X-CallbackUrl: string' \
  -H 'X-CallbackToken: string' \
  -H 'X-MerkleProof: string' \
  -H 'X-WaitForStatus: 0' \
  -H 'Authorization: Bearer {access-token}'

```

`POST /v1/tx`

This endpoint is used to send a raw transaction to a miner for inclusion in the next block that the miner creates.  The header parameters can be used to override the global settings in your Arc dashboard for these transactions.

> Body parameter

```json
"<transaction hex string>"
```

```
<transaction hex string>

```

```yaml
<transaction hex string>

```

<h3 id="submit-a-transaction.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-CallbackUrl|header|string|false|Default double spend and merkle proof notification callback endpoint.|
|X-CallbackToken|header|string|false|Access token for notification callback endpoint.|
|X-MerkleProof|header|string|false|Whether to include merkle proofs in the callbacks (true | false).|
|X-WaitForStatus|header|integer|false|Which status to wait for from the server before returning (2 = RECEIVED, 3 = STORED, 4 = ANNOUNCED_TO_NETWORK, 5 = REQUESTED_BY_NETWORK, 6 = SENT_TO_NETWORK, 7 = ACCEPTED_BY_NETWORK, 8 = SEEN_ON_NETWORK)|
|body|body|string|false|none|

> Example responses

> Success

```json
{
  "blockHash": "0000000000000000000c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6",
  "blockHeight": 736228,
  "extraInfo": "",
  "status": 200,
  "timestamp": "2023-03-09T12:03:48.382910514Z",
  "title": "OK",
  "txStatus": "MINED",
  "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
}
```

```json
{
  "blockHash": "",
  "blockHeight": 0,
  "extraInfo": "",
  "status": 200,
  "timestamp": "2023-03-09T12:03:48.382910514Z",
  "title": "OK",
  "txStatus": "SEEN_ON_NETWORK",
  "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
}
```

> 400 Response

```json
{
  "type": "https://arc.bitcoinsv.com/errors/400",
  "title": "Bad request",
  "status": 400,
  "detail": "The request seems to be malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/1234556",
  "txid": "string",
  "extraInfo": "string"
}
```

<h3 id="submit-a-transaction.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[TransactionResponse](#schematransactionresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad request|[ErrorBadRequest](#schemaerrorbadrequest)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Security requirements failed|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|Unprocessable entity - with IETF RFC 7807 Error object|[Error](#schemaerror)|
|465|Unknown|Fee too low|[ErrorFee](#schemaerrorfee)|
|466|Unknown|Conflicting transaction found|[ErrorConflict](#schemaerrorconflict)|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
BearerAuth, Api-Key, Authorization
</aside>

## Submit multiple transactions.

<a id="opIdPOST transactions"></a>

> Code samples

```http
POST /v1/txs HTTP/1.1

Content-Type: text/plain
Accept: application/json
X-CallbackUrl: string
X-CallbackToken: string
X-MerkleProof: string
X-WaitForStatus: 0

```

```javascript
const inputBody = '<transaction hex string>
<transaction hex string>';
const headers = {
  'Content-Type':'text/plain',
  'Accept':'application/json',
  'X-CallbackUrl':'string',
  'X-CallbackToken':'string',
  'X-MerkleProof':'string',
  'X-WaitForStatus':'0',
  'Authorization':'Bearer {access-token}'
};

fetch('/v1/txs',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```java
URL obj = new URL("/v1/txs");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"text/plain"},
        "Accept": []string{"application/json"},
        "X-CallbackUrl": []string{"string"},
        "X-CallbackToken": []string{"string"},
        "X-MerkleProof": []string{"string"},
        "X-WaitForStatus": []string{"0"},
        "Authorization": []string{"Bearer {access-token}"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "/v1/txs", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'text/plain',
  'Accept' => 'application/json',
  'X-CallbackUrl' => 'string',
  'X-CallbackToken' => 'string',
  'X-MerkleProof' => 'string',
  'X-WaitForStatus' => '0',
  'Authorization' => 'Bearer {access-token}'
}

result = RestClient.post '/v1/txs',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'text/plain',
  'Accept': 'application/json',
  'X-CallbackUrl': 'string',
  'X-CallbackToken': 'string',
  'X-MerkleProof': 'string',
  'X-WaitForStatus': '0',
  'Authorization': 'Bearer {access-token}'
}

r = requests.post('/v1/txs', headers = headers)

print(r.json())

```

```shell
# You can also use wget
curl -X POST /v1/txs \
  -H 'Content-Type: text/plain' \
  -H 'Accept: application/json' \
  -H 'X-CallbackUrl: string' \
  -H 'X-CallbackToken: string' \
  -H 'X-MerkleProof: string' \
  -H 'X-WaitForStatus: 0' \
  -H 'Authorization: Bearer {access-token}'

```

`POST /v1/txs`

This endpoint is used to send multiple raw transactions to a miner for inclusion in the next block that the miner creates. The header parameters can be used to override the global settings in your Arc dashboard for these transactions.

> Body parameter

```json
"<transaction hex string>\n<transaction hex string>"
```

```
|-
<transaction hex string>
<transaction hex string>

```

```yaml
|-
<transaction hex string>
<transaction hex string>

```

<h3 id="submit-multiple-transactions.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|X-CallbackUrl|header|string|false|Default double spend and merkle proof notification callback endpoint.|
|X-CallbackToken|header|string|false|Access token for notification callback endpoint.|
|X-MerkleProof|header|string|false|Whether to include merkle proofs in the callbacks (true | false).|
|X-WaitForStatus|header|integer|false|Which status to wait for from the server before returning (2 = RECEIVED, 3 = STORED, 4 = ANNOUNCED_TO_NETWORK, 5 = REQUESTED_BY_NETWORK, 6 = SENT_TO_NETWORK, 7 = ACCEPTED_BY_NETWORK, 8 = SEEN_ON_NETWORK)|
|body|body|string|false|none|

> Example responses

> Already in block template, or already mined

```json
[
  {
    "blockHash": "000000000000000001d8f4bb24dd93d4e91ce926cc7a971be018c2b8d46d45ff",
    "blockHeight": 761868,
    "extraInfo": "",
    "status": 200,
    "timestamp": "2023-03-09T12:03:48.382910514Z",
    "title": "OK",
    "txStatus": "MINED",
    "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
  }
]
```

```json
[
  {
    "blockHash": "",
    "blockHeight": 0,
    "extraInfo": "",
    "status": 200,
    "timestamp": "2023-03-09T12:03:48.382910514Z",
    "title": "OK",
    "txStatus": "SEEN_ON_NETWORK",
    "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
  }
]
```

```json
[
  {
    "detail": "Transaction is invalid because the outputs are non-existent or invalid",
    "extraInfo": "arc error 463: arc error 463: transaction output 0 satoshis is invalid",
    "instance": null,
    "status": 463,
    "title": "Invalid outputs",
    "txid": "a0d69a2dfad710770ed282cce316c5792f6101a68046a263a17a1ae02676015e",
    "type": "https://arc.bitcoinsv.com/errors/463"
  }
]
```

> 400 Response

```json
{
  "type": "https://arc.bitcoinsv.com/errors/400",
  "title": "Bad request",
  "status": 400,
  "detail": "The request seems to be malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/1234556"
}
```

<h3 id="submit-multiple-transactions.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Already in block template, or already mined|[TransactionResponses](#schematransactionresponses)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|IETF RFC 7807 Error object|[ErrorBadRequest](#schemaerrorbadrequest)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Security requirements failed|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
BearerAuth, Api-Key, Authorization
</aside>

# Schemas

<h2 id="tocS_CommonResponse">CommonResponse</h2>
<!-- backwards compatibility -->
<a id="schemacommonresponse"></a>
<a id="schema_CommonResponse"></a>
<a id="tocScommonresponse"></a>
<a id="tocscommonresponse"></a>

```json
{
  "timestamp": "2019-08-24T14:15:22Z"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|timestamp|string(date-time)|true|none|none|

<h2 id="tocS_ChainInfo">ChainInfo</h2>
<!-- backwards compatibility -->
<a id="schemachaininfo"></a>
<a id="schema_ChainInfo"></a>
<a id="tocSchaininfo"></a>
<a id="tocschaininfo"></a>

```json
{
  "blockHash": "00000000000000000854749b3c125d52c6943677544c8a6a885247935ba8d17d",
  "blockHeight": 782318
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|blockHash|string|false|none|none|
|blockHeight|integer(uint64)|false|none|none|

<h2 id="tocS_PolicyResponse">PolicyResponse</h2>
<!-- backwards compatibility -->
<a id="schemapolicyresponse"></a>
<a id="schema_PolicyResponse"></a>
<a id="tocSpolicyresponse"></a>
<a id="tocspolicyresponse"></a>

```json
{
  "timestamp": "2019-08-24T14:15:22Z",
  "policy": {
    "maxscriptsizepolicy": 500000,
    "maxtxsigopscountspolicy": 4294967295,
    "maxtxsizepolicy": 10000000,
    "miningFee": {
      "satoshis": 50,
      "bytes": 1000
    }
  }
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[CommonResponse](#schemacommonresponse)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» policy|[Policy](#schemapolicy)|true|none|none|

<h2 id="tocS_Policy">Policy</h2>
<!-- backwards compatibility -->
<a id="schemapolicy"></a>
<a id="schema_Policy"></a>
<a id="tocSpolicy"></a>
<a id="tocspolicy"></a>

```json
{
  "maxscriptsizepolicy": 500000,
  "maxtxsigopscountspolicy": 4294967295,
  "maxtxsizepolicy": 10000000,
  "miningFee": {
    "satoshis": 50,
    "bytes": 1000
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|maxscriptsizepolicy|integer(uint64)|true|none|none|
|maxtxsigopscountspolicy|integer(uint64)|true|none|none|
|maxtxsizepolicy|integer(uint64)|true|none|none|
|miningFee|[FeeAmount](#schemafeeamount)|true|none|none|

<h2 id="tocS_FeeAmount">FeeAmount</h2>
<!-- backwards compatibility -->
<a id="schemafeeamount"></a>
<a id="schema_FeeAmount"></a>
<a id="tocSfeeamount"></a>
<a id="tocsfeeamount"></a>

```json
{
  "satoshis": 0,
  "bytes": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|satoshis|integer(uint64)|true|none|none|
|bytes|integer(uint64)|true|none|none|

<h2 id="tocS_TransactionRequest">TransactionRequest</h2>
<!-- backwards compatibility -->
<a id="schematransactionrequest"></a>
<a id="schema_TransactionRequest"></a>
<a id="tocStransactionrequest"></a>
<a id="tocstransactionrequest"></a>

```json
{
  "rawTx": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rawTx|string|true|none|none|

<h2 id="tocS_TransactionResponse">TransactionResponse</h2>
<!-- backwards compatibility -->
<a id="schematransactionresponse"></a>
<a id="schema_TransactionResponse"></a>
<a id="tocStransactionresponse"></a>
<a id="tocstransactionresponse"></a>

```json
{
  "timestamp": "2023-03-09T12:03:48.382910514Z",
  "blockHash": "",
  "blockHeight": 0,
  "status": 200,
  "title": "OK",
  "extraInfo": "string",
  "txStatus": "string",
  "txid": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[CommonResponse](#schemacommonresponse)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ChainInfo](#schemachaininfo)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TransactionDetails](#schematransactiondetails)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» txid|string|true|none|none|
|» txStatus|string|true|none|none|
|» extraInfo|string¦null|true|none|none|

<h2 id="tocS_TransactionStatus">TransactionStatus</h2>
<!-- backwards compatibility -->
<a id="schematransactionstatus"></a>
<a id="schema_TransactionStatus"></a>
<a id="tocStransactionstatus"></a>
<a id="tocstransactionstatus"></a>

```json
{
  "timestamp": "2019-08-24T14:15:22Z",
  "blockHash": "00000000000000000854749b3c125d52c6943677544c8a6a885247935ba8d17d",
  "blockHeight": 782318,
  "txid": "7927233d10dacd5606cee5bf0b28668fc191e730029ace4c7fc40ede59a2825e",
  "txStatus": "MINED",
  "extraInfo": null
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[CommonResponse](#schemacommonresponse)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ChainInfo](#schemachaininfo)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» txid|string|true|none|none|
|» txStatus|string|false|none|none|
|» extraInfo|string¦null|false|none|none|

<h2 id="tocS_TransactionResponses">TransactionResponses</h2>
<!-- backwards compatibility -->
<a id="schematransactionresponses"></a>
<a id="schema_TransactionResponses"></a>
<a id="tocStransactionresponses"></a>
<a id="tocstransactionresponses"></a>

```json
{
  "timestamp": "2019-08-24T14:15:22Z",
  "blockHash": "00000000000000000854749b3c125d52c6943677544c8a6a885247935ba8d17d",
  "blockHeight": 782318,
  "transactions": [
    {
      "status": 200,
      "title": "OK",
      "blockHash": "",
      "blockHeight": 0,
      "extraInfo": "",
      "timestamp": "2023-03-09T12:03:48.382910514Z",
      "txStatus": "SEEN_ON_NETWORK",
      "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
    }
  ]
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[CommonResponse](#schemacommonresponse)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ChainInfo](#schemachaininfo)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» transactions|[oneOf]|false|none|none|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»» *anonymous*|[TransactionDetails](#schematransactiondetails)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»» *anonymous*|[Error](#schemaerror)|false|none|An HTTP Problem Details object, as defined in IETF RFC 7807 (https://tools.ietf.org/html/rfc7807).|

<h2 id="tocS_TransactionSubmitStatus">TransactionSubmitStatus</h2>
<!-- backwards compatibility -->
<a id="schematransactionsubmitstatus"></a>
<a id="schema_TransactionSubmitStatus"></a>
<a id="tocStransactionsubmitstatus"></a>
<a id="tocstransactionsubmitstatus"></a>

```json
{
  "status": 201,
  "title": "Added to mempool"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|integer(int)|true|none|none|
|title|string|true|none|none|

<h2 id="tocS_TransactionDetails">TransactionDetails</h2>
<!-- backwards compatibility -->
<a id="schematransactiondetails"></a>
<a id="schema_TransactionDetails"></a>
<a id="tocStransactiondetails"></a>
<a id="tocstransactiondetails"></a>

```json
{
  "status": 200,
  "title": "OK",
  "blockHash": "",
  "blockHeight": 0,
  "extraInfo": "",
  "timestamp": "2023-03-09T12:03:48.382910514Z",
  "txStatus": "SEEN_ON_NETWORK",
  "txid": "c0d6fce714e4225614f000c6a5addaaa1341acbb9c87115114dcf84f37b945a6"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[TransactionSubmitStatus](#schematransactionsubmitstatus)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» txid|string|false|none|Transaction ID in hex|
|» txStatus|string|false|none|Transaction status|
|» extraInfo|string¦null|false|none|Extra information about the transaction|

#### Enumerated Values

|Property|Value|
|---|---|
|txStatus|UNKNOWN|
|txStatus|RECEIVED|
|txStatus|STORED|
|txStatus|ANNOUNCED_TO_NETWORK|
|txStatus|REQUESTED_BY_NETWORK|
|txStatus|SENT_TO_NETWORK|
|txStatus|SEEN_ON_NETWORK|
|txStatus|MINED|
|txStatus|CONFIRMED|
|txStatus|REJECTED|

<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/461",
  "title": "Malformed transaction",
  "status": 461,
  "detail": "Transaction is malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

An HTTP Problem Details object, as defined in IETF RFC 7807 (https://tools.ietf.org/html/rfc7807).

### Properties

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorUnlockingScripts](#schemaerrorunlockingscripts)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorInputs](#schemaerrorinputs)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorMalformed](#schemaerrormalformed)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFrozenPolicy](#schemaerrorfrozenpolicy)|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFrozenConsensus](#schemaerrorfrozenconsensus)|false|none|none|

<h2 id="tocS_ErrorBadRequest">ErrorBadRequest</h2>
<!-- backwards compatibility -->
<a id="schemaerrorbadrequest"></a>
<a id="schema_ErrorBadRequest"></a>
<a id="tocSerrorbadrequest"></a>
<a id="tocserrorbadrequest"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/400",
  "title": "Bad request",
  "status": 400,
  "detail": "The request seems to be malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/1234556",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorFee">ErrorFee</h2>
<!-- backwards compatibility -->
<a id="schemaerrorfee"></a>
<a id="schema_ErrorFee"></a>
<a id="tocSerrorfee"></a>
<a id="tocserrorfee"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/402",
  "title": "Fee too low",
  "status": 465,
  "detail": "The fees are too low",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorConflict">ErrorConflict</h2>
<!-- backwards compatibility -->
<a id="schemaerrorconflict"></a>
<a id="schema_ErrorConflict"></a>
<a id="tocSerrorconflict"></a>
<a id="tocserrorconflict"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/409",
  "title": "Conflicting tx found",
  "status": 466,
  "detail": "Transaction is valid, but there is a conflicting tx in the block template",
  "instance": "https://arc.taal.com/errors/123453",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorUnlockingScripts">ErrorUnlockingScripts</h2>
<!-- backwards compatibility -->
<a id="schemaerrorunlockingscripts"></a>
<a id="schema_ErrorUnlockingScripts"></a>
<a id="tocSerrorunlockingscripts"></a>
<a id="tocserrorunlockingscripts"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/461",
  "title": "Malformed transaction",
  "status": 461,
  "detail": "Transaction is malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorInputs">ErrorInputs</h2>
<!-- backwards compatibility -->
<a id="schemaerrorinputs"></a>
<a id="schema_ErrorInputs"></a>
<a id="tocSerrorinputs"></a>
<a id="tocserrorinputs"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/462",
  "title": "Invalid inputs",
  "status": 462,
  "detail": "Transaction is invalid because the inputs are non-existent or spent",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorMalformed">ErrorMalformed</h2>
<!-- backwards compatibility -->
<a id="schemaerrormalformed"></a>
<a id="schema_ErrorMalformed"></a>
<a id="tocSerrormalformed"></a>
<a id="tocserrormalformed"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/463",
  "title": "Malformed transaction",
  "status": 463,
  "detail": "Transaction is malformed and cannot be processed",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorFrozenPolicy">ErrorFrozenPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaerrorfrozenpolicy"></a>
<a id="schema_ErrorFrozenPolicy"></a>
<a id="tocSerrorfrozenpolicy"></a>
<a id="tocserrorfrozenpolicy"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/471",
  "title": "Input Frozen",
  "status": 471,
  "detail": "Input Frozen (blacklist manager policy blacklisted)",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorFrozenConsensus">ErrorFrozenConsensus</h2>
<!-- backwards compatibility -->
<a id="schemaerrorfrozenconsensus"></a>
<a id="schema_ErrorFrozenConsensus"></a>
<a id="tocSerrorfrozenconsensus"></a>
<a id="tocserrorfrozenconsensus"></a>

```json
{
  "type": "https://arc.bitcoinsv.com/errors/472",
  "title": "Input Frozen",
  "status": 472,
  "detail": "Input Frozen (blacklist manager consensus blacklisted)",
  "instance": "https://arc.taal.com/errors/123452",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ErrorFields](#schemaerrorfields)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» type|any|false|none|none|
|» title|any|false|none|none|
|» status|any|false|none|none|
|» detail|any|false|none|none|
|» instance|any|false|none|none|

<h2 id="tocS_ErrorFields">ErrorFields</h2>
<!-- backwards compatibility -->
<a id="schemaerrorfields"></a>
<a id="schema_ErrorFields"></a>
<a id="tocSerrorfields"></a>
<a id="tocserrorfields"></a>

```json
{
  "type": "string",
  "title": "string",
  "status": 402,
  "detail": "The fee in the transaction is too low to be included in a block.",
  "instance": "string",
  "txid": "string",
  "extraInfo": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|true|none|Type of error, with link to more information|
|title|string|true|none|Descriptive text for error|
|status|integer(int)|true|none|Error code|
|detail|string|true|none|Longer description of error|
|instance|string¦null|false|none|(Optional) Link to actual error on server|
|txid|string¦null|false|none|Transaction ID this error is referring to|
|extraInfo|string¦null|false|none|Optional extra information about the error from the miner|
