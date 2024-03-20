# Overview
NUSDProtocol's goal is to scalably issue a $1 pegged decentralized stablecoin, FEI.

At a high level the NUSDpeg mechanism is straightforward. NUSDProtocol algorithmically manages a reserve of tokens (Protocol controlled value) which supports direct redeption of nUSDat $1.

## Direct Redeemability​
NUSDcan be minted and redeemed for $1 of collateral. Arbitrageurs ensure a tight peg on secondary markets.

The assets which can be minted or redeemed change among DAI, ETH and LUSD depending on market conditions.

## Protocol Controlled Value​

The protocol reserves are known as Protocol Controlled Value or PCV. The PCV is deployed into a combination of liquid and illiquid strategies with the following goals:

1. Defending the peg
2. Providing utility/liquidity to NUSDand Tribe DAO products
3. Growing through yield farming

## Tribe​
Tribe serves as both a governance mechanism and beneficiary of protocol productivity.

Tribe insures reserve shortfalls, if PCV ever dips below 100% collateralization, an on-chain recovery mechanism would issue new TRIBE to buy back nUSDdebt.

When a surplus exists, the protocol buys back TRIBE off of the market with nUSDat a percentage of the surplus.

# Access control
NUSD Protocol has a role based access control, where each role grants a specific permission over a specific part of the protocol. The roles are assigned to three categories: Major, Admin and Minor. They are documented in TribeRoles.

Major roles are the most powerful across the protocol, Admin have management capability over critical functionality and Minor are operational roles.

## Major roles​
There are 4 major roles:

- GOVERNOR: Ultimate control over the NUSD ecosystem. Able to create new roles and access all protocol functionality

- GUARDIAN: Emergency safety role that is used to protect the protocol. Able to pause contracts and veto malicious proposals

- PCV_CONTROLLER: Allows the movement of PCV of any size from any contract to any address

- MINTER: Can mint NUSD

## How they work​
Role creation is limited to the GOVERNOR role. Created roles are stored in the storage of Core.sol, and each created role is assigned an admin over that role.

The admin of a role is then able to grant and revoke that role from individual addresses. The API for creating, granting and revoking roles looks like:

```
core.createRole(keccak256("DUMMY_ROLE"), keccak256("GOVERN_ROLE"));

core.grantRole(keccak256("DUMMY_ROLE"), dummyAddress);

core.revokeRole(keccak256("DUMMY_ROLE"), dummyAddress);
```
This pattern is implemented using the AccessControlEnumerable.sol contract pattern from OpenZeppelin.

See more info for each role on the Detailed Access Control page.




