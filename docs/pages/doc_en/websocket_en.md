---
title: 
keywords: sample homepage
sidebar: ont_doc_en
permalink: websocket_en.html
folder: doc_en
---

English / [中文](./websocket_zh.html)

<h1 align="center">Ontology Websocket API </h1>
<p align="center" class="version">Version 0.9.0 </p>

* [Introduction](#introduction)
* [Websocket Api List](#websocket-api-list)
* [Error Code](#error-code)

## Introduction

This document describes the Websocket api format for the ws/wss used in the Onchain Ontology.

## Websocket Api List

### Response parameters descri

| Field | Type | Description |
| :--- | :--- | :--- |
| Action | string | action name |
| Desc | string | description |
| Error | int64 | error code |
| Result | object | execute result |
| Version | string | version information |
| Id | int | req Id|

###  1. heartbeat
if don't send heartbeat, the session expire after 5min

#### Request Example:

```
{
    "Action": "heartbeat",
    "Version": "1.0.0"
}
```

#### Response example:

```
{
    "Action": "heartbeat",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "SubscribeEvent":false,
        "SubscribeJsonBlock":false,
        "SubscribeRawBlock":false,
        "SubscribeBlockTxHashs":false
    }
    "Version": "1.0.0"
}
```

###  2. subscribe
subscribe service

#### Request Example:

```
{
    "Action": "subscribe",
    "Version": "1.0.0",
    "ConstractsFilter":["constractAddress"], //optional
    "SubscribeEvent":false, //optional
    "SubscribeJsonBlock":true, //optional
    "SubscribeRawBlock":false, //optional
    "SubscribeBlockTxHashs":false //optional
}
```

#### Response example:

```
{
    "Action": "subscribe",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "ConstractsFilter":["constractAddress"],
        "SubscribeEvent":false,
        "SubscribeJsonBlock":true,
        "SubscribeRawBlock":false,
        "SubscribeBlockTxHashs":false
    }
    "Version": "1.0.0"
}
```

### 3. Get the generate block time
return the time required to create a new block


#### Request Example:

```
{
    "Action": "getgenerateblocktime",
    "Version": "1.0.0"
}
```

#### Response example:

```
{
    "Action": "getgenerateblocktime",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": 6,
    "Version": "1.0.0"
}
```
### 4 Get the number of connected node

get the current number of connections for the node


#### Request Example:

```
{
    "Action": "getconnectioncount",
    "Version": "1.0.0"
}
```

#### Response Example:

```
{
    "Action": "getconnectioncount",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": 4,
    "Version": "1.0.0"
}
```
### 5 Get transactions by block height

return all transaction hash contained in the block corresponding to this height


#### Request Example:

```
{
    "Action": "getblocktxsbyheight",
    "Version": "1.0.0",
    "Height": 100
}
```

#### Response Example:

```
{
    "Action": "getblocktxsbyheight",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "Hash": "ea5e5219d2f1591f4feef89885c3f38c83d3a3474a5622cf8cd3de1b93849603",
        "Height": 100,
        "Transactions": [
            "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7"
        ]
    },
    "Version": "1.0.0"
}
```
### 6. Get the block by block height

return block details based on block height
if raw=1 return serialized block

#### Request Example:

```
{
    "Action": "getblockbyheight",
    "Version": "1.0.0",
    "Raw": "0",
    "Height": 100
}
```

#### Response Example:

```
{
    "Action": "getblockbyheight",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "Hash": "ea5e5219d2f1591f4feef89885c3f38c83d3a3474a5622cf8cd3de1b93849603",
        "Header": {
            "Version": 0,
            "PrevBlockHash": "fc3066adb581c5aee8edaa47eecda2b7cc039c8662757f8b1e3c3aed60314353",
            "TransactionsRoot": "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7",
            "BlockRoot": "7154a6dcb3c23254334bc1f5d8f054c143a39ff28f46fdeb8a9c7488147ccec6",
            "Timestamp": 1522313652,
            "Height": 100,
            "ConsensusData": 18012644264110396442,
            "NextBookkeeper": "TABrSU6ABhj6Rdw5KozV53wvZNSUATgKHW",
            "Bookkeepers": [
                "120203fe4f9ba2022b68595dd163f4a92ac80f918919674de2d6e2a7e04a10c59d0066"
            ],
            "SigData": [
                "01a2369280b0ff75bed85f351d3ef0dd58add118328c1ed2f7d3320df32cb4bd55541f1bb8e11ad093bd24da3de4cd12464800310bfdb49dc62d42d97ca0549762"
            ],
            "Hash": "ea5e5219d2f1591f4feef89885c3f38c83d3a3474a5622cf8cd3de1b93849603"
        },
        "Transactions": [
            {
                "Version": 0,
                "Nonce": 0,
                "TxType": 0,
                "Payload": {
                    "Nonce": 1522313652068190000
                },
                "Attributes": [],
                "Fee": [],
                "NetworkFee": 0,
                "Sigs": [
                    {
                        "PubKeys": [
                            "120203fe4f9ba2022b68595dd163f4a92ac80f918919674de2d6e2a7e04a10c59d0066"
                        ],
                        "M": 1,
                        "SigData": [
                            "017d3641607c894dd85f455c71a94afaea2661acbe372ff8f3f4c7921b0c768756e3a6e9308a4c4c8b1b58e717f1486a2f10f5bc809b803a27c10a2cd579778a54"
                        ]
                    }
                ],
                "Hash": "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7"
            }
        ]
    },
    "Version": "1.0.0"
}
```
### 7. Get block by blockhash

return block details based on block hash
if raw=1 return serialized block

#### Request Example:

```
{
    "Action": "getblockbyhash",
    "Version": "1.0.0",
    "Raw": "0",
    "Hash": "7c3e38afb62db28c7360af7ef3c1baa66aeec27d7d2f60cd22c13ca85b2fd4f3"
}
```

#### Response Example:

```
{
    "Action": "getblockbyhash",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "Hash": "ea5e5219d2f1591f4feef89885c3f38c83d3a3474a5622cf8cd3de1b93849603",
        "Header": {
            "Version": 0,
            "PrevBlockHash": "fc3066adb581c5aee8edaa47eecda2b7cc039c8662757f8b1e3c3aed60314353",
            "TransactionsRoot": "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7",
            "BlockRoot": "7154a6dcb3c23254334bc1f5d8f054c143a39ff28f46fdeb8a9c7488147ccec6",
            "Timestamp": 1522313652,
            "Height": 100,
            "ConsensusData": 18012644264110396442,
            "NextBookkeeper": "TABrSU6ABhj6Rdw5KozV53wvZNSUATgKHW",
            "Bookkeepers": [
                "120203fe4f9ba2022b68595dd163f4a92ac80f918919674de2d6e2a7e04a10c59d0066"
            ],
            "SigData": [
                "01a2369280b0ff75bed85f351d3ef0dd58add118328c1ed2f7d3320df32cb4bd55541f1bb8e11ad093bd24da3de4cd12464800310bfdb49dc62d42d97ca0549762"
            ],
            "Hash": "ea5e5219d2f1591f4feef89885c3f38c83d3a3474a5622cf8cd3de1b93849603"
        },
        "Transactions": [
            {
                "Version": 0,
                "Nonce": 0,
                "TxType": 0,
                "Payload": {
                    "Nonce": 1522313652068190000
                },
                "Attributes": [],
                "Fee": [],
                "NetworkFee": 0,
                "Sigs": [
                    {
                        "PubKeys": [
                            "120203fe4f9ba2022b68595dd163f4a92ac80f918919674de2d6e2a7e04a10c59d0066"
                        ],
                        "M": 1,
                        "SigData": [
                            "017d3641607c894dd85f455c71a94afaea2661acbe372ff8f3f4c7921b0c768756e3a6e9308a4c4c8b1b58e717f1486a2f10f5bc809b803a27c10a2cd579778a54"
                        ]
                    }
                ],
                "Hash": "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7"
            }
        ]
    },
    "Version": "1.0.0"
}
```

### 8. Get the current block height

return the current block height


#### Request Example:

```
{
    "Action": "getblockheight",
    "Version": "1.0.0"
}
```


#### Response Example:

```
{
    "Action": "getblockheight",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": 327,
    "Version": "1.0.0"
}
```

### 9. Get blockhash by block height

return block hash based on block height


#### Request Example:

```
{
    "Action": "getblockhash",
    "Version": "1.0.0",
    "Height": 100
}
```

#### Response Example:

```
{
    "Action": "getblockhash",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": "3b90ddc4d33c4954c3d87736120e94915f963546861987757f358c9376422255",
    "Version": "1.0.0"
}
```

### 10. get transaction by transaction hash

get transaction details based on transaction hash
if raw=1 return serialized transaction

#### Request Example:

```
{
    "Action": "gettransaction",
    "Version": "1.0.0",
    "Hash": "3b90ddc4d33c4954c3d87736120e94915f963546861987757f358c9376422255",
    "Raw": "0"
}
```
#### Response Example:

```
{
    "Action": "gettransaction",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "Version": 0,
        "Nonce": 0,
        "TxType": 0,
        "Payload": {
            "Nonce": 1522313652068190000
        },
        "Attributes": [],
        "Fee": [],
        "NetworkFee": 0,
        "Sigs": [
            {
                "PubKeys": [
                    "120203fe4f9ba2022b68595dd163f4a92ac80f918919674de2d6e2a7e04a10c59d0066"
                ],
                "M": 1,
                "SigData": [
                    "017d3641607c894dd85f455c71a94afaea2661acbe372ff8f3f4c7921b0c768756e3a6e9308a4c4c8b1b58e717f1486a2f10f5bc809b803a27c10a2cd579778a54"
                ]
            }
        ],
        "Hash": "37e017cb9de93aa93ef817e82c555812a0a6d5c3f7d6c521c7808a5a77fc93c7"
    },
    "Version": "1.0.0"
}
```

### 11. send transaction

send transaction.set PreExec=1 if want prepare exec smartcontract


#### Request Example:

```
{
    "Action":"sendrawtransaction",
    "Version":"1.0.0",
    "PreExec": 0,
    "Data":"80000001195876cb34364dc38b730077156c6bc3a7fc570044a66fbfeeea56f71327e8ab0000029b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc500c65eaf440000000f9a23e06f74cf86b8827a9108ec2e0f89ad956c9b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc50092e14b5e00000030aab52ad93f6ce17ca07fa88fc191828c58cb71014140915467ecd359684b2dc358024ca750609591aa731a0b309c7fb3cab5cd0836ad3992aa0a24da431f43b68883ea5651d548feb6bd3c8e16376e6e426f91f84c58232103322f35c7819267e721335948d385fae5be66e7ba8c748ac15467dcca0693692dac"
}
```

#### Response Example:
```
{
    "Action": "sendrawtransaction",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": "22471ab3f4b4307a99f00c9a717dbf8b26f5bf63bf47f9c560477da8181de777",
    "Version": "1.0.0"
}
```
> Result: txhash

### 12. getStorage

Returns the stored value according to the contract script hashes and stored key.

Request Example
```
{
    "Action": "getstorage",
    "Version": "1.0.0",
    "Hash": "0144587c1094f6929ed7362d6328cffff4fb4da2",
    "Key" : "4587c1094f6"
}
```
#### Response
```
{
    "Action": "getstorage",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": "58d15e17628000",
    "Version": "1.0.0"
}
```
> Result:Returns the stored value according to the contract script hashes and stored key.

### 13. GetBalanceByAddr

return the balance of base58 account address.


Request Example
```
{
    "Action": "getbalance",
    "Version": "1.0.0",
    "Addr": "TA63xZXqdPLtDeznWQ6Ns4UsbqprLrrLJk"
}
```

#### Response
```
{
    "Action": "getbalance",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "ont": "2500",
        "ong": "0",
        "ong_appove": "0"
    },
    "Version": "1.0.0"
}
```
### 14. get contractstate

According to the contract script hash, query the contract information.


#### Request Example:

```
{
    "Action": "getcontract",
    "Version": "1.0.0",
    "Hash": "fff49c809d302a2956e9dc0012619a452d4b846c"
}
```

#### Response Example:

```
{
    "Action": "getcontract",
    "Desc": "SUCCESS",
    "Error": 0,
    "Version": "1.0.0",
    "Result": {
        "VmType": 255,
        "Code": "4f4e5420546f6b656e",
        "NeedStorage": true,
        "Name": "ONT",
        "CodeVersion": "1.0",
        "Author": "Ontology Team",
        "Email": "contact@ont.io",
        "Description": "Ontology Network ONT Token"
    }
}
```

#### 15. get smart contract event txhash list by height

Get a list of transaction  with smartcontract event based on height


#### Example usage:

```
{
    "Action": "getsmartcodeeventbyheight",
    "Version": "1.0.0",
    "Height": 100
}
```

#### response
```
{
    "Action": "getsmartcodeeventbyheight",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": [
               {
                    "TxHash": "7e8c19fdd4f9ba67f95659833e336eac37116f74ea8bf7be4541ada05b13503e",
                    "State": 1,
                    "GasConsumed": 0,
                    "Notify": [
                        {
                            "ContractAddress": "0200000000000000000000000000000000000000",
                            "States": [
                                "transfer",
                                "AFmseVrdL9f9oyCzZefL9tG6UbvhPbdYzM",
                                "AFmseVrdL9f9oyCzZefL9tG6UbvhUMqNMV",
                                1000000000000000000
                            ]
                        }
                    ]
                },
                {
                    "TxHash": "fc82cd363271729367098fbabcfd0c02cf6ded1e535700d04658b596d53cf07d",
                    "State": 1,
                    "GasConsumed": 0,
                    "Notify": [
                        {
                            "ContractAddress": "0200000000000000000000000000000000000000",
                            "States": [
                                "transfer",
                                "AFmseVrdL9f9oyCzZefL9tG6UbvhPbdYzM",
                                "AFmseVrdL9f9oyCzZefL9tG6UbvhUMqNMV",
                                1000000000000000000
                            ]
                        }
                    ]
                }
    ],
    "Version": "1.0.0"
}
```
> Note: result is the txHash list.

### 16. get smart contract event by txhash


#### Request Example:
```
{
    "Action": "getsmartcodeeventbyhash",
    "Version": "1.0.0",
    "Hash": "20046da68ef6a91f6959caa798a5ac7660cc80cf4098921bc63604d93208a8ac"
}
```
#### Response:
```
{
    "Action": "getsmartcodeeventbyhash",
    "Desc": "SUCCESS",
    "Error": 0,
    "Version": "1.0.0",
    "Result": {
             "TxHash": "20046da68ef6a91f6959caa798a5ac7660cc80cf4098921bc63604d93208a8ac",
             "State": 1,
             "GasConsumed": 0,
             "Notify": [
                    {
                      "ContractAddress": "ff00000000000000000000000000000000000001",
                      "States": [
                            "transfer",
                            "A9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb",
                            "AA4WVfUB1ipHL8s3PRSYgeV1HhAU3KcKTq",
                            1000000000
                         ]
                     }
              ]
    }
}
```
### 17. Get block height by transaction hash
get blockheight of txhash

#### Request Example:
```
{
    "Action": "getblockheightbytxhash",
    "Version": "1.0.0",
    "Hash": "3e23cf222a47739d4141255da617cd42925a12638ac19cadcc85501f907972c8"
}
```
#### Response
```
{
    "Action": "getblockheightbytxhash",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": 100,
    "Version": "1.0.0"
}
```


### 18. getmerkleproof

get merkle proof

#### Request Example:
```
{
    "Action": "getmerkleproof",
    "Version": "1.0.0",
    "Hash": "0087217323d87284d21c3539f216dd030bf9da480372456d1fa02eec74c3226d"
}

```
#### Response
```
{
    "Action": "getmerkleproof",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
        "Type": "MerkleProof",
        "TransactionsRoot": "fe3a4ee8a44e3e588de55de1b8fe08f08b6184d9c062cf7316fb9481eb57b9e6",
        "BlockHeight": 600,
        "CurBlockRoot": "57476eba688531dec8555cb712835c7eda48a478431a2cfd3372aeee5298e711",
        "CurBlockHeight": 6478,
        "TargetHashes": [
            "270cd10ea235cc18cba83a070fdf18ae576983b6b9a7bb9a3fec540b3786c85c",
            "24e4697f9dd6cb944d0736bd3e11b64f64edec94fb599e25d4e5461d54174f0e",
            "9a47ab04acf6bba7bb97b83eddeb0db20e11c0627b8079b40b60031d5bd63154",
            "d1b513810b9b983014c9f8b7084b8ea8744eca8e7c942586c2b7c63f910363ca",
            "54e88360efedcf5dbbc486ea0267724a98b027b3ba780617e32569bb3fbe56e8",
            "e0c5ebca3ca191617d42e11db64778b047cd9a520538efd95d5a688cbba0c8d5",
            "52bfb23b6456cac4e5e7143287e1518dd923c5b5d32d0bfe8d825dc8195ea62b",
            "86d6be166ae1a53c052adc40b9b66c4f95f5e3b6ecc88afaea3750e1cbe98276",
            "5588530cfc4d92e979717f8ae399ac4553a76e7537a981e8eaf078d60f1d39a6",
            "3f15bec38bcf054e4f32efe475a09d3e80c2e90d3345a1428aaa262606f13267",
            "f238ed8ceb1c10a08f7eaa390cdde44ed7d160abbde4702028407b55671e7aa8",
            "b4813f1f27c0457726b58f8bf20bee70c100a4d5c5f1805e53dcd20f38479615",
            "83893713ea8ace9214b28af854b75671c8aaa62bb74b0d43ad6fb83e3dee42db"
        ]
    },
    "Version": "1.0.0"
}
```

### 19. Get session count
get session count

#### Request Example:
```
{
    "Action": "getsessioncount",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getsessioncount",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": 10,
    "Version": "1.0.0"
}
```

### 20. Get gasprice
get gasprice

#### Request Example:
```
{
    "Action": "getgasprice",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getgasprice",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": {
         "gasprice": 0,
         "height": 1
     },
    "Version": "1.0.0"
}
```

### 21. Get allowance
get allowance

#### Request Example:
```
{
    "Action": "getallowance",
    "Asset": "ont",
    "From" :  "A9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb",
    "To"   :  "AA4WVfUB1ipHL8s3PRSYgeV1HhAU3KcKTq",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getallowance",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": "10",
    "Version": "1.0.0"
}
```

### 22. Get unboundong
get unboundong

#### Request Example:
```
{
    "Action": "getunboundong",
    "Addr": "ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getunboundong",
    "Desc": "SUCCESS",
    "Error": 0,
    "Result": "204957950400000",
    "Version": "1.0.0"
}
```

### 23. Get mempooltxstate
Query the transaction state in the memory pool.

#### Request Example:
```
{
    "Action": "getmempooltxstate",
    "Hash": "0b437771a42d18d292741c5d4f1300a135fa6e65b0594e39dc299e7f8279221a",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getmempooltxstate",
    "Desc": "SUCCESS",
    "Error": 0,
    "Version": "1.0.0",
    "Result": {
              	"State": [{
              		"Type": 1,
              		"Height": 342,
              		"ErrCode": 0
              	}, {
              		"Type": 0,
              		"Height": 0,
              		"ErrCode": 0
              	}]
    }
}
```

### 24. Get mempooltxcount
Query the transaction count in the memory pool.

#### Request Example:
```
{
    "Action": "getmempooltxcount",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getmempooltxcount",
    "Desc": "SUCCESS",
    "Error": 0,
    "Version": "1.0.0",
    "Result": [100,50]
}
```


### 25. Get version
Get the version information of the node.

#### Request Example:
```
{
    "Action": "getversion",
    "Version": "1.0.0"
}
```
#### Response
```
{
    "Action": "getversion",
    "Desc": "SUCCESS",
    "Error": 0,
    "Version": "1.0.0",
    "Result": "0.9"
}
```


## Error Code

| Field | Type | Description |
| :--- | :--- | :--- |
| 0 | int64 | SUCCESS |
| 41001 | int64 | SESSION\_EXPIRED: invalided or expired session |
| 41002 | int64 | SERVICE\_CEILING: reach service limit |
| 41003 | int64 | ILLEGAL\_DATAFORMAT: illegal dataformat |
| 41004 | int64 | INVALID\_VERSION: invalid version |
| 42001 | int64 | INVALID\_METHOD: invalid method |
| 42002 | int64 | INVALID\_PARAMS: invalid params |
| 43001 | int64 | INVALID\_TRANSACTION: invalid transaction |
| 43002 | int64 | INVALID\_ASSET: invalid asset |
| 43003 | int64 | INVALID\_BLOCK: invalid block |
| 44001 | int64 | UNKNOWN\_TRANSACTION: unknown transaction |
| 44002 | int64 | UNKNOWN\_ASSET: unknown asset |
| 44003 | int64 | UNKNOWN\_BLOCK: unknown block |
| 45001 | int64 | INTERNAL\_ERROR: internel error |
| 47001 | int64 | SMARTCODE\_ERROR: smartcode error |