---
description: >-
  How to setup a local blockchain explorer and browse the blockchain from a web
  application
---

# Setup Your Own Blockchain Explorer

## Introduction

This short guide will help you setup a local blockchain explorer. This will enable you to browse and search your blockchain from a web application \(exactly the same as our official [Blockchain Explorer](https://explorer.ark.io)\).

## STEP 1: Clone Official Explorer Repository

```bash
git clone https://github.com/arkecosystem/explorer
cd explorer
```

## STEP 2: Install Package Dependencies

From the `explorer` root folder run`yarn install` command. This will build and install the required modules and packages.

## STEP 3: Run Your Local Explorer

There are several run modes available for the Explorer package. You can run it as official Mainnet or Devnet explorer, or have it run as a simple local express server, it is up to your needs. 

{% hint style="info" %}
More detailed information about possible running modes can be found in the official [Explorer Readme Document.](https://github.com/ArkEcosystem/explorer/blob/develop/README.md)
{% endhint %}

For the simple task of viewing and browsing of your local blockchain Testnet environment, all we need to do is run the following command from the Explorer root folder:

`yarn serve:testnet` // this command will start the Explorer in dev mode and it will search for a localhost core node, that should be running on `127.0.0.1:4003` by default configuration.

After running `yarn serve:testnet` command, you should see something the following:

```text
DONE  Compiled successfully in 11030ms    

No type errors found
Version: typescript 3.6.3
Time: 6973ms

  App running at:
  - Local:   http://localhost:8080/
  - Network: http://192.168.0.178:8080/

  Note that the development build is not optimized.
  To create a production build, run yarn build.
```

Head over to http://localhost:8080/ to view contents of local running blockchain with Testnet environment setup.


