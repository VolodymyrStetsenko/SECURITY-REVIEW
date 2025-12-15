# About

Volodymyr Stetsenko is an independent smart contract security researcher focused on manual
auditing, automated and static analysis, and property-based / fuzz testing and formal verifi-
cation of EVM-based protocols. His work emphasizes rigorous code review, careful reasoning about
protocol assumptions, and identifying high-impact logic, economic, and architectural weaknesses.

I’m continuously sharpening my expertise through deep study, public audit practice, and trans-
parent documentation of my methods. My approach combines manual inspection with a tool-
driven workflow — including static analyzers (e.g., Slither), fuzzers and property-based testing (e.g.,
Echidna, Foundry fuzzing), symbolic checks, invariant assertions, and formal verification where ap-
propriate — to ensure comprehensive coverage of both functional and economic risk vectors.

# Disclaimer

A smart contract security review can never verify the complete absence of vulnerabilities. This is a time, resource and expertise bound effort where we try to find as many vulnerabilities as possible. We can not guarantee 100% security after the review or even if the review will find any problems with your smart contracts. Subsequent security reviews, bug bounty programs and on-chain monitoring are strongly recommended.

# Risk Classification
 
| Severity               | Impact: High | Impact: Medium | Impact: Low |
| ---------------------- | ------------ | -------------- | ----------- |
| **Likelihood: High**   | Critical     | High           | Medium      |
| **Likelihood: Medium** | High         | Medium         | Low         |
| **Likelihood: Low**    | Medium       | Low            | Low         |

## Impact

- High - leads to a significant material loss of assets in the protocol or significantly harms a group of users.

- Medium - leads to a moderate material loss of assets in the protocol or moderately harms a group of users.

- Low - leads to a minor material loss of assets in the protocol or harms a small group of users.

## Likelihood
 
- High - attack path is possible with reasonable assumptions that mimic on-chain conditions, and the cost of the attack is relatively low compared to the amount of funds that can be stolen or lost.

- Medium - only a conditionally incentivized attack vector, but still relatively likely.

- Low - has too many or too unlikely assumptions or requires a significant stake by the attacker with little or no incentive.

## Action required for severity levels
 
- Critical - Must fix as soon as possible (if already deployed)

- High - Must fix (before deployment if not already deployed)

- Medium - Should fix

- Low - Could fix

# Protocol Summary

PasswordStore is a smart contract protocol designed to allow users to store and retrieve
passwords on the Ethereum blockchain. The protocol’s primary objective is to provide a
decentralized password management solution where only the authorized owner can access
stored credentials.

# Executive Summary

A time-boxed security review of the PasswordStore protocol was done by Volodymyr Stetsenko, with a focus on the security aspects of the application's smart contracts implementation.

| Attribute               | Details | 
| ---------------------- | ------------ |
| **Protocol**   | PasswordStore     |
| **Auditor** | Volodymyr Stetsenko         |
| **Solc Version**    | 0.8.18       |
| **Blockchain**   | Ethereum    |
| **Methodology** | Manual Code Review, Static Analysis         |
| **Review Period**    | November 24–26, 2025       |
| **Commit Hash**    | `7d55682ddc4301a7b13ae9413095feffd9924566`       |

## Issues found

| Severity          | Number of issues found |
| ----------------- | ---------------------- |
| High              | 2                      |
| Medium            | 0                      |
| Low               | 1                      |
| Info              | 1                      |
| Gas Optimizations | 0                      |
| Total             | 0                      |


### Scope

The following smart contracts were in scope of the audit:

```
./src/
└── PasswordStore.sol
```

# Findings

## High 

### [H-1] Passwords stored on-chain are visable to anyone, not matter solidity variable visibility

**Description:** All data stored on-chain is visible to anyone, and can be read directly from the blockchain. The `PasswordStore::s_password` variable is intended to be a private variable, and only accessed through the `PasswordStore::getPassword` function, which is intended to be only called by the owner of the contract. 

However, anyone can direclty read this using any number of off chain methodologies

**Impact:** The password is not private. 

**Proof of Concept:** The below test case shows how anyone could read the password directly from the blockchain. We use [foundry's cast](https://github.com/foundry-rs/foundry) tool to read directly from the storage of the contract, without being the owner. 

1. Create a locally running chain
```bash
make anvil
```

2. Deploy the contract to the chain

```
make deploy 
```

3. Run the storage tool

We use `1` because that's the storage slot of `s_password` in the contract.

```
cast storage <ADDRESS_HERE> 1 --rpc-url http://127.0.0.1:8545
```

You'll get an output that looks like this:

`0x6d7950617373776f726400000000000000000000000000000000000000000014`

You can then parse that hex to a string with:

```
cast parse-bytes32-string 0x6d7950617373776f726400000000000000000000000000000000000000000014
```

And get an output of:

```
myPassword
```

**Recommended Mitigation:** Due to this, the overall architecture of the contract should be rethought. One could encrypt the password off-chain, and then store the encrypted password on-chain. This would require the user to remember another password off-chain to decrypt the password. However, you'd also likely want to remove the view function as you wouldn't want the user to accidentally send a transaction with the password that decrypts your password. 


### [H-2] `PasswordStore::setPassword` is callable by anyone 

**Description:** The `PasswordStore::setPassword` function is set to be an `external` function, however the natspec of the function and overall purpose of the smart contract is that `This function allows only the owner to set a new password.`

```javascript
    function setPassword(string memory newPassword) external {
@>      // @audit - There are no access controls here
        s_password = newPassword;
        emit SetNetPassword();
    }
```

**Impact:** Anyone can set/change the password of the contract.

**Proof of Concept:** 

Add the following to the `PasswordStore.t.sol` test suite.

```javascript
function test_anyone_can_set_password(address randomAddress) public {
    vm.prank(randomAddress);
    string memory expectedPassword = "myNewPassword";
    passwordStore.setPassword(expectedPassword);
    vm.prank(owner);
    string memory actualPassword = passwordStore.getPassword();
    assertEq(actualPassword, expectedPassword);
}
```

**Recommended Mitigation:** Add an access control modifier to the `setPassword` function. 

```javascript
if (msg.sender != s_owner) {
    revert PasswordStore__NotOwner();
}
```


# Low Risk Findings

## <a id='L-01'></a>L-01. Initialization Timeframe Vulnerability

_Submitted by [dianivanov](/profile/clo3cuadr0017mp08rvq00v4e)._      
				
### Relevant GitHub Links
	
https://github.com/Cyfrin/2023-10-PasswordStore/blob/main/src/PasswordStore.sol

## Summary
The PasswordStore contract exhibits an initialization timeframe vulnerability. This means that there is a period between contract deployment and the explicit call to setPassword during which the password remains in its default state. It's essential to note that even after addressing this issue, the password's public visibility on the blockchain cannot be entirely mitigated, as blockchain data is inherently public as already stated in the "Storing password in blockchain" vulnerability.

## Vulnerability Details
The contract does not set the password during its construction (in the constructor). As a result, when the contract is initially deployed, the password remains uninitialized, taking on the default value for a string, which is an empty string.

During this initialization timeframe, the contract's password is effectively empty and can be considered a security gap.

## Impact
The impact of this vulnerability is that during the initialization timeframe, the contract's password is left empty, potentially exposing the contract to unauthorized access or unintended behavior. 

## Tools Used
No tools used. It was discovered through manual inspection of the contract.

## Recommendations
To mitigate the initialization timeframe vulnerability, consider setting a password value during the contract's deployment (in the constructor). This initial value can be passed in the constructor parameters.


### [I-1] The `PasswordStore::getPassword` natspec indicates a parameter that doesn't exist, causing the natspec to be incorrect

**Description:** 

```javascript
    /*
     * @notice This allows only the owner to retrieve the password.
@>   * @param newPassword The new password to set.
     */
    function getPassword() external view returns (string memory) {
```

The natspec for the function `PasswordStore::getPassword` indicates it should have a parameter with the signature `getPassword(string)`. However, the actual function signature is `getPassword()`.

**Impact:** The natspec is incorrect.

**Recommended Mitigation:** Remove the incorrect natspec line.

```diff
-     * @param newPassword The new password to set.
```