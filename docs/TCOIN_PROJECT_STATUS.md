# TCOIN Project Status

## 1. Project Identity

| Field | Value |
|-------|-------|
| Name | TheTeamCoin |
| Symbol | TCOIN |
| Network | Solana Devnet |
| Repository | siemeechang-tcoin/siemeechang-tcoin |
| Current Phase | Phase 3 — Foundation / Recovery |

---

## 2. Existing Devnet Mint

**VERIFIED ON-CHAIN FACTS** (confirmed via Phase 1 read-only inspection)

| Field | Value |
|-------|-------|
| Mint address | `4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D` |
| Token program | `TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA` |
| Decimals | 8 |
| Current supply | 0 |
| Mint authority | `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK` |
| Freeze authority | null |
| Metadata PDA | `8dZWrRB8z9VydwzhoP11iN5KU7NXLr8zRT9k95p97hNA` |

---

## 3. Verified Token Properties

**VERIFIED ON-CHAIN FACTS**

- Token standard: SPL Token (Solana Program Library)
- Decimals: 8 (matches standard fungible token configuration)
- Supply: 0 (no tokens have been minted)
- Freeze authority: null (freeze capability not enabled)

---

## 4. Existing Metadata (Metaplex)

**VERIFIED ON-CHAIN FACTS**

| Field | Value |
|-------|-------|
| Name | TheTeamCoin |
| Symbol | TCOIN |
| URI | https://gateway.pinata.cloud/ipfs/bafkreidas3wxr7me24r47wukvgdmvlpgb3bxfv7h5alqshexhjxqes3moq |
| Metadata PDA | `8dZWrRB8z9VydwzhoP11iN5KU7NXLr8zRT9k95p97hNA` |

---

## 5. Current Supply

**VERIFIED ON-CHAIN FACTS**

Supply: **0** — No tokens have been minted as of Phase 1 inspection.

---

## 6. Mint Authority

**VERIFIED ON-CHAIN FACTS**

Mint authority: `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`

> The private key for this address is **not** stored in this repository.
> Token minting requires the holder of this private key to sign a transaction externally.

---

## 7. Freeze Authority

**VERIFIED ON-CHAIN FACTS**

Freeze authority: **null** — Individual token accounts cannot be frozen.

---

## 8. Historical Transaction Information

**OWNER-PROVIDED / HISTORICAL INFORMATION** *(not independently verified in Phase 1)*

- The mint was created prior to Phase 1 inspection.
- The exact creation transaction signature is not yet recovered.
- No minting transactions have been confirmed on-chain (supply = 0).

---

## 9. What Has Been Verified

- ✅ Mint address exists on Solana Devnet
- ✅ Token program is the standard SPL Token program
- ✅ Decimals = 8
- ✅ Supply = 0
- ✅ Mint authority address confirmed
- ✅ Freeze authority = null
- ✅ Metaplex metadata PDA exists
- ✅ Metadata name = TheTeamCoin
- ✅ Metadata symbol = TCOIN
- ✅ Metadata URI resolves to Pinata/IPFS
- ✅ GitHub repository created and accessible
- ✅ Fine-grained PAT configured (read+write, scoped to this repo)

---

## 10. What Is Still Unknown

**RECOVERY / UNKNOWN**

- [ ] Original creation transaction signature
- [ ] Original wallet/keypair that created the mint (only the address is known)
- [ ] Whether the mint authority keypair is still accessible to the owner
- [ ] Full contents of the Pinata/IPFS metadata JSON
- [ ] Original tokenomics plan (supply cap, distribution, vesting)
- [ ] Any prior UI, frontend, or dashboard that existed
- [ ] Any prior backend or API that existed
- [ ] Whether any test minting was ever performed and subsequently burned
- [ ] Any prior documentation or whitepaper

---

## 11. What Has NOT Yet Been Recovered from the Old Project

**RECOVERY / UNKNOWN**

- Old source code (if any)
- Old deployment scripts (if any)
- Old wallet configuration (if any)
- Old tokenomics documents (if any)
- Old roadmap or whitepaper (if any)

---

## 12. Current Project Boundaries

**What this repository IS:**
- The new GitHub home for the existing TCOIN project
- A documentation and foundation layer
- A record of verified on-chain state

**What this repository IS NOT:**
- Connected to the SieMeeChang website
- A production/Mainnet deployment
- A wallet application
- An exchange listing

---

## 13. Proposed Future Phases

| Phase | Description | Status |
|-------|-------------|--------|
| Phase 1 | Read-only Devnet inspection | ✅ Complete |
| Phase 2 | GitHub repository connection | ✅ Complete |
| Phase 3 | Foundation documentation | ✅ Complete (this phase) |
| Phase 4 | TBD — requires explicit approval | ⏳ Not started |

> **No phase beyond Phase 3 has been authorized.**
> Each phase requires explicit written approval before beginning.

---
*Last updated: 2026-09-26*


---

## Phase 4 Audit Additions (2026-09-26)

### Updated: What Has Been Verified (Phase 4)

- ✅ Mint created approximately **February 15, 2025** (slot 361,327,888 region)
- ✅ Exactly **2 on-chain transactions** (initialization + metadata creation)
- ✅ No minting, burning, authority-change, or transfer instructions ever executed
- ✅ Mint authority is a **standard wallet** (system-owned, non-executable keypair account)
- ✅ Metadata URI is reachable (HTTP 200) — but returns **text/rtf**, not JSON
- ✅ On-chain name/symbol fields ("TheTeamCoin" / "TCOIN") are correct and unaffected by RTF issue

### Updated: Critical Finding — Metadata URI Format

The metadata URI returns a **text/rtf** file, not the JSON expected by Metaplex tooling.
Standard wallets and NFT explorers cannot parse this URI.
The on-chain name and symbol are stored directly on-chain and are unaffected.
The RTF file may contain the original description, image URL, or tokenomics — contents currently unknown.

### Updated: Token Authority Status

The mint authority (`Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`) is confirmed to be
a standard Solana wallet (system-owned, non-executable). Whether the private keypair
is still accessible to the project owner remains **UNKNOWN** — this is an owner-side question.

### See Also

Full audit details: `docs/TCOIN_AUDIT_PHASE4.md`
