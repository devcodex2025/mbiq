# MBIQ — ONE-SHOT AUTONOMOUS MVP BUILD

## MASTER DIRECTIVE

You are operating inside OpenCode as the autonomous engineering organization responsible for designing, implementing, testing, securing, documenting, and running the first working MVP of **MBIQ — a decentralized AI compute network with blockchain-native economics on Solana**.

This is **NOT a planning exercise**.

Your final objective is a **working end-to-end MVP**, not:

- an architecture proposal;
- a collection of TODOs;
- mock UI;
- pseudocode;
- an unfinished scaffold;
- documentation describing what another developer should build.

You must inspect the existing repository, construct the required development-agent organization, design the architecture, implement the system, integrate all components, test them, run the application, debug failures, and leave a reproducible working MVP.

Do not stop after planning.

Do not stop after generating code.

Do not stop after individual unit tests pass.

Continue until the complete end-to-end system works or a genuine external/environmental blocker makes a requirement impossible.

When blocked:

1. identify the exact blocker;
2. collect evidence;
3. implement everything not blocked;
4. provide the exact next executable action;
5. never pretend an unavailable feature works.

The fundamental MBIQ lifecycle is:

```text
USER
  ↓
AI REQUEST
  ↓
QUOTE
  ↓
PAYMENT / ESCROW
  ↓
JOB
  ↓
MODEL + PROVIDER DISCOVERY
  ↓
ROUTING
  ↓
PROVIDER
  ↓
OPEN AI MODEL
  ↓
RESULT
  ↓
VERIFICATION
  ↓
SETTLEMENT
  ↓
PROVIDER REWARD + PROTOCOL REVENUE
```

Initial workloads:

1. CODE GENERATION
2. VIDEO GENERATION

The architecture must allow future workloads without redesigning the core protocol.

Possible future workloads include:

- image generation;
- audio;
- speech;
- embeddings;
- inference APIs;
- AI agents;
- fine-tuning;
- scientific compute;
- multimodal inference;
- other useful compute.

---

# 1. PRODUCT PRINCIPLE

MBIQ connects:

- users who need AI computation;
- independent compute providers;
- freely runnable open-source/open-weight AI models;
- intelligent workload routing;
- measurable execution;
- blockchain payments;
- provider rewards;
- protocol revenue.

A successful job should follow approximately:

```text
User
→ creates AI request
→ receives quote
→ authorizes payment
→ funds job
→ job enters network
→ compatible providers discovered
→ compatible models discovered
→ invalid candidates removed
→ Laya selects execution strategy
→ provider accepts job
→ provider executes model
→ execution evidence collected
→ result returned
→ result verified as far as realistically possible
→ payment settled
→ provider rewarded
→ protocol receives fee
→ user receives result
```

---

# 2. DEVELOPMENT AND PRODUCTION MUST BE SEPARATE

Never confuse the **development AI stack** with the **MBIQ production AI stack**.

## DEVELOPMENT

OpenCode is the development environment.

Use **Jev only inside the development environment** as an intelligent router for development agents/models.

Development models may include:

- ChatGPT;
- DeepSeek;
- other models already available to OpenCode/Jev.

Conceptually:

```text
OpenCode
    ↓
   Jev
    ↓
Best Development Model
    ↓
Specialized Agent
    ↓
Implementation
```

Jev should route development tasks intelligently.

Examples:

```text
Architecture
→ strongest reasoning model

Solana / financial logic
→ strongest correctness/reasoning model

Security
→ strongest security/reasoning model

Frontend
→ frontend-capable coding model

Debugging
→ strong reasoning/debugging model

Large mechanical coding task
→ efficient coding model
```

Optimize development for:

- correctness;
- speed;
- context efficiency;
- cost efficiency.

Do not unnecessarily call expensive models.

---

# 3. PRODUCTION MUST NOT REQUIRE PAID AI APIs

This is a HARD requirement.

The fundamental MBIQ network MUST NOT require:

- OpenAI API;
- Anthropic API;
- DeepSeek hosted API;
- Gemini hosted API;
- proprietary inference APIs;
- Jev SaaS;
- paid third-party LLM inference.

ChatGPT, DeepSeek and Jev may help **build MBIQ**.

They must not become hidden production dependencies.

Production MBIQ should execute models on provider hardware.

---

# 4. LAYA IS THE PRODUCTION DECISION ENGINE

Use **Laya** as the free/open production decision layer.

Laya does NOT perform the actual generative inference.

Laya helps select among already valid candidates.

Production architecture:

```text
MBIQ CLIENT
     ↓
MBIQ API
     ↓
JOB NORMALIZATION
     ↓
DETERMINISTIC FILTERS
     ↓
MODEL CANDIDATES
+
PROVIDER CANDIDATES
     ↓
Laya
     ↓
MODEL + PROVIDER + EXECUTION STRATEGY
     ↓
PROVIDER RUNTIME
     ↓
OPEN MODEL
     ↓
RESULT
     ↓
VERIFICATION
     ↓
SETTLEMENT
     ↓
SOLANA
```

Create a replaceable abstraction:

```ts
interface DecisionEngine {
  decideProvider(
    input: ProviderDecisionInput
  ): Promise<ProviderDecision>;

  decideModel(
    input: ModelDecisionInput
  ): Promise<ModelDecision>;

  decideExecutionStrategy(
    input: ExecutionDecisionInput
  ): Promise<ExecutionDecision>;

  scoreCandidates(
    input: CandidateScoringInput
  ): Promise<CandidateScore[]>;
}
```

Implement:

```text
LayaDecisionEngine
```

Also implement a deterministic fallback router.

If Laya becomes unavailable:

```text
Laya unavailable
→ deterministic fallback routing
→ job may continue
```

Fallback activation must be:

- logged;
- observable;
- tested.

Never allow Laya to override deterministic safety requirements.

---

# 5. MODEL POLICY

Production models must be freely runnable open-source/open-weight models compatible with the intended use.

Do NOT assume:

```text
free download = open source
```

or:

```text
open weights = unrestricted commercial license
```

Every model must have license metadata.

Unknown or incompatible licensing must make a model ineligible for production routing.

Do not hard-code the entire system around today's specific model names.

Model selection must be registry-driven.

---

# 6. FIRST TASK: BUILD THE ENGINEERING ORGANIZATION

Before implementing product features:

1. inspect repository;
2. inspect OpenCode configuration;
3. inspect existing agents;
4. inspect skills;
5. inspect scripts;
6. inspect package manager;
7. inspect CI;
8. inspect Docker;
9. inspect Solana configuration;
10. inspect existing application architecture.

Preserve good existing infrastructure.

Do not rewrite working components unnecessarily.

Then establish the smallest useful agent organization.

Required responsibilities:

```text
ORCHESTRATOR
ARCHITECT
SOLANA ENGINEER
ECONOMICS ENGINEER
BACKEND ENGINEER
PROVIDER RUNTIME ENGINEER
AI/ML ENGINEER
MODEL ROUTING ENGINEER
FRONTEND ENGINEER
SECURITY ENGINEER
QA/E2E ENGINEER
DEVOPS ENGINEER
REVIEWER
```

Do not spawn agents just to increase agent count.

Agents may combine roles where appropriate.

The ORCHESTRATOR owns:

- architecture consistency;
- task decomposition;
- parallel execution;
- integration;
- conflict resolution;
- testing;
- final Definition of Done.

---

# 7. FREEZE SHARED CONTRACTS BEFORE MASS PARALLELIZATION

Before large parallel implementation, define canonical schemas for:

```text
Job
Provider
Model
Quote
Execution
Result
Verification
Settlement
WalletSession
ProtocolConfig
```

Also define:

- API contracts;
- event contracts;
- job state machine;
- error model;
- on-chain/off-chain boundary.

Persist these contracts in the repository.

Agents must consume shared contracts instead of inventing incompatible versions.

---

# 8. AGENT RULES

Every agent must:

1. inspect relevant code before modifying it;
2. understand assigned scope;
3. reuse existing good code;
4. avoid duplicated functionality;
5. maintain typed interfaces;
6. validate external input;
7. write meaningful tests;
8. run relevant tests;
9. report failures honestly;
10. fix failures within scope;
11. update shared contracts when necessary;
12. avoid silently breaking another subsystem;
13. avoid placeholders on critical paths.

Agents may make routine engineering decisions autonomously.

Escalate only decisions affecting:

- custody;
- token authority;
- irreversible deployment;
- real financial transfers;
- destructive operations;
- fundamental security assumptions;
- undefined core tokenomics.

Never expose:

- private keys;
- seed phrases;
- wallet secrets;
- credentials;
- API keys.

Never perform mainnet deployment without explicit human authorization.

Use:

```text
LOCAL SOLANA VALIDATOR
```

as the primary MVP environment.

DEVNET support is desirable.

---

# 9. REPOSITORY ARCHITECTURE

Prefer a monorepo unless existing architecture strongly suggests otherwise.

Suggested structure:

```text
apps/
  client/
  api/
  provider/

packages/
  protocol/
  sdk/
  model-registry/
  provider-registry/
  routing/
  verification/
  economics/
  shared/
  config/

programs/
  mbiq-protocol/

services/
  laya/
  scheduler/
  execution/
  settlement/

infra/
  docker/
  scripts/

tests/
  unit/
  integration/
  e2e/
  security/

docs/
```

Exact naming may change for a legitimate architectural reason.

Do not reorganize working code merely for aesthetics.

---

# 10. TECHNOLOGY PRINCIPLES

Prefer where compatible:

- TypeScript;
- Rust;
- Solana;
- Anchor;
- React / Next.js or compatible existing frontend;
- Docker;
- typed APIs;
- schema validation;
- structured logging.

Prefer simple reliable architecture.

Do NOT introduce infrastructure simply because it is fashionable.

Avoid unnecessary:

- Kubernetes;
- microservices;
- distributed queues;
- databases;
- abstraction layers.

Every dependency must solve an actual problem.

---

# 11. ONE MBIQ CLIENT

Build one coherent client supporting two roles:

## USER

Consumes AI computation.

## PROVIDER

Supplies computation.

A wallet may act as both.

Do not build two disconnected products.

Share:

- wallet identity;
- authentication;
- protocol state;
- UI system;
- network configuration.

---

# 12. USER EXPERIENCE

Implement:

```text
Connect Wallet
↓
Authenticate
↓
Choose workload
↓
CODE / VIDEO
↓
Enter request
↓
Configure constraints
↓
Get quote
↓
Review price
↓
Fund job
↓
Track execution
↓
Receive result
↓
Inspect settlement
```

Show useful information:

- workload;
- model;
- provider;
- job status;
- elapsed time;
- quote;
- actual settlement;
- protocol fee;
- blockchain transaction state.

Never claim something is verified if it is not.

---

# 13. PROVIDER EXPERIENCE

Provider onboarding should include:

- wallet;
- provider identity;
- hardware detection;
- runtime detection;
- supported workloads;
- available models;
- benchmark;
- health;
- earnings;
- job history.

Detect where practical:

```text
CPU
RAM
GPU
VRAM
GPU architecture
OS
disk
runtime
precision
quantization support
```

Generate capabilities automatically.

Allow controlled manual overrides.

Never trust self-reported settlement-critical information without validation.

---

# 14. PROVIDER DAEMON

Build a real provider daemon.

Responsibilities:

```text
register provider
advertise capabilities
heartbeat
health checks
receive candidate job
validate requirements
accept/reject
prepare model
cache model
execute workload
collect metrics
produce result
authenticate execution record
participate in verification
track settlement
```

Providers must NOT blindly execute arbitrary shell commands supplied by users.

CODE GENERATION means generating code.

It does not mean unrestricted execution of arbitrary user-controlled programs.

If generated code execution is needed for validation, sandbox it using:

- resource limits;
- filesystem isolation;
- network restrictions;
- timeout;
- process limits;
- explicit runtime allowlist;
- cleanup.

---

# 15. MODEL REGISTRY

Implement a first-class MODEL REGISTRY.

Minimum schema:

```text
model_id
model_family
version
task
source
license
commercial_use_allowed
runtime
architecture
parameter_count
quantization
min_ram
recommended_ram
min_vram
recommended_vram
context_length
capabilities
benchmark_scores
estimated_throughput
health
availability
metadata
```

Support:

```text
CODE
VIDEO
```

Seed the registry with a small number of actually usable models after checking:

- license;
- hardware requirements;
- runtime;
- quality;
- availability.

Do not select a model solely because it is popular or large.

---

# 16. PROVIDER CAPABILITY REGISTRY

Provider capabilities must remain independent from model definitions.

Example:

```text
provider
hardware
supported_runtimes
ram
vram
gpu_architecture
supported_quantizations
available_models
benchmark_results
availability
latency
reliability
```

Never schedule impossible combinations.

Example:

```text
model requires 48 GB VRAM
provider has 12 GB VRAM
→ INELIGIBLE
```

Do not send impossible candidates to Laya.

---

# 17. MODEL SELECTION

Do NOT implement:

```text
largest model = best model
```

Instead optimize approximately for:

```text
MAXIMIZE USEFUL RESULT
```

subject to:

```text
task compatibility
license
hardware
RAM / VRAM
runtime
availability
user budget
latency
requested quality
provider reliability
execution price
```

Pipeline:

```text
ALL MODELS
↓
TASK FILTER
↓
LICENSE FILTER
↓
RUNTIME FILTER
↓
HARDWARE FILTER
↓
MEMORY FILTER
↓
AVAILABILITY FILTER
↓
PROVIDER MATCH
↓
DETERMINISTIC METRICS
↓
LAYA
↓
FINAL VALIDATION
↓
EXECUTION PLAN
```

---

# 18. PROVIDER SELECTION

Provider selection may consider:

- hardware capability;
- model availability;
- benchmark;
- price;
- latency;
- historical reliability;
- completion rate;
- current availability;
- estimated execution time.

Separate:

```text
RAW MEASUREMENTS
```

from:

```text
DERIVED SCORES
```

A provider cannot arbitrarily declare its own reputation.

---

# 19. CODE GENERATION

Implement at least one REAL freely runnable code-generation model path.

Create a generic runtime abstraction:

```ts
interface ModelRuntimeAdapter {
  load(): Promise<void>;
  health(): Promise<RuntimeHealth>;
  estimate(input: JobInput): Promise<ExecutionEstimate>;
  execute(input: JobInput): Promise<ExecutionResult>;
  cancel(executionId: string): Promise<void>;
  metrics(): Promise<RuntimeMetrics>;
}
```

Do not tightly couple MBIQ to one inference framework.

Return:

- generated code;
- model metadata;
- provider metadata;
- execution timing;
- usage metrics;
- execution ID;
- result hash.

---

# 20. VIDEO GENERATION

Implement a real freely runnable video-generation adapter.

Video generation can require substantial VRAM.

Hardware eligibility must therefore be strict.

If development hardware cannot run the selected real video model, the E2E environment may use:

```text
TEST VIDEO ADAPTER
```

but it MUST be explicitly labeled as a test adapter.

Never present mock output as actual AI inference.

The codebase must nevertheless include a real configuration/integration path for at least one supported video model.

---

# 21. JOB PROTOCOL

Canonical Job should contain fields equivalent to:

```text
job_id
owner
workload_type
request_hash
constraints
budget
payment_token
quote
created_at
expires_at
status
assigned_provider
selected_model
execution_id
result_hash
verification
settlement
```

Implement strict transitions.

Successful path:

```text
CREATED
→ QUOTED
→ FUNDED
→ QUEUED
→ MATCHING
→ ASSIGNED
→ RUNNING
→ VERIFYING
→ COMPLETED
→ SETTLED
```

Also support:

```text
FAILED
CANCELLED
EXPIRED
REFUNDED
```

Illegal transitions must fail.

Retries must not produce duplicate settlements.

---

# 22. SOLANA PROGRAM

Build an MVP Solana program responsible for financial/protocol state that benefits from blockchain guarantees.

Potential responsibilities:

- protocol configuration;
- job/payment escrow;
- payment authorization;
- provider settlement;
- protocol fee;
- settlement state;
- treasury destination;
- token accounting.

Do NOT store large AI data on-chain.

Do not store:

- complete prompts;
- videos;
- generated source files;
- large inference metadata.

Store hashes/references where appropriate.

---

# 23. MBIQ TOKEN

MBIQ is the network economic token.

Architecture must support:

```text
USER PAYMENT → MBIQ

PROVIDER REWARD → MBIQ

PROTOCOL FEE → MBIQ
```

Do NOT invent:

- total supply;
- token price;
- emissions;
- mint policy;
- treasury allocation;
- authority policy;
- fee percentage.

If these are undefined, expose them as configuration and document them as founder decisions.

For MVP use local/devnet test MBIQ.

Never introduce uncontrolled minting.

---

# 24. PAYMENT LIFECYCLE

Implement:

```text
USER
↓
QUOTE
↓
PAYMENT AUTHORIZATION
↓
ESCROW
↓
JOB EXECUTION
↓
VERIFICATION
↓
SETTLEMENT
├── PROVIDER REWARD
└── PROTOCOL FEE
```

Handle:

- failed job;
- provider timeout;
- expiration;
- cancellation;
- refund;
- replay;
- duplicate settlement attempt.

Financial operations must be deterministic and idempotent.

---

# 25. PROTOCOL REVENUE

The protocol must have a path to revenue from the first functional MVP.

Use configurable fee mechanics.

Conceptually:

```text
gross_job_payment
=
provider_reward
+
protocol_fee
+
explicitly_configured_costs
```

Do NOT invent a percentage.

Expose:

- provider earnings;
- protocol revenue;
- job payment;
- fee;

in tests and the relevant application UI.

---

# 26. PROVIDER ECONOMICS

Reward useful completed computation.

Do NOT use:

```text
largest model = highest reward
```

MVP settlement should be simple, deterministic and understandable.

Future economics may incorporate:

- useful compute delivered;
- workload difficulty;
- requested quality;
- actual execution cost;
- hardware requirements;
- demand;
- latency;
- provider reliability;
- successful completion;
- measurable output quality.

For MVP, prefer:

```text
USER JOB PRICE
→ deterministic quote
→ execution
→ successful verification
→ deterministic settlement
```

Laya MUST NOT determine arbitrary provider rewards.

Laya may influence routing.

Laya must NOT control financial truth.

All payment calculations must be reproducible by deterministic code.

The same economic inputs must always produce the same settlement result.

---

# 27. AI DECISIONS VS FINANCIAL DECISIONS

This boundary is CRITICAL.

AI/Laya may help determine:

```text
Which compatible model?
Which compatible provider?
Which execution strategy?
Which candidate offers the best expected result?
```

AI/Laya MUST NOT independently determine:

```text
Who owns a wallet?
Does escrow exist?
Did payment occur?
What is the actual token balance?
How many tokens must be transferred?
What is the protocol fee?
Can an unauthorized transfer occur?
Has settlement already happened?
```

Financial truth comes from:

```text
DETERMINISTIC APPLICATION LOGIC
+
SOLANA STATE
```

Never from an LLM response.

---

# 28. QUOTING SYSTEM

Implement a deterministic quote engine.

A quote should contain fields equivalent to:

```text
quote_id
job_type
model_class
provider
estimated_execution_cost
provider_reward
protocol_fee
total_price
payment_token
expires_at
pricing_version
```

A quote must expire.

A quote used to fund a job must be cryptographically or structurally tied to that job.

Prevent:

- quote substitution;
- client-side price manipulation;
- stale quote execution;
- provider changing price after escrow without protocol approval.

For MVP, simple deterministic pricing is preferable to an opaque dynamic market.

Design the abstraction so competitive provider pricing can be introduced later.

---

# 29. VERIFICATION

Do NOT claim arbitrary AI computation is magically trustlessly verifiable.

Build an honest MVP verification layer.

Record where appropriate:

```text
job_id
request_hash
model_id
model_version
provider_id
execution_id
runtime
runtime_version
start_timestamp
finish_timestamp
execution_metrics
result_hash
provider_signature
verification_status
```

Deterministic facts should be verified deterministically.

Example:

```text
expected result hash
!=
submitted result hash
→ reject
```

Subjective AI quality is different from deterministic execution verification.

Do not pretend subjective quality is cryptographic proof.

Create extensible interfaces for future:

- replicated execution;
- challenge mechanisms;
- random verification;
- provider reputation;
- sampling;
- trusted execution environments;
- cryptographic proofs;
- ZK-based techniques where technically applicable.

These future systems must NOT be required to make the MVP function.

---

# 30. RESULT STORAGE

Do not store large AI outputs on Solana.

Store generated artifacts off-chain.

Blockchain state may reference:

```text
job_id
result_hash
storage_reference
settlement_state
```

For local MVP, use a simple reliable storage abstraction.

Design:

```ts
interface ResultStore {
  put(result: ResultArtifact): Promise<ResultReference>;
  get(reference: ResultReference): Promise<ResultArtifact>;
  delete(reference: ResultReference): Promise<void>;
}
```

The implementation may initially use local/object storage.

Do not tightly couple the protocol to one storage vendor.

Large video files must never be placed directly into Solana accounts.

---

# 31. DATA PRIVACY

MBIQ should minimize unnecessary exposure of user data.

Separate:

```text
PUBLIC BLOCKCHAIN DATA
```

from:

```text
PRIVATE JOB DATA
```

Never put private prompts or generated private outputs directly on Solana.

Use hashes where blockchain linkage is necessary.

Document:

- what the user sends;
- what the provider receives;
- what MBIQ backend sees;
- what is stored;
- where it is stored;
- retention behavior;
- what becomes public;
- what remains private.

Providers should receive only the information required to execute the assigned workload.

Do not unnecessarily log full prompts or outputs.

---

# 32. WALLET AUTHENTICATION

Implement safe wallet authentication.

Prefer a challenge-based flow:

```text
CLIENT
↓
request nonce
↓
SERVER generates nonce
↓
CLIENT signs structured message
↓
SERVER verifies signature
↓
SERVER invalidates nonce
↓
SESSION
```

Bind the signed message to fields such as:

```text
domain
wallet
nonce
purpose
issued_at
expiration
```

Nonce must be:

- unpredictable;
- short-lived;
- single-use.

Prevent signature replay.

Never request:

```text
seed phrase
private key
```

---

# 33. SECURITY THREAT MODEL

The SECURITY ENGINEER must explicitly threat-model at least:

### Wallet / authentication

- signature replay;
- nonce reuse;
- session theft;
- wallet impersonation;
- malformed signatures.

### Payments

- payment replay;
- double settlement;
- manipulated quote;
- wrong recipient;
- unauthorized refund;
- fake payment confirmation;
- settlement race conditions.

### Providers

- provider impersonation;
- fake hardware;
- fake model availability;
- fake benchmark;
- fake completion;
- result substitution;
- heartbeat manipulation;
- Sybil providers.

### Jobs

- job tampering;
- request substitution;
- result substitution;
- invalid state transition;
- duplicate job processing.

### AI workloads

- malicious prompts;
- prompt injection against infrastructure;
- unsafe generated code;
- arbitrary command execution;
- filesystem access;
- network abuse;
- denial of service.

### Infrastructure

- container escape;
- secret leakage;
- API abuse;
- RPC manipulation;
- dependency compromise;
- untrusted model artifacts.

For each meaningful threat:

```text
THREAT
→ IMPACT
→ MITIGATION
→ TEST
```

---

# 34. API

Build a typed API.

Domains should include where appropriate:

```text
/auth
/wallet
/jobs
/quotes
/providers
/models
/routing
/executions
/results
/settlements
/health
```

Validate all external input.

Use shared/generated types wherever practical.

Do NOT let:

```text
frontend
backend
provider
Solana client
```

invent incompatible representations of the same protocol object.

Use explicit error codes.

Do not expose internal stack traces or secrets to clients.

---

# 35. PROVIDER COMMUNICATION

Create a clear provider protocol.

For MVP this may use an appropriate combination of:

- HTTP;
- WebSocket;
- polling;
- authenticated messages.

Do not introduce a complex distributed messaging system unless required.

Provider protocol must support:

```text
REGISTER
HEARTBEAT
CAPABILITY UPDATE
JOB OFFER
JOB ACCEPT
JOB REJECT
JOB START
PROGRESS
JOB RESULT
JOB FAILURE
```

Messages should include protocol versioning.

Authenticate provider messages.

Prevent one provider from submitting results for another provider's job.

---

# 36. HEARTBEATS AND PROVIDER AVAILABILITY

Providers must maintain health/availability information.

Track:

```text
last_seen
status
active_jobs
capacity
health
```

Example:

```text
provider misses heartbeat threshold
→ mark unavailable
→ stop assigning new jobs
```

Do not immediately destroy provider reputation because of one temporary network interruption.

Separate:

```text
availability
```

from:

```text
historical reliability
```

---

# 37. BENCHMARKING

Create a provider benchmarking abstraction.

Benchmarks should help estimate:

- capability;
- expected throughput;
- model feasibility;
- approximate execution time.

Do not trust arbitrary benchmark values submitted by a provider without validation.

For MVP, implement a reproducible benchmark flow where practical.

Store:

```text
benchmark_id
provider
hardware
benchmark_type
version
result
timestamp
verification_status
```

Benchmark version matters.

Results from incompatible benchmark versions must not silently be compared as identical measurements.

---

# 38. REPUTATION

Create a minimal provider reputation model based on measurable history.

Possible inputs:

```text
completed_jobs
failed_jobs
timeouts
verification_failures
uptime
latency
```

Keep reputation separate from payment.

Do not implement an opaque AI-generated reputation number.

Prefer deterministic calculation.

Design the interface so more sophisticated reputation systems can be introduced later.

---

# 39. SCHEDULER

Implement a scheduler responsible for:

```text
queued jobs
↓
eligible providers
↓
eligible models
↓
routing
↓
assignment
```

Prevent one provider from accepting unlimited jobs beyond its declared/measured capacity.

Track provider concurrency.

Example:

```text
GPU has capacity for 1 large video job
→ do not schedule 5 simultaneously
```

Account for model memory requirements.

---

# 40. FAILURE RECOVERY

Design explicit recovery behavior.

Examples:

### Provider disappears before execution

```text
ASSIGNED
→ provider timeout
→ QUEUED
→ route again
```

### Provider disappears during execution

Depending on job semantics:

```text
RUNNING
→ timeout
→ FAILED
```

or:

```text
RUNNING
→ retryable failure
→ QUEUED
```

Avoid accidental double execution where it would produce double settlement.

### Backend restarts

Persistent job state must allow recovery.

Do not rely entirely on in-memory state.

### Laya fails

```text
Laya failure
→ deterministic fallback router
```

### Solana RPC temporarily fails

Retry safely.

Never interpret:

```text
unknown transaction state
```

as:

```text
transaction failed
```

without verification.

---

# 41. IDEMPOTENCY

Critical operations must support idempotency.

Especially:

```text
job creation
quote acceptance
payment confirmation
job assignment
result submission
settlement
refund
```

Use stable IDs / idempotency keys.

The following must be impossible:

```text
same successful job
→ settlement
→ retry
→ second settlement
```

Write tests proving this.

---

# 42. OBSERVABILITY

Implement structured logging.

Track at minimum:

```text
jobs_created
jobs_queued
jobs_running
jobs_completed
jobs_failed

providers_online
providers_offline

routing_decisions
routing_fallbacks

execution_duration
execution_failures

settlement_success
settlement_failure

provider_earnings
protocol_revenue
```

Logs should include correlation identifiers:

```text
job_id
execution_id
provider_id
```

where useful.

Never log secrets.

Avoid logging private prompts by default.

---

# 43. CLIENT DASHBOARD

The MVP client should contain a useful dashboard.

USER view:

```text
wallet
balance
create job
active jobs
job history
results
payments
```

PROVIDER view:

```text
provider status
hardware
available models
health
active jobs
completed jobs
earnings
```

PROTOCOL/DEVELOPMENT view may expose:

```text
providers online
jobs
model availability
protocol revenue
routing health
```

Do not spend excessive time on visual polish before the complete economic/execution loop works.

Functional clarity first.

---

# 44. CODE GENERATION UI

Provide a practical CODE interface.

At minimum:

```text
prompt
optional language/framework
optional constraints
quality/price preference if supported
submit
```

Result view should show:

```text
generated code
model
provider
job ID
execution time
price
verification status
```

Allow easy copy/export of generated source.

---

# 45. VIDEO GENERATION UI

Provide a practical VIDEO interface.

At minimum:

```text
prompt
supported generation parameters
submit
progress
result
```

Display:

```text
model
provider
job
execution status
price
result
verification status
```

Large generated media should use the result-storage abstraction.

---

# 46. TOKEN BALANCE AND PAYMENT UX

User must understand:

```text
available MBIQ
job price
amount reserved
amount settled
protocol fee
refund if applicable
```

Never hide financial state behind vague UI.

Do not claim fiat value unless a reliable price source exists.

The MVP can operate purely in token units.

---

# 47. CONFIGURATION

Create centralized validated configuration.

Separate:

```text
development
test
local-validator
devnet
production
```

Configuration should cover:

```text
Solana RPC
program ID
token mint
treasury
protocol fee
Laya endpoint/config
database/storage
provider settings
model registry
timeouts
routing
logging
```

Fail fast on invalid critical configuration.

Never commit production secrets.

Provide `.env.example` where appropriate.

---

# 48. DATABASE / PERSISTENCE

Choose the simplest reliable persistence layer appropriate for the existing stack.

Persist at least:

```text
jobs
quotes
providers
capabilities
models
executions
results metadata
verification
settlement metadata
auth nonces/sessions as appropriate
```

Blockchain remains authoritative for on-chain financial state.

Database state must not override contradictory confirmed Solana state.

Use migrations.

Do not rely on manual database setup.

---

# 49. ON-CHAIN / OFF-CHAIN AUTHORITY

Explicitly document authority.

Example:

```text
TOKEN BALANCE
→ Solana

ESCROW
→ Solana

FINAL ON-CHAIN SETTLEMENT
→ Solana

PROMPT
→ off-chain

VIDEO
→ off-chain

MODEL REGISTRY METADATA
→ primarily off-chain

PROVIDER HEARTBEAT
→ off-chain

ROUTING
→ off-chain

EXECUTION
→ provider/off-chain
```

Do not duplicate authoritative state unnecessarily.

---

# 50. SOLANA SECURITY

The SOLANA ENGINEER + SECURITY ENGINEER must review:

- PDA derivation;
- signer validation;
- account ownership;
- token mint validation;
- token account validation;
- arithmetic;
- duplicate initialization;
- replay;
- double settlement;
- unauthorized cancellation;
- unauthorized refund;
- treasury substitution;
- provider substitution.

Use checked arithmetic where appropriate.

Never trust client-provided financial values without validating them against protocol state.

---

# 51. SOLANA TESTS

Write tests covering at minimum:

```text
initialize protocol
create/fund job
valid settlement
provider receives expected amount
treasury receives expected fee
unauthorized settlement fails
double settlement fails
wrong provider fails
wrong token mint fails
invalid state fails
refund path works
unauthorized refund fails
```

Tests must inspect resulting balances/state.

Do not only test transaction success.

---

# 52. MODEL DOWNLOAD / SUPPLY CHAIN

Treat model files as untrusted artifacts.

Where practical:

- use known model sources;
- record source;
- record revision/version;
- support checksums;
- avoid arbitrary executable model packages;
- isolate model runtime;
- pin dependencies.

Do not execute arbitrary setup scripts downloaded with models without review.

---

# 53. RESOURCE MANAGEMENT

Provider runtime must avoid exhausting the host.

Implement controls for:

```text
GPU memory
RAM
disk
concurrent jobs
execution timeout
model cache
```

When insufficient resources exist:

```text
reject job safely
```

rather than crashing the provider.

---

# 54. MODEL CACHE

Provider should be able to cache models.

Track:

```text
model
version
size
location
last_used
health
```

Do not repeatedly download huge models for every job.

Provide safe cache cleanup behavior.

---

# 55. MODEL HEALTH

Before advertising a model as available, verify basic runtime health where practical.

States may include:

```text
AVAILABLE
LOADING
UNAVAILABLE
BROKEN
INSUFFICIENT_RESOURCES
```

Routing must not choose BROKEN models.

---

# 56. JOB CANCELLATION

Implement safe cancellation semantics.

Consider different stages:

```text
CREATED
QUOTED
FUNDED
QUEUED
ASSIGNED
RUNNING
```

Cancellation rules may differ by state.

Do not automatically promise full refund after expensive computation has already occurred unless economic policy explicitly says so.

For MVP, define deterministic behavior and document it.

---

# 57. TIMEOUTS

Define timeouts for:

- quote;
- payment;
- provider acceptance;
- heartbeat;
- job execution;
- result submission;
- settlement retry.

Do not leave jobs stuck indefinitely.

Timeout transitions must be testable.

---

# 58. PROTOCOL VERSIONING

Introduce protocol version fields where useful.

Provider and API compatibility should be detectable.

Do not silently process structurally incompatible provider messages.

---

# 59. SDK

Create a small typed MBIQ SDK shared by client/provider where useful.

Potential capabilities:

```text
authenticate wallet
create job
get quote
fund job
get job
list models
list providers
submit provider heartbeat
submit execution result
inspect settlement
```

Avoid duplicating protocol client logic across applications.

---

# 60. LOCAL DEVELOPMENT

Create a single documented path to start the MVP.

Aim for something equivalent to:

```bash
docker compose up
```

plus clearly documented Solana initialization where necessary.

Or provide a single orchestration script such as:

```bash
pnpm mbiq:dev
```

It should start as much as practical:

- persistence;
- local Solana;
- Laya;
- API;
- client;
- provider;
- required supporting services.

Automate initialization.

Avoid a 30-step manual setup.

---

# 61. SEED / DEMO DATA

Provide local development seed data.

Examples:

```text
test MBIQ mint
test user
test provider
model registry entries
protocol configuration
```

Do not use real funds.

---

# 62. TESTING STRATEGY

Testing is mandatory.

Implement:

```text
UNIT TESTS
INTEGRATION TESTS
SOLANA PROGRAM TESTS
API TESTS
ROUTING TESTS
PROVIDER TESTS
ECONOMICS TESTS
SECURITY TESTS
E2E TESTS
```

Do not merely generate test files.

Run them.

Fix failures.

---

# 63. REQUIRED FINANCIAL INVARIANTS

Tests must prove at minimum:

### Invariant 1

```text
A payment cannot settle twice.
```

### Invariant 2

```text
Provider cannot receive more than authorized.
```

### Invariant 3

```text
Protocol fee calculation is deterministic.
```

### Invariant 4

```text
Failed job cannot silently settle as successful.
```

### Invariant 5

```text
Unauthorized wallet cannot control another user's job.
```

### Invariant 6

```text
Illegal job transition fails.
```

### Invariant 7

```text
Refund + provider settlement cannot both consume the same escrow.
```

### Invariant 8

```text
Settlement amount
=
authorized job payment
-
valid refund if any
```

No tokens may appear through accounting inconsistencies.

### Invariant 9

```text
provider_reward
+
protocol_fee
+
refund
<=
funded_amount
```

for every job.

### Invariant 10

A result submitted by an unauthorized provider must never cause settlement.

### Invariant 11

A result whose hash does not match the recorded result metadata must fail verification.

### Invariant 12

Expired or replayed wallet authentication must fail.

### Invariant 13

A model incompatible with provider hardware must never reach execution.

### Invariant 14

A model with unknown or incompatible licensing must never be selected for production execution.

### Invariant 15

Laya failure must never corrupt financial state.

### Invariant 16

Backend restart must not cause duplicate execution settlement.

Test these invariants explicitly.

---

# 64. REQUIRED END-TO-END TEST

Create an automated E2E scenario demonstrating the complete MBIQ lifecycle.

The E2E test should perform:

```text
START LOCAL INFRASTRUCTURE
↓
START SOLANA LOCAL VALIDATOR
↓
DEPLOY MBIQ PROGRAM
↓
INITIALIZE PROTOCOL
↓
CREATE TEST MBIQ TOKEN
↓
INITIALIZE TREASURY
↓
CREATE TEST USER
↓
CREATE TEST PROVIDER
↓
START LAYA
↓
START BACKEND
↓
START PROVIDER DAEMON
↓
DETECT HARDWARE
↓
REGISTER PROVIDER
↓
REGISTER CAPABILITIES
↓
REGISTER AVAILABLE MODELS
↓
PROVIDER HEARTBEAT
↓
USER CONNECTS WALLET
↓
USER AUTHENTICATES
↓
USER CREATES CODE JOB
↓
SYSTEM CREATES QUOTE
↓
USER FUNDS ESCROW
↓
JOB ENTERS QUEUE
↓
DISCOVER MODELS
↓
DISCOVER PROVIDERS
↓
DETERMINISTIC FILTERS
↓
LAYA ROUTING
↓
ASSIGN PROVIDER
↓
PROVIDER ACCEPTS
↓
RUN MODEL
↓
GENERATE CODE
↓
COLLECT METRICS
↓
HASH RESULT
↓
SUBMIT RESULT
↓
VERIFY
↓
COMPLETE JOB
↓
SETTLE ESCROW
↓
PAY PROVIDER
↓
PAY PROTOCOL
↓
USER RECEIVES RESULT
```

After settlement verify:

```text
user balance
provider balance
treasury balance
escrow balance
job state
result hash
settlement record
```

Then deliberately retry settlement.

Expected:

```text
SECOND SETTLEMENT
→ REJECTED
```

This is mandatory.

---

# 65. VIDEO E2E PATH

Run the same protocol lifecycle for VIDEO.

Preferred:

```text
REAL VIDEO MODEL
+
REAL PROVIDER EXECUTION
```

when hardware supports it.

If current development hardware cannot execute the chosen video model:

use the explicitly labeled:

```text
TEST_VIDEO_RUNTIME
```

for protocol E2E.

However, simultaneously verify that:

- real video runtime adapter exists;
- configuration exists;
- capability requirements exist;
- model registry contains valid metadata;
- provider can report whether it is capable of running it.

The final report must distinguish:

```text
PROTOCOL TESTED
```

from:

```text
REAL VIDEO INFERENCE TESTED
```

Never claim the latter unless it actually happened.

---

# 66. NEGATIVE E2E TESTS

Do not test only the happy path.

Run scenarios including:

### Unauthorized settlement

Expected:

```text
REJECTED
```

### Duplicate settlement

Expected:

```text
REJECTED
```

### Wrong provider submits result

Expected:

```text
REJECTED
```

### Invalid result hash

Expected:

```text
VERIFICATION FAILED
```

### Provider disappears

Expected:

```text
TIMEOUT
→ RECOVERY / FAILURE POLICY
```

### Laya unavailable

Expected:

```text
DETERMINISTIC FALLBACK ROUTER
```

### Model exceeds provider VRAM

Expected:

```text
CANDIDATE REMOVED BEFORE ROUTING
```

### Unsupported model license

Expected:

```text
MODEL INELIGIBLE
```

### Expired wallet nonce

Expected:

```text
AUTHENTICATION REJECTED
```

### User attempts to control another user's job

Expected:

```text
REJECTED
```

---

# 67. AUTONOMOUS IMPLEMENTATION LOOP

The OpenCode organization must operate using this loop:

```text
INSPECT
↓
PLAN
↓
FREEZE CONTRACTS
↓
DECOMPOSE
↓
PARALLEL IMPLEMENTATION
↓
INTEGRATE
↓
BUILD
↓
TEST
↓
RUN
↓
OBSERVE FAILURES
↓
DEBUG
↓
FIX
↓
RETEST
↓
SECURITY REVIEW
↓
E2E
↓
FINAL REVIEW
```

A failed build is not completion.

A generated test suite is not completion.

An architecture document is not completion.

A frontend that uses fake backend data is not completion.

A backend without functioning settlement is not completion.

A Solana program without client integration is not completion.

Continue iterating.

---

# 68. NO TODO ESCAPE HATCH

Do not replace required MVP functionality with:

```text
TODO
FIXME
IMPLEMENT LATER
PLACEHOLDER
MOCK
STUB
```

on the critical path.

Mocks are allowed only where an external environmental limitation genuinely prevents execution.

When a mock/test adapter is unavoidable:

1. name it explicitly as TEST/MOCK;
2. isolate it behind the same production interface;
3. implement the real adapter path;
4. document why real execution was unavailable;
5. never report the mock as production functionality.

Search the repository before final completion for:

```text
TODO
FIXME
HACK
TEMP
MOCK
STUB
NOT IMPLEMENTED
```

Review every occurrence.

Critical-path occurrences must be resolved.

---

# 69. DO NOT FAKE SUCCESS

Never fabricate:

- successful tests;
- blockchain transactions;
- provider execution;
- model inference;
- benchmark results;
- token balances;
- security verification;
- deployment;
- Laya decisions.

If something could not run, report:

```text
NOT EXECUTED
```

and explain exactly why.

Distinguish:

```text
IMPLEMENTED
TESTED
E2E TESTED
MANUALLY VERIFIED
NOT TESTED
BLOCKED
```

---

# 70. SECURITY REVIEW GATE

Before declaring completion, SECURITY ENGINEER performs a final review.

At minimum inspect:

```text
authentication
authorization
wallet signatures
nonce handling
provider authentication
job ownership
quote integrity
escrow
settlement
refund
PDA/account validation
result integrity
provider isolation
generated-code isolation
secret management
API validation
dependency risks
```

Any CRITICAL security issue blocks completion.

Any HIGH issue affecting funds, authentication, arbitrary code execution, custody or cross-user data access blocks completion.

Fix it.

Run relevant tests again.

---

# 71. REVIEWER GATE

The REVIEWER must independently inspect the integrated system.

The reviewer should look specifically for situations where individual components work but the product does not.

Verify:

```text
CLIENT ↔ API

API ↔ DATABASE

API ↔ SOLANA

API ↔ ROUTER

ROUTER ↔ LAYA

API ↔ PROVIDER

PROVIDER ↔ MODEL

EXECUTION ↔ RESULT STORE

RESULT ↔ VERIFICATION

VERIFICATION ↔ SETTLEMENT

SETTLEMENT ↔ SOLANA

SOLANA ↔ CLIENT STATE
```

Check that shared schemas actually match at runtime.

Fix integration problems before completion.

---

# 72. PERFORMANCE AND COST SANITY CHECK

Do not prematurely optimize.

However, inspect obvious problems such as:

- repeatedly loading the same model;
- repeatedly downloading model weights;
- unnecessary blockchain writes;
- excessive polling;
- unbounded database queries;
- unbounded logs;
- provider accepting more jobs than capacity;
- sending large AI artifacts through blockchain transactions;
- excessive development-model calls.

Optimize obvious bottlenecks that materially affect MVP usability.

---

# 73. DOCUMENTATION

Create concise, useful documentation.

At minimum:

```text
README.md
docs/architecture.md
docs/protocol.md
docs/provider.md
docs/models.md
docs/economics.md
docs/security.md
docs/local-development.md
```

README must explain:

```text
What is MBIQ?
How does it work?
What is required?
How do I start it?
How do I run a provider?
How do I run tests?
How do I run E2E?
```

Do not generate enormous documentation that becomes harder to maintain than the code.

Prefer executable commands and diagrams.

---

# 74. REQUIRED LOCAL START EXPERIENCE

A developer cloning the finished repository should have a straightforward path to running the system.

Aim for something approximately equivalent to:

```bash
git clone ...
cd mbiq
pnpm install
pnpm mbiq:dev
```

or:

```bash
docker compose up
```

plus only genuinely necessary initialization.

Provide scripts for:

```text
install
build
lint
typecheck
test
test:solana
test:e2e
dev
provider
```

where appropriate.

The exact package manager/commands should follow the repository's actual stack.

Do not create competing package-management systems.

---

# 75. DEFINITION OF DONE

The MVP is complete only when the following conditions are satisfied.

## Architecture

- Development Jev stack is separated from production.
- Production uses Laya decision abstraction.
- Production does not require proprietary paid inference APIs.
- Core protocol contracts are shared and typed.
- On-chain/off-chain responsibilities are documented.

## Client

- User can connect wallet.
- User can authenticate.
- User can create CODE job.
- User can create VIDEO job.
- User can receive quote.
- User can fund job.
- User can monitor state.
- User can receive result.
- User can inspect settlement.
- Provider can inspect provider state and earnings.

## Provider

- Provider daemon runs.
- Hardware detection works.
- Capabilities can be registered.
- Heartbeat works.
- Jobs can be accepted/rejected.
- Code inference has a real execution path.
- Video has a real runtime integration path.
- Metrics/results are returned.

## Routing

- Model registry exists.
- Provider registry exists.
- Invalid candidates are deterministically filtered.
- Laya routing works.
- Deterministic fallback exists.
- Hardware incompatibility is rejected.
- License incompatibility is rejected.

## Blockchain

- Solana program builds.
- Protocol initializes.
- Test MBIQ works locally.
- Job escrow works.
- Provider settlement works.
- Protocol fee works.
- Refund/failure logic works.
- Unauthorized settlement fails.
- Duplicate settlement fails.

## Economics

- Quote is deterministic.
- Provider reward is deterministic.
- Protocol fee is deterministic.
- Provider earnings can be observed.
- Protocol revenue can be observed.
- Laya cannot arbitrarily change payment.

## Security

- Wallet auth uses safe challenge/nonce logic.
- Replay is rejected.
- Cross-user authorization is enforced.
- Provider identity is validated.
- Result integrity is checked.
- Critical Solana account/signature rules are tested.
- Generated-code execution, if present, is sandboxed.
- No secrets are committed.

## Testing

- Unit tests run.
- Integration tests run.
- Solana tests run.
- Routing tests run.
- Provider tests run.
- Economics tests run.
- Security tests run.
- CODE E2E completes.
- VIDEO protocol E2E completes.
- Negative financial tests complete.

## Operations

- Local environment can be started reproducibly.
- Configuration is validated.
- Logs are structured.
- Critical state survives service restart where required.
- README contains executable setup instructions.

---

# 76. COMPLETION STANDARD

Do NOT interpret:

```text
code written
```

as:

```text
task completed
```

The standard is:

```text
CODE WRITTEN
+
CODE BUILDS
+
TESTS PASS
+
SERVICES START
+
COMPONENTS COMMUNICATE
+
E2E FLOW EXECUTES
+
FINANCIAL INVARIANTS HOLD
+
SECURITY REVIEW PASSES
```

Only then may the system be described as a working MVP.

---

# 77. FINAL EXECUTION PHASE

After implementation, execute this sequence:

```text
INSTALL
↓
FORMAT
↓
LINT
↓
TYPECHECK
↓
BUILD
↓
UNIT TESTS
↓
INTEGRATION TESTS
↓
SOLANA TESTS
↓
SECURITY TESTS
↓
START LOCAL STACK
↓
CODE E2E
↓
VIDEO E2E
↓
NEGATIVE E2E
↓
FINAL REVIEW
```

When a step fails:

```text
FAIL
↓
ROOT CAUSE
↓
FIX
↓
RUN RELEVANT TEST
↓
RUN DOWNSTREAM TESTS AGAIN
```

Do not simply suppress errors to make CI green.

---

# 78. AUTONOMY

Do not repeatedly ask the human developer routine questions.

When several technically reasonable implementation choices exist:

1. inspect existing repository conventions;
2. choose the simplest production-sensible option;
3. document the decision;
4. continue.

Only stop for human input if proceeding would require:

- real funds;
- mainnet deployment;
- private credentials unavailable to you;
- irreversible external action;
- undefined token authority decision;
- destructive operation with meaningful risk;
- a fundamental product decision that cannot safely be represented as configuration.

Everything else should proceed autonomously.

---

# 79. PRIORITY ORDER

When tradeoffs are necessary, prioritize:

```text
1. SECURITY OF FUNDS AND USERS
2. CORRECTNESS
3. COMPLETE END-TO-END FUNCTIONALITY
4. RELIABILITY
5. SIMPLE ARCHITECTURE
6. TESTABILITY
7. PROVIDER ECONOMICS
8. PERFORMANCE
9. UX
10. VISUAL POLISH
```

Do not sacrifice financial correctness for demo appearance.

---

# 80. MVP SCOPE DISCIPLINE

Do NOT turn the first build into an attempt to solve every decentralized-compute problem.

The MVP needs to prove:

```text
USER CAN BUY USEFUL AI COMPUTE

PROVIDER CAN SUPPLY USEFUL AI COMPUTE

OPEN MODEL CAN EXECUTE THE JOB

ROUTER CAN MATCH THEM

SOLANA CAN HANDLE PAYMENT/SETTLEMENT

PROVIDER CAN EARN

PROTOCOL CAN EARN

USER CAN RECEIVE RESULT
```

That is the core proof.

Avoid unnecessary features until this loop works.

---

# 81. FUTURE-COMPATIBLE, NOT FUTURE-BLOATED

Design clean interfaces for future:

```text
more workloads
more model runtimes
more providers
more verification methods
more pricing mechanisms
provider staking
disputes
reputation improvements
additional storage backends
additional blockchain integrations
```

But do not implement speculative complexity unless required by the MVP.

Use interfaces and modular boundaries instead of unfinished feature code.

---

# 82. FINAL REPORT

When the build is genuinely complete, return a concise engineering report.

Use this structure:

```text
MBIQ MVP BUILD REPORT

STATUS
- Working / Partially Working / Blocked

IMPLEMENTED
- ...

ARCHITECTURE
- ...

AGENTS USED
- ...

DEVELOPMENT MODEL ROUTING
- Jev usage
- models/roles used

PRODUCTION AI
- Laya status
- fallback status
- code model/runtime
- video model/runtime

SOLANA
- program
- escrow
- settlement
- protocol fee
- tests

PROVIDER
- hardware detection
- registration
- execution
- earnings

E2E
- CODE: PASS / FAIL / BLOCKED
- VIDEO: PASS / FAIL / TEST-ADAPTER / BLOCKED

SECURITY
- tests/review
- unresolved findings

TESTS
- exact commands
- pass/fail counts where available

HOW TO RUN
- exact commands

KNOWN LIMITATIONS
- ...

FOUNDER DECISIONS REQUIRED
- only genuinely undefined product/economic decisions

NEXT RECOMMENDED STEP
- ...
```

Never report:

```text
WORKING
```

if only mocks or isolated components were tested.

---

# 83. FINAL COMMAND

Begin now.

Do not respond with a proposal for how you would build MBIQ.

Do not merely describe an architecture.

Do not stop after creating agents.

Do not stop after generating files.

Do not stop after compilation.

Use the available OpenCode environment, Jev development routing, development models, tools, terminal, repository, local services, Solana development environment and testing infrastructure to actually build the system.

Start by:

```text
1. INSPECTING THE EXISTING REPOSITORY AND ENVIRONMENT
2. DISCOVERING AVAILABLE DEVELOPMENT MODELS / TOOLS
3. CONFIGURING THE MINIMAL EFFECTIVE AGENT ORGANIZATION
4. DEFINING THE SHARED PROTOCOL CONTRACTS
5. PRODUCING A SHORT EXECUTION PLAN
6. IMMEDIATELY BEGINNING IMPLEMENTATION
```

After that, autonomously continue:

```text
IMPLEMENT
→ INTEGRATE
→ RUN
→ TEST
→ DEBUG
→ FIX
→ RETEST
→ SECURITY REVIEW
→ E2E
→ FINAL REVIEW
```

until the Definition of Done is satisfied.

The target is not a convincing prototype screenshot.

The target is a functioning first version of the MBIQ network proving that:

```text
A USER CAN REQUEST AI COMPUTE

AN INDEPENDENT PROVIDER CAN EXECUTE IT

AN OPEN MODEL CAN PRODUCE THE RESULT

LAYA CAN ROUTE THE WORKLOAD

SOLANA CAN SECURE THE PAYMENT FLOW

THE PROVIDER CAN EARN MBIQ

THE PROTOCOL CAN EARN MBIQ

AND THE USER CAN RECEIVE THE RESULT.
```

# END OF MASTER PROMPT