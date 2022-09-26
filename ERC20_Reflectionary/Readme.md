




ERC20_Reflectionary / Reward Token ( RWD ) Token Contract: -
(Gas used: 0.00605054 GWEI )
https://rinkeby.etherscan.io/address/0xC7cF2110f2Ff415F4bb971C53F5e5a250c066434#code



ETHEREUM Reflectionary Token (RWD ): -

https://docs.google.com/document/d/1phIeL4UXa-gbeQ_ZO26er_zmUtEpgNcarA9ozEi8G4c/


Usage:-

NOTE-: Using Remix Ide for Contract creating and deployment.

Reflectionary Token:

Now, we are going to focus on creating a Reflectionary Token  (ERC20 Based). As you know the ERC20 Token is open zeppelin Standard. We are just importing files from the open zeppelin of ERC20 Token. After importing, flattened the file of ERC20_ReflectionaryToken.sol.Then all the importing files will be expanded into one file.

Now, we see the Read and Write functions of Staking Token on Remix Ide after compiling and deploying. And also can check on EtherScan Rinkeby Testnet given link (https://rinkeby.etherscan.io/address/0xC7cF2110f2Ff415F4bb971C53F5e5a250c066434#code ) of deployed contract.


Read Functions:-
1.AdminWallet
This function returns the address of the current Admin Wallet. 

2. allowance
This function returns the current approved number of tokens by an owner to a specific delegate, as set in the approve function.

3.balanceOf
balanceOf will return the current token balance of an account, identified by its owner’s address.

4. decimals
An optional field is used to determine to what decimal place the amount of the token will be calculated. The most common number of decimals to consider is 18.

5. name
This is an optional field, but many popular tokens include it so that popular wallets like Mist and MyEtherWallet are able to identify them.

6. holders
This function returns the bool (true or false) value as you are given input as address value. Tells about whether this address is the holder or not.
7. owner
the owner will return the current owner account address of the contract/token.

8.liquidityPoolAddress
This function returns the address of the current Liquidity Pool Contract Address. 
9. symbol
Another optional field used to identify a token is a three or four-letter abbreviation of the token, just like BTC, ETH, AUG, or SJCX.

10.tokenHolderAddresses
This function returns the addresses of all token holders. As given input unit (id) value.

11.totalSupply
Although the supply could easily be fixed, as with Bitcoin, this function allows an instance of the contract to calculate and return the total amount of the token that exists in circulation.

Write Functions:-

NOTE:- All the Reflectionary Token logic in the transfer function. The main thing is the transfer function.

 1.approve
When calling this function, the contract owner authorizes or approves, the given address to withdraw instances of the token from the owner’s address.
Here, and in later snippets, you may see a variable msg . This is an implicit field provided by external applications such as wallets so that they can better interact with the contract. The Ethereum Virtual Machine (EVM) lets us use this field to store and process data given by the external application. msg.sender is the address of the contract owner.
 2. changeAdminWallet
When calling this function, the contract owner can change the Admin Wallet Address.
 3. changeLiquidityPool
When calling this function, the contract owner can change the Liquidity Pool Address.

4.decreaseAllowance
When calling this function, the owner decreases the approved amount of spender.

5.increaseAllowance
When calling this function, the owner increases the approved amount of spender.

6.renounceOwnership
When calling this function, Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.
7.transfer
This transfer function is not the same as the traditional one. This function is written for the Reflectionary Token. In which has some checks and calculates the percentage of adminWalletAddress,liquidityPoolAddress, and tokenHoldersAddress. Then after performing the following functionality for all the Addresses and transfer the amount after calculating the percentage.
This function lets the owner of the contract send a given amount of the token to another address just like a conventional cryptocurrency transaction.
8.transferFrom
This transferFrom function is not the same as the traditional one. This function is written for the Reflectionary Token. In which has some checks and calculates the percentage of adminWalletAddress,liquidityPoolAddress, and tokenHoldersAddress. Then after performing the following functionality for all the Addresses and transfer the amount after calculating the percentage.
This function allows a smart contract to automate the transfer process and send a given amount of the token on behalf of the owner.
One may question why we need both transfer() and transferFrom() functions.
Consider transferring money to pay a bill. It’s extremely common to send money manually by taking the time to write a check and mail it to pay the bill off. This is like using transfer() : you’re doing the money transfer process yourself, without the help of another party.
In another situation, you could set up automatic bill pay with your bank. This is like using transferFrom() : your bank’s machines send money to pay off the bill on your behalf, automatically. With this function, a contract can send a certain amount of the token to another address on your behalf, without your intervention.

9.transferOwnership
When calling this function, the owner changes the given address for ownership.

Implemented ERC20 Reflectionary/Reward Tokens:-

ERC20 Reflectionary/Reward Token is the same token standard discussed in our ERC20 Token detailed overview. If you want to explore it you can go to the given (). We just changed the following parameters and added some functionality related to the Reflectionary.

To make use of the ERC20 smart contract, simply copy the ERC20_Reflectionary.sol file in the contract folder and use it after changing the following parameters.

Token Info / Changes:-

Name: Reward Token (Change as per your requirements)
Symbol: RWD (Change as per your requirements)
Decimals: 18  (Change as per your requirements)
Supply: 500,000,000 (Change as per your requirements)

Change Addresses:-


AdminWallet
liquidityPoolAddr



Change Taxes:-

Just give percentage+00. E.g : 2 => 2% || 45 => 45 %

taxToAdminWallet
taxToLiquidityPoolAddr
taxToTokenHolder





Disclaimer:-

This ERC-20-based Reflectionary/Reward smart contract was created for use in production-level blockchain applications and is thoroughly tested to the best of the developers' knowledge to work as intended.



That's it! you're done. 

