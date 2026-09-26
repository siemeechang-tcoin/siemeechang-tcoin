# TCOIN Architecture — System Separation

## Overview

The TCOIN project and the SieMeeChang website are **currently separate systems**.
No integration between them exists or has been authorized.

## System Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        TCOIN PROJECT                            │
│                                                                 │
│   Solana Devnet                                                 │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │  Mint: 4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D   │  │
│   │  Supply: 0  |  Decimals: 8  |  Freeze: null            │  │
│   └─────────────────────────────────────────────────────────┘  │
│                            │                                    │
│                     GitHub Repository                           │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │  siemeechang-tcoin/siemeechang-tcoin                    │  │
│   │  Branch: main                                           │  │
│   │  Phase 3: Foundation documentation only                 │  │
│   └─────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘

                    ← NO CONNECTION →

┌─────────────────────────────────────────────────────────────────┐
│                    SIEMEECHANG WEBSITE                          │
│                                                                 │
│   siemeechang.com                                               │
│   ┌─────────────────────────────────────────────────────────┐  │
│   │  Public TCOIN info page (/tcoin)                        │  │
│   │  Reads Devnet data for display only (read-only)         │  │
│   │  No wallet, no transactions, no minting                 │  │
│   └─────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

## Separation Rules

| Rule | Status |
|------|--------|
| TCOIN repo does NOT import SieMeeChang code | ✅ Enforced |
| SieMeeChang website does NOT write to TCOIN repo | ✅ Enforced |
| No shared secrets between the two systems | ✅ Enforced |
| No on-chain writes from either system | ✅ Enforced (Phase 3) |

## What the SieMeeChang Website Does (Read-Only)

The public `/tcoin` page on siemeechang.com performs **read-only** Devnet RPC
calls to display token information. It does not:

- Hold or use any private key
- Submit any transactions
- Connect to this GitHub repository
- Share any code or secrets with this repository

## Future Integration Considerations

Any future integration between this repository and the SieMeeChang website
requires **explicit written approval** and a dedicated phase plan.

No integration is currently planned or authorized.

---

## Repository Structure

```
siemeechang-tcoin/siemeechang-tcoin/
├── README.md                        ← Project overview and rules
└── docs/
    ├── TCOIN_PROJECT_STATUS.md      ← Full status, history, unknowns
    ├── TCOIN_ONCHAIN_RECORD.md      ← Verified on-chain data only
    └── TCOIN_ARCHITECTURE.md        ← This file
```

---
*Phase 3 — Foundation established 2026-09-26*
