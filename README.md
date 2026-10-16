# BlockWarehouse

**Private Blockchain Platform for Secure File Transfer and Verification in a Business Environment**

A working prototype of a hybrid decentralized system for sharing business files. Files are stored on IPFS, ownership and access rights are kept in a Solidity smart contract, and a Merkle root anchored on-chain verifies file integrity.

> Master's thesis, Josip Juraj Strossmayer University of Osijek, 2026. Author: Filip Krpeš.

## Features

- Registration and login with an automatically generated custodial wallet
- File upload: 4 KB chunking, Merkle tree, IPFS storage, on-chain registration (CID and Merkle root)
- Download with integrity verification of 10 random chunks against the on-chain root
- Granting and revoking access by user or group
- Activity log of uploads, shares, downloads and revocations
- Admin panel: user deactivation, password reset, gas usage per user
- Gas tracking for every on-chain transaction

## Tech stack

| Area | Technology |
|---|---|
| Frontend | React, Vite, CSS |
| Backend | Node.js, Express |
| Database | SQLite (better-sqlite3) |
| Smart contract | Solidity, Hardhat |
| Blockchain client | ethers.js |
| File storage | IPFS (Kubo) |
| Security | JWT, bcrypt, AES-256-GCM, ECDSA (secp256k1), Keccak-256 |

## Architecture

```
Browser (React)
     │  REST + JWT
     ▼
Express backend ──── SQLite   (metadata, activity, gas log)
     │
     ├──── IPFS node          (file content, addressed by CID)
     │
     └──── Smart contract     (ownership, access rights, Merkle root)
              via ethers.js, signed with the user's custodial wallet
```
