# Public-Blockchain
You will learn how to create a private blockchain.
<b>Setting up the environment</b>
First, you need to install Geth which is a command-line interface (CLI) tool that communicates with the Ethereum network and acts as the link between your computer and the rest of the Ethereum nodes.
Go to the Go Ethereum site. Download and install the binary for your operating system.
# Downlaod Geth from Ethereum webiste
https://geth.ethereum.org/downloads/
<br.
#Creating a genesis block by creating a Genesis file
To run a private network, you need to provide geth with some basic information required to create the initial block. Every blockchain starts with a Genesis Block, the very first block in the chain. To create our private blockchain, we will create a genesis block with a custom genesis file. Then, ask Geth to use that genesis file to create our own genesis block.
Custom Genesis file

<code>
{
    "nonce": "0x0000000000000042",
    "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x00",
    "gasLimit": "0x8000000",
    "difficulty": "0x400",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",
    "alloc": {},
    "config": {"chainId": 987, "homesteadBlock": 0, "eip155Block": 0, "eip158Block": 0, "eip150Block": 0}
}
  </code>
