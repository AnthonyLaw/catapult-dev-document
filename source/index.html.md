---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - typescript
  - javascript

toc_footers:
  - <a href='http://mijin.io/en/catapult'>Sign Up Catapult Developers Preview</a>
  - <a href='https://github.com/lord/slate'>Theme Powered by Slate</a>

# includes:
#   - errors

search: true
---

# Catapult REST API Reference

**Version:** 0.7.7

**License:** [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

[Find out more about NEM2](https://nemtech.github.io/)

# Account

### Account information

`GET /account/{accountId}`

**Summary:** Get account information

**Description:** Returns AccountInfo for an account.

**Parameters**

| Name      | Located in | Description                   | Required | Schema |
| --------- | ---------- | ----------------------------- | -------- | ------ |
| accountId | path       | Account address or publicKey. | Yes      | string |

**Responses**

| Code | Description        | Schema                            |
| ---- | ------------------ | --------------------------------- |
| 200  | success            | [AccountInfoDTO](#accountinfodto) |
| 404  | resource not found |                                   |
| 409  | invalid argument   |                                   |

### Account list

`POST /account`

**Summary:** Get accounts information

**Description:** Returns AccountsInfo for different accounts.

**Parameters**

| Name      | Located in | Description         | Required | Schema                  |
| --------- | ---------- | ------------------- | -------- | ----------------------- |
| addresses | body       | Array of addresses. | Yes      | [addresses](#addresses) |

**Responses**

| Code | Description      | Schema                                |
| ---- | ---------------- | ------------------------------------- |
| 200  | success          | [ [AccountInfoDTO](#accountinfodto) ] |
| 400  | invalid content  |                                       |
| 409  | invalid argument |                                       |

### Incoming transactions

`GET /account/{publicKey}/transactions/incoming`

**Summary:** Get incoming transactions information

**Description:** Gets an array of transactions for which an account is the recipient. A transaction is said to be incoming regarding an account if the account is the recipient of a transaction.

**Parameters**

| Name      | Located in | Description                                                                        | Required | Schema  |
| --------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| publicKey | path       | Account publicKey.                                                                 | Yes      | string  |
| pageSize  | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id        | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 409  | invalid argument |            |

### Outgoing transactions

`GET /account/{publicKey}/transactions/outgoing`

**Summary:** Get outgoing transactions information

**Description:** Gets an array of transactions for which an account is the sender. A transaction is said to be outgoing regarding an account if the account is the sender of a transaction.

**Parameters**

| Name      | Located in | Description                                                                        | Required | Schema  |
| --------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| publicKey | path       | Account publicKey.                                                                 | Yes      | string  |
| pageSize  | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id        | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 409  | invalid argument |            |

### Confirmed transactions

`GET /account/{publicKey}/transactions`

**Summary:** Get confirmed transactions information

**Description:** Gets an array of confirmed transaction for which an account is signer or recipient.

**Parameters**

| Name      | Located in | Description                                                                        | Required | Schema  |
| --------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| publicKey | path       | Account publicKey.                                                                 | Yes      | string  |
| pageSize  | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id        | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 409  | invalid argument |            |

### Unconfirmed transactions

`GET /account/{publicKey}/transactions/unconfirmed`

##### **_GET_**

**Summary:** Get unconfirmed transactions information

**Description:** Gets the array of transactions for which an account is the sender or receiver and which have not yet been included in a block.

**Parameters**

| Name      | Located in | Description                                                                        | Required | Schema  |
| --------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| publicKey | path       | Account publicKey.                                                                 | Yes      | string  |
| pageSize  | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id        | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 409  | invalid argument |            |

`GET /account/{publicKey}/transactions/partial`

**Summary:** Get aggregate bonded transactions information

**Description:** Gets an array of aggregate bonded transactions for which an account is the sender or has signed the transaction. A transaction is said to be aggregate bonded regarding an account if announced but there are missing signatures.

**Parameters**

| Name      | Located in | Description                                                                        | Required | Schema  |
| --------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| publicKey | path       | Account publicKey.                                                                 | Yes      | string  |
| pageSize  | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id        | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 409  | invalid argument |            |

### Multisig account

`GET /account/{accountId}/multisig`

**Summary:** Get multisig account information

**Description:** Returns MultisigAccountInfo for an account.

**Parameters**

| Name      | Located in | Description                    | Required | Schema |
| --------- | ---------- | ------------------------------ | -------- | ------ |
| accountId | path       | Account address or public key. | Yes      | string |

**Responses**

| Code | Description        | Schema                                            |
| ---- | ------------------ | ------------------------------------------------- |
| 200  | success            | [MultisigAccountInfoDTO](#multisigaccountinfodto) |
| 404  | resource not found |                                                   |
| 409  | invalid argument   |                                                   |

### Multisig account graph

`GET /account/{accountId}/multisig/graph`

**Summary:** Get multisig account graph information

**Description:** Returns MultisigAccountGraphInfo for an account.

**Parameters**

| Name      | Located in | Description                    | Required | Schema |
| --------- | ---------- | ------------------------------ | -------- | ------ |
| accountId | path       | Account address or public key. | Yes      | string |

**Responses**

| Code | Description        | Schema                                                          |
| ---- | ------------------ | --------------------------------------------------------------- |
| 200  | success            | [ [MultisigAccountGraphInfoDTO](#multisigaccountgraphinfodto) ] |
| 404  | resource not found |                                                                 |
| 409  | invalid argument   |                                                                 |

### Namespace by account id

`GET /account/{accountId}/namespaces`

**Summary:** Get namespaces an account owns

**Description:** Returns an array of NamespaceInfo for an account.

**Parameters**

| Name      | Located in | Description                                                                      | Required | Schema  |
| --------- | ---------- | -------------------------------------------------------------------------------- | -------- | ------- |
| accountId | path       | Account address or public key.                                                   | Yes      | string  |
| pageSize  | query      | The number of namespaces to return.                                              | No       | integer |
| id        | query      | Identifier of the namespace after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema                                    |
| ---- | ---------------- | ----------------------------------------- |
| 200  | success          | [ [NamespaceInfoDTO](#namespaceinfodto) ] |
| 409  | invalid argument |                                           |

### Namespace by account address

`POST /account/namespaces`

**Summary:** Get namespaces information

**Description:** Returns an array of NamespaceInfo for a given set of addresses.

**Parameters**

| Name      | Located in | Description                                                                      | Required | Schema                  |
| --------- | ---------- | -------------------------------------------------------------------------------- | -------- | ----------------------- |
| addresses | body       | Accounts address array.                                                          | Yes      | [addresses](#addresses) |
| pageSize  | query      | The number of namespaces to return.                                              | No       | integer                 |
| id        | query      | Identifier of the namespace after which we want the transactions to be returned. | No       | string                  |

**Responses**

| Code | Description      | Schema                                    |
| ---- | ---------------- | ----------------------------------------- |
| 200  | success          | [ [NamespaceInfoDTO](#namespaceinfodto) ] |
| 400  | invalid content  |                                           |
| 409  | invalid argument |                                           |

# Blocks

### Block information

`GET /block/{height}`

**Summary:** Get block information

**Description:** Returns BlockInfo for a given block height.

**Parameters**

| Name   | Located in | Description   | Required | Schema |
| ------ | ---------- | ------------- | -------- | ------ |
| height | path       | Block height. | Yes      | long   |

**Responses**

| Code | Description        | Schema                        |
| ---- | ------------------ | ----------------------------- |
| 200  | success            | [BlockInfoDTO](#blockinfodto) |
| 404  | resource not found |                               |
| 409  | invalid argument   |                               |

### Request block height

`GET /blocks/{height}/limit/{limit}`

**Summary:** Get blocks information

**Description:** Returns an array of BlockInfo for a given block height and limit.

**Parameters**

| Name   | Located in | Description                                | Required | Schema        |
| ------ | ---------- | ------------------------------------------ | -------- | ------------- |
| height | path       | Block height.                              | Yes      | long          |
| limit  | path       | Number of following blocks to be returned. | Yes      | integer (int) |

**Responses**

| Code | Description      | Schema                            |
| ---- | ---------------- | --------------------------------- |
| 200  | success          | [ [BlockInfoDTO](#blockinfodto) ] |
| 409  | invalid argument |                                   |

### Get transactions

`GET /block/{height}/transactions`

**Summary:** Get transactions from a block

**Description:** Returns array of transactions included in a block for a block height.

**Parameters**

| Name     | Located in | Description                                                                        | Required | Schema  |
| -------- | ---------- | ---------------------------------------------------------------------------------- | -------- | ------- |
| height   | path       | Block height                                                                       | Yes      | long    |
| pageSize | query      | The number of transactions to return. Should be between 10 and 100, otherwise 10.  | No       | integer |
| id       | query      | Identifier of the transaction after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description        | Schema     |
| ---- | ------------------ | ---------- |
| 200  | success            | [ object ] |
| 404  | resource not found |            |
| 409  | invalid argument   |            |

# Chain

### Height

`GET /chain/height`

**Summary:** Get the current height of the chain

**Description:** Returns the current blockchain height.

**Responses**

| Code | Description | Schema                  |
| ---- | ----------- | ----------------------- |
| 200  | success     | [HeightDTO](#heightdto) |

### Score

`GET /chain/score`

**Summary:** Get the current score of the chain

**Description:** Returns the current chain score.

**Responses**

| Code | Description | Schema                                    |
| ---- | ----------- | ----------------------------------------- |
| 200  | success     | [BlockchainScoreDTO](#blockchainscoredto) |

# Diagnostic

### Storage info

`GET /diagnostic/storage`

**Summary:** Get the storage information

**Description:** Returns statistical information about the blockchain.

**Responses**

| Code | Description | Schema                                                |
| ---- | ----------- | ----------------------------------------------------- |
| 200  | success     | [BlockchainStorageInfoDTO](#blockchainstorageinfodto) |

# Mosaic

### Mosaic information

`GET /mosaic/{mosaicId}`

**Summary:** Get mosaic information

**Description:** Returns MosaicInfo for a given mosaicId.

**Parameters**

| Name     | Located in | Description        | Required | Schema |
| -------- | ---------- | ------------------ | -------- | ------ |
| mosaicId | path       | Mosaic identifier. | Yes      | string |

**Responses**

| Code | Description        | Schema                          |
| ---- | ------------------ | ------------------------------- |
| 200  | success            | [MosaicInfoDTO](#mosaicinfodto) |
| 404  | resource not found |                                 |
| 409  | invalid argument   |                                 |

### Mosaic list

`POST /mosaic`

**Summary:** Get information for a set of mosaics

**Description:** Returns MosaicInfo for a given set of mosaicIds.

**Parameters**

| Name      | Located in | Description         | Required | Schema                  |
| --------- | ---------- | ------------------- | -------- | ----------------------- |
| mosaicIds | body       | Array of mosaicIds. | Yes      | [mosaicIds](#mosaicids) |

**Responses**

| Code | Description      | Schema                              |
| ---- | ---------------- | ----------------------------------- |
| 200  | success          | [ [MosaicInfoDTO](#mosaicinfodto) ] |
| 400  | invalid content  |                                     |
| 409  | invalid argument |

### Mosaic name

`POST /mosaic/names`

**Summary:** Get readable names for a set of mosaics

**Description:** Returns names for mosaics.

**Parameters**

| Name      | Located in | Description         | Required | Schema                  |
| --------- | ---------- | ------------------- | -------- | ----------------------- |
| mosaicIds | body       | Array of mosaicIds. | Yes      | [mosaicIds](#mosaicids) |

**Responses**

| Code | Description      | Schema                              |
| ---- | ---------------- | ----------------------------------- |
| 200  | success          | [ [MosaicNameDTO](#mosaicnamedto) ] |
| 400  | invalid content  |                                     |
| 409  | invalid argument |                                     |
|      |

# Namespace

#### /namespace/{namespaceId}/mosaics

`GET /namespace/{namespaceId}/mosaics`

**Summary:** Get mosaics information.

**Description:** Returns an array of MosaicInfo from mosaics created under provided namespace.

**Parameters**

| Name        | Located in | Description                                                                   | Required | Schema  |
| ----------- | ---------- | ----------------------------------------------------------------------------- | -------- | ------- |
| namespaceId | path       | Namespace identifier.                                                         | Yes      | string  |
| pageSize    | query      | The number of mosaics to return.                                              | No       | integer |
| id          | query      | Identifier of the mosaic after which we want the transactions to be returned. | No       | string  |

**Responses**

| Code | Description      | Schema                              |
| ---- | ---------------- | ----------------------------------- |
| 200  | success          | [ [MosaicInfoDTO](#mosaicinfodto) ] |
| 409  | invalid argument |                                     |

### Namespace information

`GET /namespace/{namespaceId}`

**Summary:** Get namespace information

**Description:** Returns NamespaceInfo for a given namespaceId.

**Parameters**

| Name        | Located in | Description           | Required | Schema |
| ----------- | ---------- | --------------------- | -------- | ------ |
| namespaceId | path       | Namespace identifier. | Yes      | string |

**Responses**

| Code | Description        | Schema                                |
| ---- | ------------------ | ------------------------------------- |
| 200  | success            | [NamespaceInfoDTO](#namespaceinfodto) |
| 404  | resource not found |                                       |
| 409  | invalid argument   |                                       |

### Namespace list

`POST /namespace/names`

**Summary:** Get readable names for a set of namespaces

**Description:** Returns names for namespaces.

**Parameters**

| Name         | Located in | Description            | Required | Schema                        |
| ------------ | ---------- | ---------------------- | -------- | ----------------------------- |
| namespaceIds | body       | Array of namespaceIds. | Yes      | [namespaceIds](#namespaceids) |

**Responses**

| Code | Description      | Schema                                    |
| ---- | ---------------- | ----------------------------------------- |
| 200  | success          | [ [NamespaceNameDTO](#namespacenamedto) ] |
| 400  | invalid content  |                                           |
| 409  | invalid argument |                                           |

# Transaction

### Transaction information

`GET /transaction/{transactionId}`

**Summary:** Get transaction information

**Description:** Returns transaction given its transactionId or hash.

**Parameters**

| Name          | Located in | Description            | Required | Schema |
| ------------- | ---------- | ---------------------- | -------- | ------ |
| transactionId | path       | TransactionId or hash. | Yes      | string |

**Responses**

| Code | Description        | Schema |
| ---- | ------------------ | ------ |
| 200  | success            | object |
| 404  | resource not found |        |
| 409  | invalid argument   |        |

### Transaction list

`POST /transaction`

**Summary:** Get transactions information

**Description:** Returns transaction information for a given set of transactionId or hash.

**Parameters**

| Name           | Located in | Description                        | Required | Schema                            |
| -------------- | ---------- | ---------------------------------- | -------- | --------------------------------- |
| transactionIds | body       | Array of transactionIds or hashes. | Yes      | [transactionIds](#transactionids) |

**Responses**

| Code | Description      | Schema     |
| ---- | ---------------- | ---------- |
| 200  | success          | [ object ] |
| 400  | invalid content  |            |
| 409  | invalid argument |            |

##### **_PUT_**

**Summary:** Announce a new transaction

**Description:** Announces a transaction to the network.

**Parameters**

| Name    | Located in | Description          | Required | Schema                                    |
| ------- | ---------- | -------------------- | -------- | ----------------------------------------- |
| payload | body       | Transaction payload. | Yes      | [transactionPayload](#transactionpayload) |

**Responses**

| Code | Description      | Schema |
| ---- | ---------------- | ------ |
| 202  | success          | object |
| 400  | invalid content  |        |
| 409  | invalid argument |        |

### Announce ABT

`PUT /transaction/partial`

**Summary:** Announce an aggregate bonded transaction

**Description:** Announces an aggregate bonded transaction to the network.

**Parameters**

| Name    | Located in | Description          | Required | Schema                                    |
| ------- | ---------- | -------------------- | -------- | ----------------------------------------- |
| payload | body       | Transaction payload. | Yes      | [transactionPayload](#transactionpayload) |

**Responses**

| Code | Description      | Schema |
| ---- | ---------------- | ------ |
| 202  | success          | object |
| 400  | invalid content  |        |
| 409  | invalid argument |        |

### Announce cosignature transaction

`PUT /transaction/cosignature`

**Summary:** Announce a cosignature transaction

**Description:** Announces a cosignature transaction to the network.

**Parameters**

| Name    | Located in | Description          | Required | Schema                                    |
| ------- | ---------- | -------------------- | -------- | ----------------------------------------- |
| payload | body       | Transaction payload. | Yes      | [transactionPayload](#transactionpayload) |

**Responses**

| Code | Description      | Schema |
| ---- | ---------------- | ------ |
| 202  | success          | object |
| 400  | invalid content  |        |
| 409  | invalid argument |        |

### Transaction status

`GET /transaction/{hash}/status`

**Summary:** Get transaction status

**Description:** Returns transaction status for a given transactionId or hash.

**Parameters**

| Name | Located in | Description       | Required | Schema |
| ---- | ---------- | ----------------- | -------- | ------ |
| hash | path       | Transaction hash. | Yes      | string |

**Responses**

| Code | Description        | Schema                                        |
| ---- | ------------------ | --------------------------------------------- |
| 200  | success            | [TransactionStatusDTO](#transactionstatusdto) |
| 404  | resource not found |                                               |
| 409  | invalid argument   |                                               |

### Transaction statuses list

`POST /transaction/statuses`

**Summary:** Get transactions status.

**Description:** Returns an array of transaction statuses for a given set of transactionId or hash.

**Parameters**

| Name              | Located in | Description                        | Required | Schema                                  |
| ----------------- | ---------- | ---------------------------------- | -------- | --------------------------------------- |
| transactionHashes | body       | Array of transactionIds or hashes. | Yes      | [transactionHashes](#transactionhashes) |

**Responses**

| Code | Description      | Schema                                            |
| ---- | ---------------- | ------------------------------------------------- |
| 200  | success          | [ [TransactionStatusDTO](#transactionstatusdto) ] |
| 400  | invalid content  |                                                   |
| 409  | invalid argument |                                                   |

# Network

### Network information

`GET /network`

**Summary:** Get the current network type of the chain

**Description:** Returns the current network type.

**Responses**

| Code | Description | Schema                            |
| ---- | ----------- | --------------------------------- |
| 200  | success     | [NetworkTypeDTO](#networktypedto) |

# Models

### AccountInfoDTO

| Name    | Type                              | Description | Required |
| ------- | --------------------------------- | ----------- | -------- |
| meta    | [AccountMetaDTO](#accountmetadto) |             | Yes      |
| account | [AccountDTO](#accountdto)         |             | Yes      |

### AccountMetaDTO

| Name           | Type   | Description | Required |
| -------------- | ------ | ----------- | -------- |
| AccountMetaDTO | object |             |          |

### AccountDTO

| Name             | Type                        | Description | Required |
| ---------------- | --------------------------- | ----------- | -------- |
| address          | string                      |             | Yes      |
| addressHeight    | [UInt64DTO](#uint64dto)     |             | Yes      |
| publicKey        | string                      |             | Yes      |
| publicKeyHeight  | [UInt64DTO](#uint64dto)     |             | Yes      |
| mosaics          | [ [MosaicDTO](#mosaicdto) ] |             | Yes      |
| importance       | [UInt64DTO](#uint64dto)     |             | Yes      |
| importanceHeight | [UInt64DTO](#uint64dto)     |             | Yes      |

### MultisigAccountGraphInfoDTO

| Name            | Type                                                  | Description | Required |
| --------------- | ----------------------------------------------------- | ----------- | -------- |
| level           | integer                                               |             | Yes      |
| multisigEntries | [ [MultisigAccountInfoDTO](#multisigaccountinfodto) ] |             | Yes      |

### MultisigAccountInfoDTO

| Name     | Type                  | Description | Required |
| -------- | --------------------- | ----------- | -------- |
| multisig | [Multisig](#multisig) |             | Yes      |

### Multisig

| Name             | Type       | Description | Required |
| ---------------- | ---------- | ----------- | -------- |
| account          | string     |             | Yes      |
| accountAddress   | string     |             | No       |
| minApproval      | integer    |             | Yes      |
| minRemoval       | integer    |             | Yes      |
| cosignatories    | [ string ] |             | Yes      |
| multisigAccounts | [ string ] |             | Yes      |

### AnnounceTransactionInfoDTO

| Name    | Type   | Description | Required |
| ------- | ------ | ----------- | -------- |
| message | string |             | Yes      |

### TransactionStatusDTO

| Name     | Type                    | Description | Required |
| -------- | ----------------------- | ----------- | -------- |
| group    | string                  |             | No       |
| status   | string                  |             | Yes      |
| hash     | string                  |             | No       |
| deadline | [UInt64DTO](#uint64dto) |             | No       |
| height   | [UInt64DTO](#uint64dto) |             | No       |

### MosaicDTO

| Name   | Type                    | Description | Required |
| ------ | ----------------------- | ----------- | -------- |
| id     | [UInt64DTO](#uint64dto) |             | Yes      |
| amount | [UInt64DTO](#uint64dto) |             | Yes      |

### MosaicInfoDTO

| Name   | Type                                              | Description | Required |
| ------ | ------------------------------------------------- | ----------- | -------- |
| meta   | [NamespaceMosaicMetaDTO](#namespacemosaicmetadto) |             | Yes      |
| mosaic | [MosaicDefinitionDTO](#mosaicdefinitiondto)       |             | Yes      |

### NamespaceMosaicMetaDTO

| Name   | Type    | Description | Required |
| ------ | ------- | ----------- | -------- |
| active | boolean |             | Yes      |
| index  | integer |             | Yes      |
| id     | string  |             | Yes      |

### MosaicDefinitionDTO

| Name        | Type                                        | Description | Required |
| ----------- | ------------------------------------------- | ----------- | -------- |
| namespaceId | [UInt64DTO](#uint64dto)                     |             | Yes      |
| mosaicId    | [UInt64DTO](#uint64dto)                     |             | Yes      |
| supply      | [UInt64DTO](#uint64dto)                     |             | Yes      |
| height      | [UInt64DTO](#uint64dto)                     |             | Yes      |
| owner       | string                                      |             | Yes      |
| properties  | [MosaicPropertiesDTO](#mosaicpropertiesdto) |             | Yes      |
| levy        | object                                      |             | Yes      |

### MosaicPropertiesDTO

| Name                | Type  | Description | Required |
| ------------------- | ----- | ----------- | -------- |
| MosaicPropertiesDTO | array |             |          |

### MosaicNameDTO

| Name     | Type                    | Description | Required |
| -------- | ----------------------- | ----------- | -------- |
| parentId | [UInt64DTO](#uint64dto) |             | Yes      |
| mosaicId | [UInt64DTO](#uint64dto) |             | Yes      |
| name     | string                  |             | Yes      |

### NamespaceInfoDTO

| Name      | Type                                              | Description | Required |
| --------- | ------------------------------------------------- | ----------- | -------- |
| meta      | [NamespaceMosaicMetaDTO](#namespacemosaicmetadto) |             | Yes      |
| namespace | [NamespaceDTO](#namespacedto)                     |             | Yes      |

### NamespaceDTO

| Name         | Type                    | Description | Required |
| ------------ | ----------------------- | ----------- | -------- |
| type         | integer                 |             | Yes      |
| depth        | integer                 |             | Yes      |
| level0       | [UInt64DTO](#uint64dto) |             | Yes      |
| level1       | [UInt64DTO](#uint64dto) |             | No       |
| level2       | [UInt64DTO](#uint64dto) |             | No       |
| parentId     | [UInt64DTO](#uint64dto) |             | Yes      |
| owner        | string                  |             | Yes      |
| ownerAddress | string                  |             | No       |
| startHeight  | [UInt64DTO](#uint64dto) |             | Yes      |
| endHeight    | [UInt64DTO](#uint64dto) |             | Yes      |

### NamespaceNameDTO

| Name        | Type                    | Description | Required |
| ----------- | ----------------------- | ----------- | -------- |
| parentId    | [UInt64DTO](#uint64dto) |             | No       |
| namespaceId | [UInt64DTO](#uint64dto) |             | Yes      |
| name        | string                  |             | Yes      |

### BlockInfoDTO

| Name  | Type                          | Description | Required |
| ----- | ----------------------------- | ----------- | -------- |
| meta  | [BlockMetaDTO](#blockmetadto) |             | Yes      |
| block | [BlockDTO](#blockdto)         |             | Yes      |

### BlockMetaDTO

| Name            | Type                    | Description | Required |
| --------------- | ----------------------- | ----------- | -------- |
| hash            | string                  |             | Yes      |
| generationHash  | string                  |             | Yes      |
| totalFee        | [UInt64DTO](#uint64dto) |             | Yes      |
| numTransactions | number                  |             | Yes      |

### BlockDTO

| Name                  | Type                    | Description | Required |
| --------------------- | ----------------------- | ----------- | -------- |
| signature             | string                  |             | Yes      |
| signer                | string                  |             | Yes      |
| version               | number                  |             | Yes      |
| type                  | number                  |             | Yes      |
| height                | [UInt64DTO](#uint64dto) |             | Yes      |
| timestamp             | [UInt64DTO](#uint64dto) |             | Yes      |
| difficulty            | [UInt64DTO](#uint64dto) |             | Yes      |
| previousBlockHash     | string                  |             | Yes      |
| blockTransactionsHash | string                  |             | Yes      |

### HeightDTO

| Name   | Type                    | Description | Required |
| ------ | ----------------------- | ----------- | -------- |
| height | [UInt64DTO](#uint64dto) |             | Yes      |

### BlockchainScoreDTO

| Name      | Type                    | Description | Required |
| --------- | ----------------------- | ----------- | -------- |
| scoreHigh | [UInt64DTO](#uint64dto) |             | Yes      |
| scoreLow  | [UInt64DTO](#uint64dto) |             | Yes      |

### BlockchainStorageInfoDTO

| Name            | Type    | Description | Required |
| --------------- | ------- | ----------- | -------- |
| numBlocks       | integer |             | Yes      |
| numTransactions | integer |             | Yes      |
| numAccounts     | integer |             | Yes      |

### NetworkTypeDTO

| Name        | Type   | Description | Required |
| ----------- | ------ | ----------- | -------- |
| name        | string |             | Yes      |
| description | string |             | Yes      |

### mosaicIds

| Name      | Type       | Description | Required |
| --------- | ---------- | ----------- | -------- |
| mosaicIds | [ string ] |             | No       |

### namespaceIds

| Name         | Type       | Description | Required |
| ------------ | ---------- | ----------- | -------- |
| namespaceIds | [ string ] |             | No       |

### addresses

| Name      | Type       | Description | Required |
| --------- | ---------- | ----------- | -------- |
| addresses | [ string ] |             | No       |

### transactionIds

| Name           | Type       | Description | Required |
| -------------- | ---------- | ----------- | -------- |
| transactionIds | [ string ] |             | No       |

### transactionHashes

| Name   | Type       | Description | Required |
| ------ | ---------- | ----------- | -------- |
| hashes | [ string ] |             | No       |

### transactionPayload

| Name    | Type   | Description | Required |
| ------- | ------ | ----------- | -------- |
| payload | string |             | No       |

### UInt64DTO

| Name      | Type  | Description | Required |
| --------- | ----- | ----------- | -------- |
| UInt64DTO | array |             |          |
