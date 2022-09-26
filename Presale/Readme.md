











ETHEREUM
PreSale (ERC20 based)



Implementation:-
( All contracts are optimized )

Presale:- ( Gas used: 0.00352608 GWEI )
https://goerli.etherscan.io/address/0x2c65716efbdd689c23d19ade455b73007c552d7e#code

ERC20_StakingToken:- ( Gas used: 0.00395976 GWEI )
https://goerli.etherscan.io/address/0xf166ecb87308137994a4e72ca7fca04e69eaf158#code

ETHEREUM PreSale ERC20 AhmedAli Documentation:-
https://docs.google.com/document/d/15fK0jVY9al8iJtRfyunFc_BPnF85JUWVTfToTtVC_0k/




What is PreSale?
Presale is a process or a set of activities/sales normally carried out before a customer is acquired, though sometimes presales also extend into the period the product or service is delivered to the customer.


What is PreSale in Blockchain?
Pre-selling is a practice performed by some crypto projects ahead of an initial coin offering, in which tokens are sold to interested parties at a certain price. This could be considered beneficial for both investors and the development team if all were to go well and the digital currency would be a success.



Basic Intro of PreSale:-
Pre-selling is a practice performed by some crypto projects ahead of an initial coin offering, in which tokens are sold to interested parties at a certain price.
This could be considered beneficial for both investors and the development team if all were to go well and the digital currency would be a success. 
While the project’s creators would receive much-needed funds to finalize the project, investors have the potential to acquire an altcoin that could be worth a lot more in the future.
Developers may also perform a pre-sale to create buzz ahead of the ICO, hoping for a price surge when the asset goes public.

It is worth noting that pre-selling can come with risks. If a project fails, investors can find themselves owning worthless tokens, unable to make a profit from their investment. This adds to the fact that, when the actual ICO takes place, the plethora of coins now available to the public might dampen the value of the ones they initially bought.

 







ERC20  Functions :

ERC-20 defines six different implementation coding functions for the benefit of other tokens within the Ethereum system.
In terms of implementation coding for ERC-20 tokens, the six basic coding functions are:
total supply (Total Supply of your Token)
balance of  (Balance of the wallet & Contract Address)
allowance  (Check the allowance of the Token to the spender on behalf of the owner)
transfer      (Transfer the token from Owner to any Address ) 
approve      (Approval to the spender to send the token from the owner address approved token)
transfer from (Transfer from the owner address to any address connected with the spender wallet   address)



Implementation:- 
( All contracts are optimized )


Presale:-  ( Gas used: 0.00352608  GWEI  )
https://goerli.etherscan.io/address/0x2c65716efbdd689c23d19ade455b73007c552d7e#code
ERC20_StakingToken:- ( Gas used: 0.00395976 GWEI )
https://goerli.etherscan.io/address/0xf166ecb87308137994a4e72ca7fca04e69eaf158#code

Deployment procedure:- ( Remix )

Deploying a Contract to Mainnet or Testnet Using Remix.
Step 1- Create a file in Remix with your project name. And paste your code. Select the correct compiler version.

Step 2- Navigate to the Compile sidebar option and press the Compile PreSale.sol button or just CTRL + S, it will compile your contract.

Step 3- Select PreSale from CONTRACT. 

Step 4- Now you can deploy the contract by navigating to the Deployment sidebar option. You need to change the top ENVIRONMENT dropdown from JavaScript VM to Injected Web3. This tells Remix to use the MetaMask injected provider to point it to your Mainnet or Testnet development node.
If you wanted to try this using another network, you would have to connect MetaMask to the correct network instead of your local development node.

When you select Injected Web3, you will be prompted to allow Remix to connect to your MetaMask account. Press Next in MetaMask to enable Remix to access the selected account.

Step 5- Back on Remix, you should see that the account you wish to use for deployment is now managed by MetaMask.Next to the Deploy button, paste the addresses of Wallet & Token.
Select Deploy.

You will be prompted in MetaMask to confirm the contract deployment transaction.
After you press Confirm and the deployment is complete, you will see the transaction listed in MetaMask. The contract will appear under Deployed Contracts in Remix.


Video Tutorial: Ethereum Smart Contract with Remix



PreSale.sol

This PreSale contract sells the tokens to everyone or just whitelisted addresses at the set rate by the owner.


Read Functions:-
1- isPreSaleStarted: This function tells us if the PreSale is started or not.
2- owner: This function will return the current owner's address.
3- rate: This function will return the rate, set by the owner at which people will buy tokens.
4- senderWhitelist: This function will return true or false if the address is whitelisted or not. If not it can’t do the transaction.
5- useSenderWhitelist: This function will return true or false if at least one sender is whitelisted, then ONLY whitelisted senders are allowed.
6- wallet: This function will return the address of the wallet.
7- weiRaised: This function will return the total of Wei we raised in PreSale.






Write Functions:-

Constructor arguments:-

WalletAddress: It is the wallet to which ether will be sent whenever a user will buy tokens.
Token: Address of your ERC20 Token.


Only Owner Functions:-

 1. startPresale: Start the preSale of your tokens, give the rate in the function argument and call this function.

 2. changeRate: This function is used to the rate of your tokens at which people will buy.

 3. changeWalletAddress: This function is used to change the address of the wallet.
 
 4. whitelistSender: This function is used to whitelist the user’s address, so that address can buy tokens.
Note: If you don’t whitelist any address then everyone can buy tokens, If you give 1 address then only that address can buy tokens.

5. blacklistSender: This function is used to blacklist the user’s address, so that address cannot buy tokens.

6. endPresale: End the preSale of your tokens.

6. sellEveryone: This function is used to sell tokens to everyone after using the whitelisted function.






User Functions:-

 4. buyTokens: To buy tokens, give the address of the beneficiary and give the ether amount of how much you want.
Note: Just send ethers to the contract, and it will automatically send the tokens to your address.

PreSaleERC20

Just an ordinary preSale contract, which can be reused in your project.

Usage Flow:-

After deploying the PreSale contract with your token & wallet address in the constructor on the Ethereum network.

Step 1: Transfer the number of tokens you want to sell in the PreSale contract.

Step 2: Start preSale with the rate in the argument of the function.  

Step 3: Whitelist the addresses of users or investors.
Note: If you want everyone to buy tokens, then don’t give any address. Or call sellEveryone function.

Step 4: End the preSale when you are done.







Rate Explanation:-

Firstly, all currency math is done in the smallest unit of that currency and converted to the correct decimal places when displaying the currency.
 
This means that when you do math in your smart contracts, you need to understand that you’re adding, dividing, and multiplying the smallest amount of a currency (like wei), not the commonly-used displayed value of the currency (Ether).
 
In Ether, the smallest unit of the currency is wei, and 1 ETH === 10^18 wei. In tokens, the process is very similar: 1 TKN === 10^(decimals) TKNbits.
The smallest unit of a token is "bits" or TKNbits.
The display value of a token is TKN, which is TKNbits * 10^(decimals)
What people usually call "one token" is actually a bunch of TKNbits, displayed to look like 1 TKN. This is the same relationship that Ether and wei have. And what you’re always doing calculations in is TKNbits and wei.
 
So, if you want to issue someone "one token for every 2 wei" and your decimals are 18, your rate is 0.5e18. Then, when I send you 2 Wei, your preSale issues me 2 * 0.5e18 TKNbits, which is exactly equal to 10^18 TKNbits and is displayed as 1 TKN.
 
If you want to issue someone “1 TKN` for every 1 ETH”, and your decimals are 18, your rate is `1. This is because what’s actually happening with the math is that the contract sees a user send 10^18 wei, not 1 ETH. Then it uses your rate of 1 to calculate TKNbits = rate * wei, or 1 * 10^18, which is still 10^18. And because your decimals are 18, this is displayed as 1 TKN.
 
One more for practice: if I want to issue "1 TKN for every dollar (USD) in Ether", we would calculate it as follows:
assume 1 ETH == $400
therefore, 10^18 wei = $400
therefore, 1 USD is 10^18 / 400, or 2.5 * 10^15 wei
we have a decimal of 18, so we’ll use 10 ^ 18 TKNbits instead of 1 TKN
therefore, if the participant sends the crowdsale 2.5 * 10^15 wei we should give them 10 ^ 18 TKNbits
therefore the rate is 2.5 * 10^15 wei === 10^18 TKNbits, or 1 wei = 400 TKNbits
therefore, our rate is 400
(this process is pretty straightforward when you keep 18 decimals, the same as Ether/wei)







Disclaimer:-

This PreSale smart contract was created for use in production-level blockchain applications and is thoroughly tested to the best of the developers' knowledge to work as intended.



That's it! you're done. 
