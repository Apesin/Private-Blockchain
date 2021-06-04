# Private-Blockchain
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

<li>chainId: A unique identifier of the new private blockchain. This provides a way to send transactions that work on ethereum without working on ETC (ethereum classic) or the Morden testnet. EIP 155 suggests following chainid values for different networks: ethereum mainnet (1), morden /expanse mainnet (2), ropsten (3), rinkeby (4), rootstock mainnet (30), rootstock testnet (31), kovan (42), ethereum classic mainnet (61), ethereum classic testnet (62), geth private chains (1337 by default). In our example we have used 15, which is not used by any of these networks.</li>
<li>homesteadBlock: Homestead is the first production release of Ethereum and since the developers are already using this version the value of this parameter can be left as ‘0’.</li>
<li>eip155Block/eip158Block: EIP stands for “Ethereum Improvement Proposals”, these were implemented to release Homestead. In a private blockchain development, hard forks aren’t needed, hence the parameter value should be left as ‘0’.</li>
<li>difficulty: Controls the complexity of the mining puzzle and a lower value enables quicker mining. Gas is the internal pricing for running a transaction or contract in ethereum. Each instruction sent to the Ethereum Virtual Machine (EVM) to process a transaction or smart contract costs a specific amount of gas. If the required amount of gas is not provided to the transaction, it will fail before completion. When you do any ethereum transaction, you specify a gas limit — that is the maximum gas all the operations corresponding to that transaction can consume. The gasLimit parameter in the block specifies, the aggregated gasLimit from all the transactions included in the block.</li>
<li>gasLimit: Establishes an upper limit for executing smart contracts.</li>
<li>alloc: Allows allocation of Ether to a specific address.</li>
<b>Paste the above code in the genesis.json file and save it in a folder on your computer.
Next, open the terminal and run the following code snippet. This will instruct Geth to use genesis.json file to be the first block of your custom blockchain. We also specify a data directory where our private chain data will be stored. Choose a location on your computer (separate folder from the public Ethereum chain folder, if you have one) and Geth will create the data directory for you.</b>
<br>
<code>
    geth --rpc --rpcport "8085" --datadir /path_to_your_data_directory/pblockchain init /path_to_folder/genesis.json
 </code>
 <li>Where pblockchain is the folder where we stored the genesis.json file</li>
 <img src="https://github.com/Apesin/Private-Blockchain/blob/main/screen1.png">
 <br>
 
# Create a Private Network
<br>
Next, we will start our private network to mine new blocks to our private chain. Run the following code snippet on your terminal. The parameter “networkid” is a unique id to identify our private blockchain network. The main Ethereum network has “1” as the networkid. Give any random number except “1” to create our unique network.
geth --rpc --rpcport "8085" --datadir /path_to_your_data_directory/pblockchain --networkid 123 --nodiscover
Now your private network will go live. 
<br>
After running the above snippet, the terminal gives the following result.
<img src="https://github.com/Apesin/Private-Blockchain/blob/main/screen2.png">

<br>

 # Create Accounts
To create an account simply enter the following snippet in your console
<br>
<code>
geth account new --datadir /path/to/data/dir/pblockchain
</code>
on success anew wallet will be created.

<br>

 # Start Mining 
Now we can start mining with geth using the following command. The networkid parameter here differentiates this ethereum network from the others. All the miners who want to connect to this network, have to use the same networkid along with the same genesis block. Here my network id is 123
<br>
<code>
geth --mine --rpc --networkid 123 --datadir /path_to_your_data_directory/pblockchain
</code>
<br>
<linetworkid: network identifier of this ethereum network. You pick a value you want. For example: olympic (0), frontier (1), morden (2), ropsten(3). mine: enables mining. rpc: enables an HTTP-RPC server. Wallet applications can connect to this mining node over http.</li>
<br>
<li>rpcaddr: specifies the HTTP-RPC server listening interface (default: “localhost”)</li>
<li>rpcport: specifies the HTTP-RPC server listening port (default: 8545)</li>
<li>rpcapi: specifies the API’s offered over the HTTP-RPC interface (default: “eth,net,web3”).</li>
<br>

<code>
    --rpcapi "web3,eth"
    </code>
 <li>rpccorsdomain: enables CORS by specifying a comma separated list of domains from which to accept cross origin requests. This is useful when using browser based solidity editors (remix) to deploy smart contracts or browser based wallets. For example, following will accept CORS from any domain</li>
 <br>
 
 <code>
    --rpccorsdomain "*"
    </code>
    
   <li>nodiscover: disables the peer discovery mechanism. None of the other nodes in the network will not be able to find your node. If you intend to have this private blockchain being used within your local network with others, do not use this parameter</li>
   <li>console: with this command we can start the mining node with an interactive javascript environment. We will learn more about this in the next section.</li>
   <br>
    
   <code>geth --mine --rpc --networkid 1999 --datadir /path/to/data/dir console</code>
   
   <br>
   
   # Attach Geth Console
   Either you can start the mining node as a console — or you run the console separately and attach it to a mining node, with the attach command. The following shows how to do it, and make sure you follow the same parameter order
   <br>
   
  <code>geth --datadir /path_to_your_directory/pblockchain attach ipc:/path_to_your_directory/pblockchain /geth.ipc</code>
  <br>
  Incase the snippet above did not work try this one below, it usually happens on windows 10. Also make sure your Geth is running before you enter this command
<code>
geth attach ipc:\\.\pipe\geth.ipc
</code>
<br>
