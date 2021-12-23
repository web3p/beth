# beth.sh

## What is it?

beth.sh supports (a part of) Ethereum JSON-RPC in terminal for `zsh` and `bash`.
Focus is on portability, (nearly) no dependencies and ease of use. I wanted
an easy and ergonomic way to query some data.

## What is supported?

Supported are read-only RPCs, excluding filters, tx signing and that kind of stuff.

## Installation

The only dependency is `curl` and some fairly widespread UNIX tools. Just do

```
cd && git clone https://github.com/th4s/beth && echo "source beth/.beth.sh" >> .bashrc && source .bashrc
```

That's it. You can now enter `eth_` and `TAB` in you terminal to see the supported RPCs.

## Examples


