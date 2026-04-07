# Python-Blockchain

![Repo Size](https://img.shields.io/github/repo-size/drussell33/Python-Blockchain)
![Last Commit](https://img.shields.io/github/last-commit/drussell33/Python-Blockchain)
![Top Language](https://img.shields.io/github/languages/top/drussell33/Python-Blockchain)

Python-Blockchain is a small educational blockchain implementation written in Python. The project models the core building blocks of a blockchain system, including blocks, transactions, proof-of-work validation, wallet-based signing, and a command-line node interface. It stores chain data locally on disk and is designed to demonstrate blockchain fundamentals in a compact, readable codebase.

## Key Features

- Implements a `Block` model with index, previous hash, timestamp, transactions, and proof fields
- Implements a `Transaction` model with deterministic ordered serialization for hashing
- Manages blockchain state, open transactions, mining, and balance calculation through a dedicated `Blockchain` class
- Uses proof-of-work validation with SHA-256 hashing
- Supports RSA key generation, transaction signing, and signature verification through a `Wallet` class
- Provides blockchain integrity and transaction validation helpers in a separate verification module
- Includes a command-line `Node` interface for adding transactions, mining blocks, printing the chain, and managing wallet keys
- Persists blockchain data to `blockchain.txt` and wallet keys to `wallet.txt`

## Tech Stack

### Backend
- Python
- Standard library modules: `functools`, `hashlib`, `json`, `binascii`, `collections`, `time`, `uuid`

### Frontend
- None
- Command-line interface via standard input/output

### Database
- No database is configured
- Local file-based persistence using:
  - `blockchain.txt`
  - `wallet.txt`

### Tools / Services
- PyCryptodome (`Crypto.PublicKey`, `Crypto.Signature`, `Crypto.Hash`, `Crypto.Random`)

## Architecture Overview

This project is a single-process Python application with a command-line interface rather than a web-based frontend. The `Node` class acts as the entry point and user interaction layer, collecting input, invoking wallet operations, and delegating blockchain actions such as transaction creation, mining, and validation.

The `Blockchain` class is the central coordinator for domain logic. It maintains the chain, tracks open transactions, calculates balances, performs mining, and saves or restores state from local files. Transactions are represented by the `Transaction` class, while mined blocks are represented by the `Block` class.

Cryptographic responsibilities are isolated in the `Wallet` class, which generates RSA key pairs, signs transactions, and verifies signatures. Validation logic is further separated into `utility.verification`, and hashing helpers live in `utility.hash_util`, giving the project a lightweight separation of concerns across models, blockchain management, wallet logic, and utility helpers.

### Runtime Flow

1. `node.py` creates a wallet and initializes a `Blockchain` instance with the wallet's public key.
2. The user selects actions from the CLI menu.
3. New transactions are signed by the wallet and submitted to the blockchain.
4. The blockchain validates transactions, computes proof of work, and mines a new block.
5. Chain state and open transactions are written to disk.
6. Wallet keys can be created, loaded, and saved independently.

## Project Structure

```tree
Python-Blockchain/
├── .gitignore
├── README.md
├── block.py
├── blockchain.py
├── node.py
├── transaction.py
├── wallet.py
└── utility/
    ├── __init__.py
    ├── hash_util.py
    ├── printable.py
    └── verification.py
```

### Important Files

- `node.py` - CLI entry point that runs the interactive blockchain node
- `blockchain.py` - Core blockchain logic, persistence, mining, balance calculation, and transaction management
- `block.py` - Block domain model
- `transaction.py` - Transaction domain model
- `wallet.py` - RSA key generation, signing, saving/loading keys, and signature verification
- `utility/hash_util.py` - SHA-256 hashing helpers for strings and blocks
- `utility/verification.py` - Chain, proof-of-work, and transaction verification helpers
- `utility/printable.py` - Small base class that improves object string output

## Getting Started

### Prerequisites

- Python 3
- `pip`
- PyCryptodome

> The repository does not include a `requirements.txt`, `pyproject.toml`, or `setup.py`, so dependencies must be installed manually based on imports present in the source.

### Installation

```bash
git clone https://github.com/drussell33/Python-Blockchain.git
cd Python-Blockchain
pip install pycryptodome
```

### Usage

Run the command-line node:

```bash
python node.py
```

The interactive menu supports:
- adding a transaction
- mining a block
- printing blockchain contents
- validating open transactions
- creating wallet keys
- loading wallet keys
- saving wallet keys

### Generated Runtime Files

When the application runs, it may create local files in the project directory:

```text
wallet.txt
blockchain.txt
```

## Roadmap

- [x] Block model implementation
- [x] Transaction model implementation
- [x] Blockchain manager with open transaction tracking
- [x] Proof-of-work validation
- [x] Wallet key generation and transaction signing
- [x] Signature verification
- [x] Local file persistence for chain and wallet data
- [x] Interactive command-line node
- [ ] Add a dependency manifest such as `requirements.txt`
- [ ] Add automated tests
- [ ] Add error handling around malformed persisted data
- [ ] Add peer-to-peer networking between nodes
- [ ] Add REST API or web interface
- [ ] Improve configuration for mining difficulty and storage paths

## Contributing

Contributions are welcome through the standard GitHub workflow:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Commit with clear messages
5. Push your branch
6. Open a pull request

For larger changes, consider opening an issue first to discuss the proposed improvement.

## Screenshots / Demo

Screenshots, terminal captures, or a short demo GIF can be added here to show:
- the CLI menu
- transaction creation
- mining a block
- blockchain output

## Contact

- GitHub: [drussell33](https://github.com/drussell33)

