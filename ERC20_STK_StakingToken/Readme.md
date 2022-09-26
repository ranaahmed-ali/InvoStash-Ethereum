
See Documentation for extra details.
Docs : https://docs.google.com/document/d/1XE2AJ18Lb7X5xDOnsUmQf5i4V9TaMH3IWdpPdYUvOrk/

Staking Token ( STK ) ERC20 Token Contract: - ( Gas used: 0.00389616 GWEI )
https://rinkeby.etherscan.io/address/0xa5312489fc99ae91a37a5a8646a436cbea4cbe14#code






ETHEREUM
Staking Token (ERC20 based)


Usage:-
Basic Intro of ERC20 Token:-

The popular Blockchain System Ethereum is based on the use of Tokens. One of the most significant Ethereum tokens is known as ERC-20. ERC-20 has emerged as the technical standard; it is used for all smart contracts on the Ethereum blockchain for token implementation and provides a list of rules that all Ethereum-based tokens must follow. 
Plenty of well-known digital currencies use the ERC-20 standard, including Maker (MKR), Basic Attention Token (BAT), Augur (REP), and OmiseGO (OMG).


ERC20  Functions :

ERC-20 defines six different implementation coding functions for the benefit of other tokens within the Ethereum system.
In terms of implementation coding for ERC-20 tokens, the six basic coding functions are:
total supply (Total Supply of your Token)
balance of  (Balance of the wallet & Contract Address)
allowance  (Check the allowance of the Token to the spender on the behalf of the owner)
transfer      (Transfer the token from Owner to any Address ) 
approve      (Approval to the spender to send the token from the owner address approved token)
transfer from (Transfer from the owner address to any address connected with the spender wallet   address)
You can also read the detailed documentation of the above-mentioned functions from the following link Open Zeppelin Standard.



Openzeppelin Standard:

OpenZeppelin is an open-source framework to build secure smart contracts. OpenZeppelin provides a complete suite of security products and audit services to build, manage, and inspect all aspects of software development and operations for decentralized applications.


ERC-20 Token using Openzeppelin Standard (https://docs.openzeppelin.com/contracts/2.x/api/token/erc20).All the functionalities of ERC20 Token are provided previously by the given link of Open Zeppelin Standard. Please visit the previously given link to explore more about ERC20 Token.



Implementation of ERC20 Token :
This contract is optimized.


ERC20 Staking Token:- ( Gas used: 0.00389616 GWEI )    https://rinkeby.etherscan.io/address/0xa5312489fc99ae91a37a5a8646a436cbea4cbe14#code 


Deployment procedure:- ( Remix )

Deploying a Contract to Mainnet or Testnet Using Remix.
Step 1- Create a file in Remix with your project name. And paste your code. Select the correct compiler version.

Step 2- Navigate to the Compile sidebar option and press the Compile ERC20_StakinToken.sol button or just CTRL + S, it will compile your contract.

Step 3- Select your desired contract with a contract name from CONTRACT. 

Step 4- Now you can deploy the contract by navigating to the Deployment sidebar option. You need to change the topmost ENVIRONMENT dropdown from JavaScript VM to Injected Web3. This tells Remix to use the MetaMask injected provider, which will point it to your Mainnet or Testnet development node.
If you wanted to try this using another network, you would have to connect MetaMask to the correct network instead of your local development node.

As soon as you select Injected Web3, you will be prompted to allow Remix to connect to your MetaMask account. Press Next in MetaMask to allow Remix to access the selected account.

Step 5- Back on Remix, you should see that the account you wish to use for deployment is now managed by MetaMask. Select Deploy.

You will be prompted in MetaMask to confirm the contract deployment transaction.
After you press Confirm and the deployment is complete, you will see the transaction listed in MetaMask. The contract will appear under Deployed Contracts in Remix.


Video Tutorial: Ethereum Smart Contract with Remix NOTE-: Using Remix Ide for Contract creating and deployment.





Staking Token:

Now, we are going to focus on creating a Staking Token (ERC20 Based). As you know about the ERC20 Token is open zeppelin Standard.We are just importing file from open zeppelin of ERC20 Token.After importing flattened the file of ERC20_StakingToken.sol.Then all the importing file will be expand in one file.


Now, we see the Read and Write functions of Staking Token on Remix Ide after compile and deploying.And also can check on EtherScan Rinkeby Testnet given link (https://rinkeby.etherscan.io/address/0xa5312489fc99ae91a37a5a8646a436cbea4cbe14#code ) of deployed contract.









Read Functions:-

1.allowance
This function returns the current approved number of tokens by an owner to a specific delegate, as set in the approve function.

2.balanceOf
balanceOf will return the current token balance of an account, identified by its owner’s address.

3.decimals
An optional field used to determine to what decimal place the amount of the token will be calculated. The most common number of decimals to consider is 18.

4.name
This is an optional field, but many popular tokens include it so that popular wallets like Mist and MyEtherWallet are able to identify them.

5.owner
owner will return the current owner  account address of contract/token.

6.symbol
Another optional field used to identify a token, this is a three or four letter abbreviation of the token, just like BTC, ETH, AUG, or SJCX.

7.totalSupply
Although the supply could easily be fixed, as it is with Bitcoin, this function allows an instance of the contract to calculate and return the total amount of the token that exists in circulation.

Write Functions:-

 1.approve
When calling this function, the owner of the contract authorizes, or approves, the given address to withdraw instances of the token from the owner’s address.
Here, and in later snippets, you may see a variable msg . This is an implicit field provided by external applications such as wallets so that they can better interact with the contract. The Ethereum Virtual Machine (EVM) lets us use this field to store and process data given by the external application. msg.sender is the address of the contract owner.

2.decreaseAllowance
When calling this function, the owner decreases the approved amount of spender.

3.increaseAllowance
When calling this function, the owner increases the approved amount of spender.

4.renounceOwnership
When calling this function, Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.
5.transfer
This function lets the owner of the contract send a given amount of the token to another address just like a conventional cryptocurrency transaction.
6.transferFrom
This function allows a smart contract to automate the transfer process and send a given amount of the token on behalf of the owner.
One may question why we need both transfer() and transferFrom() functions.
Consider transferring money to pay a bill. It’s extremely common to send money manually by taking the time to write a check and mail it to pay the bill off. This is like using transfer() : you’re doing the money transfer process yourself, without the help of another party.
In another situation, you could set up automatic bill pay with your bank. This is like using transferFrom() : your bank’s machines send money to pay off the bill on your behalf, automatically. With this function, a contract can send a certain amount of the token to another address on your behalf, without your intervention.

7.transferOwnership
When calling this function, the owner changes the given address for ownership.


Implemented Staking Token:-
To make use of the ERC20 smart contract, simply copy the ERC20_StakingToken.sol from the repo, flattened file (flattened file included all the import library in Smart Contract regarding ERC20 Token) in the contract folder and use it after changing the following parameters.

Token Info / Changes:-

Name: Staking Token (Your Token Name)
Symbol: STK (Symbol your Token)
Decimals: 18 (Ethereum standard is 18 decimals)
Supply: 500,000,000 (Total Supply of your Token)


Compile & Run Smart Contract (ERC20).

After changing parameters (Name, Symbol, Decimals, Supply) as your requirements. Compile & Run the Smart Contract on Remix Ide (Browser-Based IDE). 

Disclaimer:-

This ERC-20 smart contract was created for the purpose to use in production-level blockchain applications and is thoroughly tested to the best of the developers' knowledge to work as intended.



That's it! you're done. 












