# beth.sh

## What is it?

beth.sh supports (a part of) Ethereum JSON-RPC in terminal for `zsh` and `bash`.
Focus is on portability, (nearly) no dependencies and ease of use. I wanted
an easy and ergonomic way to query some data.

## What is supported?

Supported are read-only RPCs, excluding filters, tx signing and that kind of stuff.

## Installation

The only dependency is `curl` and some fairly widespread UNIX tools. Just do

#### Bash

```
cd && curl -sLJO https://raw.githubusercontent.com/th4s/beth/main/.beth.sh && echo 'source "$HOME/.beth.sh"' >> .bashrc && source .bashrc
```

#### Zsh

```
cd && curl -sLJO https://raw.githubusercontent.com/th4s/beth/main/.beth.sh && echo 'source "$HOME/.beth.sh"' >> .zshrc && source .zshrc
```

That's it. You can now enter `eth_` and press `TAB` in you terminal to see the supported RPCs.

## Configuration

Per default `https://cloudflare-eth.com` is used. In order to use another node just set
the `ETH_RPC_URL` variable, e.g.:

```
ETH_RPC_URL=https://my-node-endpoint.xyz/geth/
```

You can also inject auth headers into the requests. This is useful if your node 
is behind some reverse proxy for authentication. Just set either `ETH_RPC_AUTH_BASIC`
or `ETH_RPC_AUTH_BEARER`, e.g.:

```
ETH_RPC_AUTH_BASIC=dGg..........Mg==
```

## Examples

Some of these examples use [jq](https://stedolan.github.io/jq/) for JSON processing
in the terminal.

```bash
# Get current block number 
eth_block_number

# Get curent gas price
eth_gas_price | 2gwei

# Query an account balance
eth_get_balance 0x000000000000000000000000000000000000dead | 2eth

# Query gas of a transaction
eth_get_transaction_by_block_number_and_index latest 0 | jq .gas | 2dec

# Get current block excluding transactions and pretty-print
eth_get_block_by_number latest false | jq .

# Show the 10 transactions of the most recent block containing the highest value in gwei
eth_get_block_by_number true | jq '.transactions[].value' | 2dec | sort -nr | 2gwei | head -n10

# Show all senders of transactions in the current txpool which are pending
eth_txpool_content | jq '.pending | values[] | values[] | .from'
```

