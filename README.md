

#  STX-EnerDAO – Decentralized Clean Energy Investment and Governance

This Clarity smart contract powers a decentralized investment and governance platform for **tokenized clean energy assets** (solar, wind, hydro, biomass). It allows users to register new assets, purchase fractional shares, participate in governance proposals, and track asset performance metrics on-chain.

---

## 📘 Overview

The contract provides a framework for:

* Decentralized registration and tracking of real-world energy-producing assets.
* Fractional ownership through tokenized shares.
* Revenue sharing and governance based on shareholding.
* Transparent on-chain metrics for operational and financial performance.
* Proposal and voting systems for decentralized decision-making.

---

## 🧠 Key Concepts

| Concept       | Description                                           |
| ------------- | ----------------------------------------------------- |
| **Assets**    | Real-world clean energy projects registered on-chain. |
| **Shares**    | Fractional ownership units tied to each asset.        |
| **Owners**    | Principals that hold shares in specific assets.       |
| **Proposals** | Governance decisions about asset-related actions.     |
| **Metrics**   | Real-time operational performance of each asset.      |

---

## 📦 Features

### 🛠️ Asset Management

* Register new energy assets with metadata, share price, and geo-coordinates.
* Enforces validation on asset name, type, and minimum value (`>= 1 STX`).
* Automatically initializes asset performance metrics and governance settings.

### 💸 Share Purchase

* Buy shares in active assets using STX.
* Voting power and revenue participation are automatically updated.
* Enforces validations on:

  * Availability of shares
  * Asset status (must be `"active"`)
  * Positive share count

### 📊 Asset Metrics

Each asset maintains:

* Energy produced
* Operational hours
* Maintenance cost
* Efficiency rating
* Carbon offset
* Peak output
* Lifetime ROI

### 🧾 Governance

Every asset is governed via:

* Proposal lifecycle with quorum, vote periods, and execution delays
* Configurable thresholds (e.g., 75% vote threshold)
* Voting power proportional to shares held

### 🧑‍🤝‍🧑 Ownership Mapping

Tracks:

* Shares held
* Voting power
* Claimed revenue
* Last claim block height

### 🌍 Geo-location Support

Assets include:

* `latitude` and `longitude` coordinates
* Useful for mapping energy project locations on external interfaces

---

## 🧱 Data Structures

### `assets` (Map)

```clarity
{
  name: string,
  asset-type: string,
  total-shares: uint,
  available-shares: uint,
  share-price: uint,
  ...
}
```

### `ownership` (Map)

```clarity
{
  shares: uint,
  revenue-claimed: uint,
  voting-power: uint,
  ...
}
```

### `asset-metrics`, `governance-settings`, `proposals`

* Tracks performance and governance data per asset

---

## 🚨 Error Codes

| Code   | Description               |
| ------ | ------------------------- |
| `u401` | Not authorized            |
| `u402` | Asset already exists      |
| `u403` | Invalid amount            |
| `u404` | Asset not found           |
| `u405` | Insufficient shares       |
| `u406` | Transfer failed           |
| `u407` | Not found                 |
| `u408` | Invalid name              |
| `u409` | Invalid asset type        |
| `u410` | Invalid recipient         |
| `u411` | Self-transfer not allowed |
| `u412` | Zero shares error         |
| `u413` | Proposal already active   |
| `u414` | Proposal expired          |
| `u415` | Already voted             |
| `u416` | Invalid status            |
| `u417` | Insufficient quorum       |

---

## 🧪 Testing Suggestions

* Register asset with invalid name or asset type → should fail
* Register asset with valid inputs → should succeed and return asset ID
* Purchase shares for a non-active asset → should fail
* Purchase shares with more than available → should fail
* Purchase valid shares → should transfer STX and update voting power

---

## 📍 Deployment Configuration

* `CONTRACT-OWNER`: Set to deploying principal.
* `SHARE-SCALE`: Used to normalize fractional voting power.
* `MAINTENANCE-WINDOW`: Blocks before a proposal can be modified or reissued (\~24 hours).

---

## 🔒 Security and Design Notes

* All inputs are validated for length, formatting, and types.
* Governance and voting thresholds are asset-specific and can be configured per project.
* Voting and ownership logic ensure fair, stake-based influence on decisions.
* Contract prevents contract-self-interaction and self-transfers.
* Uses `unwrap!`, `asserts!`, and `try!` for safe operations and predictable error handling.

---

## 🧠 Future Enhancements

* Revenue distribution mechanics
* Proposal execution logic
* Event emissions for external indexing
* UI integration with GPS map and performance dashboards
* Multi-contract modularization for scale

---
