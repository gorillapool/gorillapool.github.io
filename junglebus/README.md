# JungleBus

> Data for Bitcoin applications

JungleBus is an indexer that indexes all the transactions on the Bitcoin blockchain. All transactions are parsed
and processed into a database, with special indexes created for data transactions.

## Subscriptions

Subscriptions are the main way to get data out of JungleBus into your own secondary indexer. You can create a subscription
in the JungleBus UI at https://junglebus.gorillapool.io.

When creating a subscription, you can specify what data to filter from the database, by specifying keywords on the data
fields that have been indexed.

|              | Description                                                                                                                |
| ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Addresses    | Comma seperated list of Bitcoin addresses to search for                                                                    |
| Output Types | Data output types that have been recognized by JungleBus<br/>example: `pubkeyhash`, `nulldata`, `map`, `aip`, `run`, `bap` |
| Contexts     | The main data of the transaction output type                                                                               |
| Sub contexts | The secondary data of the transaction output type                                                                          |
| Data keys    | Key value list of other data found in the transaction (example `app=junglebus`)                                            |

JungleBus tries to get as much data from the transactions as possible. If your transactions are not using a standard
format, the best way to see how your transaction is parsed is to request an example transaction from the API endpoint
and infer from there what you want to filter on.

https://junglebus.gorillapool.io/v1/transaction/get/[transaction_id]

## Addresses

Per-transaction aggregation of all addresses found across inputs, outputs, and data references.

## Output Types

`“aip”, “b”, “bap”, “bitcom”, “map”, “run”`

#### Contexts

Up to 255 characters. Derived from data after the OP_RETURN. Value is populated according to protocols found.

## SUPPORTED PROTOCOLS

### 1Sat Outputs

Embedded prefix: N/A

Output Value: 1 satoshi

Output Type: `"1sat"`

Context: none

Subcontext: none

Data: none

### 1Sat Ordinals (Inscriptions)

Embedded prefix: `ord`

Output Type: `"ord"`

Context: `content-type`

Sample Context Value: `text/plain;charset=utf8`

Subcontext: none

Data: none

### AIP Protocol

Bitcom Prefix: `15PciHG22SNLQJXMoSUaWVi7WSqc7hCfva`

Output Type: `“aip”`

Context: `none`

Subcontext: `none`

Populates Addresses

More Info: [AIP docs](https://github.com/attilaaf/AUTHOR_IDENTITY_PROTOCOL)

### B Protocol

Bitcom Prefix: `19HxigV4QyBv3tHpQVcUEQyq1pzZVdoAut`

Output Type: `“b”`

Context: `media type`

Sample Context Value: `“image/png”`

Subcontext: none

Data: `[“encoding=<encoding>”, ”filename=<somefilename>”]`

### BAP Protocol

Bitcoin Attestation Protocol
Bitcom Prefix: `1BAPSuaPnfGnSBM3GLV9yhxUdYe4vGbdMT`

Context: `idKey`

Subcontext: type, eg `“ATTEST”`

Data: `[“sequence=<seq>”, “hash=<urnHash>”]`

Populates Addresses

More info: [BAP Docs](https://github.com/icellan/bap)

### Boost Protocol

Boost POW
Embededed prefix: "boostpow"

Context: Content

Subcontext: Topic

Data: none

More Info: [pow.co](https://pow.co)

### Bitcom

Bitcom is a scheme for defining your own protocol and registering it online. Jungle Bus will tag the “bitcom” output type whenever OP_RETURN data begins with a valid Bitcoin address as a protocol prefix.

Protocol Prefix: `$`

Output Type: `“bitcom”`

Context: `<Bitcom Protocol Prefix>`

Sample Context Value: `“17yyXL4raLZFU95ixkRESa2ZBPSSYxSsS5”`

Subcontext: none

More info: [Bitcom Site](https://bitcom.bitdb.network/)

### MAP Protocol

Magic Attribute Protocol
Bitcom Prefix: `1PuQa7K62MiKCtssSLKy1kh56WWU7MtUR5`

Output Type: `“map”`
Context: `“MAP.app”` value

Sample value: `“jamify.xyz”`

Data: `[“key=val”, “key=val1,val2,val3”]`

More Info: [MAP Docs](https://github.com/rohenaz/map)

### Run Protocol

Protocol Prefix: `“run”`

Output Type: `“run”`

More Info: [Run Github](https://github.com/runonbitcoin)

### Data format

The transactions published by the JungleBus on subscriptions is limited, compared to the API endpoint. The idea here is
that you only really need the information that is published to populate your own indexer with data.

```json
{
    "id": "e597af34eb78b599b7d458110a3cc602a40dedd020db684992b40926217612a4",
    "block_hash": "000000000000000006296f1e5437dd6c01b9b5471691a89a9c7d8e9f06920da5",
    "block_height": 750000,
    "block_index": 3,
    "block_time": 1658878267,
    "transaction": "010000000215c06fc0a41be7e62ed82173745d0aea194246fbe5ac78491b6a6c9545f61ce7010000006b483045022100c133da9c8e5fc2c519720de92f0b22c933503a54dac48c55acdccde9300e0a0e02201d665d3e3a713bac5a1d4019f9354f848bbd3b5a1c57ea0c4d2c90ce168fcd0c41210312ac92d0030cd2acb56de3edd2c98bf5a31cbcb39010a1570d1db838c8c42f63ffffffff4b32816b3b1f258ad77031576eb6dd76d2400bc3c39814f4953a5416ea8ae96b010000006b483045022100f46fb07614a9e5ae9dac36b38679d740feb1d3ae740634fe90dad8de7126547902207b56d9a8eb85bc9a0b00c8b7f4a646e17d7b74e338c6b5389ac4e6ce448454b041210312ac92d0030cd2acb56de3edd2c98bf5a31cbcb39010a1570d1db838c8c42f63ffffffff030000000000000000fd2b02006a0372756e01050c63727970746f6669676874734d13027b22696e223a322c22726566223a5b22653636626630653338646162376336343632363161633639623966373634316132303262303161653732323563643265316265663231363662643665616264335f6f31222c22353535616164313935336263666566386337373739643234366661303365666165303431326564373030623935353433353833313831346635626533613832625f6f31222c22656364386235363537646530333164613031653862663438383038663034666437396435323563323130323163306130333338656163636366363063346537665f6f31222c22633263346339373165383562343939633239613861623231343866643332346665313262353530623866346635373635386134363836653031316438666435385f6f31225d2c226f7574223a5b2232653732396433396139636433303066353130303034346135343230346536643862343366653439353535333039333631666463336438353635333233343939225d2c2264656c223a5b2264666138373032373335313464356438313563643636613537396462363138666338313339626631383135643264663439643536353039303562393738316138225d2c22637265223a5b5d2c2265786563223a5b7b226f70223a2243414c4c222c2264617461223a5b7b22246a6967223a307d2c227265636f7264426174746c65222c5b7b22246a6967223a317d2c747275655d5d7d5d7d11010000000000001976a914f28c3992dd6a43eccaed16f3f7fb6ac8da1bc3c288ace1000000000000001976a9144f7d6a485e09770f947c0ba38d15050a5a80b6fa88ac00000000",
    "merkle_proof": "0003a41276212609b4924968db20d0ed0da402c63c0a1158d4b799b578eb34af97e5d2765ce19ad0dcb0279db6b0e2d87ef9b69b27a52532776984b510ea44abc9d50e00c4c7db0d9f71deb09c9cf5f3e29dcfa8493ec5ce6dcc33a19066dbbb99889a2f00be8290c1d96da9f70c3246e0166123c711680298d68a451a30c49a3a6d897c7c00b7aa26d1cff8d56e14ff1e4b44763a346bdcb509033ac6196d36a292b620e5d900298859ef5057a279ceec3578761076723f7c768b37f11eb66d6012fb58fd8f1400aba977079a84deec41809d45263c8978a4c5138355b341f2581da1c14458a19f005a61f3c9e73ab5dd6375222d4c350d2ecd153fb9d84df32568c2d366c39b222e000332bfa9ca6044c4cf1958b68dc8c7737ebd4ffa7dac9c294e31b0f0a3f7230500141fd014488088a108a50007fb75b1bc53486264ab6006db72a51a6e804860070013f67f63b807907275374ddedc7ff3e93966d7cc567e63cc0ba3c7fc8351e798007d8c5941dad2a05623cca69b764a63e8f1d5d1a10d6878dcfe66871c373d184100b36bec9c2537a060f6e39fa4faf99e784471aa4f506aa42049d7f59cb671442f0053ac83051443711a77011504a5986f11ce58c7c9b7578e82d77f7f9a66221480004a91dbc6d466396c8a6183d0dc5732e86fcb5d3280c504239f1566e1703f376c0052574e2bc236a0f43577f7b8bafb795ded0fae5a96c24171398af61701fc28bd"
}
```

| Field        | Description                                                            |
| ------------ | ---------------------------------------------------------------------- |
| id           | The ID of the transaction                                              |
| block_hash   | The hex hash of the block this transaction was mined into              |
| block_height | The height of the block this transaction was mined into                |
| block_index  | The index (position) of the transaction in the block it was mined into |
| transaction  | Full transaction in hex                                                |
| merkle_proof | TSC compatible binary merkle proof of the transaction in hex           |

### Control messages

JungleBus sends messages on a separate channel to indicate status, errors, etc. on the active subscriptions.

The control messages have the following structure:

```json
{
    "status_code": 200,
    "status": "block-done",
    "message": "Block 1233 done with 2 transactions",
    "block": 1233,
    "transactions": 2
}
```

The possible status codes that can be sent back are:

| Code | Action             | Description                                                       |
| ---- | ------------------ | ----------------------------------------------------------------- |
| 1    | connecting         | Sent when connecting to the JungleBus server                      |
| 2    | connected          | Sent when connected to the JungleBus server                       |
| 10   | disconnecting      | Sent when disconnecting from the JungleBus server                 |
| 11   | disconnected       | Sent when disconnected from the JungleBus server                  |
| 20   | subscribing        | Sent when subscribing on a subscription on the JungleBus server   |
| 21   | subscribed         | Sent when subscribed on a subscription on the JungleBus server    |
| 29   | unsubscribed       | Sent when unsubscribed on a subscription on the JungleBus server  |
| 100  | waiting            | A ping message that is sent to indicate waiting for a new block   |
| 101  | subscription_error | Sent when an error occurs on a subscription                       |
| 200  | block_done         | Sent when all transaction of a block have been processed and sent |
| 300  | reorg              | Sent when a reorg has occurred                                    |
| 999  | error              | Sent when a generic error occurs                                  |

You can listen to the control messages with `onStatus` callback function in the JungleBus libraries. Special note should
be taken to the `block_done` (code 200) message, which can be used to store what the last block was that was published
on your subscription.

## API endpoints

JungleBus exposes several API endpoints to allow developers to access data on the Bitcoin blockchain. The endpoints
expose the raw underlying data in the JungleBus database and are formatted slightly differently from the data coming
from the subscriptions.

| Endpoint                              | Description                                                                                                      |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| GET /v1/transaction/get/:id           | Get all information about a single transaction                                                                   |
| GET /v1/address/get/:address          | Get transaction meta data for all transactions associated with the given address                                 |
| GET /v1/address/transactions/:address | Get the transaction document for all transactions associated with the given address                              |
| GET /v1/block_header/get/:height      | Get a single block header by height (or hash)                                                                    |
| GET /v1/block_header/list/:height     | Get block headers from the given height (or hash)<br/>Can be passed a limit parameter `?limit=1000` (max 10,000) |

All these endpoints are built into the JungleBus [libraries](#Libraries)

### Data format

The API endpoints return the full data from each of the database tables.

#### Transaction

```json
{
    "id": "e597af34eb78b599b7d458110a3cc602a40dedd020db684992b40926217612a4",
    "block_hash": "000000000000000006296f1e5437dd6c01b9b5471691a89a9c7d8e9f06920da5",
    "block_height": 750000,
    "block_time": 1658878267,
    "block_index": 3,
    "transaction": "AQAAAAIVwG/ApBvn5i7YIXN0XQrqGUJG++WseEkbamyVRfYc5wEAAABrSDBFAiEAwTPanI5fwsUZcg3pLwsiyTNQOlTaxIxVrNzN6TAOCg4CIB1mXT46cTusWh1AGfk1T4SLvTtaHFfqDE0skM4Wj80MQSEDEqyS0AMM0qy1bePt0smL9aMcvLOQEKFXDR24OMjEL2P/////SzKBazsfJYrXcDFXbrbddtJAC8PDmBT0lTpUFuqK6WsBAAAAa0gwRQIhAPRvsHYUqeWunaw2s4Z510D+sdOudAY0/pDa2N5xJlR5AiB7Vtmo64W8mgsAyLf0pkbhfXt04zjGtTiaxObORIRUsEEhAxKsktADDNKstW3j7dLJi/WjHLyzkBChVw0duDjIxC9j/////wMAAAAAAAAAAP0rAgBqA3J1bgEFDGNyeXB0b2ZpZ2h0c00TAnsiaW4iOjIsInJlZiI6WyJlNjZiZjBlMzhkYWI3YzY0NjI2MWFjNjliOWY3NjQxYTIwMmIwMWFlNzIyNWNkMmUxYmVmMjE2NmJkNmVhYmQzX28xIiwiNTU1YWFkMTk1M2JjZmVmOGM3Nzc5ZDI0NmZhMDNlZmFlMDQxMmVkNzAwYjk1NTQzNTgzMTgxNGY1YmUzYTgyYl9vMSIsImVjZDhiNTY1N2RlMDMxZGEwMWU4YmY0ODgwOGYwNGZkNzlkNTI1YzIxMDIxYzBhMDMzOGVhY2NjZjYwYzRlN2ZfbzEiLCJjMmM0Yzk3MWU4NWI0OTljMjlhOGFiMjE0OGZkMzI0ZmUxMmI1NTBiOGY0ZjU3NjU4YTQ2ODZlMDExZDhmZDU4X28xIl0sIm91dCI6WyIyZTcyOWQzOWE5Y2QzMDBmNTEwMDA0NGE1NDIwNGU2ZDhiNDNmZTQ5NTU1MzA5MzYxZmRjM2Q4NTY1MzIzNDk5Il0sImRlbCI6WyJkZmE4NzAyNzM1MTRkNWQ4MTVjZDY2YTU3OWRiNjE4ZmM4MTM5YmYxODE1ZDJkZjQ5ZDU2NTA5MDViOTc4MWE4Il0sImNyZSI6W10sImV4ZWMiOlt7Im9wIjoiQ0FMTCIsImRhdGEiOlt7IiRqaWciOjB9LCJyZWNvcmRCYXR0bGUiLFt7IiRqaWciOjF9LHRydWVdXX1dfREBAAAAAAAAGXapFPKMOZLdakPsyu0W8/f7asjaG8PCiKzhAAAAAAAAABl2qRRPfWpIXgl3D5R8C6ONFQUKWoC2+oisAAAAAA==",
    "merkle_proof": "AAOkEnYhJgm0kklo2yDQ7Q2kAsY8ChFY1LeZtXjrNK+X5dJ2XOGa0NywJ522sOLYfvm2myelJTJ3aYS1EOpEq8nVDgDEx9sNn3HesJyc9fPinc+oST7Fzm3MM6GQZtu7mYiaLwC+gpDB2W2p9wwyRuAWYSPHEWgCmNaKRRowxJo6bYl8fAC3qibRz/jVbhT/HktEdjo0a9y1CQM6xhltNqKStiDl2QApiFnvUFeiec7sNXh2EHZyP3x2izfxHrZtYBL7WP2PFACrqXcHmoTe7EGAnUUmPIl4pMUTg1WzQfJYHaHBRFihnwBaYfPJ5zq13WN1Ii1MNQ0uzRU/udhN8yVowtNmw5siLgADMr+pymBExM8ZWLaNyMdzfr1P+n2snClOMbDwo/cjBQAUH9AUSICIoQilAAf7dbG8U0hiZKtgBttypRpugEhgBwAT9n9juAeQcnU3Td7cf/PpOWbXzFZ+Y8wLo8f8g1HnmAB9jFlB2tKgViPMppt2SmPo8dXRoQ1oeNz+ZoccNz0YQQCza+ycJTegYPbjn6T6+Z54RHGqT1BqpCBJ1/WctnFELwBTrIMFFENxGncBFQSlmG8RzljHybdXjoLXf3+aZiIUgABKkdvG1GY5bIphg9DcVzLob8tdMoDFBCOfFWbhcD83bABSV04rwjag9DV397i6+3ld7Q+uWpbCQXE5ivYXAfwovQ==",
    "addresses": [
        "18FJd9tDLAC2S6PCzfnqNfUMXhZuPfsFUm",
        "1P7UWRLdL5pH2Si1GauwASYAA1LQHs2z45"
    ],
    "inputs": [],
    "outputs": [
        "76a9144f7d6a485e09770f947c0ba38d15050a5a80b6fa88ac",
        "76a914f28c3992dd6a43eccaed16f3f7fb6ac8da1bc3c288ac"
    ],
    "input_types": [],
    "output_types": ["nulldata", "pubkeyhash", "run"],
    "contexts": [
        "555aad1953bcfef8c7779d246fa03efae0412ed700b955435831814f5be3a82b_o1",
        "c2c4c971e85b499c29a8ab2148fd324fe12b550b8f4f57658a4686e011d8fd58_o1",
        "e66bf0e38dab7c646261ac69b9f7641a202b01ae7225cd2e1bef2166bd6eabd3_o1",
        "ecd8b5657de031da01e8bf48808f04fd79d525c21021c0a0338eacccf60c4e7f_o1"
    ],
    "sub_contexts": [
        "2e729d39a9cd300f5100044a54204e6d8b43fe49555309361fdc3d8565323499"
    ],
    "data": []
}
```

| Field        | Description                                                                                                                          |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| id           | The ID of the transaction.                                                                                                           |
| block_hash   | The hex hash of the block this transaction was mined into.                                                                           |
| block_height | The height of the block this transaction was mined into.                                                                             |
| block_index  | The index (position) of the transaction in the block it was mined into.                                                              |
| transaction  | Full transaction in hex.                                                                                                             |
| merkle_proof | TSC compatible binary merkle proof of the transaction in hex.                                                                        |
| addresses    | List of all addresses found in the transaction. This could be in the pubkeyhash output, or in one of the data outputs.               |
| inputs       | _not used_                                                                                                                           |
| outputs      | The output scripts of each of the outputs of the transaction, capped to the first 1024 characters.                                   |
| input_types  | _not used_                                                                                                                           |
| output_types | Output type classifications found by JungleBus. All output types that JungleBus matches in a transaction will be added to this list. |
| contexts     | Any contexts mapped from data outputs by JungleBus.                                                                                  |
| subcontexts  | Any secondary contexts mapped from data outputs by JungleBus.                                                                        |
| data         | Other data attributes found by JungleBus, stored in `key=value` pairs.                                                               |

#### Block Header

```json
{
    "hash": "000000000000000006296f1e5437dd6c01b9b5471691a89a9c7d8e9f06920da5",
    "coin": 1,
    "height": 750000,
    "time": 1658878267,
    "nonce": 4188280238,
    "version": 671080448,
    "merkleroot": "e88b40ac9367eb11dd918416b668e67f09bf24550eac93de7f2d68a0ca0c6eae",
    "bits": "180f4e90",
    "synced": 8971
}
```

| Field      | Description                                                   |
| ---------- | ------------------------------------------------------------- |
| hash       | The hash of the block header.                                 |
| coin       | _not used_                                                    |
| height     | Block height in the full chain                                |
| time       | Current block timestamp as seconds since 1970-01-01T00:00 UTC |
| nonce      | 32-bit number (starts at 0)                                   |
| version    | Block version                                                 |
| merkleroot | 256-bit hash based on all of the transactions in the block    |
| bits       | Current target in compact format                              |
| synced     | How many transactions were synced by JungleBus for this block |

For more information about block headers, see https://wiki.bitcoinsv.io/index.php/Block_header

#### Address

Address is a transaction metadata format, that shows only the minimal information needed from the transactions associated with that address.

```json
{
    "id": "8859250950ecbb7025731c1206e277e344a6db5f285274b7a1d2817980ab8e64",
    "address": "13qRymPwRxAr7oRdAoFdo5Wp8815sstHE5",
    "transaction_id": "eb197a43a7c4ed230a7125d7e7bf5990cd60be8ff0f59b8fffdfd91d52dfce82",
    "block_hash": "0000000000000000002be95240df5e4215e6878259dce8b9df08650641fdd40a",
    "block_index": 50545
}
```

| Field          | Description                                                             |
| -------------- | ----------------------------------------------------------------------- |
| id             | The ID of the address field (unique hash).                              |
| address        | Bitcoin address.                                                        |
| transaction_id | The ID of the transaction.                                              |
| block_hash     | The hex hash of the block this transaction was mined into.              |
| block_index    | The index (position) of the transaction in the block it was mined into. |

## Libraries

JungleBus offers JavaScript and Go libraries for interacting with JungleBus.

-   Javascript: https://www.npmjs.com/package/@gorillapool/js-junglebus
-   Go: https://github.com/GorillaPool/go-junglebus

<!-- tabs:start -->

#### **JavaScript**

```javascript
import { JungleBusClient, ControlMessageStatusCode } from "@gorillapool/js-junglebus";

const client = new JungleBusClient("junglebus.gorillapool.io", {
    useSSL: true,
    onConnected(ctx) {
        console.log("CONNECTED", ctx);
    },
    onConnecting(ctx) {
        console.log("CONNECTING", ctx);
    },
    onDisconnected(ctx) {
        console.log("DISCONNECTED", ctx);
    },
    onError(ctx) {
        console.error(ctx);
    },
});

const onPublish = function(tx) {
    console.log("TRANSACTION", tx);
};
const onStatus = function(message) {
    if (message.statusCode === ControlMessageStatusCode.BLOCK_DONE) {
      console.log("BLOCK DONE", message.block);
    } else if (message.statusCode === ControlMessageStatusCode.WAITING) {
      console.log("WAITING FOR NEW BLOCK...", message);
    } else if (message.statusCode === ControlMessageStatusCode.REORG) {
      console.log("REORG TRIGGERED", message);
    } else if (message.statusCode === ControlMessageStatusCode.ERROR) {
      console.error(message);
    }
};
const onError = function(err) {
    console.error(err);
};
const onMempool = function(tx) {
    console.log("MEMPOOL TRANSACTION", tx);
};

(async () => {
    await client.Subscribe("${subscriptionId}", ${fromBlock}, onPublish, onStatus, onError, onMempool);
})();
```

#### **Go**

```go
package main

import (
    "context"
    "log"
    "os"
    "strconv"
    "time"

    "github.com/GorillaPool/go-junglebus"
    "github.com/GorillaPool/go-junglebus/models"
)

func main() {
    junglebusClient, err := junglebus.New(
        junglebus.WithHTTP("https://junglebus.gorillapool.io"),
    )
    if err != nil {
        log.Fatalln(err.Error())
    }

    argsWithoutProg := os.Args[1:]
    if len(argsWithoutProg) < 2 {
        panic("no subscription id or block height given")
    }
    subscriptionID := argsWithoutProg[0]
    var fromBlock uint64
    if fromBlock, err = strconv.ParseUint(argsWithoutProg[1], 10, 64); err != nil {
        panic("invalid block height given")
    }

    eventHandler := junglebus.EventHandler{
        // do not set this function to leave out mined transactions
        OnTransaction: func(tx *models.TransactionResponse) {
            log.Printf("[TX]: %d: %v", tx.BlockHeight, tx.Id)
        },
        // do not set this function to leave out mempool transactions
        OnMempool: func(tx *models.TransactionResponse) {
            log.Printf("[MEMPOOL TX]: %v", tx.Id)
        },
        OnStatus: func(status *models.ControlResponse) {
            log.Printf("[STATUS]: %v", status)
        },
        OnError: func(err error) {
            log.Printf("[ERROR]: %v", err)
        },
    }

    var subscription *junglebus.Subscription
    if subscription, err = junglebusClient.Subscribe(context.Background(), subscriptionID, fromBlock, eventHandler); err != nil {
        log.Printf("ERROR: failed getting subscription %s", err.Error())
    } else {
        time.Sleep(10 * time.Second) // stop after 10 seconds
        if err = subscription.Unsubscribe(); err != nil {
            log.Printf("ERROR: failed unsubscribing %s", err.Error())
        }
    }
    os.Exit(0)
}
```

<!-- tabs:end -->

## Secondary indexers using JungleBus

-   https://b.map.sv/query - a Planaria indexer for MAP data
