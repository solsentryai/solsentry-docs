# SolSentry 🛡️
### Solana's Threat Intelligence Graph — Autonomous Operator-Level Detection

> **"RugCheck tells you a fire is burning. SolSentry tells you who lit it — and where they're going next."**

SolSentry is an autonomous threat intelligence system for Solana that tracks **operators**, not just tokens.  
While existing tools analyze each token or wallet in isolation, SolSentry maps the people behind the scams — across deployments, across wallets, over time.

🔗 **Telegram:** [t.me/solsentryai](https://t.me/solsentryai)  
🔗 **X/Twitter:** [@solsentryai](https://x.com/solsentryai)  
🔗 **Hackathon:** Colosseum Frontier (April–May 2026)

---

## The Problem

Serial scam operators on Solana deploy dozens of rug pulls using different wallets, rotating bot clusters, and paid KOL networks. Each new token looks clean on launch.

Existing tools analyze tokens in isolation — RugCheck flags insider holders within a single token. SolScanner maps wallet connections when you ask. ChainAware scores individual wallet fraud probability. But nobody connects a serial deployer's latest token to their previous attacks.

The gap isn't token-level detection — it's **cross-attack operator intelligence**.

---

## How It Works

```mermaid
flowchart TD
    A[🔍 New Token Detected] --> B
    B["STAGE 1 — Fast Scan
    getAccountInfo + metadata (~2s)
    Authorities · Holders · Concentration
    Known token early-return"]
    B -->|Elevated risk?| C
    C["STAGE 2 — Deep Analysis
    HolderEngine · InsightX · DexScreener
    Serial deployer check
    Social Graph cross-reference"]
    C -->|Confirmed threat?| D
    D["STAGE 3 — Forensic
    Bundle detection (Helius Enhanced TX)
    Drain tracking (3-hop fund flow)
    AI Explainer (multilingual)"]
    D --> E[🚨 ALERT — Telegram Bot]

    style A fill:#1e293b,color:#94a3b8
    style B fill:#0f172a,color:#38bdf8
    style C fill:#0f172a,color:#38bdf8
    style D fill:#0f172a,color:#38bdf8
    style E fill:#7f1d1d,color:#fca5a5
```

---

## Case Study — Operator 4kxscute

SolSentry's hunter agents were already tracking deployer wallet `4kxscute` as part of a **coordinated bot cluster** — wallets sharing SOL funding sources and executing same-block buy patterns across multiple tokens.

When 4kxscute deployed a new token, the hunter fired instantly:

| Detail | Value |
|---|---|
| Risk Score | **100/100** |
| Holders | 1 |
| Top Holder Ownership | 100% |
| Flags | MINT_AUTHORITY_ENABLED, FREEZE_AUTHORITY_ENABLED, TOP_HOLDER_OWNS_100%, VERY_FEW_HOLDERS |
| Detection method | Hunter agent already tracking operator + auto-scan on new deploy |

**No other tool connected this deploy to the operator's previous activity.**  
SolSentry already knew who he was.

### Live Alert Output

![4kxscute Hunter Alert](4kxscute-alert.png)

> Real output from SolSentry's Telegram alert system. Hunter_1570 tracking  
> operator `4kxscute` auto-triggered a scan on the new deployment —  
> returning Risk 100/100 with all critical flags active.

---

## Current Metrics (v2.3.1 — April 10, 2026)

| Metric | Value |
|---|---|
| Token scans executed | 5,688 |
| Token discoveries (monitored) | 254,357 |
| Tokens flagged elevated risk | 4,618 |
| Prediction accuracy | **96.7% (584/604 resolved)** |
| False positives | **0** |
| Autonomous agents alive | 30 |
| Hunters active | 30 |
| Wallets tracked | 3,669 |
| Operators mapped | 109 |
| Bot clusters identified | 229 |
| Connected operator wallets | 847 |
| KOL accounts tracked | 106 |
| Continuous runtime | 157.7h (local, no VPS yet) |
| RPC endpoints | 9 (Helius, Alchemy, Triton) |

---

## ALife Agent Ecosystem

SolSentry uses **Artificial Life principles** — inspired by Tierra, Avida, and Conway's Game of Life — to evolve its detection agents autonomously.

- **30 agents** with 7-gene DNA (spawn_threshold, max_hunters, risk_weight, etc.)
- **Fitness tracking** — agents that predict accurately gain energy and reproduce
- **Genetic mutation** — 30+ real mutations recorded with autonomous timestamps
- **Natural selection** — ineffective agents are culled at 2x population cap
- **Energy metabolism** — -0.3 per tick, births cost 15 energy
- **MetaLearning** — market regime detection (CALM/SURGE/CRASH/MEME) every 120s

This isn't marketing: `genome.json` contains recorded mutations showing parameter changes like `spawn_threshold` evolving from 70 → 95 and `max_hunters` from 10 → 30.

---

## Social Graph of Scam

Three entity types linked across every scan:

| Entity | Description | Count |
|---|---|---|
| **OperatorProfiles** | Serial deployer identities tracked across wallets | 109 operators, 847 wallets |
| **BotClusters** | Coordinated wallet groups (same-block buys, shared funding) | 229 clusters |
| **ShillNetworks** | KOL-to-operator connections via early-buy patterns | 106 KOLs tracked |

Every scan cross-references the graph. The more the system scans, the harder it is for operators to hide behind new wallets.

---

## Competitive Landscape

| Capability | RugCheck | SolScanner | ChainAware | Blockaid | **SolSentry** |
|---|:---:|:---:|:---:|:---:|:---:|
| Token-level analysis | ✅ | — | — | ✅ | ✅ |
| Wallet graph visualization | ❌ | ✅ | ❌ | ❌ | 🔜 |
| Per-wallet fraud scoring | ❌ | ❌ | ✅ | ❌ | ✅ |
| Transaction simulation | ❌ | ❌ | ❌ | ✅ | ❌ |
| Operator tracking (cross-attack) | ❌ | ❌ | ❌ | ❌ | ✅ |
| Serial deployer detection | ❌ | ❌ | ❌ | ❌ | ✅ |
| Social graph mapping | ❌ | ❌ | ❌ | ❌ | ✅ |
| Bot cluster fingerprinting | ❌ | ✅ | ❌ | ❌ | ✅ |
| KOL-operator correlation | ❌ | ❌ | ❌ | ❌ | ✅ |
| Autonomous detection (24/7) | ❌ | ❌ | ❌ | ✅ | ✅ |
| ALife agent evolution | ❌ | ❌ | ❌ | ❌ | ✅ |
| Drain flow tracking | ❌ | ✅ | ❌ | ❌ | ✅ |

> **SolScanner** shows you the graph when you ask. **SolSentry** builds the graph while you sleep.

---

## Technical Stack

- **Language:** Python 3 (full async architecture)
- **RPC:** Helius (5 keys) · Alchemy (3 keys) · Triton (1 key + WSS)
- **Data Sources:** Helius DAS + Enhanced TX · DexScreener · InsightX · Nansen · Jupiter
- **AI:** Claude Sonnet (multilingual risk explainer, 10 calls/hr)
- **Delivery:** Telegram Bot API (forum topics, real-time alerts)
- **Testing:** 218 tests · 9 test files · 91+ commits
- **Applied:** DD.xyz/Webacy API grant · Helius Startup Launchpad

---

## Roadmap

**Q2 2026** — VPS deployment (24/7) · WebSocket Stage 3 · Free public API · Token-2022 extension checks  
**Q3 2026** — React dashboard (drain map, operator timeline) · MCP server · x402 micropayments · B2B API  
**Q4 2026** — Wallet Reputation Score API · Copy Trade Safety Filter · Launchpad Vetting API  
**2027+** — Cross-chain operator tracking (ETH, BSC) · Institutional compliance API · Seed round

---

## Built By

**Crash Diniz** — Solo founder and developer.  
Self-taught since the early 2000s: Slackware, Unix, Oracle networking. No university, no bootcamp.  
Started learning Python last year — 218 tests, full async architecture, 5,688 mainnet scans.

> *"Started learning Python last year" is the setup. The metrics above are the punchline.*

**Looking for:** Frontend dev (React dashboard) · Security researcher · BD/growth

---

*Built for the Colosseum Frontier Hackathon · April–May 2026*  
*Powered by Helius · Alchemy · Triton · Claude AI*  
*"Nunca estagnar. Sempre evoluir."*
