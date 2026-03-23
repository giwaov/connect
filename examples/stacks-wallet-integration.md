# Stacks Wallet Integration Patterns

## Overview

Stacks Connect provides a simple way to integrate Stacks wallet functionality into web applications.

## Authentication Flow

```javascript
import { AppConfig, UserSession, showConnect } from "@stacks/connect";

const appConfig = new AppConfig(["store_write", "publish_data"]);
const userSession = new UserSession({ appConfig });

function authenticate() {
  showConnect({
    appDetails: {
      name: "My Stacks App",
      icon: window.location.origin + "/logo.svg",
    },
    redirectTo: "/",
    onFinish: () => { window.location.reload(); },
    userSession,
  });
}
```

## Contract Calls

```javascript
import { openContractCall } from "@stacks/connect";
import { uintCV, stringAsciiCV } from "@stacks/transactions";

async function callContract() {
  const options = {
    contractAddress: "SP...",
    contractName: "my-contract",
    functionName: "my-function",
    functionArgs: [uintCV(100), stringAsciiCV("hello")],
    network: "mainnet",
    onFinish: (data) => console.log("TX:", data.txId),
  };
  await openContractCall(options);
}
```

## STX Transfer

```javascript
import { openSTXTransfer } from "@stacks/connect";

async function sendSTX() {
  await openSTXTransfer({
    recipient: "SP2...",
    amount: "1000000",
    memo: "Payment",
    network: "mainnet",
    onFinish: (data) => console.log("TX:", data.txId),
  });
}
```
