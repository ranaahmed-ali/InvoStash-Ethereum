STATIC_STAKING_CONTRACTS:-

StaticStakingContract :- ( Gas used: 0.00753592 GWEI )
https://rinkeby.etherscan.io/address/0x8401919f15899f9ee446c859d5cf64dde3f670d8#code

ERC20 Staking Token:- ( Gas used: 0.00389616 GWEI )
https://rinkeby.etherscan.io/address/0xa5312489fc99ae91a37a5a8646a436cbea4cbe14#code

ERC20 Reflectionary/Reward Token:- ( Gas used: 0.00605054 GWEI )
https://goerli.etherscan.io/address/0x9d50f46ddaf35971d6165633984ff0e2ffc4af91#code

ETHEREUM Static_Staking_Contract Documentation:-https://docs.google.com/document/d/1gDJP3WgrLpY9ozBULrpZkvKo9YzIcSRXbrm7FyP0eg0/








What is Staking :
Staking is the way many cryptocurrencies verify their transactions, and it allows participants to earn rewards on their holdings. But what is crypto staking? Staking cryptocurrencies is a process that involves committing your crypto assets to support a blockchain network and confirm transactions. You can explore it by the provided link(https://www.coinbase.com/learn/crypto-basics/what-is-staking).

Ethereum Staking :

What is staking? Staking is the act of depositing 32 ETH to activate validator software. As a validator, you'll be responsible for storing data, processing transactions, and adding new blocks to the blockchain. This will keep Ethereum secure for everyone and earn you new ETH in the process. You can learn more about it by the provided link(https://ethereum.org/en/staking/).


Implementation:- 
( All contracts are optimized )

StaticStakingContract:-  ( Gas used: 0.00753592 GWEI )
https://rinkeby.etherscan.io/address/0x8401919f15899f9ee446c859d5cf64dde3f670d8#code
ERC20_Reflectionary:-  ( Gas used: 0.00605054 GWEI  )
https://rinkeby.etherscan.io/address/0xC7cF2110f2Ff415F4bb971C53F5e5a250c066434#code
ERC20_StakinToken:- ( Gas used: 0.00389616 GWEI )
https://rinkeby.etherscan.io/address/0xa5312489fc99ae91a37a5a8646a436cbea4cbe14#code



Deployment procedure:- ( Remix )

Deploying a Contract to Mainnet or Testnet Using Remix.
Step 1- Create a file in Remix with your project name. And paste your code. Select the correct compiler version.

Step 2- Navigate to the Compile sidebar option and press the Compile StaticStakingContract.sol button or just CTRL + S, it will compile your contract.

Step 3- Select your desired contract with a contract name from CONTRACT. 

Step 4- Now you can deploy the contract by navigating to the Deployment sidebar option. You need to change the topmost ENVIRONMENT dropdown from JavaScript VM to Injected Web3. This tells Remix to use the MetaMask injected provider, which will point it to your Mainnet or Testnet development node.
If you wanted to try this using another network, you would have to connect MetaMask to the correct network instead of your local development node.

When you select Injected Web3, you will be prompted to allow Remix to connect to your MetaMask account. Press Next in MetaMask to allow Remix to access the selected account.

Step 5- Back on Remix, you should see that the account you wish to use for deployment is now managed by MetaMask.  Next to the Deploy button, paste the addresses of staking_Token & Reflectionary_Token.
Select Deploy.

You will be prompted in MetaMask to confirm the contract deployment transaction.
After you press Confirm and the deployment is complete, you will see the transaction listed in MetaMask. The contract will appear under Deployed Contracts in Remix.


Video Tutorial: Ethereum Smart Contract with Remix
ERC20 Static Staking :

Now, we are going to focus on creating a Static Staking   (ERC20 Based). As you know the ERC20 Token is open zeppelin Standard. We are just using the Interface of deployed Staking Token () and Reflectionary/Reward Token as ER20-based Token.


NOTE:- We are using Interface in this Contract. You can learn about the Smart Contract Interface by providing the link (https://www.newline.co/courses/creating-an-erc20-token-on-ethereum/smart-contract-interfaces)


Now, we see the Read and Write functions of Static Staking on Remix Ide after compiling and deploying. And also can check on EtherScan Rinkeby Testnet given link (https://rinkeby.etherscan.io/address/0x8401919f15899f9ee446c859d5cf64dde3f670d8#code) of deployed contract.




Read Functions:-

1. durationRewardRate: This function returns the reward rate ( % age ) of the duration.

2. durations: This function returns the fixed Size array (4) of time duration starting from 0 indexes to 3.

3. getAllStakes: This function returns the all stakes of the user.

4. governor: This function returns the address of the owner of this contract.

5. paused: This function returns true ( if the contract is paused ) otherwise false.

6. rates: This function returns the fixed Size array (4) of  % age of staked amount, starting from 0 indexes to 3. 

7. rewardToken: This function returns an address of the reflectionary/reward token contract. 
8. stakingToken: This function returns an address of the staking token contract. 

9. totalCurrentHoldings: This function returns the total amount user staked in the contract. 

10. totalExpectedRewards: This function returns the total reward you will get based on your all-staked amount.

11. totalOutstanding: This function returns the total reward amount, we need to have in the contract to give users their reward.

12. totalStaked: This function returns the total staked amount user staked and also returns the totalStakeCount of the user.

13. userStakes: This function returns all the information regarding user stakes.


Write Functions:-


Only Owner Functions:-

 1. setPaused: When calling this function, the contract owner can lock the staking functionality by typing true.

2. transferGovernance: This function is used to transfer the ownership to another address.

 3. claimGovernance: This function transfer the ownership to your address if the current governor gave your address to transferGovernance.






User Functions:-

 4. stake: When calling this function, you can stake an amount after approval from the Staking Token to this Static Staking Contract Address. You can stake the amount of token at durations and the percentages of reward rates (0 => 15 sec with 4% ,1=> 30 sec with 6% , 2=> 45 sec with 8% , 3=> 60 sec with 9% ) . 

5. Unstake: When you call this function, You can unstake the stake amount with the stakeId. This will give you your staked amount & reward ( based on rate ) in reflectionary / reward token.

6. exit: When you call this function, you will exit from the contract. All your staked amount & reward ( based on rate ) will be transferred to your account. If some stake timing hasn’t been completed, this will skip that stake.


Usage Flow:-

After deploying all three contracts e.g: static_Staking_Contract , staking_Token & reflectionary/ reward_Token .

Step 1: Transfer the totalSupply of rewardToken (or how much reward you want to give + all stake amount will be returned in rewardToken) to this contract. All stake amount will be returned in rewardToken.

Step 2: Approve the amount you want to stake from the staking_Token contract.
Note:  give Static_Staking contract address in spender.

Step 3: Call or use the stake function from the Static_Staking contract. 
( amount you want to stake, duration (choose 1) ).

Step 4: Call or use the Unstake function from the Static_Staking contract.
 ( your staking_Id). Or just exit.


Changes:- 

Change the static array values of durations [15 seconds, 30 seconds, 45 seconds, 60 seconds ] according to your needs.

Change the static array values of rates [4 , 6 , 8 , 9 ] ( 4 % , 6 % , 8 % , 9 % )
 Just give percentage E.g : 2 => 2% || 45 => 45 % .

Durations:-

durations 0 = 0 represents [ 15 second duration & 4 % reward ]
durations 1 = 1 represents [ 30 second duration & 6% reward ]
durations 2 = 2 represents [ 45 second duration & 8% reward ]
durations 3 = 3 represents [ 60 second duration & 9 % reward ]



Disclaimer:-

This ERC-20-based Static Staking smart contract was created for use in production-level blockchain applications and is thoroughly tested to the best of the developers' knowledge to work as intended.



That's it! you're done. 
