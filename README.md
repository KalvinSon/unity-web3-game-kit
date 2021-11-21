# `ethereum-unity3d-boilerplate`

> Unity3d components and hooks for fast building games without running your own backend

This boilerplate is built on moralis-dotnet-sdk and [Moralis](https://moralis.io?utm_source=github&utm_medium=readme&utm_campaign=ethereum-boilerplate). Also has its own context provider for quick access to `chainId` or `ethAddress`

There are many components in this boilerplate that do not require an active web3 provider, they use Moralis Web3 API. Moralis supports the most popular blockchains and their test networks. You can find a list of all available networks in [Moralis Supported Chains](https://docs.moralis.io/moralis-server/web3-sdk/intro#supported-chains)

Please check the [official documentation of Moralis](https://docs.moralis.io/#user) for all the functionalities of Moralis.


# ⭐️ `Star us`
If this boilerplate helps you build Ethereum dapps faster - please star this project, every star makes us very happy!

# 🤝 `Need help?`
If you need help with setting up the boilerplate or have other questions - don't hesitate to write in our community forum and we will check asap. [Forum link](https://forum.moralis.io/t/ethereum-unity3d-boilerplate-questions/4553). The best thing about this boilerplate is the super active community ready to help at any time! We help each other.

# 🚀 Quick Start
📄 Clone or fork `ethereum-boilerplate`:
```sh
git clone https://github.com/ethereum-boilerplate/ethereum-unity-boilerplate.git
```
💿 Install all dependencies:
- [Unity Hub](https://unity3d.com/get-unity/download)
- [Visual Studio](https://visualstudio.microsoft.com/)

💿 Open Unity Hub and Add the Project
- Open Unity Hub
- click on the 'ADD' button.
- Navigate to the folder you cloned the boiler plate project to.
- Click on the "Select Folder" button.
- The project named "Boilerplate" will now be in the "Projects List". Click on it.
- When Unity3D opens, in the "Hierachy" section expand "Menu Scene" then select "MenuCanvas"
- In the "Inspector" section find the sub-section titled "MainMenuScript".
- If the "MainMenuScript" sub-section is not expanded, expand it.
- Using the information from your Moralis Server, fill in Application Id and Server URL.
- If the Wallet Connect property is set to "None" drag WalletConnect from the "Hierarchy" section to this input.
- Click the Play icon located at the top, center of the Unity3D IDE.

# 🧭 Table of contents

- [`ethereum-unity-boilerplate`](#ethereum-unity-boilerplate)
- [🚀 Quick Start](#-quick-start)
- [🧭 Table of contents](#-table-of-contents)
- [🧰 Moralis SDK](#-moralis-sdk)
    - [`Client`](#client)
    - [`Authentication`](#authentication)  
    - [`Queries`](#queries)  
    - [`Live Queries`](#live-queries)
    - [`Custom Objects`](custom-objects)
    - [`User Object`](#user-object)
    - [`HostManifestData`](#hostmanifestdata)
    - [`ServerConnectionData`](#server-connectiondata)
- [🏗 Ethereum Web3Api Methods](#-ethereum-web3api-methods)
    - [`Web3Api Notes`](#web3api-notes)
    - [`Chains`](#chains)
    - [`Account`](#account)
        - [`GetNativeBalance`](#getnativebalance)
        - [`GetNFTs`](#getnfts)
        - [`GetNFTsForContract`](#getnftsforcontract)
        - [`GetNFTTransfers`](#getnfttransfers)
        - [`GetTokenBalances`](#gettokenbalances)
        - [`GetTokenTransfers`](#gettokentransfers)
        - [`GetTransactions`](#gettransactions)
    - [`Defi`](#defi)
    - [`Native`](#native)
        - [`GetBlock`](#GetBlock)
        - [`GetContractEvents`](#GetContractEvents)
        - [`GetDateToBloc`](#GetDateToBloc)
        - [`GetLogsByAddress`](#GetLogsByAddress)
        - [`GetNFTTransfersByBlock`](#GetNFTTransfersByBlock)
        - [`GetTransaction`](#GetTransaction)
        - [`RunContractFunction`](#RunContractFunction)
    - [`Resolve`](#resolve)
    - [`Storage`](#erc20balance)
    - [`Token`](#erc20transfers)
- [Helpful Tools](#helpful-tools)
  
# 🏗 Moralis SDK
  The.NET Moralis SDK provides easy to use method that make integrating your application with Moralis a snap. You will find that the.NET SDK works much the same as in JavaScript. For use in Unity3D we have added additional quick start objects that make integrating the Moralis SDK in a Unity3D application. 
  For the examples that follow we provide examples of how to use the Moralis.NET SDK directly and perform the same functionality using the provided Moralis Unity3D quick start tools.
  
## `Client`
  The Moralis SDK Client provides a way to easily interact with Moralis database and the Web3API. In .NET we use the *MoralisClient*
  to interact with Moralis. For Unity3D we have provided a signleton wrapper named *MoralisInterface* that makes it easy to initialize the MoralisClient and then access it from anywhere in your Unity3D application. With either option you can initialize the Moralis Client with a single line of code
  
### SDK Client Initialization
**Required Using Statements**
```
using Moralis;
using Moralis.Platform; 
using Moralis.Web3Api.Client;
```
**Initialize Client**
```
MoralisClient moralis = new MoralisClient(new ServerConnectionData() { ApplicationID = "YOUR_APPLICATION_ID_HERE", ServerURI = "YOUR_SERER_URL_HERE"}, new Web3ApiClient());
```
_note: The **new Web3ApiClient()** parameter is optional and should be included only when you will be using functionality fromt the Moralis Web3AP REST service._

### Unity3D Client Initialization
**Initialize Client**
```
MoralisInterface.Initialize(MoralisApplicationId, MoralisServerURI, hostManifestData);
```
_note: For the **hostManifestData** parameter see [`HostManifestData`](#hostmanifestdata). This is requried for Unity3D applications._

## `Authentication`
Description here

## `Queries`
Description here

## `Live Queries`
Description here

## `Custom Object`
Description here

## `User Object`
Description here

## `HostManifestData`
Description here

## `ServerConnectionData`
Description here


# 🏗 Ethereum Web3Api Methods

## `Web3Api Notes`
The complete Moralis Web3API schema including endpoints, operations and models, can be found by loggining into your Moralis Server and selecting **Web3 API***

For use with either Moralis SDK or in Unity3d, the following using statements are requried:
```
using System.Collections.Generic;
using Moralis.Web3Api.Models;
```

## `Chains`
Use the code snippet below to retrieve a list of EVM chains supported in the Moralis Web3API. This list can be used for populating dropdown lists etc.
```
List<ChainEntry> chains = MoralisInterface.SupportedChains;
```

## `Account`
Code examples demonstrating how to use the Moralis Web3API Account endpoint and operations.

### `GetNativeBalance`
Gets native balance for a specific address
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **providerUrl** _string_ OPTIONAL web3 provider url to user when using local dev chain
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
```
NativeBalance balance = MoralisInterface.GetClient().Web3Api.Account.GetNativeBalance(address.ToLower(), ChainList.eth);
```

### `GetNFTs`
Gets NFTs owned by the given address
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **format** _string_ OPTIONAL The format of the token id
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
- **order** _string_ OPTIONAL The field(s) to order on and if it should be ordered in ascending or descending order. Specified by: fieldName1.order,fieldName2.order. Example 1: "name", "name.ASC", "name.DESC", Example 2: "Name and Symbol", "name.ASC,symbol.DESC"
```
NftOwnerCollection balance = MoralisInterface.GetClient().Web3Api.Account.GetNFTs(address.ToLower(), ChainList.eth);
```

### `GetNFTsForContract`
Gets NFTs owned by the given address
- **address** _string_ REQUIRED Target address
- **tokenAddress** _string_ REQUIRED Address of the contract
- **chain** _ChainList_ REQUIRED The chain to query
- **format** _string_ OPTIONAL The format of the token id
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
- **order** _string_ OPTIONAL The field(s) to order on and if it should be ordered in ascending or descending order. Specified by: fieldName1.order,fieldName2.order. Example 1: "name", "name.ASC", "name.DESC", Example 2: "Name and Symbol", "name.ASC,symbol.DESC"
```
NftOwnerCollection balance = MoralisInterface.GetClient().Web3Api.Account.GetNFTsForContract(address.ToLower(), tokenAddress, ChainList.eth);
```

### `GetNFTTransfers`
Gets the transfers of the tokens matching the given parameters
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **format** _string_ OPTIONAL The format of the token id
- **direction** _string_ OPTIONAL The transfer direction
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
- **order** _string_ OPTIONAL The field(s) to order on and if it should be ordered in ascending or descending order. Specified by: fieldName1.order,fieldName2.order. Example 1: "name", "name.ASC", "name.DESC", Example 2: "Name and Symbol", "name.ASC,symbol.DESC"
```
NftTransferCollection balance = MoralisInterface.GetClient().Web3Api.Account.GetNFTTransfers(address.ToLower(), ChainList.eth);
```

### `GetTokenBalances`
Gets token balances for a specific address
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
```
List<Erc20TokenBalance> balance = MoralisInterface.GetClient().Web3Api.Account.GetTokenBalances(address.ToLower(), ChainList.eth);
```

### `GetTokenTransfers`
Gets ERC20 token transactions in descending order based on block number
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **fromBlock** _string_ OPTIONAL The minimum block number from where to get the logs.
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
- **fromDate** _string_ OPTIONAL The date from where to get the logs (any format that is accepted by momentjs).
- **toDate** _string_ OPTIONAL Get the logs to this date (any format that is accepted by momentjs)
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
```
List<Erc20Transaction> balance = MoralisInterface.GetClient().Web3Api.Account.GetTokenTransfers(address.ToLower(), ChainList.eth);
```

### `GetTransactions`
Gets native transactions in descending order based on block number
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **fromBlock** _string_ OPTIONAL The minimum block number from where to get the logs.
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
- **fromDate** _string_ OPTIONAL The date from where to get the logs (any format that is accepted by momentjs).
- **toDate** _string_ OPTIONAL Get the logs to this date (any format that is accepted by momentjs)
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
```
TransactionCollection balance = MoralisInterface.GetClient().Web3Api.Account.GetTransactions(address.ToLower(), ChainList.eth);
```

## `Defi`
Code examples demonstrating how to use the Moralis Web3API Defi endpoint and operations.


## `Native`
Code examples demonstrating how to use the Moralis Web3API Native endpoint and operations.

### `GetBlock`
Gets the contents of a block by block hash
- **blockNumberOrHash** _string_ REQUIRED The block hash or block number
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
```
Block block = MoralisInterface.GetClient().Web3Api.Native.GetBlock(blockNumberOrHash, ChainList.eth);
```

### `GetContractEvents`
Gets events in descending order based on block number
- **address** _string_ REQUIRED Target address
- **topic** _string_ REQUIRED The topic of the event
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **providerUrl** _string_ OPTIONAL web3 provider url to user when using local dev chain
- **fromBlock** _string_ OPTIONAL The minimum block number from where to get the logs.
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
- **fromDate** _string_ OPTIONAL The date from where to get the logs (any format that is accepted by momentjs).
- **toDate** _string_ OPTIONAL Get the logs to this date (any format that is accepted by momentjs)
- **offset** _integer_ REQUIRED Offset
- **limit** _integer_ REQUIRED Limit
```
List<LogEvent> logEvents = MoralisInterface.GetClient().Web3Api.Native.GetContractEvents(address, topic, ChainList.eth);
```

### `GetDateToBlock`
Gets the closest block of the provided date
- **data** _string_ REQUIRED Unix date in miliseconds or a datestring (any format that is accepted by momentjs)
- **chain** _ChainList_ REQUIRED The chain to query
- **providerUrl** _string_ OPTIONAL web3 provider url to user when using local dev chain
```
BlockDate blockDate = MoralisInterface.GetClient().Web3Api.Native.GetDateToBlock(date, ChainList.eth);
```

### `GetLogsByAddress`
Gets the logs from an address
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **blockNumber** _string_ OPTIONAL The block number.
- **fromBlock** _string_ OPTIONAL The minimum block number from where to get the logs.
- **toBlock** _string_ OPTIONAL The maximum block number from where to get the logs.
- **fromDate** _string_ OPTIONAL The date from where to get the logs (any format that is accepted by momentjs).
- **toDate** _string_ OPTIONAL Get the logs to this date (any format that is accepted by momentjs)
- **topic0** _string_ OPTIONAL 
- **topic1** _string_ OPTIONAL 
- **topic2** _string_ OPTIONAL 
- **topic3** _string_ OPTIONAL 
```
LogEventByAddress logEvents = MoralisInterface.GetClient().Web3Api.Native.GetLogsByAddress(address, ChainList.eth);
```

### `GetNFTTransfersByBlock`
Gets NFT transfers by block number or block hash
- **blockNumberOrHash** _string_ REQUIRED The block hash or block number
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
```
NftTransferCollection nftTransfers = MoralisInterface.GetClient().Web3Api.Native.GetNFTTransfersByBlock(blockNumberOrHash, ChainList.eth);
```

### `GetTransaction`
Gets the contents of a block transaction by hash
- **transactionHash** _string_ REQUIRED The transaction hash
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)

```
BlockTransaction blockTransaction = MoralisInterface.GetClient().Web3Api.Native.GetTransaction(transactionHash, ChainList.eth);
```

### `RunContractFunction`
Runs a given function of a contract abi and returns readonly data
- **address** _string_ REQUIRED Target address
- **chain** _ChainList_ REQUIRED The chain to query
- **subdomain** _string_ OPTIONAL The subdomain of the moralis server to use (Only use when selecting local devchain as chain)
- **providerUrl** _string_ OPTIONAL web3 provider url to user when using local dev chain
- **functionName** _string_ OPTIONAL Function name of the target function.
```
string result = MoralisInterface.GetClient().Web3Api.Native.RunContractFunction(address, functionName, ChainList.eth);
```


## `Resolve`
Code examples demonstrating how to use the Moralis Web3API Resolve endpoint and operations.


## `Storage`
Code examples demonstrating how to use the Moralis Web3API Storage endpoint and operations.


## `Token`
Code examples demonstrating how to use the Moralis Web3API Token endpoint and operations.

# Helpful Tools
1. [Unity3d Assets](https://assetstore.unity.com/)
    The best place to find Unity3d Assets for a range of budgets.
2. [The Gimp](https://www.gimp.org/)
    Open source image editing tool
3. [Blender](https://www.blender.org/)
    Open source tool for creating 3D models, animations, textures, andeverything else you need for game characters and objects.
4. [Maximo](https://www.mixamo.com/)
    Free to use (with registration) Animations for huminoid rigged models.
