# MBIQ

**An open marketplace for AI inference.**

Built in response to Solana's [Request for Startups → *An open marketplace for AI inference*](https://solana.com/request-for-startups#ai-inference-marketplace).

Started September 2026.

One request interface. Independent providers join without a central listing. Payment settles per request on Solana. Every job carries a signed attestation of which model actually served it.

> **Status:** protocol specification complete (`docs/spec/`). MVP in progress — one provider, one open model, code generation workload, devnet.

---

## The problem

A developer who needs a specific open model today has two options:

1. **A closed aggregator.** Cheap, fast, and it will not tell you which model answered. You are billed for a model you cannot verify.
2. **Self-hosting.** You control everything, and you pay for idle GPU time whether or not anyone is using it.

Neither gives a verifiable record of model identity. Every team building agents on Solana answers this question privately, or not at all.

## What MBIQ does

```
request → quote → payment authorized → escrow funded
        → providers discovered → routing → execution
        → signed attestation → verification → settlement
        → provider reward + protocol fee
```

- **Providers register themselves.** No central listing process, no application queue.
- **Users pay per request.** A payment channel collapses thousands of tiny charges into one on-chain commitment.
- **Every job produces evidence.** Job id, model id and version, runtime, timestamps, result hash, provider signature, verification status.
- **Reputation accrues to useful providers.** Performance and model usage attach to the provider that did the work.

## Why Solana

Inference is billed in fractions of a cent per request. On a chain where settlement costs more than the service, this marketplace cannot exist.

Solana payment channels make per-request settlement economically rational: the network sees one commitment instead of ten thousand transactions, and the provider still gets paid for each job.

## Verification — what it does and does not prove

Deterministic facts are verified deterministically: result hashes, replay, model identity attestations, runtime metadata.

Subjective output quality is **not** a cryptographic claim and will never be presented as one. Replicated execution, sampling and challenge mechanisms are defined as extension points, not shipped features.

## Proof of work: MineBench

MBIQ is not a first attempt at this problem. The same team shipped **MineBench** — a desktop application that turns consumer hardware into a mining network:

- [`MineBench-Client`](https://github.com/devcodex2025/MineBench-Client) — Electron + React desktop runtime: hardware benchmarking, miner process orchestration, wallet-aware reward views
- [`MineBench-UI`](https://github.com/devcodex2025/minebench-ui) — public site, dashboard, leaderboard, whitepaper
- [`MineBench-CPU-ZEPH`](https://github.com/devcodex2025/MineBench-CPU-ZEPH) / [`MineBench-GPU-RVN`](https://github.com/devcodex2025/MineBench-GPU-RVN) — auditable miner distribution
- `MineBench-Pool` — pool deployment and coordination

**What it taught us.** At low miner scale, reward attribution and payout settlement break before the product does. We paused the service in October 2026 to rebuild those foundations rather than scale a system we could not trust.

MBIQ is the direct answer to that lesson: price per job instead of per hashrate, escrow funds before execution instead of reconciling rewards afterwards, and attach verifiable evidence to every delivered result.

## Repository layout

```
docs/
  spec/                 protocol specification (job lifecycle, payments, verification, economics)
  rfs-response.md       one-pager answering the Solana request
  application-drafts.md grant and program applications
```

## Roadmap

| Phase | Scope |
|---|---|
| M1 | Provider daemon, gateway, escrow on devnet, one open model, code generation |
| M2 | Payment channels, signed attestations, reputation v0, three external providers |
| M3 | Public testnet, SDK, benchmark harness, verification schema published as a standalone spec |
| Later | Video generation, additional workloads, independent verification (sampling, replication, challenges) |

## Contact

`{{X_PROJECT}}` · `{{EMAIL}}`

## License

Protocol specification and documentation: all rights reserved for now. Verification schema, provider daemon and client SDK are intended to be released under MIT.
