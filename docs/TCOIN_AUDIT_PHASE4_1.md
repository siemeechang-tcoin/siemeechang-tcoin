# TCOIN Phase 4.1 — Historical Metadata & Creation Evidence Recovery

**Audit Date:** 2026-09-26
**Method:** Read-only — Pinata/IPFS fetch + Solana Devnet RPC parsed transaction retrieval
**Zero blockchain writes. No wallet use. No website modification.**

---

## 1. Original IPFS Metadata — Full Recovery

### Source
URI: `https://gateway.pinata.cloud/ipfs/bafkreidas3wxr7me24r47wukvgdmvlpgb3bxfv7h5alqshexhjxqes3moq`
HTTP Status: 200
Content-Type: text/rtf
File size: 750 bytes
RTF generator: Apple TextEdit / Cocoa (cocoartf2513, macOS)

### RTF File — Preserved Verbatim

The file is a macOS-generated RTF document (Apple TextEdit, cocoartf2513) containing
a JSON object as its text body. The JSON was typed or pasted into TextEdit and saved
as RTF rather than as a plain .json file. This explains the text/rtf content-type.

```rtf
{\rtf1\ansi\ansicpg1252\cocoartf2513
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww21800\viewh14840\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 \{\
  "name": "TheTeamCoin",\
  "symbol": "TCOIN",\
  "description": "The official token for TheTeamCoin, powering travel, rewards, and investment.",\
  "image": "https://your-logo-url.png",\
  "attributes": [],\
  "properties": \{\
    "files": [\
      \{\
        "uri": "https://your-logo-url.png",\
        "type": "image/png"\
      \}\
    ],\
    "category": "image"\
  \}\
\}\
}
```

### Extracted JSON (as intended by the creator)

```json
{
  "name": "TheTeamCoin",
  "symbol": "TCOIN",
  "description": "The official token for TheTeamCoin, powering travel, rewards, and investment.",
  "image": "https://your-logo-url.png",
  "attributes": [],
  "properties": {
    "files": [
      {
        "uri": "https://your-logo-url.png",
        "type": "image/png"
      }
    ],
    "category": "image"
  }
}
```

### Metadata Field Analysis

| Field | Value | Status |
|-------|-------|--------|
| name | TheTeamCoin | ✅ Matches on-chain |
| symbol | TCOIN | ✅ Matches on-chain |
| description | "The official token for TheTeamCoin, powering travel, rewards, and investment." | ✅ RECOVERED |
| image | https://your-logo-url.png | ⚠️ Placeholder — not a real URL |
| attributes | [] | Empty array |
| properties.files[0].uri | https://your-logo-url.png | ⚠️ Placeholder — not a real URL |
| properties.category | image | Standard Metaplex category |

### Key Findings

1. **Description recovered:** "The official token for TheTeamCoin, powering travel, rewards, and investment."
   This is the first confirmed project description. It establishes the intended use case:
   travel, rewards, and investment.

2. **Image URL is a placeholder:** `https://your-logo-url.png` is a literal placeholder string,
   not a real image URL. No logo was ever uploaded to IPFS or linked from the metadata.

3. **RTF format was an error:** The file was created in Apple TextEdit on macOS and saved as RTF
   instead of plain JSON. This is a tooling error, not intentional. The JSON content itself is valid.

4. **No social links, no website URL, no tokenomics, no creator addresses** are present in the metadata.

5. **No external_url field** — the standard Metaplex field for a project website was not included.

---

## 2. Creation Transaction — Full Recovery

### Transaction 1 (Earliest) — Mint Initialization

| Field | Value |
|-------|-------|
| Signature | `3kzVYxnqto7u6g4VG1TpCarXuD9KUdWy6dfhRSjdHU986GZfNwW5qXTRE8qyjXuMnVGN5oaGzwCnvUsu5KknWz6b` |
| Slot | 361,326,435 |
| Timestamp | **2025-02-15T21:00:02.000Z** |
| Fee | 10,000 lamports (0.00001 SOL) |
| Error | None |
| Status | Finalized |

**Instructions:**

1. System Program — `createAccount`
   - Source (fee payer): `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`
   - New account (mint): `4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D`
   - Owner assigned to: `TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA` (SPL Token program)
   - Lamports deposited: 1,461,600 (rent-exempt minimum for 82-byte account)
   - Space allocated: 82 bytes

2. SPL Token Program — `initializeMint`
   - Mint: `4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D`
   - Decimals: **8**
   - Mint authority: `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`
   - Freeze authority: **not set** (null)
   - Rent sysvar: `SysvarRent111111111111111111111111111111111`

**Accounts involved:**
| Address | Role | Signer | Writable |
|---------|------|--------|----------|
| `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK` | Fee payer / mint authority | ✅ Yes | ✅ Yes |
| `4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D` | New mint account | ✅ Yes | ✅ Yes |
| `11111111111111111111111111111111` | System Program | No | No |
| `SysvarRent111111111111111111111111111111111` | Rent Sysvar | No | No |
| `TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA` | SPL Token Program | No | No |

**Log messages:**
```
Program 11111111111111111111111111111111 invoke [1]
Program 11111111111111111111111111111111 success
Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
Program log: Instruction: InitializeMint
Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2919 of 399850 compute units
Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
```

---

### Transaction 2 (Latest) — Metaplex Metadata Creation

| Field | Value |
|-------|-------|
| Signature | `5TgsvfVQvz33apz8dAL56RWVDTebvBVxc67RigRMxT4sDZgBQMAP2edjyVhbP22TgyWg3qbFvW7dpdbRuw3VPD7D` |
| Slot | 361,327,888 |
| Timestamp | **2025-02-15T21:09:22.000Z** |
| Fee | 5,002 lamports |
| Error | None |
| Status | Finalized |
| Time gap from TX1 | ~9 minutes 20 seconds |

**Instructions:**

1. ComputeBudget — set compute unit limit
2. ComputeBudget — set compute unit price
3. Metaplex Token Metadata Program (`metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s`) — `Create`
   - Creates the metadata PDA at `8dZWrRB8z9VydwzhoP11iN5KU7NXLr8zRT9k95p97hNA`
   - Sets name, symbol, URI on-chain

**Accounts involved:**
| Address | Role | Signer | Writable |
|---------|------|--------|----------|
| `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK` | Fee payer / update authority | ✅ Yes | ✅ Yes |
| `4K8nhtZuR53hTehr1R9c5FtsNogkaRHegPk8Dsxtb29D` | Mint | No | ✅ Yes |
| `8dZWrRB8z9VydwzhoP11iN5KU7NXLr8zRT9k95p97hNA` | Metadata PDA (created here) | No | ✅ Yes |
| `11111111111111111111111111111111` | System Program | No | No |
| `ComputeBudget111111111111111111111111111111` | Compute Budget Program | No | No |
| `Sysvar1nstructions1111111111111111111111111` | Instructions Sysvar | No | No |
| `metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s` | Metaplex Token Metadata | No | No |

**Log messages:**
```
Program ComputeBudget111111111111111111111111111111 invoke [1]
Program ComputeBudget111111111111111111111111111111 success
Program ComputeBudget111111111111111111111111111111 invoke [1]
Program ComputeBudget111111111111111111111111111111 success
Program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s invoke [1]
Program log: IX: Create
Program 11111111111111111111111111111111 invoke [2]
Program 11111111111111111111111111111111 success
Program log: Allocate space for the account
Program 11111111111111111111111111111111 invoke [2]
Program 11111111111111111111111111111111 success
Program log: Assign the account to the owning program
Program 11111111111111111111111111111111 invoke [2]
Program 11111111111111111111111111111111 success
Program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s consumed 46754 of 55804 compute units
Program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s success
```

---

## 3. Complete Creation Timeline

| Event | Timestamp (UTC) | Slot | Signature |
|-------|-----------------|------|-----------|
| Mint account created + initialized | 2025-02-15T21:00:02Z | 361,326,435 | `3kzVYxnqto7u6g4VG1TpCarXuD9KUdWy6dfhRSjdHU986GZfNwW5qXTRE8qyjXuMnVGN5oaGzwCnvUsu5KknWz6b` |
| Metaplex metadata PDA created | 2025-02-15T21:09:22Z | 361,327,888 | `5TgsvfVQvz33apz8dAL56RWVDTebvBVxc67RigRMxT4sDZgBQMAP2edjyVhbP22TgyWg3qbFvW7dpdbRuw3VPD7D` |

**Total time from mint init to metadata creation: ~9 minutes 20 seconds.**
Both transactions were signed by the same wallet: `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`

---

## 4. Mint Authority — Confirmed Details

| Field | Value |
|-------|-------|
| Address | `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK` |
| Role in TX1 | Fee payer + mint authority setter (signer) |
| Role in TX2 | Fee payer + Metaplex update authority (signer) |
| Account type | Standard Solana wallet (system-owned keypair) |
| Keypair accessibility | **UNKNOWN — owner must confirm** |

This address signed both transactions. It is the sole creator of the mint and metadata.
No other addresses were involved in creation.

---

## 5. Verified vs. Unverified (Phase 4.1 Additions)

### VERIFIED (confirmed from on-chain data + IPFS)
- Mint creation timestamp: **2025-02-15T21:00:02Z**
- Mint creation signature: `3kzVYxnqto7u6g4VG1TpCarXuD9KUdWy6dfhRSjdHU986GZfNwW5qXTRE8qyjXuMnVGN5oaGzwCnvUsu5KknWz6b`
- Metadata creation timestamp: **2025-02-15T21:09:22Z**
- Metadata creation signature: `5TgsvfVQvz33apz8dAL56RWVDTebvBVxc67RigRMxT4sDZgBQMAP2edjyVhbP22TgyWg3qbFvW7dpdbRuw3VPD7D`
- Both transactions signed solely by `Aqgn3AW7j92qkRjFhzYXbyACkaJSz8zKsSqSZunBLrTK`
- Decimals set to 8 in the initializeMint instruction (confirmed)
- Freeze authority explicitly not set during initialization
- Metadata PDA created by Metaplex Token Metadata program
- Project description: "The official token for TheTeamCoin, powering travel, rewards, and investment."
- Image URL in metadata: placeholder (`https://your-logo-url.png`) — never a real image
- RTF file was created on macOS using Apple TextEdit (cocoartf2513)
- No social links, no website URL, no tokenomics in metadata

### PROBABLE BUT UNCONFIRMED
- The RTF format was an accidental tooling error (TextEdit saves as RTF by default on macOS)
- The creator used a standard Metaplex CLI or similar tool for the metadata transaction

### UNKNOWN / NEEDS RECOVERY
- Whether the mint authority keypair is still accessible to the owner
- Whether a real logo image was ever created or intended
- Whether any tokenomics plan existed beyond the description text
- Whether any prior website or application was built and subsequently taken down

---

## 6. RPC / Source Limitations

All data was retrieved successfully in this phase. No rate-limiting or timeouts occurred.
Public Devnet RPC was sufficient for full transaction parsing.

---
*Phase 4.1 recovery completed: 2026-09-26*
