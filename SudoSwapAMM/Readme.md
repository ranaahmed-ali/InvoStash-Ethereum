











ETHEREUM
SudoSwap AMM


SudoSwap AMM Documentation:-
https://docs.google.com/document/d/1cn0-VnH0Exm9fqCvEmKnXgHsk2X1wl9eTF9bMBKzyrs/edit#

Example Video for SudoSwap Flow:-
https://trello.com/1/cards/6311dc8170f3ca01f3249e80/attachments/6329a0d16c3d8b00ed0aa43f/download/SudoSwapAMM_Flow.mkv



What is sudoswap AMM?

The sudoswap AMM is a minimal, gas-efficient AMM protocol for facilitating NFT (ERC721s) to token (ETH or ERC20) swaps using customizable bonding curves. Liquidity providers (LPs) can deposit into single-sided buy or sell pools, or provide both sides with a spread to capture fees.

The base unit of the protocol is the LSSVMPair which can hold NFTs, tokens or both. End users then interact with LSSVMRouter to swap across multiple pools and manage their approvals on one contract.

Similar to other floor NFT protocols, the current sudoswap AMM protocol makes no distinction between different ERC721 IDs. Pools willing to buy or sell NFTs will return the same price no matter which NFT is sent in or out from the collection.



SudoAMM
An implementation of the AMM protocol is described here.
Liquidity providers use LSSVMPairFactory to deploy a modified minimal proxy LSSVMPair for a specific NFT collection. From there, the deployed pool maintains its own TOKEN/NFT inventory. Users can then call the various swap functions on the pool to trade TOKEN/NFTs.
LSSVMPairs are either LSSVMPairEnumerable or LSSVMPairMissingEnumerable depending on whether or not the pair's ERC721 contract supports Enumerable or not. If it doesn't, we implement our own ID set to allow for easy access to NFT IDs in the pool.
For the actual token, NFTs are paired either with an ERC20 or ETH, so there are 4 types of pairs:
Missing Enumerable | ETH
Missing Enumerable | ERC20
Enumerable | ETH
Enumerable | ERC20
The LSSVMRouter allows splitting swaps across multiple LSSVMPairs to purchase and sell multiple NFTs in one call.
An LSSVMPair can be TOKEN, NFT, or TRADE. The type refers to what the pool holds:
a TOKEN pool has tokens that it is willing to give to traders in exchange for NFTs
an NFT pool has NFTs that it is willing to give to traders in exchange for tokens
TRADE pools allow for both TOKEN-->NFT and NFT-->TOKEN swaps.
The LSSVMPair swap functions are named from the perspective of the end user. EX: swapTokenForAnyNFTs means the caller is sending ETH and receiving NFTs.
In order to determine how many NFTs or tokens to give or receive, each LSSVMPair calls a discrete bonding curve contract that conforms to the ICurve interface. Bonding curve contracts are intended to be pure; it is the responsibility of LSSVMPair to update its state and perform input/output validation.
See inline comments for more on swap/bonding curve logic.

 


 
 
 
 
 
 
Architecture:-
See the diagram below for a high-level overview:








 
 
 
Creating A Pair:-
New pairs for the sudoswap AMM are created with the LSSVMPairFactory. LPs will call either createPairETH or createPairERC20 depending on their token type (i.e. if they wish to utilize ETH or an ERC20). This will deploy a new LSSVMPair contract.
Each pair has one owner (initially set to be the caller), and multiple pools for the same token and NFT pair can exist, even for the same owner. This is due to each pair having its own potentially different spot price and bonding curve.
 
Pair Types
Each pair can be one of 3 types: Token, NFT, or Trade.

A Token pair holds either ETH or an ERC20 token and will give a quote for how much it will pay for any NFT in the collection it has been created for.

An NFT pair holds NFTs and will give a quote for how much it will sell for any NFT it has in its inventory.

A Trade pair holds both NFTs and tokens, and it will give a quote for both buying and selling, with a spread between the quotes as the LP fee.



Pair Parameters
During the creation call, LPs supply the following parameters:
IERC721 _nft, // The ERC721 token side of the pair
ICurve _bondingCurve, // The bonding curve used to price the pair
address payable _assetRecipient, // If set to a non-zero address, assets sent to the pair during a swap will be forwarded to this address. NOTE: unavailable for Trade pairs.
LSSVMPair.PoolType _poolType, // The pair's type (Token, NFT, Trade)
uint256 _delta, // The bonding curve's parameter (more on this in the Bonding Curve section)
uint256 _fee, // The spread between buy and sell quotes. NOTE: only for Trade pairs.
uint256 _spotPrice, // The initial sell quote the pair will return if an NFT is sold into it.
uint256[] calldata _initialNFTIDs // The list of IDs to transfer from the caller to the pair

 
 
 
For an ERC20 pair, two other parameters are also added:
ERC20 token // The token to be used for the token side of the pair.
uint256 initialTokenBalance // The amount of tokens to send into the pair. (The createPairETH call is payable, and msg.value is used instead)

The factory uses a modified minimal proxy pattern to allow deployed pairs to cheaply access certain values the same way that immutable normally works. See LSSVMPairCloner for more technical details.
As a result, several of the above parameters cannot be changed after a pool is deployed:
_nft,
_bondingCurve,
_poolType,
token // NOTE: only for ERC20 pairs

 
Managing A Pair
The owner of a pair can modify certain parameters to change the pair's pricing and inventory.
To modify spotPrice, delta, and fee, the owner can call changeSpotPrice, changeDelta, and changeFee (only for Trade pairs).
To withdraw any NFTs or tokens sent to the pair, the owner can call withdrawERC721, withdrawERC20, and withdrawETH (only for ETH pairs).


Bonding Curves and Pricing:-
To determine pricing, each LSSVMPair is associated with a specific bonding curve set by the LP. At present, there are two choices: LinearCurve and ExponentialCurve. Both curves are parameterized by one variable, delta, which is set in the pair itself. More bonding curve contracts can be whitelisted in the future for use with LSSVMPairFactory.
After a user trades with a pair, the pair consults its bonding curve to determine what its new price should be.
Technical note: the bonding curves are intended to be pure, i.e. they do not modify the state of pairs that call them. The actual logic for input/output validation and price updating happens in the LSSVMPair contract itself.
Linear Curve
The linear curve performs an additive operation to update the price. delta is assumed to be set properly by the LP to be the same precision as the pair's underlying token.
If the pair has just sold an NFT by giving out an NFT and receiving tokens, the next price it will quote to sell NFTs will be delta more. Conversely, if the pair has just bought an NFT by giving out tokens and receiving an NFT, the next price it will quote to purchase NFTs at will be delta less.
 
 
 
Exponential Curve
The exponential curve performs a multiplicative operation. delta is treated as a multiplier assuming a fixed point system where 1e18 is 1.
For example, if delta is 1e18 + 1e17, this represents a 10% change in price each time.
If the pair has just sold an NFT by giving out an NFT and receiving tokens, the next price it will quote to sell NFTs at will be multiplicatively delta more. Conversely, if the pair has just bought an NFT by giving out tokens and receiving an NFT, the next price it will quote to purchase NFTs will be multiplicatively delta less.
 
Understanding Spot Price
In addition to modifying delta to change the pair's price reactivity, it is important to understand how the spotPrice variable in LSSVMPair behaves.
The spot price refers to the instantaneous price of selling 1 NFT to the pair. The instantaneous price of buying 1 NFT from the pair is set to be the spotPrice adjusted upwards by 1 unit of delta with respect to the pair's bonding curve.
For example, say that we have a Trade LSSVMPair for ETH with a spotPrice of 1 ETH, and a linear curve with a delta of 0.1 ETH. (Assume fee is 0.) Then a user selling 1 NFT to the pair would receive 1 ETH, whereas a user purchasing 1 NFT from the pair would have to send (1 + 0.1) = 1.1 ETH.
In other words, the price to purchase an NFT from a pair will always be delta greater (either additively on multiplicatively) than the price to sell an NFT to the pair.
Pair managers who are manually adjusting spotPrice should keep this in mind.
(Note that for simplicity, some examples in this documentation may use "spot price" to also refer to the instantaneous buy price.)
 
Pricing For Multi-Swaps
If a user buys or sells multiple NFTs in one swap transaction, the spotPrice will update by delta for each NFT bought or sold.
For example, say that we have a Trade LSSVMPair for ETH with a spotPrice of 1 ETH, and a linear curve with a delta of 0.1 ETH. (Assume fee is 0.)
If a user sells 5 NFTs to this pair, they will receive:
1 ETH for the first NFT
0.9 ETH for the second NFT
0.8 ETH for the third NFT
0.7 ETH for the fourth NFT
0.6 ETH for the fifth NFT
At the end of the multi-swap, the new spotPrice will be set to 0.5 ETH.


 
 
Swapping Across Pairs
The recommended way to make swaps across various pairs is to use the LSSVMRouter. Users can set allowances for tokens and NFTs once for the router, instead of for each new pool they wish to swap with.
On the protocol level, the sudoswap AMM does not perform any routing optimization on-chain. Users are expected to know their desired swap paths when calling the router, e.g. via the use of off-chain indexing service.
 
NFT<>Token Swaps
When swapping tokens for NFTs, users can either specify which NFT IDs they want from each pair, or they can ask for any ID from the pair.
When swapping from NFT to tokens or from tokens to NFTs, the LSSVMRouter has two types of swaps: a Normal Swap and a Robust Swap.
 
 
Normal Swap
A Normal Swap is conceptually similar to token-to-token swaps on other DEXs. The user sends the router a maximum input amount or minimum output amount (i.e. allowed slippage), as well as a swap route and a deadline. The router will then swap across the various pairs specified. At the end of all the swaps, the router will total all tokens to be received or sent, and revert if the total is beyond the user's specified slippage.
Robust Swap
In contrast, a Robust Swap does a slippage check per swap pair rather than an aggregate check at the end. If the price for a specified swap pair is past the allowable slippage, the router will silently skip that route and move on to the next one, with no reverts or errors.
This is intended for situations where the price can move quickly between your transaction submission and execution.
Normal vs Robust Swap
To see the difference between these swap types, consider this example: say there are 2 pairs for NFT and ETH. The first pair has a spot price of 1 ETH and a linear curve with a delta of 0.1 ETH. The second pair has a spot price of 1 ETH and a linear curve with a delta of 1 ETH.
A user wishes to purchase NFTs, one from each pool for 1 ETH each, with 10% slippage.
The user submits a swap transaction. Before this transaction is executed, someone else goes and buys 1 NFT from each pool for 1 ETH each.
The new spot price for the first pair is 1.1 ETH, and for the second pair is 2 ETH.
If the user had submitted a Normal Swap, they would have sent 2.2 ETH (2 ETH + 0.2 ETH to cover the additional 10% slippage), and the transaction would fail, as they would have sent enough ETH to cover the first swap at the new price of 1.1 ETH, but not enough to cover the second swap at 2 ETH.
In contrast, if the user had submitted a Robust Swap, they would have also sent 2.2 ETH, but with a per-swap max cost of 1.1 ETH. The router would have enough to cover the first swap at 1.1 ETH. Then, upon seeing the second swap would cost 2 ETH, the router would skip this pair entirely. The transaction would succeed, refunding 1.1 ETH back to the user, as well as sending them the one NFT they purchased for 1.1 ETH.
Thus, the Robust Swap is generally recommended for a better user experience in higher volatility environments, at the cost of slightly more gas.

NFT<>NFT Swaps
As another added convenience, the LSSVMRouter also supports swapping NFTs for tokens and then tokens to other NFTs in one transaction.
Like the token to NFT swap, users can either specify specific NFT IDs from a pair or ask for any NFT ID.





Implementation:- 
( All contracts are optimized )


Mainnet Contract Addresses
EXPONENTIAL_CURVE:-  ( Gas used: 0.00720991 GWEI  )
https://etherscan.io/address/0x432f962D8209781da23fB37b6B59ee15dE7d9841#code
LINEAR_CURVE:-	( Gas used: 0.00607323 GWEI  )
https://etherscan.io/address/0x5B6aC51d9B1CeDE0068a1B26533CAce807f883Ee#code
PAIR_FACTORY:-	( Gas used: 0.03329575 GWEI  )
https://etherscan.io/address/0xb16c1342E617A5B6E4b631EB114483FDB289c0A4#code
PAIR_ROUTER:-	( Gas used: 0.21073008 GWEI  )
https://etherscan.io/address/0x2b2e8cda09bba9660dca5cb6233787738ad68329#code


 
 
Rinkeby Contract Addresses
EXPONENTIAL_CURVE:-	( Gas used: 0.00094571 GWEI  )
https://rinkeby.etherscan.io/address/0xBc6760B11e433D25aAf5c8fCBC6cE99b14aC5D52
LINEAR_CURVE:-	( Gas used: 0.00085912 GWEI  )
https://rinkeby.etherscan.io/address/0x3764b9FE584719C4570725A2b5A2485d418A186E
PAIR_FACTORY:-	( Gas used: 0.00435997 GWEI  )
https://rinkeby.etherscan.io/address/0xcB1514FE29db064fa595628E0BFFD10cdf998F33#code
PAIR_ROUTER:-	( Gas used: 0.00654244 GWEI  )
https://rinkeby.etherscan.io/address/0x9ABDe410D7BA62fA11EF37984c0Faf2782FE39B5#code






Usage Flow:-
Step-by-step Guide to Using Sudoswap
There are many ways to use Sudoswap, so let's start from scratch. 
Head over to Sudoswap. 
Connect your wallet at the top-right corner. 
Click on "Your Pools".
On a new page, click on "Create New Pool". At this point, you'll be presented with several options.
These options are to...
Buy NFTs with tokens
Sell NFTs for tokens
Do both and earn protocol fees

Clicking on any of the options will take you to a new page. For the token, only ETH is currently available. When the time comes to select an NFT, you may select only NFTs you already hold in your wallet. 
On the next page, you set up your pool. Here, what you should pay special attention to are the Bonding Curve and the Delta. The Bonding Curve is either Linear or Exponential, Linear being denoted in ETH, and Exponential being denoted as a percentage value. The Delta connotes the amount of change in price per NFT sold or bought. 
In the final step, all you need to do is review your information and then click "Create Pool". That's it. You're done.


Sample Video of Sudo Swap Flow:

Click on the given link: SudoSwapAMM Flow video.mkv




