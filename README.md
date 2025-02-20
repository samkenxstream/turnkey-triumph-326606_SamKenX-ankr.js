# ⚓️ ankr.js

Compact JavaScript library for interacting with Ankr's [Advanced APIs](https://www.ankr.com/advanced-api/).

## Get started in 2 minutes

#### 1. Install the package from npm

```bash
# with npm
npm install @ankr.com/ankr.js

# with yarn
yarn add @ankr.com/ankr.js
```

#### 2. Initialize the provider

```javascript
import { AnkrProvider } from '@ankr.com/ankr.js';

const provider = new AnkrProvider();

// or if you have a premium account
const provider = new AnkrProvider('YOUR_API_KEY');
```

#### 3. Use the provider and call one of the supported methods

```javascript
await provider.getNFTsByOwner({
  blockchain: 'eth',
  walletAddress: '0x0E11A192d574b342C51be9e306694C41547185DD',
});
```

## Supported chains

`ankr.js` supports the following chains at this time:

- ETH: `"eth"`
- BSC: `"bsc"`
- Polygon: `"polygon"`
- Fantom: `"fantom"`
- Arbitrum: `"arbitrum"`
- Avalanche: `"avalanche"`
- Syscoin NEVM: `"syscoin"`
- Optimism: `"optimism"`

## Available methods

`ankr.js` supports the following methods:

- [`getNFTsByOwner`](#getnftsbyowner)
- `getNFTMetadata`
- `getNFTHolders`
- [`getTokenHolders`](#gettokenholders)
- [`getAccountBalance`](#getaccountbalance)
- [`getTokenHoldersCount`](#gettokenholderscount)
- [`getCurrencies`](#getcurrencies)
- [`getLogs`](#getlogs)
- [`getBlocks`](#getblocks)
- [`getTransactionsByHash`](#gettransactionsbyhash)
- `getTransactionsByAddress`
- `getTokenPrice`
- [`getTokenPriceHistory`](#gettokenpricehistory)

#### `getLogs`

Get logs matching the filter.

```javascript
const logs = async () => {
  return await provider.getLogs({
    blockchain: 'eth',
    fromBlock: 1181739,
    toBlock: 1181739,
    topics: [
      [],
      ['0x000000000000000000000000feb92d30bf01ff9a1901666c5573532bfa07eeec'],
    ],
    address: '0x3589d05a1ec4af9f65b0e5554e645707775ee43c',
    decodeLogs: false,
  });
};
```

#### `getBlocks`

Query data about blocks within a specified range.

```javascript
const blocks = async () => {
  return await provider.getBlocks({
    blockchain: 'bsc',
    fromBlock: 100,
    toBlock: 200,
  });
};
```

#### `getTransactionsByHash`

Query data about transaction(s) by the transaction hash.

```javascript
const transactions = async () => {
  return await provider.getTransactionsByHash({
    transactionHash:
      '0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f',
    decodeTxData: true,
  });
};
```

#### `getAccountBalance`

Get the coin and token balances of a wallet.

```javascript
const balances = async () => {
  return await provider.getAccountBalance({
    blockchain: 'eth',
    walletAddress: '0xfa9019df60d3c710d7d583b2d69e18d412257617',
  });
};
```

#### `getNFTsByOwner`

Get data about all the NFTs (collectibles) owned by a wallet.

````javascript
const nfts = async () => {
  return await provider.getNFTsByOwner({
    blockchain: 'eth',
    walletAddress: '0x0E11A192d574b342C51be9e306694C41547185DD',
    filter: [
      { '0x700b4b9f39bb1faf5d0d16a20488f2733550bff4': [] },
      { '0xd8682bfa6918b0174f287b888e765b9a1b4dc9c3': ['8937'] },
    ],
  });
};
````

#### `getTokenHolders`

Get the list of token holders for a given contract address.

```javascript
const tokenHolders = async () => {
  return await provider.getTokenHolders({
    blockchain: 'eth',
    contractAddress: '0xdac17f958d2ee523a2206206994597c13d831ec7',
  });
};
```

#### `getTokenHoldersCount`

Get current and historical data about the number of token holders for a given contract address.

```javascript
const tokenHoldersCount = async () => {
  return await provider.getTokenHoldersCount({
    blockchain: 'eth',
    contractAddress: '0xdac17f958d2ee523a2206206994597c13d831ec7',
  });
};
```

#### `getCurrencies`

Get a list of supported currencies for a given blockchain.

```javascript
const currencies = async () => {
  return await provider.getCurrencies({ blockchain: 'fantom' });
};
```

#### `getTokenPriceHistory`

Shows price history for provided token on specific chain
You can provide **only one param**: `fromTimestamp` or `toTimestamp`. Timestamps and intervals must be provided in seconds.
If a `fromTimestamp` is not supplied, the `interval` will be applied in reverse from `toTimestamp`
if no `toTimestamp` => take by period & limit
```
fromTimestamp----|p1|----|p2|----|pN|---->
<----|pN|----|p2|----|p1|----toTimestamp
```
Defaults:
defaultInterval - 24 hours
maxInterval - 365 days
maxLimit - 1000 (under testing)
defaultLimit - 100 (under testing)

```javascript
const prices = async () => {
  return await provider.getTokenPriceHistory({
        blockchain: "eth",
        contractAddress: "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        fromTimestamp: 1667195581, 
        interval: 86400, // 24h
        limit: 337
  });
};
```

### About API keys

For now, Ankr is offering _free_ access to these APIs with no request limits i.e. you don't need an API key at this time.

Later on, these APIs will become a part of Ankr Protocol's [Premium Plan](https://www.ankr.com/protocol/plan/).
