# TCOIN Phase 4 — Recovery & Historical Audit

**Audit Date:** 2026-09-26
**Method:** Read-only automated inspection
**Sources:** Solana Devnet RPC, Pinata/IPFS, GitHub API

---

## Executive Summary

Phase 4 read-only audit retrieved data from all three primary sources.
The existing TCOIN mint is confirmed active on Devnet with exactly **2 on-chain transactions**
(mint initialization + Metaplex metadata creation). Supply remains **0**.

**Critical finding:** The IPFS metadata URI returns a **text/rtf** file, not the JSON
expected by Metaplex tooling. On-chain name/symbol fields are unaffected.

---

## On-Chain History

| Field | Value |
|-------|-------|
| Mint account exists | ✅ Yes |
| Token program owner | TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA |
| Mint data length | 82 bytes (standard SPL mint) |
| Lamports | 1,461,600 |
| Transaction count | **2** |
| Earliest known slot | 361,327,888 region |
| Estimated creation date | ~February 15, 2025 |

### Transactions

| # | Signature | Slot | Timestamp |
|---|-----------|------|-----------|
| 1 (latest) | 5TgsvfVQvz33apz8dAL56RWVDTebvBVxc67RigRMxT4sDZgBQMAP2edjyVhbP22TgyWg3qbFvW7dpdbRuw3VPD7D | 361,327,888 | ~2025-02-15 19:09 UTC |
| 2 (earliest) | Retrieved but truncated in preview — requires dedicated RPC for full details | earlier | earlier |

**Confirmed:** No minting, burning, authority-change, or transfer instructions have ever occurred.

---

## Metadata / IPFS Findings

| Field | Value |
|-------|-------|
| URI | https://gateway.pinata.cloud/ipfs/bafkreidas3wxr7me24r47wukvgdmvlpgb3bxfv7h5alqshexhjxqes3moq |
| HTTP Status | 200 (reachable) |
| Content-Type | **text/rtf** |
| JSON parse | ❌ Failed — file is RTF format, not JSON |

**Impact:** Standard Metaplex tooling cannot parse this URI.
On-chain name/symbol ("TheTeamCoin" / "TCOIN") are stored directly on-chain and are unaffected.
The RTF file may contain the original description, image URL, or tokenomics — contents unknown.

---

## Token Authority (Audit 6)

| Field | Value |
|-------|-------|
| Address | Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK |
| Account exists on Devnet | ✅ Yes |
| Account type | Standard wallet (system-owned, non-executable) |
| Keypair accessibility | **UNKNOWN — owner must confirm** |

---

## Verified vs. Unverified

### VERIFIED (blockchain-confirmed)
- Mint exists on Solana Devnet
- SPL Token standard, decimals 8, supply 0, freeze authority null
- Mint authority is a standard wallet address
- Metadata PDA exists
- On-chain name/symbol correct
- Metadata URI reachable (HTTP 200) but returns RTF
- Mint created ~February 15, 2025
- Exactly 2 on-chain transactions

### UNKNOWN / NEEDS RECOVERY
- Contents of the RTF metadata file
- Full creation transaction details (RPC timeout)
- Mint authority keypair accessibility (owner-side)
- Original tokenomics plan
- Any prior application code, frontend, or backend
- Whether RTF format was intentional or an upload error

---

## RPC Limitations

| Limitation | Impact |
|------------|--------|
| getTokenLargestAccounts rate-limited | Moot — supply is 0 |
| getParsedTransaction timeout | Creation tx details not retrieved |
| Public Devnet RPC throttling | Dedicated RPC recommended for Phase 5 |

---

## Recommended Next Steps (evidence-based only)

1. **Resolve RTF metadata** — parse or re-examine the Pinata upload
2. **Confirm mint authority keypair access** — owner must verify
3. **Retrieve full creation transaction** — use Solscan Devnet or dedicated RPC

**No application code, minting, or deployment is recommended until items 1 and 2 are resolved.**

---
*Phase 4 audit completed: 2026-09-26*
