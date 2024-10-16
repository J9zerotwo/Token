# Token

## Description

This Solidity smart contract, `MyToken`, defines a basic cryptocurrency token with minting and burning functionality. The contract includes three main public variables:

1. **`tokenName`**: Holds the full name of the token (e.g., `"GIT"`).
2. **`tokenAbbrv`**: Stores the token's abbreviation (e.g., `"HUB"`).
3. **`totalSupply`**: Tracks the total number of tokens in circulation.

Additionally, the contract includes a mapping, `balances`, to track the balance of each address holding tokens. 

It features two primary functions:

1. **Mint Function (`mint`)**: Allows the creation of new tokens. It takes an address and a value as inputs, increases the `totalSupply` by the specified amount, and adds the new tokens to the address's balance.

2. **Burn Function (`burn`)**: Allows the destruction of tokens from a specific address. It takes an address and a value as inputs, checks if the address's balance is sufficient, then reduces both the address’s balance and `totalSupply` by the specified amount if the balance meets the required threshold.

This contract implements basic token management but lacks access controls, meaning any address can currently call the `mint` or `burn` functions.

### Executing program

Here’s a step-by-step breakdown of how the `MyToken` contract works, explaining each action and how it impacts the contract's variables.

---

### Step 1: Deployment of the Contract
When the `MyToken` contract is deployed to the blockchain:
- The **public variables** (`tokenName`, `tokenAbbrv`, `totalSupply`) are initialized. In this case:
  - `tokenName` is set to `"GIT"`.
  - `tokenAbbrv` is set to `"HUB"`.
  - `totalSupply` is set to `0`, indicating no tokens have been minted yet.
- A **mapping** named `balances` is created, which maps addresses to their token balances. Initially, every address has a balance of `0`.

---

### Step 2: Minting New Tokens
The `mint` function is used to create new tokens and assign them to a specified address.

#### How `mint` Works:
1. **Function Call**: The function is called with two parameters:
   - `_address`: The address to which the minted tokens will be assigned.
   - `_value`: The number of tokens to mint.
   
2. **Token Creation**:
   - The `totalSupply` is increased by `_value`, reflecting the creation of new tokens.
   - The `balances` mapping is updated so that the balance of `_address` increases by `_value`.

#### Example:
```solidity
mint(0x123...abc, 100);
```
- If `totalSupply` was `0`, it becomes `100`.
- The balance of `0x123...abc` becomes `100`.

---

### Step 3: Burning Tokens
The `burn` function allows tokens to be destroyed, reducing both the total supply and the balance of a specified address.

#### How `burn` Works:
1. **Function Call**: The function is called with two parameters:
   - `_address`: The address from which tokens will be burned.
   - `_value`: The number of tokens to burn.
   
2. **Balance Check**:
   - The function checks if `balances[_address]` is greater than or equal to `_value`.
   - If true, it proceeds; if false, the function does nothing, preventing an insufficient balance error.

3. **Token Destruction**:
   - `totalSupply` is reduced by `_value`, reflecting the destruction of tokens.
   - `balances[_address]` is decreased by `_value`, reducing the address's balance by the specified amount.

#### Example:
```solidity
burn(0x123...abc, 50);
```
- If `0x123...abc` has `100` tokens, it decreases to `50`.
- `totalSupply` is reduced by `50` as well.

---

### Summary of Key Variables After Each Step
- **`totalSupply`**: Increases with each call to `mint`, decreases with each successful call to `burn`.
- **`balances`**: Updated to reflect token transfers, either adding or subtracting tokens from specific addresses based on minting or burning.

---

### Limitations to Consider
- **Access Control**: Currently, any address can call the `mint` and `burn` functions, which could be problematic if unauthorized entities create or destroy tokens.
  
Adding access control (e.g., only allowing the owner to mint or burn tokens) could improve security and make the contract production-ready.

