<div align="center">
PUMP-X
A High-Speed Automated Trading Bot for Solana — Built for pump.fun & Beyond
Show Image
Show Image
Show Image
Show Image
</div>
PUMP-X is a fast, modular Solana trading bot designed for real-time token sniping, automated buying/selling, and multi-platform swap execution. It monitors new token launches on pump.fun, detects early bonding curve activity, and executes trades through Raydium and Jupiter — all with low-latency RPC connections and configurable strategy logic.

Features

pump.fun New Token Monitoring — Stream and filter new token launches in real time, with customizable filters for liquidity, dev wallets, and bonding curve progress
Bonding Curve Detection — Identify early-stage tokens before they migrate to Raydium; snipe at optimal entry points
Auto Buy / Auto Sell — Set target buy amounts, take-profit percentages, stop-loss thresholds, and let the bot handle execution automatically
Raydium & Jupiter Swap Integration — Route swaps through Raydium pools or Jupiter aggregator for best price execution
RPC Acceleration — Supports custom RPC endpoints (Helius, Triton, QuickNode, etc.) with priority fee management for faster transaction confirmation


Quick Start
Install and run your first snipe in minutes:
git clone https://github.com/phh02356-a11y/Meme-Engine-V1.git

cd Meme-Engine-V1
pip install -e .
Configure your wallet and RPC in .env:
envPRIVATE_KEY=your_base58_private_key
RPC_URL=https://your-rpc-endpoint.com
WS_URL=wss://your-ws-endpoint.com
Start the bot:
pythonfrom pumpx import PumpXBot

bot = PumpXBot.from_config("config.yaml")
bot.run()
The bot will begin monitoring pump.fun for new token launches and execute trades based on your configured strategy.

Installation
Basic (trading only):
bashpip install -e .
With analytics dashboard:
bashpip install -e ".[dashboard]"
With all dev dependencies:
bashpip install -e ".[dev]"

Configuration
All strategy parameters are set in config.yaml:
yamlwallet:
  private_key_env: PRIVATE_KEY       # reads from .env
  
rpc:
  http: https://your-rpc.com
  ws:   wss://your-rpc.com
  priority_fee: 100000               # microlamports

monitor:
  platform: pump.fun
  min_liquidity_sol: 5               # ignore tokens below this
  ignore_mint_authority: true        # skip risky tokens

strategy:
  buy_amount_sol: 0.1
  take_profit: 2.0                   # 2x = sell 100%
  stop_loss: 0.5                     # -50% = cut loss
  slippage_bps: 500

swap:
  router: jupiter                    # "jupiter" or "raydium"

Project Structure
pump-x/
├── pumpx/
│   ├── bot.py               # Main bot loop and strategy orchestration
│   ├── monitor.py           # pump.fun WebSocket listener and token filter
│   ├── sniper.py            # Bonding curve detection and buy trigger logic
│   ├── swap.py              # Raydium & Jupiter swap execution
│   ├── wallet.py            # Keypair management and transaction signing
│   ├── rpc.py               # RPC client with retry and priority fee support
│   └── config.py            # Config loader and validation
├── config.yaml              # Strategy and connection configuration
├── .env.example             # Environment variable template
└── README.md

How It Works

Monitor — The bot connects via WebSocket to pump.fun's token stream and filters incoming launches by your configured criteria (liquidity, bonding curve %, dev wallet flags)
Detect — When a qualifying token is found, the bonding curve stage is evaluated to determine optimal entry timing
Buy — A swap transaction is built and sent through your configured router (Jupiter or Raydium) with priority fees to maximize confirmation speed
Manage — The bot tracks open positions and automatically triggers sell orders when take-profit or stop-loss conditions are met


Supported Platforms
PlatformBuySellMonitorpump.fun✅✅✅Raydium✅✅—Jupiter✅✅—

Disclaimer
This software is for educational and research purposes only. Cryptocurrency trading involves significant financial risk. Always use funds you can afford to lose, test with small amounts first, and never share your private key. The author is not responsible for any financial losses incurred through the use of this software.

License
This project is licensed under the MIT License. See LICENSE for details.

Contributing
PRs are welcome. Please open an issue first to discuss what you'd like to change.
