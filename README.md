# Zenti ⚡
**USSD-to-Solana Treasury for the Next Billion Users.**

Zenti is a financial inclusion tool built for the **Solana Frontier Hackathon 2026**. It allows SME owners in emerging markets to manage crypto treasuries and pay suppliers using simple feature phones—no internet, no smartphone, just USSD.

Agentic Finance for the Unbanked via USSD & Solana

The Problem
Nigerian SMEs face high barriers to Web3: expensive data, complex seed phrases, and lack of professional treasury tools.

💡 The Solution
An AI Agent Coordinator that allows SMEs to manage business funds via USSD (no internet required).

AI-Powered: Uses Groq to parse natural language USSD commands.
OWS Secured: Manages vaults via the Open Wallet Standard, removing the need for users to manage private keys.
Solana Network: Built to integrate Solana for near-instant, low-fee business payments.
🛠 Tech Stack
Backend: Flask (Python) in GitHub Codespaces
Blockchain: Solana + OWS
Frontend: Lovable (React)
Mobile: Africa's Talking USSD Gateway
Storage: In-memory (Mock DB) for rapid hackathon deployment
How to Use
Dial *384*57157# on a mobile device (Nigeria sandbox).
Choose '1' to check your OWS Vault balance.
Choose '2' to authorize a supplier payment
### 🌟 Features
- **Offline Banking:** Interact with the Solana blockchain via GSM networks.
- **AI Intent Engine:** Natural language processing via Llama-3 to parse transactions.
- **Real-Time Forex:** Instant conversion from SOL to NGN (Nigerian Naira).
- **OWS Standard:** Built using Open Wallet Standard for secure, interoperable vault management.

### 🏗️ Architecture


### 🚀 Setup
1. Clone & Install:
   ```bash
   pip install -r requirements.txt
   
2. Environment Variables:
GROQ_API_KEY: For AI parsing.
EXCHANGE_RATE_API_KEY: For Naira conversion.
VAULT_ADDRESS: Solana Public Key.
🛠️ Track
Primary: Consumer Applications
Secondary: Payments & On-chain Commerce
Developed with conviction for the Solana Frontier Hackathon 2026.

### Possible Future Roadmap
Zenti is just getting started. Our goal is to become the primary financial operating system for offline SMEs.

Phase 1: Security & Trust (Q3 2026)
MPC Wallet Integration: Moving from single-key vaults to Multi-Party Computation (MPC) via OWS to ensure no single point of failure for merchant funds.
Biometric USSD: Exploring voice-print authentication as a second factor for high-value transactions to prevent SIM-swap fraud.

Phase 2: Ecosystem Expansion (Q4 2026)
Zenti Micro-Loans: Using on-chain transaction history to create a "Zenti Credit Score," allowing market women to access low-interest SOL-collateralized loans.
Stablecoin Native Support: Automated swapping between SOL and USDC/PYUSD to protect merchants from market volatility.

Phase 3: The "Zenti Agent" Network (2027)
Cash In/Out Nodes: Partnering with local kiosk owners to act as physical "on-ramps," allowing users to trade physical Naira for Zenti digital credits via a simple USSD transfer.
Multi-Chain Support: Expanding the Zenti bridge to other high-speed networks while maintaining the same simple USSD interface.

Built by Senseii Ciel 
