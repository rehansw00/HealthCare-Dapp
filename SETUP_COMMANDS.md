# Blockchain Healthcare DApp - Complete Setup & Deployment Guide

## Quick Start Command Sequence

### Part A: Initial Setup (One-Time)

#### 1. Clone and Navigate to Project

```bash
# Clone the repository
git clone <repository-url>
cd "Blockchain-Health-DApp"
cd "Blockchain Health DApp"
```

#### 2. Install Frontend Dependencies

```bash
# Install all npm packages
npm install

# Verify installation
npm --version    # Should be 9.x or higher
node --version   # Should be 20.x or higher

# Expected output:
# added X packages, and audited Y packages in Zs
```

#### 3. Install Smart Contract Dependencies

```bash
# Navigate to web3 folder
cd web3

# Install Hardhat and dependencies
npm install

# Verify Hardhat installation
npx hardhat --version    # Should show version

# Go back to root
cd ..
```

---

### Part B: Environment Variables Setup

#### 1. Create Frontend Environment File

**Create file**: `.env.local` in root directory

```bash
# .env.local

# === For Local Testing (Hardhat) ===
NEXT_PUBLIC_CONTRACT_ADDRESS=0x5FbDB2315678afccb333f8a9c812ab65ca569c800
NEXT_PUBLIC_OWNER_ADDRESS=0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
PINATA_JWT=pnxxxxxx_your_pinata_jwt_token_here_xxxxxx
NEXT_PUBLIC_PINATA_GATEWAY=https://gateway.pinata.cloud
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=your_wallet_connect_project_id_here

# After Sepolia deployment, replace first two lines with:
# NEXT_PUBLIC_CONTRACT_ADDRESS=0xcba321...
# NEXT_PUBLIC_OWNER_ADDRESS=0x1234...
```

#### 2. Create Smart Contract Environment File

**Create file**: `web3/.env` in web3 directory

```bash
# web3/.env

# === Sepolia Network Configuration ===
# Get RPC from Alchemy (https://www.alchemy.com/) or DRPC (https://drpc.org)
NETWORK_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_ALCHEMY_KEY

# Your private key (KEEP SECRET! Never commit!)
# Get from MetaMask: Settings → Account Details → Export Private Key
PRIVATE_KEY=0xac0974bec39a17e36ba4a6b4d238ff944bacb476chadce41699d0b13ced7eee

# Optional: Etherscan API for contract verification
ETHERSCAN_API_KEY=your_etherscan_api_key_here
```

#### 3. Get Pinata JWT Token

```bash
# Steps:
# 1. Go to https://pinata.cloud
# 2. Sign up or log in
# 3. Go to API Keys section
# 4. Create new API key
# 5. Generate JWT
# 6. Copy JWT and paste into .env.local
```

---

### Part C: Local Development Testing

#### Step 1: Terminal 1 - Start Local Blockchain

```bash
# Terminal 1:
cd web3
npx hardhat node

# Output shows:
# Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/
# 
# Accounts (10 test accounts):
# Account #0: 0x1234...abc (has 10000 ETH for testing)
# Account #1: 0x5678...def
# ...

# Keep this terminal open and running
```

#### Step 2: Terminal 2 - Deploy Contract Locally

```bash
# Terminal 2 (new terminal window):
cd web3
npx hardhat run scripts/deploy.js --network localhost

# Output:
# Deploying contracts with the account: 0x1234...abc
# Account balance: 10000000000000000000
# 
# Deploying Healthcare contract...
# 
# Deployment Successful!
# ========================
# NEXT_PUBLIC_Healthcare_ADDRESS: 0x5FbDB2315678afccb333f8a9c812ab65ca569c800
# NEXT_PUBLIC_OWNER_ADDRESS: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266

# Copy these addresses!
# Update .env.local with these values
```

#### Step 3: Configure MetaMask for Local Network

```
1. Open MetaMask chrome extension
2. Click network selector (top left)
3. Click "Add Network"
4. Fill in:
   - Network Name: Hardhat Local
   - RPC URL: http://127.0.0.1:8545
   - Chain ID: 1337
   - Currency: ETH
5. Click Save
6. Switch to "Hardhat Local" network
7. Click Account icon → Import Account
8. Paste private key from hardhat node output: 0xac0974bec39a17...
9. Click Import

Now you'll see 10000 ETH balance (test only)
```

#### Step 4: Terminal 3 - Start Frontend

```bash
# Terminal 3 (new terminal window):
# Make sure you're in root directory (not web3/)

npm run dev

# Output:
# ready - started server on 0.0.0.0:3000

# Open browser:
# http://localhost:3000
```

#### Step 5: Test Locally

```bash
# In browser at http://localhost:3000:

1. Click "Connect Wallet"
   - Select MetaMask
   - Select Hardhat Local account
   - Click Connect
   - Balance shows 10000 ETH (test)

2. Register as Doctor:
   - Click "Doctor Registration" or navigation
   - Fill form: Name, Specialization, License, etc.
   - Click Register
   - MetaMask popup confirms transaction
   - Should see success message
   - Transaction cost: ~0.0025 ETH (visible in MetaMask)

3. Check Admin Dashboard:
   - You're the admin (deployer account)
   - Should see pending doctor approval

4. Approve the Doctor:
   - In admin dashboard, find the doctor
   - Click Approve
   - Confirm transaction

5. Register as Patient (Different Account):
   - Click account selector in MetaMask
   - Create or select different account
   - Go to Patient Registration
   - Fill form
   - Register
   - Cost: ~0.00025 ETH

6. Book Appointment:
   - Switch to patient account (MetaMask)
   - Click "Book Appointment"
   - Select approved doctor
   - Choose date/time
   - Fill condition and message
   - Confirm payment
   - Cost: ~0.0025 ETH

# All tests successful on local network!
```

---

### Part D: Sepolia Testnet Deployment

#### Step 1: Get Sepolia Testnet ETH

```bash
# 1. Go to: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
# 2. Connect MetaMask wallet (make sure on Sepolia network)
# 3. Click "Give Me Eth"
# 4. Wait 1-2 minutes
# 5. Check MetaMask - should show ~0.5 ETH on Sepolia

# If MetaMask doesn't show Sepolia:
# 1. Click network selector
# 2. Find "Sepolia" in list
# 3. Click to switch
# 4. If not in list, add manually:
#    - Network Name: Sepolia
#    - RPC URL: https://eth-sepolia.g.alchemy.com/v2/YOUR_ALCHEMY_KEY
#    - Chain ID: 11155111
#    - Currency: ETH
```

#### Step 2: Update Smart Contract Environment Variables

```bash
# web3/.env - Update with Sepolia details

# Get Sepolia RPC from Alchemy:
# 1. Go to https://www.alchemy.com/
# 2. Sign up or log in
# 3. Create new app, select Sepolia
# 4. Get HTTPS URL
# 5. Paste below:

NETWORK_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY

# Get Private Key:
# 1. Open MetaMask
# 2. Settings → Account Details
# 3. Export Private Key (enter password)
# 4. Paste below (KEEP SECRET):

PRIVATE_KEY=0xac0974bec39a17e36ba4a6b4d238ff944bacb476chadce41699d0b13ced7eee
```

#### Step 3: Deploy Smart Contract to Sepolia

```bash
# Terminal (new or clear previous):

cd web3
npx hardhat run scripts/deploy.js --network sepolia

# Output:
# Deploying contracts with the account: 0x1234...abc
# Account balance: 500000000000000000
# 
# Deploying Healthcare contract...
# 
# Deployment Successful!
# ========================
# NEXT_PUBLIC_Healthcare_ADDRESS: 0xcba321xyz...
# NEXT_PUBLIC_OWNER_ADDRESS: 0x1234...abc

# Wait 30-60 seconds for confirmation

# Save these addresses!
```

#### Step 4: Verify Contract on Etherscan

```bash
# 1. Go to: https://sepolia.etherscan.io
# 2. Search for contract address from deployment: 0xcba321xyz...
# 3. Should see:
#    - Contract created
#    - Transaction confirmed
#    - Creator address (your wallet)
#    - Contract code
```

#### Step 5: Update Frontend Configuration for Sepolia

```bash
# Update .env.local:
# Replace with Sepolia addresses and update wagmi config

NEXT_PUBLIC_CONTRACT_ADDRESS=0xcba321xyz...    # From deployment
NEXT_PUBLIC_OWNER_ADDRESS=0x1234...abc         # From deployment
PINATA_JWT=pnxxxxx...
NEXT_PUBLIC_PINATA_GATEWAY=https://gateway.pinata.cloud
```

#### Step 6: Update Wagmi Configuration

```bash
# Update config/wagmi.js:
# Change from localhost to sepolia

# OLD:
import { localhost } from 'wagmi/chains'
chains: [localhost],

# NEW:
import { sepolia } from 'wagmi/chains'
chains: [sepolia],
```

#### Step 7: Switch MetaMask to Sepolia

```
1. Open MetaMask
2. Click network selector
3. Select "Sepolia"
4. Verify showing ~0.5 ETH balance
```

#### Step 8: Test on Sepolia

```bash
# Terminal (new):
# Stop any local npm dev, then:

npm run dev

# Browser: http://localhost:3000

# Test flows (same as local, but on Sepolia):
1. Connect Wallet
2. Register Doctor (costs ~$0.05-0.10 in real ETH value)
3. Register Patient
4. Book Appointment
5. View appointments

# Note: Each transaction takes 15-30 seconds on Sepolia
# (vs instant on local Hardhat)
```

---

## Production Build & Deployment

### Build for Production

```bash
# From root directory:
npm run build

# Output:
# > next build
# Creating an optimized production build...
# Compiled successfully
# 
# Route (pages)                              Size      First Load JS
# ┌ ○ /                                      123 kB    234 kB
# ├ ○ /doctors                               45 kB     156 kB
# ... more routes ...

# Creates .next/ folder with optimized build
# Takes 2-5 minutes
```

### Start Production Build Locally

```bash
# Test production build locally:
npm start

# Output:
# > next start
# ready - started server on 0.0.0.0:3000

# Browser: http://localhost:3000
# Production build is now running
```

### Deploy to Vercel (Recommended)

```bash
# Install Vercel CLI:
npm install -g vercel

# Deploy:
vercel

# Prompts:
# ? Set up "..." and deploy? [Y/n] Y
# ? Which scope do you want to deploy to? [your-account]
# ? Link to existing project? [y/N]
# ? What's your project's name? blockchain-health-dapp
# ? In which directory is your code? ./
# ? Want to modify vercel.json? [y/N]

# Deploys and gives you:
# Deployment URL: https://blockchain-health-dapp-xxxxx.vercel.app
# GitHub integration for automatic deploys
```

### Deploy to Traditional Server

```bash
# Build locally:
npm run build

# Create deployment directory on server:
ssh user@server "mkdir -p /app/health-dapp"

# Copy files to server:
scp -r .next/ package.json package-lock.json user@server:/app/health-dapp/

# On server, install and run:
ssh user@server "
cd /app/health-dapp
npm install --production
npm start
"

# Your app runs on: http://your-server:3000
# Use reverse proxy (Nginx) for port 80 access
```

### Docker Deployment

```bash
# Create Dockerfile:
cat > Dockerfile << 'EOF'
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --production
COPY .next ./.next
COPY public ./public
COPY next.config.js ./
EXPOSE 3000
CMD ["npm", "start"]
EOF

# Build image:
docker build -t blockchain-health-dapp:latest .

# Run container:
docker run -p 3000:3000 blockchain-health-dapp:latest

# Or with environment variables:
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_CONTRACT_ADDRESS=0xcba321... \
  -e NEXT_PUBLIC_OWNER_ADDRESS=0x1234... \
  -e PINATA_JWT=pnxxxxx \
  blockchain-health-dapp:latest
```

---

## Quick Reference Commands

### Development

```bash
npm run dev              # Start dev server (localhost:3000)
npm run build           # Build for production
npm start               # Run production build
npm run lint            # Check code quality
npm run clear           # Clear cache and node_modules
```

### Smart Contracts (from web3/)

```bash
npx hardhat compile     # Compile contracts
npx hardhat node        # Start local blockchain
npx hardhat test        # Run tests
npx hardhat clean       # Clear artifacts

# Deploy
npx hardhat run scripts/deploy.js --network localhost
npx hardhat run scripts/deploy.js --network sepolia
```

### Useful Links

```
Sepolia Faucet: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
Etherscan: https://sepolia.etherscan.io
Pinata: https://pinata.cloud
Wagmi Docs: https://wagmi.sh
Hardhat Docs: https://hardhat.org/docs
```

---

## Common Issues & Solutions

### Issue 1: "Cannot find module 'wagmi'"

```bash
# Solution:
npm install
# or if that doesn't work:
npm run clear
npm install
```

### Issue 2: "MetaMask not connecting"

```
1. Refresh browser (F5)
2. Check MetaMask is on correct network (Hardhat Local or Sepolia)
3. Check MetaMask extension is enabled
4. Reload MetaMask extension
```

### Issue 3: "Contract not found at address"

```bash
# Check:
1. .env.local has correct NEXT_PUBLIC_CONTRACT_ADDRESS
2. Contract deployed successfully (check terminal output)
3. MetaMask is on correct network
4. Hardhat node is still running (if using local)
```

### Issue 4: "Insufficient funds for gas"

```bash
# Solution:
1. You need ETH on the network
2. For Sepolia: Get from faucet (https://cloud.google.com/application/web3/faucet/ethereum/sepolia)
3. For local: Hardhat provides 10000 ETH automatically
4. Refresh MetaMask (Cmd/Ctrl + Shift + R)
```

### Issue 5: "Transaction reverted"

```
Check error message (usually in MetaMask or console)
Common reasons:
1. Wrong fee amount (check contract fee in error)
2. Doctor not approved by admin
3. Patient not registered
4. Duplicate registration attempt
5. Insufficient balance
```

### Issue 6: "Port 3000 already in use"

```bash
# Kill process on port 3000:

# Mac/Linux:
lsof -i :3000
kill -9 <PID>

# Windows (PowerShell):
Get-Process -Id (Get-NetTCPConnection -LocalPort 3000).OwningProcess | Stop-Process
```

---

## File Locations Reference

```
.env.local              ← Frontend environment variables (root)
web3/.env               ← Smart contract environment (web3 folder)
config/contract.js      ← Contract address & ABI
config/wagmi.js         ← Wagmi configuration
hooks/useContract.js    ← Contract interaction functions
utils/ipfs.js           ← IPFS integration
pages/                  ← All routes (Next.js)
components/             ← React components
web3/contracts/         ← Solidity contracts
web3/scripts/           ← Deployment scripts
```

---

## Testing Workflow

```
1. Start local Hardhat node (Terminal 1)
2. Deploy contract to local network (Terminal 2)
3. Start frontend dev server (Terminal 3)
4. Test all features locally
5. Deploy to Sepolia
6. Perform end-to-end testing on testnet
7. Build production version
8. Deploy to hosting provider
```

---

## Deployment Checklist

- [ ] Node.js v20+ installed
- [ ] All dependencies installed (npm install)
- [ ] .env.local configured with Pinata JWT
- [ ] web3/.env configured with private key and RPC URL
- [ ] MetaMask set up and funded
- [ ] Local testing completed successfully
- [ ] Smart contract deployed to Sepolia
- [ ] Frontend .env.local updated with contract address
- [ ] Wagmi config updated for Sepolia
- [ ] Sepolia testing completed
- [ ] Production build passes (npm run build)
- [ ] Deployed to hosting provider
- [ ] Domain configured and SSL enabled
- [ ] Contract verified on Etherscan
- [ ] User documentation completed

---

**Last Updated**: March 2026
**Status**: Ready for Production Deployment
