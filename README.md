# Public-Blockchain
You will learn how to create a private blockchain.
<b>Setting up the environment</b>
First, you need to install Geth which is a command-line interface (CLI) tool that communicates with the Ethereum network and acts as the link between your computer and the rest of the Ethereum nodes.
Go to the Go Ethereum site. Download and install the binary for your operating system.
# Downlaod Geth from Ethereum webiste
https://geth.ethereum.org/downloads/
<br>.

# Creating a genesis block by creating a Genesis file
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

# Explanation on the config file

<li>chainId: A unique identifier of the new private blockchain</li>
<li>homesteadBlock: Homestead is the first production release of Ethereum and since the developers are already using this version the value of this parameter can be left as ‘0’.</li>
<li>eip155Block/eip158Block: EIP stands for “Ethereum Improvement Proposals”, these were implemented to release Homestead. In a private blockchain development, hard forks aren’t needed, hence the parameter value should be left as ‘0’.</li>
<li>difficulty: Controls the complexity of the mining puzzle and a lower value enables quicker mining.</li>
<li>gasLimit: Establishes an upper limit for executing smart contracts.</li>
<li>alloc: Allows allocation of Ether to a specific address.</li>
<b>Paste the above code in the genesis.json file and save it in a folder on your computer.
Next, open the terminal and run the following code snippet. This will instruct Geth to use genesis.json file to be the first block of your custom blockchain. We also specify a data directory where our private chain data will be stored. Choose a location on your computer (separate folder from the public Ethereum chain folder, if you have one) and Geth will create the data directory for you.</b>
<br>
<code>
    geth --rpc --rpcport "8085" --datadir /path_to_your_data_directory/TestChain init /path_to_folder/genesis.json
 </code>
 <li>Where TestChain is the folder where we stored the genesis.json file</li>
 <img src="https://github.com/Apesin/Private-Blockchain/screenshots/blob/main/Screenshot 2021-05-19 160429.png">
