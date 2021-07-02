# UniswapFlashSwap

An abstraction for UniswapV2 flash swaps.
Enables the user to borrow any token and repay using any other token.
Abstracts away most of the nitty-gritty details of the UniswapV2 core contracts.

## How to use
1. Deploy the FlashSwapContract the parameters to Constructor are two addresses. _WETH and _DAI are the parameters which are addresses of WETH and DAI token on respective network.
2. You need some tokens in the contract before executing a flash swap. You can do this by simply sending the token from the wallet to the address of contract. In order to understand how much balance is required, please check fees section.
3. In order to execute a Flash Swap, call the flashSwap() function. The parameters of this function are:
- _tokenBorrow The address of the token you want to flash-borrow, use 0x0000000000000000000000000000000000000000 for ETH.  
- _amount The amount of _tokenBorrow you will borrow.  
- _tokenPay The address of the token you want to use to payback the flash-borrow, use 0x0000000000000000000000000000000000000000 for ETH.  
- _userData Data that will be passed to the `execute` function for the user. You can send some value like 'flash'.  
4. You can see the flash swap on the network.
5. In order to withdraw the Token, call withdraw() function. This function takes address of token as input. If you want to withdraw ETH, pass 0x0000000000000000000000000000000000000000 as parameter.

### Address

The contract is deployed on Ropsten Testnet. The address is [0x936f988CdD068C9e2e94800Cf712515c2E3F78C5](https://ropsten.etherscan.io/address/0x936f988cdd068c9e2e94800cf712515c2e3f78c5)

#### Sample Transactions:
##### Flash Swap
- Flash Swap ETH [0xe5c37eafc26f7064479b1df87acc6824fbd0043ac34b860f2d89fcd0fae340b4](https://ropsten.etherscan.io/tx/0xe5c37eafc26f7064479b1df87acc6824fbd0043ac34b860f2d89fcd0fae340b4)  
- Flash Swap DAI[0x3f1c317a2e2cecc8d1de91d4fa7f8491daccc5021a92f9dbe7d08447fa766a58 ](https://ropsten.etherscan.io/tx/0x3f1c317a2e2cecc8d1de91d4fa7f8491daccc5021a92f9dbe7d08447fa766a58)  
##### Withdraw
- Withdraw ETH [0x138056d580bbd727285d7ebb814f01eebfb8de7af8f3423b86617c1879301392](https://ropsten.etherscan.io/tx/0x138056d580bbd727285d7ebb814f01eebfb8de7af8f3423b86617c1879301392)
- Withdraw DAI [0x69211cbb7a69945dd8ee7f32b9497ffb953548da2efdd944f19ad101df11cf93](https://ropsten.etherscan.io/tx/0x69211cbb7a69945dd8ee7f32b9497ffb953548da2efdd944f19ad101df11cf93)

## Fees

Each UniswapV2 pair charges a `0.3%` fee.

- If you are doing a traditional "flash loan", where you repay using the same token that you borrowed, you'll be charged a `0.3%` fee.
- If you are borrowing ETH or WETH and repaying with a non-{ETH, WETH} token, you'll be charged a `0.3%` fee.
- If you are borrowing a non-{ETH, WETH} token and repaying with ETH or WETH, then you'll be charged a `0.3%` fee.
- If you are swapping a non-{ETH, WETH} token for another non-{ETH, WETH} token, then you'll be charged a `0.6%` fee because your swap will touch _two_ UniswapV2 pairs (they are routed through the WETH).

# Reference
https://github.com/Austin-Williams/uniswap-flash-swapper
