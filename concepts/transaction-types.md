---
description: >-
  This section provides an overview of Mainnet supported transaction types and
  their structure.
---

# Transaction Types Overview

## Introduction

This sections describes mainnet transaction types and its structure related to `serde` process \(serialization and deserialization of transactions\).

Transactions are the heart of any blockchain, cryptocurrency or otherwise. They represent a transfer of value from one network participant to another. In ARK, transactions can be of one of multiple types, specified in AIP11, which can affect the content and data structure of each transaction's payload.

Using[ ARK SDKs](https://sdk.ark.dev), developers can employ the programming language of their choice to build applications utilizing the ARK blockchain. The ARK SDKs are split into two packages for each language: Client and Cryptography.

**Client** SDKs help developers fetch information from the ARK blockchain about its current state: which delegates are currently forging, what transactions are associated with a given wallet, and so on.

**Cryptography** SDKs, by contrast, assist developers in working with transactions: signing, serializing, deserializing, etc.

For more information about SDK implementations visit [ARK SDKs hub](https://sdk.ark.dev/).

In the following sections basic transaction types and their structure is presented. If you are interested in the signature generation process and algorithm used, please check the [Cryptography Overview](cryptography.md) page.

## Transfer Transaction Type

### No VendorField

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 0,
    "nonce": "1",
    "senderPublicKey": "03a02b9d5fdd1307c2ee4652ba54d492d1fd11a7d1bb3f3a44c4a05e79f19de933",
    "fee": "10000000",
    "amount": "100000",
    "expiration": 0,
    "recipientId": "AJWRd23HNEhPLkK1ymMnwnDBX2a7QBZqff",
    "signature": "4f01bd21828a633a3c821b9984fe642deab87237b99e62a543ca6948ff1d6d32f2475ada1f933da0591c40603693614afa69fcb4caa2b4be018788de9f10c42a",
    "id": "8c85167cb1ca6f70e350f30173deb4c0a00ce7169d04f78fe4e4bcf2c3a75214"
}
```

### Serialized Payload

```text
ff0217010000000000010000000000000003a02b9d5fdd1307c2ee4652ba54d492d1fd11a7d1bb3f3a44c4a05e79f19de933809698000000000000a08601000000000000000000171dfc69b54c7fe901e91d5a9ab78388645e2427ea4f01bd21828a633a3c821b9984fe642deab87237b99e62a543ca6948ff1d6d32f2475ada1f933da0591c40603693614afa69fcb4caa2b4be018788de9f10c42a
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0000` |
| **Nonce:** | **\[9\]** | **8** | `0x0100000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x03a02b9d5fdd1307c2ee4652ba54d492d1fd11a7d1bb3f3a44c4a05e79f19de933` |
| **Fee:** | **\[50\]** | **8** | `0x8096980000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Amount:** | **\[59\]** | **8** | `0xa086010000000000` |
| **Expiration:** | **\[67\]** | **4** | `0x00000000` |
| **Recipient:** | **\[71\]** | **21** | `0x171dfc69b54c7fe901e91d5a9ab78388645e2427ea` |
| **Signature:** | **\[92\]** | **64** | `0x4f01bd21828a633a3c821b9984fe642deab87237b99e62a543ca6948ff1d6d32f2475ada1f933da0591c40603693614afa69fcb4caa2b4be018788de9f10c42a` |

### With VendorField

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 0,
    "nonce": "2",
    "senderPublicKey": "03d59f3b7d698536f6925a77f22d484d518b06a2c09318e8e5ff487afcdedefb2c",
    "fee": "10000000",
    "amount": "1",
    "vendorFieldHex": "302e3132373131363230373030383934323434",
    "vendorField": "0.12711620700894244",
    "expiration": 0,
    "recipientId": "AUbLwNEQWMshw4vBGYyR8JWn4Lx6sJbj6M",
    "signature": "504215bf61f7e8e0d4cd7c7e1511b501367e8c2f3543972906a3b80d42cebc3e4ec974f938124661cb65eab93dacba6ba0f5045861ac28fc0287462557ffd99b",
    "id": "8bd461006dc6481c17b38f652e775d151fb36e8b3f390fb213b6b5c399df6c97"
}
```

### Serialized Payload

```text
ff0217010000000000020000000000000003d59f3b7d698536f6925a77f22d484d518b06a2c09318e8e5ff487afcdedefb2c809698000000000013302e3132373131363230373030383934323434010000000000000000000000178c9bd74222025a19063c8fca8a50c39a891feeca504215bf61f7e8e0d4cd7c7e1511b501367e8c2f3543972906a3b80d42cebc3e4ec974f938124661cb65eab93dacba6ba0f5045861ac28fc0287462557ffd99b
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0000` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x03d59f3b7d698536f6925a77f22d484d518b06a2c09318e8e5ff487afcdedefb2c` |
| **Fee:** | **\[50\]** | **8** | `0x8096980000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x13` |
| **VendorField:** | **\[59\]** | **19** | `0x302e3132373131363230373030383934323434` |
| **Amount:** | **\[78\]** | **8** | `0x0100000000000000` |
| **Expiration:** | **\[86\]** | **4** | `0x00000000` |
| **Recipient:** | **\[90\]** | **21** | `0x178c9bd74222025a19063c8fca8a50c39a891feeca` |
| **Signature:** | **\[111\]** | **64** | `0x504215bf61f7e8e0d4cd7c7e1511b501367e8c2f3543972906a3b80d42cebc3e4ec974f938124661cb65eab93dacba6ba0f5045861ac28fc0287462557ffd99b` |

## Second Signature Registration

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 1,
    "nonce": "2",
    "senderPublicKey": "02e0c063777427ac196af3c426fd648231ebc4ea06fff5edb1652b98f9c8420c69",
    "fee": "500000000",
    "amount": "0",
    "asset": {
        "signature": {
            "publicKey": "02877e4f35c76abaeb152b128670db0a7ae10b3999afcd28a42938b653fbf87ae9"
        }
    },
    "signature": "adb983dd28827860f69c6a98b2f9db88a9e084cc7fe3a691463377c3225b02fee24547b516d1cf05f2f77b65a9c36069f6540605c01694008e2a5cb4fc88f62f",
    "id": "4c2cd8c4281a34a60505f260d067e5c678d3c57510bfbcda24c5e0da5f46bd5e"
}
```

### Serialized Payload

```text
ff0217010000000100020000000000000002e0c063777427ac196af3c426fd648231ebc4ea06fff5edb1652b98f9c8420c690065cd1d000000000002877e4f35c76abaeb152b128670db0a7ae10b3999afcd28a42938b653fbf87ae9adb983dd28827860f69c6a98b2f9db88a9e084cc7fe3a691463377c3225b02fee24547b516d1cf05f2f77b65a9c36069f6540605c01694008e2a5cb4fc88f62f
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0100` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x02e0c063777427ac196af3c426fd648231ebc4ea06fff5edb1652b98f9c8420c69` |
| **Fee:** | **\[50\]** | **8** | `0x0065cd1d00000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Second PublicKey:** | **\[59\]** | **8** | `0x02877e4f35c76abaeb152b128670db0a7ae10b3999afcd28a42938b653fbf87ae9` |
| **Signature:** | **\[67\]** | **64** | `0xadb983dd28827860f69c6a98b2f9db88a9e084cc7fe3a691463377c3225b02fee24547b516d1cf05f2f77b65a9c36069f6540605c01694008e2a5cb4fc88f62f` |

## Delegate Registration

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 2,
    "nonce": "2",
    "senderPublicKey": "02a574b8995542631976691a7f73b59e4700cd84badb831331ab18ae2113a184ba",
    "fee": "2500000000",
    "amount": "0",
    "asset": {
        "delegate": {
            "username": "02a574b8995542631976"
        }
    },
    "signature": "f2cf8acf6ccb71fa0e848ca185a93e6ff44e0dd266b08c4bc0dfc7984499acd759f6067ace6bb00eae404eafa6af3548f5d35f8727f4ddeba69b6d925c604338",
    "id": "9b232e31c6385a2c730f5bec3c0220da6a184320e6c38bd7b6fd5a18b8501472"
}
```

### Serialized Payload

```text
ff0217010000000200020000000000000002a574b8995542631976691a7f73b59e4700cd84badb831331ab18ae2113a184ba00f902950000000000143032613537346238393935353432363331393736f2cf8acf6ccb71fa0e848ca185a93e6ff44e0dd266b08c4bc0dfc7984499acd759f6067ace6bb00eae404eafa6af3548f5d35f8727f4ddeba69b6d925c604338
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0200` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x02a574b8995542631976691a7f73b59e4700cd84badb831331ab18ae2113a184ba` |
| **Fee:** | **\[50\]** | **8** | `0x00f9029500000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Username Length:** | **\[59\]** | **1** | `0x14` |
| **Username:** | **\[60\]** | **20** | `0x3032613537346238393935353432363331393736` |
| **Signature:** | **\[80\]** | **64** | `0xf2cf8acf6ccb71fa0e848ca185a93e6ff44e0dd266b08c4bc0dfc7984499acd759f6067ace6bb00eae404eafa6af3548f5d35f8727f4ddeba69b6d925c604338` |

## Vote Transaction

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 3,
    "nonce": "2",
    "senderPublicKey": "02555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d",
    "fee": "100000000",
    "amount": "0",
    "asset": {
        "votes": [
            "+02555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d"
        ]
    },
    "signature": "77a40e4b4170ce613c8f9ccc0650887349330a9a8b459189ee379c88cf2c8506d65aa3ca8293705373f1bde8d6b27e5071de1785ac9c0182f41e364f8f9e3b64",
    "id": "fd59eaa4a2bbb3570c7b01ad464c968aa9bf73a40e0417c802ab30553ded8476"
}
```

### Serialized Payload

```text
ff0217010000000300020000000000000002555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d00e1f5050000000000010102555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d77a40e4b4170ce613c8f9ccc0650887349330a9a8b459189ee379c88cf2c8506d65aa3ca8293705373f1bde8d6b27e5071de1785ac9c0182f41e364f8f9e3b64
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0300` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x02555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d` |
| **Fee:** | **\[50\]** | **8** | `0x00e1f50500000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Number of Votes:** | **\[59\]** | **1** | `0x01` |
| **Vote:** | **\[60\]** | **34** | `0x0102555806bca6737eaeaff6434d5171bac8aeb72533ed9bafb280dd11b328a3822d` |
| **Signature:** | **\[94\]** | **64** | `0x77a40e4b4170ce613c8f9ccc0650887349330a9a8b459189ee379c88cf2c8506d65aa3ca8293705373f1bde8d6b27e5071de1785ac9c0182f41e364f8f9e3b64` |

## MultiSignature Transaction

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 4,
    "nonce": "2",
    "senderPublicKey": "03b593aa66b53525c5399b4af5a4f583dede1c2a46176c6796a7284ee9c0a1167f",
    "fee": "2000000000",
    "amount": "0",
    "asset": {
        "multiSignature": {
            "publicKeys": [
                "037eaa8cb236c40a08fcb9d6220743ee6ae1b5c40e8a77a38f286516c3ff663901",
                "0301fd417566397113ba8c55de2f093a572744ed1829b37b56a129058000ef7bce",
                "0209d3c0f68994253cee24b23df3266ba1f0ca2f0666cd69a46544d63001cdf150"
            ],
            "min": 2
        }
    },
    "signature": "16b09ed47ce05cc9096b87b73008f73aa51d4ddc8713d4ca0fcbcabeacfd738e0181201d55a92d5b2978d0c458684489cf133d18c521fbec431dd759d16bedbb",
    "signatures": [
        "004495d593cfb8be3293e2473acf504870d2dcf71dbee7620270e136ed63c5eef259099d225f7866178968f0c3581509d92d902914674c8f86b99eb55aaa97586e",
        "0171d86f3f6552b237dd81272a7b0da7718c4d26682255223dcf1928174082ce72b07218162938c674afe741119650135338eb3da159e0626ddab6b7851882e08b",
        "02d44d9bde77c9ea02d3516ab3263a77f4f9fbb90c30b47eba7a8bb87325edeb78dd69f914f28426e6ff661c4bc001f253130f4e7eb092a9131c8ca69dbfaff32f"
    ],
    "id": "46343c36bf7497b68e14d4c0fd713e41a737841b6a858fa41ef0eab6c4647938",
    "MultiSignatureAddress": "ATp6gFCEu4P1TWNngyD8mvg8UYdu7kps97",
}
```

### Serialized Payload

```text
ff0217010000000400020000000000000003b593aa66b53525c5399b4af5a4f583dede1c2a46176c6796a7284ee9c0a1167f0094357700000000000203037eaa8cb236c40a08fcb9d6220743ee6ae1b5c40e8a77a38f286516c3ff6639010301fd417566397113ba8c55de2f093a572744ed1829b37b56a129058000ef7bce0209d3c0f68994253cee24b23df3266ba1f0ca2f0666cd69a46544d63001cdf15016b09ed47ce05cc9096b87b73008f73aa51d4ddc8713d4ca0fcbcabeacfd738e0181201d55a92d5b2978d0c458684489cf133d18c521fbec431dd759d16bedbb004495d593cfb8be3293e2473acf504870d2dcf71dbee7620270e136ed63c5eef259099d225f7866178968f0c3581509d92d902914674c8f86b99eb55aaa97586e0171d86f3f6552b237dd81272a7b0da7718c4d26682255223dcf1928174082ce72b07218162938c674afe741119650135338eb3da159e0626ddab6b7851882e08b02d44d9bde77c9ea02d3516ab3263a77f4f9fbb90c30b47eba7a8bb87325edeb78dd69f914f28426e6ff661c4bc001f253130f4e7eb092a9131c8ca69dbfaff32f
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0400` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x03b593aa66b53525c5399b4af5a4f583dede1c2a46176c6796a7284ee9c0a1167f` |
| **Fee:** | **\[50\]** | **8** | `0x0094357700000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Key Min:** | **\[59\]** | **1** | `0x02` |
| **Key Count:** | **\[60\]** | **1** | `0x03` |
| **Key 1:** | **\[61\]** | **33** | `0x037eaa8cb236c40a08fcb9d6220743ee6ae1b5c40e8a77a38f286516c3ff663901` |
| **Key 2:** | **\[94\]** | **33** | `0x0301fd417566397113ba8c55de2f093a572744ed1829b37b56a129058000ef7bce` |
| **Key 3:** | **\[127\]** | **33** | `0x0209d3c0f68994253cee24b23df3266ba1f0ca2f0666cd69a46544d63001cdf150` |
| **Signature:** | **\[160\]** | **64** | `0x16b09ed47ce05cc9096b87b73008f73aa51d4ddc8713d4ca0fcbcabeacfd738e0181201d55a92d5b2978d0c458684489cf133d18c521fbec431dd759d16bedbb` |
| **Signature 1 Flag:** | **\[224\]** | **1** | `0x00` |
| **Signature 1:** | **\[225\]** | **64** | `0x4495d593cfb8be3293e2473acf504870d2dcf71dbee7620270e136ed63c5eef259099d225f7866178968f0c3581509d92d902914674c8f86b99eb55aaa97586e` |
| **Signature 2 Flag:** | **\[289\]** | **1** | `0x01` |
| **Signature 2:** | **\[290\]** | **64** | `0x71d86f3f6552b237dd81272a7b0da7718c4d26682255223dcf1928174082ce72b07218162938c674afe741119650135338eb3da159e0626ddab6b7851882e08b` |
| **Signature 3 Flag:** | **\[354\]** | **1** | `0x02` |
| **Signature 3:** | **\[355\]** | **64** | `0xd44d9bde77c9ea02d3516ab3263a77f4f9fbb90c30b47eba7a8bb87325edeb78dd69f914f28426e6ff661c4bc001f253130f4e7eb092a9131c8ca69dbfaff32f` |

## IPFS Transaction

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 5,
    "nonce": "2",
    "senderPublicKey": "038e000c902d4551065ac5705637c685d52e6ac4032e158ad0370c5ef2bbafae2c",
    "fee": "500000000",
    "amount": "0",
    "asset": {
        "ipfs": "QmYSK2JyM3RyDyB52caZCTKFR3HKniEcMnNJYdk8DQ6KKB"
    },
    "signature": "ed8e729b40e73ab86c3b6675d463c19d88495bf4e091037e80352afe0ea29efff04d2667bfe8d78e5c4ad410fb0f7a0f511fbd657a54181aca8de4e8c6ebfe2c",
    "id": "77d8134144780e50db71adb496e02bcbde43e76a0cd7eeae7ff3641db75187ec",
}
```

### Serialized Payload

```text
ff02170100000005000200000000000000038e000c902d4551065ac5705637c685d52e6ac4032e158ad0370c5ef2bbafae2c0065cd1d000000000012209608184d6cee2b9af8e6c2a46fc9318adf73329aeb8a86cf8472829fff5bb89eed8e729b40e73ab86c3b6675d463c19d88495bf4e091037e80352afe0ea29efff04d2667bfe8d78e5c4ad410fb0f7a0f511fbd657a54181aca8de4e8c6ebfe2c
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **TypeGroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0500` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x038e000c902d4551065ac5705637c685d52e6ac4032e158ad0370c5ef2bbafae2c` |
| **Fee:** | **\[50\]** | **8** | `0x0065cd1d00000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **IPFS Hash:** | **\[59\]** | **34** | `0x12209608184d6cee2b9af8e6c2a46fc9318adf73329aeb8a86cf8472829fff5bb89e` |
| **Signature:** | **\[93\]** | **64** | `0xed8e729b40e73ab86c3b6675d463c19d88495bf4e091037e80352afe0ea29efff04d2667bfe8d78e5c4ad410fb0f7a0f511fbd657a54181aca8de4e8c6ebfe2c` |

### IPFS Hash Breakdown

| Item | Length | Value |
| :--- | :---: | :--- |
| **IPFS Hash** | **46** _**\(chars\)**_ | `QmYSK2JyM3RyDyB52caZCTKFR3HKniEcMnNJYdk8DQ6KKB` |
| **Decoded Base58** | **34** _**\(bytes\)**_ | `0x12209608184d6cee2b9af8e6c2a46fc9318adf73329aeb8a86cf8472829fff5bb89e` |
| **Hash Type** | **1** _**\(byte\)**_ | `0x12` |
| **Hash Length** | **1** _**\(byte\)**_ | `0x20` |
| **32-Byte Hash** | **32** _**\(bytes\)**_ | `0x9608184d6cee2b9af8e6c2a46fc9318adf73329aeb8a86cf8472829fff5bb89e` |

## MultiPayment Transaction

## Signed Json Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 6,
    "nonce": "2",
    "senderPublicKey": "02a53371b23f991740f968e3d96de42a67b4242e267cad8050ae4b68bf9ac20af2",
    "fee": "10000000",
    "amount": "0",
    "asset": {
        "payments": [
            { "amount": "1", "recipientId": "AJkSjZPqRFksw6CDyCrAqPqpRzTJ9y2JVg" },
            { "amount": "1", "recipientId": "AdmKdL2yUHa2wEq1QajidRMD5KAQ92HY1p" },
            { "amount": "1", "recipientId": "AQUBtovaVuwDuHSrjLZRbPzhuDGMp7iUje" },
            { "amount": "1", "recipientId": "AQBCwmStjJAhc665FD81swaot6NMKDmWSe" },
            { "amount": "1", "recipientId": "AZUet7svbkQ54EhkXjtHFQuz1G8Hg3k29o" },
            { "amount": "1", "recipientId": "AZy7zpA7d61Zxy51nhrVUEK52LX9dxNhwE" },
            { "amount": "1", "recipientId": "AJi63aGakFJo4aYcH5U5s3HUzmx5B31tqA" },
            { "amount": "1", "recipientId": "ARbzRpB4uQsMwjXqohA1bURVNrURHWcbRB" },
            { "amount": "1", "recipientId": "AFqBJKjoGiMBiaUA5ZvuaoHCtsAtVaYfiQ" },
            { "amount": "1", "recipientId": "AZ9W5GCvLjYn86uS4gVvLF3dUeff7Sm7kZ" },
            { "amount": "1", "recipientId": "ALetETJv5kUDaXxGyqgfbvCAq7Xd4LkNcR" },
            { "amount": "1", "recipientId": "AHNAYaC9SoWBtyiHYs8BoY6dkrFc8e1r6t" },
            { "amount": "1", "recipientId": "APHZ1wBFg2CtYSxUEoVztzrPXpjZWB7Ed3" },
            { "amount": "1", "recipientId": "ASYHnawx4LYnS3qgEshPXg1ovAMgqPvMyd" },
            { "amount": "1", "recipientId": "AJ3rQcLRmfu8myq3Riob1P1PhwoTmx1uGM" },
            { "amount": "1", "recipientId": "AdaRMae1p4XuyniQSwEF7KJMTzTDjLEtrA" },
            { "amount": "1", "recipientId": "ARXPxwvq3NzHd2h9SiGbnxB3WEHhcf3m9r" },
            { "amount": "1", "recipientId": "ATKBDzyWYJ1EWDLypzN7pP1KiTtmMYWRAd" },
            { "amount": "1", "recipientId": "AUVnmcZ3BaBTcNcp1TANSXeQqeCJnL5ajG" },
            { "amount": "1", "recipientId": "AJyp9HagSbNGo587BX37yhm6bYvJqmhfDq" },
            { "amount": "1", "recipientId": "AKVSJqTpPEPp7hrwuMfuSAzEUbRBFMivsD" },
            { "amount": "1", "recipientId": "AXVUG59zkbnGXCsVZjHN8WvX1tjEhuaJbH" },
            { "amount": "1", "recipientId": "AM6GrCiESsELYsaSxUXtLzBrZo1SGu9RGs" },
            { "amount": "1", "recipientId": "AKqaDdoNpMU234jm8tocn8rP13paJcLhc7" },
            { "amount": "1", "recipientId": "APRgmUz1jjcDqGMN9jju9DC1ZEeUE9AywY" },
            { "amount": "1", "recipientId": "AcHeBGLwiPU2X8wzVPLon1WpkpokP4Wohq" },
            { "amount": "1", "recipientId": "AWgKzu21eySyu7iqyYjWa2EfpFA7mZvQZU" },
            { "amount": "1", "recipientId": "AcKhDtSsyr9Q863PDEV5myZFChKCPfyD18" },
            { "amount": "1", "recipientId": "Ae6T9ZUTR6RSCoGD6CnhB9yVyYX7QsrZbA" },
            { "amount": "1", "recipientId": "AUDuhQsp3eCPwYxAbJa49DouCjjXtpzjjG" },
            { "amount": "1", "recipientId": "APf4R1acVovfZiccBCPLYwrcbYZPUeGKcC" },
            { "amount": "1", "recipientId": "Ab36vcphZSgPo3TfRxRUM9mgjE3D6Rcqve" },
            { "amount": "1", "recipientId": "Aai1yVoVAJcwzza8Kh9q2X7UCYHWRRsjHP" },
            { "amount": "1", "recipientId": "ATEi5aLWNrXCtLSEBwEUFJ9a3NdU2L5Cx3" },
            { "amount": "1", "recipientId": "AdxVQZpf2EZoEzr8dCY81wcGRBKksqt9uJ" },
            { "amount": "1", "recipientId": "AGvec84izZTQ4EkDdSQHdn6eQ8WHAXbRK8" },
            { "amount": "1", "recipientId": "AL7Cmvd2LukSvzUFLB729wfgfjxkFrwxKK" },
            { "amount": "1", "recipientId": "AK8sqUy3jNc1YD9rEQaHEeMmt4KkFWbiKL" },
            { "amount": "1", "recipientId": "AcZBzGrciGZQrChYdqEpRxUT28G2uEUddY" },
            { "amount": "1", "recipientId": "AaSPkSNxtsKRspwvWtvc8gvmRME5aASaEx" },
            { "amount": "1", "recipientId": "ARAjyStxuU45PqLH6kzQMrAJEqc89qZVzV" },
            { "amount": "1", "recipientId": "AdnoS6ZA7sE384pRamg9sdqC6cxjkD7pg3" },
            { "amount": "1", "recipientId": "AXH4hXPpFkRJU3HbGUUFsDbVEGxwcQLmhA" },
            { "amount": "1", "recipientId": "AX3xKYm66DeJqXUEbVeZytT8Lf6GQf4koL" },
            { "amount": "1", "recipientId": "AW7wPm9Pw3oMwBzpq24VLEwYk9CoMmYh9h" },
            { "amount": "1", "recipientId": "AapstTvRBRUWsxhEna4QC3w91sF7fKiEyC" },
            { "amount": "1", "recipientId": "AFoSv2fJK1neaNJvRDJ2bnxRUbcT8BLpxd" },
            { "amount": "1", "recipientId": "AaEQy4PNo69MWuQxBjYPv5fbX9ffj6eGxo" },
            { "amount": "1", "recipientId": "APfMoW1D7nyYjCas77UjXYG1r4ae5Z8egK" },
            { "amount": "1", "recipientId": "AdyTCFa57K44vzUHMe3cAZzN5LughnEnk1" },
            { "amount": "1", "recipientId": "AU5UYf4ARSzPVcZmEEoxygmbMFypJQU7ns" },
            { "amount": "1", "recipientId": "ALXjSdt8Bis4avRZGmUU4Kfd9D3hH4mxta" },
            { "amount": "1", "recipientId": "ALNkATjVhskN1cqnLjLYGUKxFivMTWRbR4" },
            { "amount": "1", "recipientId": "AcBKDRDbfek1ZdmP2Hz5zNyprU3bHVNZfe" },
            { "amount": "1", "recipientId": "Ab2MNhvrBGgK7ropw43sC4mXzcdiSzW8hN" },
            { "amount": "1", "recipientId": "AVMBceVMRPeZgM83qpdpQ1ytyTPCowi1F5" },
            { "amount": "1", "recipientId": "AJJNxLu5M9oPVMkx8etDPRcNs4tFaDURsz" },
            { "amount": "1", "recipientId": "AGRapiHRcPnwo3MvASwrQLppM5MKGUAHqs" },
            { "amount": "1", "recipientId": "AehS4gnFTzfnkmJqre4a5kn2sze3H28MYY" },
            { "amount": "1", "recipientId": "APQJh9sF2wZ7cDy4R3FUiepqPnefP1ByR4" },
            { "amount": "1", "recipientId": "AHVSsxZ7x7rbHEszpBzonMVYxJdRXpQX5x" },
            { "amount": "1", "recipientId": "AJ2QEu7gpzG5WkYxA7c82ojPLWMvYhpu4d" },
            { "amount": "1", "recipientId": "AMckjhZaJxoJwNke4pf43sYXBoS8xxGW3Z" },
            { "amount": "1", "recipientId": "AMutAXid6DPedsbgD6ZdSQEk1bh7ki7j5z" },
            { "amount": "1", "recipientId": "AG1RfaaZwqB8KDpFfJj75kLF1mwSAyh7jQ" },
            { "amount": "1", "recipientId": "AZebGuQaDQKWqztxoUuFyQ7jSKEobjDEtF" },
            { "amount": "1", "recipientId": "AeijCQzpk7HYpaHXS1f15TaLuHnLiqJ3td" },
            { "amount": "1", "recipientId": "AZNu9h6RTxHtMAFfH3NqLJQ7MMEr11b4jH" },
            { "amount": "1", "recipientId": "Aek93NcQX2XoEAUut4rdbWkuC4At8FQNgP" },
            { "amount": "1", "recipientId": "AK9xvxKkYJbJra2FCdYMyk4YpCBawTDqzP" },
            { "amount": "1", "recipientId": "APUvdtL5vRU4p672gkXBmk1jB7WsfnAjcg" },
            { "amount": "1", "recipientId": "ANhh6BPh8FerPGdAoEy1ZTg6XXRrWDLvGG" },
            { "amount": "1", "recipientId": "AXnsAa9Xfsmv4yR27zq3sKpwhzFASdQqHS" },
            { "amount": "1", "recipientId": "ANLKvT56LBvj6FX5bsvHLcEcFcrZgdYUhL" },
            { "amount": "1", "recipientId": "ARsEFbgLn8c76PbfaQ6NybuUSNBLx2WTFz" },
            { "amount": "1", "recipientId": "AU6JgpZeCEMACmHuDHE4KgDuNbodPLNTQj" },
            { "amount": "1", "recipientId": "AezxGoySwd5mzapEudihsPxTRC9N3mje65" },
            { "amount": "1", "recipientId": "ASu9fJ97gfwEV1BbUJQ8v6jvjehGsx7MhB" },
            { "amount": "1", "recipientId": "AcP6Mv39rvvJh2Pm2sZJb8eVRkPLdFnk31" },
            { "amount": "1", "recipientId": "AM89Z5L92EPGcntXRgjeBjaC6bvXhuXhsf" },
            { "amount": "1", "recipientId": "AdBxDtBWULrx9oi8Vw8PASg2vsAMBkfu8N" },
            { "amount": "1", "recipientId": "AYuHPh1PYkAQmWoPxFCBFkarXuHZQzr6q8" },
            { "amount": "1", "recipientId": "AHki3X6Y9oD2aC48C7nYJxBXtQrEDavw1C" },
            { "amount": "1", "recipientId": "AYsF7goWELTH1yWNHV7NuPQLFYh8Wewsy3" },
            { "amount": "1", "recipientId": "AQ4r535GMJBq9YGWNy7ZWmmiKezLPPKKVB" },
            { "amount": "1", "recipientId": "AJWMxAj163ZKE3K8oq8oGJQpsr7QhXcFjG" },
            { "amount": "1", "recipientId": "APEniF2gdeLLKL8WYwgLcp5HjebYUxpd3m" },
            { "amount": "1", "recipientId": "AeRb1mGCAus2KuR2EaaeDCs1eJSotnnSVJ" },
            { "amount": "1", "recipientId": "ALNbbL6qhRg1NmRhBBCeWNscZgdtD9FN5J" },
            { "amount": "1", "recipientId": "AMdWG71SKHgcNtwQNHYVUqmKSMTPpBDRe6" },
            { "amount": "1", "recipientId": "ASN6yDJPqAo2j2NkY4aakTSRuTVuJtgTnY" },
            { "amount": "1", "recipientId": "AFqD175UbMhHeaEJsoGpoFSyWwbpWLD7Z3" },
            { "amount": "1", "recipientId": "ALaWGuGcq6gb11Gf8rZx2LBwDHEtAAjR39" },
            { "amount": "1", "recipientId": "AJMtGbZudwPjmeUA2JtaFBbcp4aMNGEpmw" },
            { "amount": "1", "recipientId": "AWJUMu5Re8V7HjnDruAiPsVGaVyPiFt9PS" },
            { "amount": "1", "recipientId": "ATJaqBbP9BQFnjBhztVwSJnWx5stV4STVY" },
            { "amount": "1", "recipientId": "ATVNCQsWRpSrSrNkN35JfYTnm2DDP1TgSe" },
            { "amount": "1", "recipientId": "AJ9Cs9czY165T1Pbqr2NE6cAkuZxjmc1mJ" },
            { "amount": "1", "recipientId": "AbvkpAvmnVfLTWpQNGgjRGPzg18NsaZvoj" },
            { "amount": "1", "recipientId": "ASQGzFRaYaznkwTyK5XnGaSXBtct75mSAA" },
            { "amount": "1", "recipientId": "AS8JK9R8CsF7TwzjgcoWur4doCtmcdSgJD" },
            { "amount": "1", "recipientId": "AdAkT5mbKyEHZqetXDUQGkATRLgyEsGr7g" },
            { "amount": "1", "recipientId": "AZhSj2JZx5aEHaKFr2RHCrhEwTGBtaR7RY" },
            { "amount": "1", "recipientId": "AK8LqchMVGTyiAhDaCb5jcvZ6SftuEEzmj" },
            { "amount": "1", "recipientId": "AXLQ6xPHxTdhZ7YZvCwSoZ4dQ7E3qXVtWH" },
            { "amount": "1", "recipientId": "AQGeF1NLTyP5zraBCdjTdsodJCnPWR2xxZ" },
            { "amount": "1", "recipientId": "AH4b7u5gFWh7Uu4TNVD1NfETqEByxaRJNY" },
            { "amount": "1", "recipientId": "AXYdBaj8hKaqHp7kUB1LSbkdDV9vSAbpLv" },
            { "amount": "1", "recipientId": "AbU2225mM8941Fsp1K4GcVtVeEizzGsu18" },
            { "amount": "1", "recipientId": "AGNRPoJf6GmzEyaWjNV5Du63ueVdeNnb7C" },
            { "amount": "1", "recipientId": "AW732HLfot4iGJnAcvJmBshUKZHfGy5mw1" },
            { "amount": "1", "recipientId": "AWMhtF3uJiNACNAfvmzrGKhgjSHTUFbTn1" },
            { "amount": "1", "recipientId": "AXX8NPgCYnZA2ydomv5JUaFdLm3Fy5M1nE" },
            { "amount": "1", "recipientId": "ASx99YydmwakbnQ4MVrmxc7iurkhvigLew" },
            { "amount": "1", "recipientId": "Ad4gQwza6uYMNdykVBaPQGJPqcmw1xdVee" },
            { "amount": "1", "recipientId": "AUantbHXLw9mScYeaZLiee3CVYXC4hkR74" },
            { "amount": "1", "recipientId": "AThLYvvyiVeCfQAh5PAX8Qno4Wd6S62tyH" },
            { "amount": "1", "recipientId": "AWqJzREQHu3fjDxH5rqT2VSbeUM7SxEhna" },
            { "amount": "1", "recipientId": "ATzPon6cYKnadQRcdvvihooXKY9Ck1Liec" },
            { "amount": "1", "recipientId": "AaZjRkpC18yLxuSuPfgJL6LHUbda56HnSs" },
            { "amount": "1", "recipientId": "AN9T4RBCdA87aSdChpAHh7uUAG4B8uBoUq" },
            { "amount": "1", "recipientId": "AX44ttMS5RVscdiS6ij7RNevJ7DHH5qNph" },
            { "amount": "1", "recipientId": "ATLTB78g3a5w17TBU55aKjLduRbAGoThpK" },
            { "amount": "1", "recipientId": "AKarCMgn7Bk9Nei1DAr6JeYSzwtnFgBSDQ" },
            { "amount": "1", "recipientId": "AKEDqDqa78RbZupNVvGkKLtYsXA8NegCRN" },
            { "amount": "1", "recipientId": "ARYDs5Ld3waYyRdnhcfori13cXHaEDEeau" },
            { "amount": "1", "recipientId": "AeBCh8GTkJcjZGk9WZNPBAdv3rU7iggLY7" },
            { "amount": "1", "recipientId": "AX6gUdyHxZVqnoZCSA4SGt43K5RtJ7ThBu" },
            { "amount": "1", "recipientId": "AGDtW75CApDYNd5u54uFcuLB35hjQ1AtAR" },
            { "amount": "1", "recipientId": "APwfcZa61hT4CNptRWjykv8J8UNG26WKZk" },
            { "amount": "1", "recipientId": "AGyANoQJRETkdiADXMrB8EkBxYCVCiVxq4" },
            { "amount": "1", "recipientId": "AQ21SC3vq3iYf4CyQhAPuX4p9LHPhRaKUY" },
            { "amount": "1", "recipientId": "AUBKVPGUzLrHz4nh2o9wms9kf44KtiQBzF" },
            { "amount": "1", "recipientId": "AKFPFgGiv26n4LcTzCJ1FhHytgk86qZ5fk" },
            { "amount": "1", "recipientId": "AVdv6aogUAf93MnWLhjze3971P4yMqcBMY" },
            { "amount": "1", "recipientId": "AWkg5GAdQ34NApvGE4kj2t3cQw5MupuemH" },
            { "amount": "1", "recipientId": "AUwDWzNS6rvtvGuX9mp313vpSsNASMxgJc" }
        ]
    },
    "signature": "a5ad9228b3f6717d471411ac733629d561c19a945dbe956261f707c303c9327e12a87c48e429dc9f8ee7cfa026798aacaed59a27d650bfc2095291f816955f05",
    "id": "b5e1c95a33ff1c70a96a91c2f190268189778f28f5330b0afd49aebb74da30c4"
}
```

### Serialized Payload

```text
ff0217010000000600020000000000000002a53371b23f991740f968e3d96de42a67b4242e267cad8050ae4b68bf9ac20af28096980000000000008900000001000000000000001720a32a4fd007065355e791cffd598bb0c6fa52bc010000000000000017f13809c4c5fb2b3967a9b40efc70843f7db462ad0100000000000000175f60e0594115b71d5b136cf929c8504082ac199d0100000000000000175c2aaead4ce542788406c54e1ae31f1afdb7f081010000000000000017c2308975254751ead4df705fc76aa84116c5e34e010000000000000017c792d1958bb950596d0e7cd0bef32506200968480100000000000000172031100e628422b8409810fdb438e874765846ba0100000000000000176bd2c24bded5fdfd7888a28b3c6990503699b5e8010000000000000017009ffbb10efc47ad00a0a29cc2ef6e6c83d8c6ec010000000000000017be9147febbfe462cdbfda8575c18dabe85db4f5b010000000000000017358634b58d88abf4aef3a6fe264b4ad18b74e98b01000000000000001711745fc47a9c58c4e6f5a74eb59411ac102c6a880100000000000000175265ceb5d6102474ea7d0f401d6e6b9f13864a050100000000000000177617b5f3b82f153e388b4b200abd8636fff73dd501000000000000001718f5df4fe3108277bfa4e39071fead9d59b35b8f010000000000000017ef283e95c3fdf0e2df9ba8321407c5621f9868760100000000000000176af453a17439c9c258c25c707aa9fc1f3b59d9b40100000000000000177e94f3954665ebd80ced3d434c67cd4351966f2b0100000000000000178b8ee88e27291e33ce5403ea9b159235887dcfa9010000000000000017232a71b6b2586d5b02b6a72db08759066ba2a92b01000000000000001728c4b220f14f3745f3fff6d3c066ba2353393eb6010000000000000017ac67d5bfbef4a7ed8149727b93a01e903d84ee0c0100000000000000173a537bef2ed296a54adc354967efe3a5e52cdfb80100000000000000172c939e4633bd96ccc1d1509dbe794299603aad9901000000000000001753ef9af027797e4827d708d9ed47c511f4ea5524010000000000000017e103c02fc06140aeac275f8e579f3397d041f817010000000000000017a37d6366d765f5e446fc18ddcc3da3fa300cf6bb010000000000000017e1671fea563be042824751a3465a7dbbc4827942010000000000000017f4d63847bf07a9faad83bd69fed408b3b734dce8010000000000000017888e092eba4cbd5eab9e10646661f5a440915f9d0100000000000000175677152f9d640b175894c8da0b9f30bad3801aff010000000000000017d34bb692e52d515398d00fd57ce2c8bfd3480554010000000000000017cfafad73ebddc38d53317c80cdbf6d343c331d620100000000000000177dbca0c01f96de655cf41eb53e1b8d5e2ffa2607010000000000000017f354c71350a110a7b45b5095ed0a4601bf4bbf9d0100000000000000170ca0fbbfb8e3f615ec4eedaef6281d4d60a8f2b20100000000000000172f885faaf6a3fcc38b1f35c652bf72f0fd7ac60301000000000000001724e14548f3874b9413a28f258c2b73d35ec2b2f9010000000000000017e3f48b5211d1f21034bc15908259901ecf972be8010000000000000017ccbb32ea36fad927cb2c46cbc63930db6cda829d010000000000000017670c4b3896983f37a0d113eb6afc329c39232aa4010000000000000017f17faa6a2a251d2ac73033ea1868387542b798fa010000000000000017aa0f2cf081d9609a44dde12e0c805ebb0880c857010000000000000017a794717598f2f4379bc787be2d5730e19cef6bc50100000000000000179d5d3507b35431cd3ec3ab6dad8663a64c41772e010000000000000017d0fbd6baf73fa195989ea418aa04c90c873f8ec5010000000000000017004c2fbebda958eb1173f9f8eab22a171e0cafba010000000000000017ca7739477089657a1dd6061411cfeafec50f6d28010000000000000017568598ea898f21b665b681425f91666b910da328010000000000000017f38358caf39c93d2d1b4db950606dc703378554c01000000000000001786f5b6951d2c9578a790612f6f3c59b387105180010000000000000017342bf4e8884754b6867903ef9c5e27c03ac036e50100000000000000173278d0a270000126e0dd97e6c0641755b145babe010000000000000017dfd16cf066ffced2c1cfbb10e3ca2a9fb584578a010000000000000017d3275bfaeba7b49d2ef55673bbb3c1fb08b08d9f01000000000000001794e65c65d7abcf07f67b67a23793682f43efeb420100000000000000171bb531fb6335c6a8926a3c00eeba5fe0511856dd0100000000000000170721c33e5b98f0227b2cb8fc64b83dd510317b0b010000000000000017fb73dfa44b21e88e72c234b8c80ed9c634aae35901000000000000001753acc3249244171686f3e7162204b941ebc7261801000000000000001712d4ebc3c271406ce007e3c6f3347b14e447c13601000000000000001718af9ce5f8c983184c9650b021a645bcfebf3cfb01000000000000001740173e1b8672e92982e53c98b53c680748c725b5010000000000000017435483bed11c1b57f692d1c46389b2c5cb3157f2010000000000000017029022a47dc76855101fff5eb0243e3083af78e7010000000000000017c411af7a4a5062066dd5872ddc5373bfea2b8861010000000000000017fbb29777b4d2a728cddab9bd67c957a7b1558994010000000000000017c119f3b087e7fc3038cafea35b127ce40a797a1a010000000000000017fbf6e96524f5e752a5e4c888b21d41de9d3c52620100000000000000172515f06be5786f8be1381c55be104d90ad627112010000000000000017548c6e2d4016a41e378fda3c8873886543fa70ab0100000000000000174bfe676769da8da1f93192e079c482ecc5bc174f010000000000000017afb206cdfb25578ce365d27304470c49e4125fed01000000000000001747f3ffafa5426a110cd350443e9fe9d0f174e3b40100000000000000176eb489b953096524e44f36c85c73144bd532d402010000000000000017871de62afc7f1d49e1ee7c42b0404ba142fc7ea6010000000000000017fec42984da0e01d4a7bac024a5e475c063ac9c460100000000000000177a09a9b82ed74e61fbbcfbe7aec3cbba7cafa12e010000000000000017e20bb0016cd9f294dad34a8bb561fd11e637244a0100000000000000173aae39ea7d1f75a6e9e2227f609c4d14970c852d010000000000000017eae871ae15c3257628161ab7e32ffbb2482c78a9010000000000000017bbe0df02533620dfc8a6a5033a7345e0a34be0cb01000000000000001715b7d1c17acc078e851a177a1d367a9d3dd68d23010000000000000017bb7e23ad26914f168656213867fae480dda65c470100000000000000175af6c2e27b91e61f8e2aeeb97b1eccf227a3bebd0100000000000000171df95978e737f2fb09b8c84e14965ea93340d18601000000000000001751dffdd691c32b7eb725cadb1d079f307f95f664010000000000000017f874b060408bf32f69abd7075ef1996d73f60be00100000000000000173271a8fa8423a3deed5f428c246c570b55698437010000000000000017403b9325626c8cdef7d72607b81293c2d470a97b010000000000000017742a8590b18189f9a48ea5d6130ca261c0a4c22401000000000000001700a167a5d6b0f9ce2412c1b5df562b6d864a711001000000000000001734b2366cee1ec416e66388d3af5fd9b139a5603b0100000000000000171c5ee9ef8a8fe1f9f9b342e1eb7a386f6b8994f50100000000000000179f5b37aa9925ad7e998c3bd4b5ddbe31e9f58e8d0100000000000000177e783dc832674a0ee644cdfb29e9232f68ee505d01000000000000001780824545d87e1eb691b2171e4bb493607724e55001000000000000001719f9077cac3d96ecdca2f51f4c98407aac43868d010000000000000017dd108e250a81bda83e4613b71455753786ee746e0100000000000000177493b7565f8636184e83c6932fc92a5d5a296bd7010000000000000017718e2ae0facdbf29671853177560c5005a9f0e79010000000000000017eaae33738759c292d482eab208a0a0bf435c85af010000000000000017c49bcbe3455ba122f872e690c74fc0ec9210414f01000000000000001724c7652304c41c93aead26419604de7f5b8de442010000000000000017aab09efda1232d347381be809e1c8dfc3c0744fc0100000000000000175d31e11438d5ef1140d6296f05f7a03b6c6630100100000000000000170e21668e2123e42e03272fa24e46137242a6ff65010000000000000017ad0087f23f59dd30f586de1442cbb8b986d50fd4010000000000000017d80204238e3e94f99bfe2e44a20671ace2deb55c0100000000000000170688a4b5d8b90c9ce1703d5bfe660ddb6f1d9dc00100000000000000179d317d97a1c29ce4d134c4101673d68d8ec8b56a0100000000000000179ff7c1007941f86c2ba2a33dc420dd30dbad52d7010000000000000017acb8100b3d329598a4f0881df2ca7921a9da659d0100000000000000177a9a7b964ee2e823fcb237b352a4b3769c69e9d7010000000000000017e98855e1023a60dbe3fec3e139e496fad176ac160100000000000000178c8116b26ea08128470bd157e94214a9ef8b234801000000000000001782c5e34f55def2baa9c795064759ebeca7d71eb3010000000000000017a5304a50845a14eb3d056738c8de3c30ee49dd1901000000000000001785ffad6012d89b11b510fe32dbf85ca448249050010000000000000017ce1e89721c1df2d1b4165a622bf1288fa764a6e301000000000000001745e561944786f513c5ad3d31c3c3c88e3aa4dcc8010000000000000017a799ee7a9fc25df86361192ffbee64a8d52386ad0100000000000000177ed2ae936601fc2f079279afe249f510df5efc9101000000000000001729cab77105a600d1843c56b34c877d1b1bddd8bd01000000000000001725e40ab73be8507a874986d35bd3737463ea113f0100000000000000176b1c4f8024768772d2383d87af7d8990f732413c010000000000000017f5bc3b8ab8a28f0700df6f3602f231dc434bdcbc010000000000000017a818773d8d77e6fc74970dd488c033965669d39b01000000000000001704eb876ab3b7e2f136889dadeddc0219b47dac8a010000000000000017599b1ef53e7c4fbe6c682afda54ebdc87049391f0100000000000000170d1aaa9441c60a0e51212a5b84892aa9759cf6d20100000000000000175a6d54a6ee7e6225a4325a5e05d59b452e279d9b0100000000000000178810a6294399c640e23d42c372494e9159b1ace0010000000000000017261c52971d5e1024a7c0ececf5197f01005fe9bc01000000000000001798107a6ceb0fcf15a7b05208c29564f34eeafc98010000000000000017a44fcf637c830148b941e977ac155d2bc2f016e7010000000000000017905df747e8999695f92c58cbaac4324b11345e73a5ad9228b3f6717d471411ac733629d561c19a945dbe956261f707c303c9327e12a87c48e429dc9f8ee7cfa026798aacaed59a27d650bfc2095291f816955f05
```

### Deserialized Hex Payload

| Key | Pos. | Size  _\(bytes\)_ | Value   _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **TypeGroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0600` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x02a53371b23f991740f968e3d96de42a67b4242e267cad8050ae4b68bf9ac20af2` |
| **Fee:** | **\[50\]** | **8** | `0x8096980000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Number of Payments:** | **\[59\]** | **2** | `0x89000000` |
| **Amount 1:** | **\[61\]** | **8** | `0x0100000000000000` |
| **Recipient 1:** | **\[69\]** | **21** | `0x1720a32a4fd007065355e791cffd598bb0c6fa52bc` |
| **............** | **....** | **..** | `..................` |
| **Amount 137:** | **\[4008\]** | **1** | `0x0100000000000000` |
| **Recipient 137:** | **\[4009\]** | **21** | `0x17905df747e8999695f92c58cbaac4324b11345e73` |
| **Signature:** | **\[4030\]** | **64** | `0xa5ad9228b3f6717d471411ac733629d561c19a945dbe956261f707c303c9327e12a87c48e429dc9f8ee7cfa026798aacaed59a27d650bfc2095291f816955f05` |

## Delegate Resignation

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 7,
    "nonce": "2",
    "senderPublicKey": "037a12518205254e6ebf25290d9786fd9821c43bb7319c9fc2499c8d472809dfaf",
    "fee": "2500000000",
    "amount": "0",
    "signature": "ad7a61a76433260ef9dc687311ab6c657f6c733dbf1a80c3514da823d43226235a70a94fa1a0b8cb2f4b3d0be5011945bfbe8c8fc5b5ca0e07f6c2a37e3cf11b",
    "id": "ee2a5253e28f66d5546b28bba96b4fa88973305e2e0d3b82afd5b3386ab0b6d4"
}
```

### Serialized Payload

```text
ff02170100000007000200000000000000037a12518205254e6ebf25290d9786fd9821c43bb7319c9fc2499c8d472809dfaf00f902950000000000ad7a61a76433260ef9dc687311ab6c657f6c733dbf1a80c3514da823d43226235a70a94fa1a0b8cb2f4b3d0be5011945bfbe8c8fc5b5ca0e07f6c2a37e3cf11b
```

### Deserialized Hex Payload

| Key | Pos. | Size _\(bytes\)_ | Value  _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0700` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x037a12518205254e6ebf25290d9786fd9821c43bb7319c9fc2499c8d472809dfaf` |
| **Fee:** | **\[50\]** | **8** | `0x00f9029500000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Amount:** | **\[..\]** | **0** | Not Serialized |
| **Signature:** | **\[59\]** | **64** | `0xad7a61a76433260ef9dc687311ab6c657f6c733dbf1a80c3514da823d43226235a70a94fa1a0b8cb2f4b3d0be5011945bfbe8c8fc5b5ca0e07f6c2a37e3cf11b` |

## HTLC Lock

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 8,
    "nonce": "2",
    "senderPublicKey": "020d272fab67c179a9e4df4d006344d3ca47fb531b4246b483373940f0603a9216",
    "fee": "10000000",
    "amount": "1",
    "recipientId": "ATNGUiu6sYRb7MXtdcVc7KjoyM6TdfuoC1",
    "asset": {
        "lock": {
            "secretHash": "09b9a28393efd02fcd76a21b0f0f55ba2aad8f3640ff8cae86de033a9cfbd78c",
            "expiration": {
                "type": 1,
                "value": 78740307
            }
        }
    },
    "signature": "11b1c06b4e5ba7c196f6f36fca2540275173a472e61581e949cd24a7cf5ee98af6a74f3c919f9b82a2e65b51b737bdf22f7a08ffcf52b88dc4a16d6ac5c10bfe",
    "id": "f84efeab77224af8959301a7185597a7cfbfbc9a4d99cb021af62f3714feb9d3"
}
```

### Serialized Payload

```text
ff02170100000008000200000000000000020d272fab67c179a9e4df4d006344d3ca47fb531b4246b483373940f0603a9216809698000000000000010000000000000009b9a28393efd02fcd76a21b0f0f55ba2aad8f3640ff8cae86de033a9cfbd78c01537bb104177f2a95c7076ea278776d8fcecc5b18e588976da611b1c06b4e5ba7c196f6f36fca2540275173a472e61581e949cd24a7cf5ee98af6a74f3c919f9b82a2e65b51b737bdf22f7a08ffcf52b88dc4a16d6ac5c10bfe
```

### Deserialized Hex Payload

| Key | Pos. | Size   _\(bytes\)_ | Value   _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0800` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x020d272fab67c179a9e4df4d006344d3ca47fb531b4246b483373940f0603a9216` |
| **Fee:** | **\[50\]** | **8** | `0x8096980000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Amount:** | **\[59\]** | **8** | `0x0100000000000000` |
| **Secret Hash:** | **\[67\]** | **32** | `0x09b9a28393efd02fcd76a21b0f0f55ba2aad8f3640ff8cae86de033a9cfbd78c` |
| **Expiration Type:** | **\[99\]** | **1** | `0x01` |
| **Expiration Value:** | **\[100\]** | **4** | `0x537bb104` |
| **Recipient:** | **\[104\]** | **21** | `0x177f2a95c7076ea278776d8fcecc5b18e588976da6` |
| **Signature:** | **\[125\]** | **64** | `0x11b1c06b4e5ba7c196f6f36fca2540275173a472e61581e949cd24a7cf5ee98af6a74f3c919f9b82a2e65b51b737bdf22f7a08ffcf52b88dc4a16d6ac5c10bfe` |

## HTLC Claim

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 9,
    "nonce": "3",
    "senderPublicKey": "039d974aa6feff6a19fde69a8a8b25b991798e98252765a887118ba61218f473a2",
    "fee": "0",
    "amount": "0",
    "asset": {
        "claim": {
            "lockTransactionId": "f84efeab77224af8959301a7185597a7cfbfbc9a4d99cb021af62f3714feb9d3",
            "unlockSecret": "f5ea877a311ced90cf4524cb489e972f"
        }
    },
    "signature": "c2b9f3655174c13686dde428cf18d5d18f465712985a7086b04860457e8d2db64443083bdf69fdc5b94dcd2c4c722606cf0e058ffae98d8f9f069177c5c189ab",
    "id": "d8acf49eba509e94494f454a86add1fab8b2130f223c9cc25e8e92745a584813"
}
```

### Serialized Payload

```text
ff02170100000009000300000000000000039d974aa6feff6a19fde69a8a8b25b991798e98252765a887118ba61218f473a2000000000000000000f84efeab77224af8959301a7185597a7cfbfbc9a4d99cb021af62f3714feb9d36635656138373761333131636564393063663435323463623438396539373266c2b9f3655174c13686dde428cf18d5d18f465712985a7086b04860457e8d2db64443083bdf69fdc5b94dcd2c4c722606cf0e058ffae98d8f9f069177c5c189ab
```

### Deserialized Hex Payload

| Key | Pos. | Size   _\(bytes\)_ | Value   _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **TypeGroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0900` |
| **Nonce:** | **\[9\]** | **8** | `0x0200000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x039d974aa6feff6a19fde69a8a8b25b991798e98252765a887118ba61218f473a2` |
| **Fee:** | **\[50\]** | **8** | `0x0000000000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Lock Id:** | **\[59\]** | **32** | `0xf84efeab77224af8959301a7185597a7cfbfbc9a4d99cb021af62f3714feb9d3` |
| **Unlock Secret:** | **\[91\]** | **32** | `0x6635656138373761333131636564393063663435323463623438396539373266` |
| **Signature:** | **\[123\]** | **64** | `0xc2b9f3655174c13686dde428cf18d5d18f465712985a7086b04860457e8d2db64443083bdf69fdc5b94dcd2c4c722606cf0e058ffae98d8f9f069177c5c189ab` |

## HTLC Refund

### Signed JSON Payload

```javascript
{
    "version": 2,
    "network": 23,
    "type": 10,
    "nonce": "3",
    "senderPublicKey": "037fc2e14f626586722a4f9e00dca2efbc4ac409c1ca63bc4309f56184265f95d5",
    "fee": "0",
    "amount": "0",
    "asset": {
        "refund": {
            "lockTransactionId": "c62bd36c162dd0116a08bf8a75cd6d1f83b8f5f1e17e89c8231ebb7af595f64d"
        }
    },
    "signature": "ae272f4650ee1d46260b8f62e7e956af33cd25587318fed056aec8e9d518e2394d0fd3166d8cd8506abfc303c644041a4bab35daf7c8aaa77f916ef09dc90336",
    "id": "4d9ee7f8b27999d4ce7acf6afee08e3da67bc1fca258f2bd17e426933a846602"
}
```

### Serialized Payload

```text
ff0217010000000a000300000000000000037fc2e14f626586722a4f9e00dca2efbc4ac409c1ca63bc4309f56184265f95d5000000000000000000c62bd36c162dd0116a08bf8a75cd6d1f83b8f5f1e17e89c8231ebb7af595f64dae272f4650ee1d46260b8f62e7e956af33cd25587318fed056aec8e9d518e2394d0fd3166d8cd8506abfc303c644041a4bab35daf7c8aaa77f916ef09dc90336
```

### Deserialized Hex Payload

| Key | Pos. | Size   _\(bytes\)_ | Value   _\(hex\)_ |
| :--- | :---: | :---: | :--- |
| **Header:** | **\[0\]** | **1** | `0xff` |
| **Version:** | **\[1\]** | **1** | `0x02` |
| **Network:** | **\[2\]** | **1** | `0x17` |
| **Typegroup:** | **\[3\]** | **4** | `0x01000000` |
| **Type:** | **\[7\]** | **2** | `0x0a00` |
| **Nonce:** | **\[9\]** | **8** | `0x0300000000000000` |
| **SenderPublicKey:** | **\[17\]** | **33** | `0x037fc2e14f626586722a4f9e00dca2efbc4ac409c1ca63bc4309f56184265f95d5` |
| **Fee:** | **\[50\]** | **8** | `0x0000000000000000` |
| **VendorField Length:** | **\[58\]** | **1** | `0x00` |
| **Lock Id:** | **\[59\]** | **32** | `0xc62bd36c162dd0116a08bf8a75cd6d1f83b8f5f1e17e89c8231ebb7af595f64d` |
| **Signature:** | **\[91\]** | **64** | `0xae272f4650ee1d46260b8f62e7e956af33cd25587318fed056aec8e9d518e2394d0fd3166d8cd8506abfc303c644041a4bab35daf7c8aaa77f916ef09dc90336` |
