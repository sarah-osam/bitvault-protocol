# BitVault Protocol (BVP)

A next-generation decentralized finance protocol enabling Bitcoin-native stablecoin minting with advanced risk management and governance, built on Stacks L2.

## Overview

BitVault Protocol is a revolutionary Bitcoin-native stablecoin system that leverages Stacks L2 for enhanced scalability and security. Users can lock their Bitcoin as collateral through trustless vaults to mint BVP stablecoins while maintaining strict collateralization ratios and automated risk management.

## Key Features

- **Trustless Bitcoin Collateralization**: Lock BTC as collateral to mint stablecoins
- **Dynamic Multi-Oracle Price Feeds**: Reliable price data through multiple oracle sources
- **Automated Liquidation Mechanisms**: Protect protocol solvency
- **Governance-Controlled Risk Parameters**: Adaptable risk management
- **Enhanced Security Measures**: Robust error handling and access controls

## Core Components

### Token Standard

- Implements the SIP-010 token standard for fungible tokens
- Includes standard methods: transfer, get-name, get-symbol, get-decimals, get-balance, get-total-supply

### Vault System

- Users can create vaults to lock collateral
- Each vault tracks:
  - Collateral amount
  - Stablecoin minted
  - Creation timestamp
  - Owner information

### Risk Management

- Minimum collateralization ratio: 150%
- Liquidation threshold: 125%
- Dynamic price feeds from authorized oracles
- Automated liquidation mechanisms

### Oracle System

- Multi-oracle support for price feeds
- Price validation and timestamp checks
- Authorized oracle management

## Core Functions

### Vault Management

```clarity
(create-vault (collateral-amount uint))
(mint-stablecoin (vault-owner principal) (vault-id uint) (mint-amount uint))
(redeem-stablecoin (vault-owner principal) (vault-id uint) (redeem-amount uint))
```

### Risk Management

```clarity
(liquidate-vault (vault-owner principal) (vault-id uint))
(update-collateralization-ratio (new-ratio uint))
```

### Oracle Operations

```clarity
(add-btc-price-oracle (oracle principal))
(update-btc-price (price uint) (timestamp uint))
```

### Read-Only Functions

```clarity
(get-latest-btc-price)
(get-vault-details (vault-owner principal) (vault-id uint))
(get-total-supply)
```

## Security Features

### Error Handling

- Comprehensive error codes for all operations
- Strict parameter validation
- Access control checks

### Constants and Limits

- Maximum BTC price validation
- Timestamp bounds checking
- Mint limits and fee structures

## Protocol Parameters

### Initial Configuration

- Collateralization Ratio: 150%
- Liquidation Threshold: 125%
- Mint Fee: 0.5%
- Redemption Fee: 0.5%

### Governance Controls

- Contract owner can modify risk parameters
- Oracle management system
- Protocol fee adjustments

## Usage Examples

### Creating a Vault

```clarity
;; Create a new vault with 1 BTC collateral
(create-vault u100000000)
```

### Minting Stablecoins

```clarity
;; Mint 1000 BVP tokens
(mint-stablecoin tx-sender u1 u1000)
```

### Liquidating an Undercollateralized Vault

```clarity
;; Liquidate vault when below threshold
(liquidate-vault vault-owner u1)
```

## Error Codes

| Code  | Description               |
| ----- | ------------------------- |
| u1000 | Not authorized            |
| u1001 | Insufficient balance      |
| u1002 | Invalid collateral        |
| u1003 | Undercollateralized       |
| u1004 | Oracle price unavailable  |
| u1005 | Liquidation failed        |
| u1006 | Mint limit exceeded       |
| u1007 | Invalid parameters        |
| u1008 | Unauthorized vault action |

## Security Considerations

1. **Access Control**

   - Only authorized oracles can update prices
   - Only vault owners can mint/redeem
   - Only contract owner can modify parameters

2. **Price Safety**

   - Maximum price bounds
   - Multiple oracle validation
   - Timestamp checks

3. **Vault Safety**
   - Minimum collateralization requirements
   - Automatic liquidation mechanisms
   - Strict parameter validation

## Contributing

The BitVault Protocol is open for community contributions. Please ensure all changes:

- Maintain or enhance security
- Include comprehensive tests
- Follow existing code style
- Include detailed documentation
