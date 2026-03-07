# ⬡ SHGChain — BC-02
## Transparent Crowdfunding Platform for Rural Self-Help Groups with On-Chain Fund Tracking

**Stack:** Solidity · Hardhat · React · MetaMask · Polygon Amoy Testnet

---

## 📁 What's in This Project

```
shgchain/
├── contracts/
│   ├── SHGCrowdfund.sol       ← Main contract: campaigns, donations, escrow, milestones
│   ├── SoulBoundToken.sol     ← ERC-5192 non-transferable donor badge
│   └── RefundGovernance.sol   ← 48hr voting + auto-execute refund
├── scripts/
│   └── deploy.js              ← Deploy all 3 contracts to Polygon Amoy
├── test/
│   └── SHGCrowdfund.test.js   ← Unit tests
├── frontend/
│   └── src/
│       ├── pages/             ← Home, Campaign, CreateCampaign, Governance, DonorProfile, Dashboard
│       ├── components/        ← Navbar with MetaMask connect
│       ├── hooks/             ← useWallet (MetaMask), useContract (ethers.js)
│       └── context/           ← WalletContext (global wallet state)
├── hardhat.config.js          ← Polygon Amoy config
├── .env.example               ← Copy to .env and fill in
└── README.md
```

---

## 🚀 HOW TO RUN — Step by Step

### STEP 1 — Install Node.js
```
Download from: https://nodejs.org
Choose: LTS version (18 or 20)
After install, open terminal and check:
  node --version   → should show v18.x or v20.x
  npm --version    → should show 9.x or 10.x
```

### STEP 2 — Install project dependencies
```bash
# In the shgchain folder:
npm install

# In the frontend folder:
cd frontend
npm install
cd ..
```

### STEP 3 — Set up environment variables
```bash
# Copy the example file
cp .env.example .env

# Open .env and fill in:
# PRIVATE_KEY        = your MetaMask private key
# POLYGON_AMOY_RPC   = from Alchemy (free): https://alchemy.com
# POLYGONSCAN_API_KEY = from https://amoy.polygonscan.com
# REACT_APP_CLAUDE_API_KEY = from https://console.anthropic.com
```

### STEP 4 — Get free test MATIC
```
Go to: https://faucet.polygon.technology
Connect wallet → Select "Polygon Amoy"
Click "Submit" → You get 0.5 free test MATIC
```

### STEP 5 — Compile contracts
```bash
npm run compile
```

### STEP 6 — Run tests
```bash
npm run test
```

### STEP 7 — Deploy to Polygon Amoy
```bash
npm run deploy:amoy
```
This will:
- Deploy SHGCrowdfund, SoulBoundToken, RefundGovernance
- Seed 2 test campaigns
- Save contract addresses to frontend/src/constants/addresses.js

### STEP 8 — Start the React frontend
```bash
npm run frontend
# Opens at http://localhost:3000
```

### STEP 9 — Add Polygon Amoy to MetaMask
```
Open MetaMask → Add Network → Add manually:
  Network Name: Polygon Amoy Testnet
  RPC URL:      https://rpc-amoy.polygon.technology/
  Chain ID:     80002
  Symbol:       MATIC
  Explorer:     https://amoy.polygonscan.com
```
(The app also does this automatically when you connect!)

---

## 🔗 Useful Links

| Resource | URL |
|---|---|
| Polygon Amoy Faucet | https://faucet.polygon.technology |
| Polygon Amoy Explorer | https://amoy.polygonscan.com |
| Alchemy (free RPC) | https://www.alchemy.com |
| MetaMask | https://metamask.io |
| OpenZeppelin | https://openzeppelin.com |
| Claude API | https://console.anthropic.com |

---

## 🏗 BC-02 Features Implemented

| Feature | Contract | Status |
|---|---|---|
| Milestone-based escrow | SHGCrowdfund.sol | ✅ |
| Impact Score (0-100, documented formula) | SHGCrowdfund.sol | ✅ |
| Soul-Bound Token donor badges (ERC-5192) | SoulBoundToken.sol | ✅ |
| Refund governance (48hr vote + auto-execute) | RefundGovernance.sol | ✅ |
| SHG peer vouching | SHGCrowdfund.sol | ✅ |
| Donor live fund trail | React frontend | ✅ |
| Recurring micro-donations | (extend SHGCrowdfund) | 🔧 Extend |
| Auto PDF impact report | (backend service) | 🔧 Extend |

---

## ⚠️ Important Notes

- Use TEST MATIC only — no real money
- Never commit your `.env` file to GitHub
- Impact Score formula is public and documented in the contract comments
- All fund releases are automatic — no admin can manually approve
