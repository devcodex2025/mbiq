# MBIQ — response to the Solana request

Answers `solana.com/request-for-startups#ai-inference-marketplace`, using the structure the brief's own agent guide asks for: user, problem, product wedge, onchain role, first milestone, biggest open risk.

---

## User

An AI app developer who needs a specific open model at a predictable price, and who has no way to prove which model actually answered.

Today they choose between a closed aggregator that hides model identity and self-hosting that bills them for idle GPU time. Both are wrong for anyone shipping an agent that acts on the output.

## Problem

Inference is sold as a black box. The buyer pays for a model and receives a response, with no binding evidence connecting the two. When the output drives a financial action, a security decision, or a transaction, "trust us" is not a sufficient answer.

## Product wedge

**Verification first, marketplace second.**

A single request interface where providers join without a central listing, quote a price, execute on their own hardware, and return a signed attestation binding the job to the model that served it. Payment releases from escrow on settlement. Reputation attaches to the provider that did the work.

The smallest useful version proves one thing: a user can buy useful compute from a stranger, and can check who served it.

## Onchain role

Solana carries exactly the state that benefits from shared guarantees, and nothing else:

- job escrow and payment authorization
- settlement and provider payout
- protocol fee and treasury destination
- attestation hashes and reputation updates

Prompts, outputs, weights and model files stay offchain. Only hashes and references go on-chain.

## First milestone

One provider, one open-weight model, code generation workload, devnet. A request goes in, a quote comes back, payment settles over a channel, the provider executes, the attestation verifies, escrow releases, the protocol books a fee. Public repo and a 90-second recording of the whole path.

## Biggest open risk

**Provider liquidity.** An empty marketplace is worthless, and an inference marketplace is the one product that cannot be demoed without paying for GPU time.

Mitigations: grant-funded GPU hours for the first three providers, recruitment from the Solana ecosystem before testnet, and a workload choice (code generation) where a single consumer GPU is genuinely useful rather than needing a datacenter.

Second risk: verification cost. Independent verification can cost as much as the job. Sampling with escrow-aware incentives, not full replication.

---

## What we do not claim

- That Solana verifies model execution. It does not. MBIQ specifies its own verification system and documents its limits.
- That subjective output quality is cryptographically provable. It is not.
- That this is a novel idea. It is not — it is a well-known gap that the brief names, and the execution is what is being offered.

## Prior work

MineBench: a shipped desktop application that turns consumer hardware into a mining network — client runtime, pool, wallet payouts, public dashboard. Learned where reward attribution and settlement break at low scale. MBIQ prices per job and escrows before execution as a direct result.
