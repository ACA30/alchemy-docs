---
description: >-
  Gets all NFTs currently owned by a given address.
---

# getNFTs

{% hint style="info" %}
**NOTE: **This endpoint is currently only available on Mainnet and Testnets for Ethereum and Polygon, as well as [Flow Mainnet](https://docs.alchemy.com/flow/documentation/flow-nft-apis).
{% endhint %}

## Parameters

* `owner`: address for NFT owner
* `pageKey`: (optional) UUID for pagination. If more results are available, a UUID pageKey will be returned in the response. Pass that uuid into pageKey to fetch the next 100 NFTs. NOTE: pageKeys expire after 10 minutes. 
* `contractAddresses`: (optional) array of contract addresses to filter the responses with. Max limit 20 contracts.

{% hint style="info" %}
**Note on pagination**
We paginate our responses with a default limit of **100 responses**. We've chosen this number via thorough testing to determine the best balance of reliability and speed. In the future, you will be able to specify your own default size. If the owner has more than 100 nfts, we'll provide a pageKey you can include in the next request to return the remaining responses. This uses cursor based pagination with an idempotent result. This means if you provide one it serves as a static reference to the NFTs owned at time of the first call. This means if an owner acquires or transfers an NFT in between a paginated call, this will **NOT** be reflected.
{% endhint %}

## Returns

* totalCount: total number of NFTs owned by the given address. 
* pageKey : (optional) UUID for pagination - returned if there are more NFTs to fetch. Max NFTs per page = 100.
* ownedNfts: list of objects that represent NFTs owned by the address. Max results per response = 100. 
    * Object schema:
        * contract: 
            * address: address of NFT contract
        * id: 
            * token_id: token ID of given NFT

## Examples

For an example request with pagination, see [Request (with pagination)](#request-with-pagination).

For examples with contract filtering, see [Request (with contract filtering)](#request-with-contract-filtering).


{% hint style="danger" %}
** Version **
You must update your api_key from your dashboard from V2 --> V1, for example: 
https://eth-mainnet.g.alchemy.com/your-api-key/v2
should be
https://eth-mainnet.g.alchemy.com/your-api-key/v1

** Network **
The examples below is for Ethereum Mainnet. If you are using Polygon you'll need to use your polygon endpoint instead: https://polygon-mainnet.g.alchemy.com/your-api-key/v1/getNFTs...
{% endhint %}

### Request
```
curl 'https://eth-mainnet.g.alchemy.com/your-api-key/v1/getNFTs/?owner=0xfAE46f94Ee7B2Acb497CEcAFf6Cff17F621c693D'
```

### Response
```
{
    "ownedNfts": [{
        "contract": {
            "address": "0x7eef591a6cc0403b9652e98e88476fe1bf31ddeb"
        },
        "id": {
            "tokenId": "0x2a"
        }
    }, {
        "contract": {
            "address": "0x9abb7bddc43fa67c76a62d8c016513827f59be1b"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000baa"
        }
    }, {
        "contract": {
            "address": "0x495f947276749ce646f68ac8c248420045cb7b5e"
        },
        "id": {
            "tokenId": "0x7b1507011c173ea0b6365f54131e1fefa1562032000000000000850000000001"
        }
    }, {
        "contract": {
            "address": "0x0beed7099af7514ccedf642cfea435731176fb02"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000001d"
        }
    }, {
        "contract": {
            "address": "0x0beed7099af7514ccedf642cfea435731176fb02"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000001c"
        }
    }, {
        "contract": {
            "address": "0x3f4a885ed8d9cdf10f3349357e3b243f3695b24a"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000003cd"
        }
    }, {
        "contract": {
            "address": "0x495f947276749ce646f68ac8c248420045cb7b5e"
        },
        "id": {
            "tokenId": "0x7b1507011c173ea0b6365f54131e1fefa1562032000000000000800000000001"
        }
    }, {
        "contract": {
            "address": "0x9abb7bddc43fa67c76a62d8c016513827f59be1b"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000bb6"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000001597"
        }
    }, {
        "contract": {
            "address": "0x57f1887a8bf19b14fc0df6fd9b2acc9af147ea85"
        },
        "id": {
            "tokenId": "0x80d3ddec2574b25ee9237c0ca14095c163b335a4b48ffcc717ad882954eeff97"
        }
    }, {
        "contract": {
            "address": "0x3f4a885ed8d9cdf10f3349357e3b243f3695b24a"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000001527"
        }
    }],
    "totalCount": 11
} 
```

### Request (with pagination)
{% hint style="info" %}
This example request url will not return a valid response because the `pageKey` expires after 10 minutes.
{% endhint %}

```
curl 'https://eth-mainnet.g.alchemy.com/your-api-key/v1/getNFTs/?owner=0x8e7644918b3e280fb3b599ca381a4efcb7ade201&pageKey=12e032c5-ce4a-4389-8764-b980e1a17da8'
```

### Response (with pagination)

```
{
    "ownedNfts": [{
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000009cb"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000009cc"
        }
    }, {
        "contract": {
            "address": "0x5ab21ec0bfa0b29545230395e3adaca7d552c948"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000006dc"
        }
    }, {
        "contract": {
            "address": "0x3b3ee1931dc30c1957379fac9aba94d1c48a5405"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000001a"
        }
    }, {
        "contract": {
            "address": "0x69c40e500b84660cb2ab09cb9614fa2387f95f64"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000391"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000008d5"
        }
    }, {
        "contract": {
            "address": "0x495f947276749ce646f68ac8c248420045cb7b5e"
        },
        "id": {
            "tokenId": "0xe96752534bf35669ce26f5605ac4e525962a9b05000000000000030000000005"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000037b"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000037c"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000037e"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a1c"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a1b"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a1e"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a1d"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000009da"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000009db"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a1f"
        }
    }, {
        "contract": {
            "address": "0xf9a423b86afbf8db41d7f24fa56848f56684e43f"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000180"
        }
    }, {
        "contract": {
            "address": "0x3b3ee1931dc30c1957379fac9aba94d1c48a5405"
        },
        "id": {
            "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000a62"
        }
    }, {
        "contract": {
            "address": "0xd4e4078ca3495de5b1d4db434bebc5a986197782"
        },
        "id": {
            "tokenId": "0x00000000000000000000000000000000000000000000000000000000000001a6"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000038b"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000038c"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000002a"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000038e"
        }
    }, {
        "contract": {
            "address": "0x97597002980134bea46250aa0510c9b90d87a587"
        },
        "id": {
            "tokenId": "0x000000000000000000000000000000000000000000000000000000000000244b"
        }
    }],
    "pageKey": "88434286-7eaa-472d-8739-32a0497c2a18",
    "totalCount": 277
}
```

### Request (with contract filtering)
Only one contract in filter array:
```
curl 'https://eth-mainnet.g.alchemy.com/your-api-key/v1/getNFTs/?owner=0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045&contractAddresses%5B%5D=0x39ed051a1a3a1703b5e0557b122ec18365dbc184'
```

Multiple contracts in filter array:
```
curl 'https://eth-mainnet.g.alchemy.com/your-api-key/v1/getNFTs/?owner=0x8e7644918b3e280fb3b599ca381a4efcb7ade201&pageKey=12e032c5-ce4a-4389-8764-b980e1a17da8'
```

### Response (With contract filtering)
```
{
    "ownedNfts": [
        {
            "contract": {
                "address": "0x39ed051a1a3a1703b5e0557b122ec18365dbc184"
            },
            "id": {
                "tokenId": "0x0000000000000000000000000000000000000000000000000000000000000742"
            },
            "balance": "1"
        }
    ],
    "totalCount": 1
}
```