---
title: Blockchain
descrip:
---


*A blockchain is basically a distributed state machine replicated across many nodes.*

wallets do not store crypto. they only store private keys. the blockchain is the one who stores stuff like balances, ownership and state. a wallet is just an interface + signer.

when an user initiates action e.g.: send ETH, swap tokens the wallet builds that transaction:
- from
- to
- value
- gas limit
- calidata
and then it signs the transaction with the user's private key + eliptic curve criptography.

from there, it is the blockchain network that handles the rest of the flow.

first, RPC sends transaction (usually via `eth_sendRawTransaction`). 
second, the network validates signature validity, enough balance, gas and nonce. 
next the EVM executes the transaction, where the smart contract code executes.
finally the state is updated across all nodes.

*Wallets are primarily transaction signers and blockchain interfaces. the blockchain itself maintains the canonical state.*

ok, but what does all of those in betweens mean? let's start with RPC (Remote Procedure Call).

it allows one system to call functions on another system remotely. in a blockchain, that means the frontend/backend communicates with blockchain nodes via RPC.
usually, this is a JSON-RPC payload over HTTP or WebSocket. this is what it looks like:

```json
{
  "jsonrpc":"2.0",
  "method":"eth_blockNumber",
  "params":[],
  "id":1
}
```

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0x1b4"
}
```

important distinction of RPC methods:
1. Read-only: no gas required. `eth_blockNumber, eth_getBalance, eth_call`.
2. State-changing: require signed transactions. `eth_sendRawTransaction`.

`eth_call`
- read-only
- no gas spent
- simulated locally
`eth_sendRawTransaction`
- modifies blockchain state
- costs gas
- broadcast to network

HTTP vs WebSocket are employed because HTTP is a good protocol for transaction submission, while the WebSocket is a persistent connection, good for live block updates and subscriptions.

the two-way communication happens on a Client <-> Node model. the Client sends a request "what is wallet balance?" and the node responds "balance is X".
with WebSockets, a node can push updates automatically (persistent connection) e.g.: "new block mined" -> pushes update -> "transaction confirmed".

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/ethereum/go-ethereum/ethclient"
)

func main() {
    client, err := ethclient.Dial("https://mainnet.infura.io/v3/YOUR_KEY")
    if err != nil {
        log.Fatal(err)
    }

    blockNumber, err := client.BlockNumber(context.Background())
    if err != nil {
        log.Fatal(err)
    }

    fmt.Println(blockNumber)
}
```
*Go example code calling Ethereum RPC.*

all of this happens on an execution engine. one of these engines is the EVM (Ethereum Virtual Machine). it's job is to execute smart contracts identically, across all Ethereum nodes.

it's responsibilities include:
- execute smart contracts
- change blockchain state
- calculate gas usage
- ensure deterministic execution
the last one is important: **every node runs the same EVM execution**.

this means the EVM is **deterministic**: the same input must produce same output on every node.
therefore smart contracts cannot use random local machine data, nor access internet or use the system clock freely. this would break consensus, breaking the identical state replicae.

EVM executes bytecode. this bytecode stems from a programming language called Solidity, it has a compiler that transforms it's code into EVM bytecode.

*the EVM is a deterministic sandboxed runtime that executes smart contract bytecode identically across all Ethereum nodes.*

and what is the computational cost for all of that? it can be measured by Gas.
