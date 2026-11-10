# MBIQ — чернетки заявок

Статус: **чернетка**. Позначки `{{...}}` — дані, які заповнює засновник.
Дата підготовки: 2026-11-10.

---

## 0. Дані, які потрібні (заповнити перед подачею)

| Поле | Значення |
|---|---|
| Повне імʼя | `{{FULL_NAME}}` |
| Email | `{{EMAIL}}` |
| Місто, країна | `{{CITY_COUNTRY}}` |
| Назва проєкту | MBIQ |
| Сайт проєкту | `{{WEBSITE}}` (можна залишити порожнім, якщо немає) |
| X проєкту | `{{X_PROJECT}}` |
| X засновника | `{{X_FOUNDER}}` |
| GitHub | `https://github.com/devcodex2025/mbiq` |
| LinkedIn | `{{LINKEDIN}}` (необовʼязково) |
| Юрособа | `{{ENTITY}}` (або «none») |
| Команда | `{{TEAM_SIZE}}` |

---

## 1. Solana Builder Program

Форма: Google Forms, `docs.google.com/forms/d/e/1FAIpQLScOeyOQcW2VK271z9EexZXk3xuEkBpKSALLTc4IP4Fd4A-a7g`
Логін не потрібен. Поля нижче — точні назви з форми.

**Your name** *
`{{FULL_NAME}}`

**Email** *
`{{EMAIL}}`

**Where do you live? (city and country)** *
`{{CITY_COUNTRY}}`

**Project name**
`MBIQ`

**Project website**
`{{WEBSITE}}`

**X handle for founder and project** *
`{{X_FOUNDER}} / {{X_PROJECT}}`

**Github** *
`https://github.com/devcodex2025/mbiq`

**Linkedin**
`{{LINKEDIN}}`

**What are you building?** *

> Responding to solana.com/request-for-startups#ai-inference-marketplace.
>
> MBIQ is an open marketplace for AI inference. A developer sends one request; independent providers quote a price; payment settles per request; the job runs on an open model on the provider's own hardware; the provider returns a signed attestation of which model actually served the request; escrow releases, and provider reputation plus protocol fee update on-chain.
>
> The wedge is verification: existing aggregators resell access but cannot prove which model answered. MBIQ treats that as the core product, not an add-on. Solana is what makes per-request settlement viable at all — a payment channel turns thousands of tiny inference charges into one on-chain commitment.
>
> Prior work: the same team shipped MineBench, a desktop application that turns consumer hardware into a mining network — client runtime, pool coordination, wallet payouts, public dashboard. That is the provider-side problem MBIQ needs, already built once.
>
> Current stage: protocol architecture specified end to end; MVP in progress — one provider, one open model, code generation, devnet.

**What sort of support are you looking for?** *
☑ Grant
☑ GTM
☑ Builder tools
☑ Credits
☐ Hiring
☐ Other

**Anything else you want to share?**

> MBIQ was started in September 2026 — before the request was published — as an independent attempt at the same gap. The brief is confirmation, not the starting point.
>
> Immediate need is compute credits: an inference marketplace is the one product that cannot be demoed without paying for GPU time. Grant funding covers the provider side during the first three months. GTM help matters more than usual here — the first external providers are the product, and they live in the Solana ecosystem.
>
> Track record: MineBench ran as a live mining network on consumer hardware. We paused it in October 2026 because reward attribution and payout settlement broke at low scale — and rebuilt the thesis around per-job pricing and pre-funded escrow instead of scaling a system we could not trust. That failure is the reason MBIQ is designed the way it is.

---

## 2. Superteam Earn — мікрогрант

Потребує акаунта (вхід через email/X). Сума запиту: `{{AMOUNT}}` (рекомендовано 3 000–5 000 USD).

**Project title**
`MBIQ — open marketplace for verifiable AI inference`

**One-liner**
`One request interface where independent AI providers compete, get paid per job on Solana, and prove which model actually served the request.`

**Description**

> MBIQ answers the Solana Request for Startups brief *An open marketplace for AI inference*.
>
> **Problem.** A developer who needs a specific open model today has two options: a closed aggregator that hides which model answered, or self-hosting, which is expensive and operationally heavy. Neither gives a verifiable record of model identity.
>
> **What we are building.** A provider-agnostic gateway. Providers register without a central listing, quote a price, execute on their own hardware, and return a signed attestation binding job id, model id, model version, runtime, timestamps and result hash. Payment moves through a Solana payment channel; escrow releases on settlement; the protocol takes a fee and provider reputation updates.
>
> **Why Solana.** Per-request settlement only works if the transaction cost is below the charge. Payment channels make thousands of inference charges collapse into one on-chain commitment — this is the mechanism the brief itself names.
>
> **What exists now.** Full protocol specification: job lifecycle, payment and escrow state machine, verification records, reputation, provider economics. On the provider side, the team has already shipped MineBench — a desktop runtime that benchmarks consumer hardware, orchestrates miners, coordinates a pool and pays wallets, with a public dashboard. Implementation of the MBIQ MVP slice is in progress.
>
> **What the grant covers.** GPU hours for the first external provider, devnet infrastructure, and one month of full-time build to reach a working end-to-end demo.

**Deliverables**

| # | Result | Amount | Timeframe |
|---|---|---|---|
| 1 | Provider daemon + gateway + escrow on devnet, one open model, code generation, public demo video | `{{M1}}` | 3 тижні |
| 2 | Payment channels, signed attestations, reputation v0, 3 external providers | `{{M2}}` | 4 тижні |
| 3 | Public testnet, SDK, documentation, benchmark harness | `{{M3}}` | 6 тижнів |

**Links**
Repo: `https://github.com/devcodex2025/mbiq` · Demo: `{{VIDEO_URL}}`

---

## 3. Solana Foundation Grant

Форма: `share.hsforms.com/1GE1hYdApQGaDiCgaiWMXHA5lohw`
Тип: **стандартний грант** на публічне благо + окремо **convertible** на комерційну частину, якщо сума перевищує public-good бюджет.

**Project overview**

> **Responding to:** solana.com/request-for-startups#ai-inference-marketplace
>
> MBIQ is an open marketplace for AI inference: one request interface, independent providers with no central listing, per-request settlement, and a verifiable record of which model actually served each job.
>
> This work began in September 2026, before the request was published. The convergence is independent: MBIQ and the brief address the same gap — the absence of a way to verify which model actually served a request.
>
> **Public good component.** MBIQ will open source three pieces the ecosystem does not currently have as a shared primitive:
> 1. The verification record format — job id, model id and version, runtime, timestamps, result hash, provider signature, verification status — as a documented, reusable schema.
> 2. The provider daemon — anyone can attach hardware and serve open models.
> 3. The client SDK and a benchmark harness that measures provider performance against the same jobs.
>
> **Commercial component.** The hosted gateway, routing and reputation layer operate as a business and take a protocol fee per settled job. This part would sit under a convertible grant.
>
> **Track record.** The team previously shipped MineBench: a desktop client, miner distribution, pool infrastructure, wallet payouts and a public dashboard, all live. It was paused in October 2026 when reward attribution and settlement stopped working at low scale. MBIQ is the redesign that follows from that failure — price per job, escrow before execution, evidence with every result.

**How this is a public good**

> Today every Solana team building AI agents has to independently answer the same question: can I trust that this response came from the model I paid for? Each team solves it privately, or not at all. MBIQ makes the answer shared: an open schema, an open provider implementation, and an open verification path that any program, agent or marketplace on Solana can consume. The Foundation does not need to endorse model execution verification — MBIQ specifies its own verification system and documents exactly what it does and does not prove.

**Why Solana (only-possible-on-Solana argument)**

> Inference is billed in fractions of a cent per request. On a chain where a settlement transaction costs more than the service, this model does not exist. Solana payment channels collapse thousands of per-request charges into a single on-chain commitment, which is the only configuration where a competitive per-request marketplace is economically rational. The brief names this mechanism explicitly; MBIQ is a direct implementation of it.

**Honest limits of verification**

> Deterministic checks (result hash, replay, model identity attestation) are verified deterministically. Subjective output quality is not a cryptographic claim and will not be presented as one. Replicated execution, sampling and challenge mechanisms are defined as extension points, not as shipped features.

**Milestones**

| # | Deliverable | Amount | Weeks |
|---|---|---|---|
| M1 | Provider daemon + gateway + escrow on devnet, 1 open model, demo video, public repo | `{{M1}}` | 3 |
| M2 | Payment channels, signed attestations, reputation v0, 3 independent external providers | `{{M2}}` | 4 |
| M3 | Public testnet, open SDK, documentation, benchmark harness, verification schema published as a standalone spec | `{{M3}}` | 6 |

**Risks**

> 1. **Provider liquidity** — an empty marketplace is worthless. Mitigation: first three providers recruited from the Solana ecosystem before testnet launch, with grant-funded GPU hours.
> 2. **Verification cost** — independent verification can cost as much as the job. Mitigation: sampled verification with escrow-aware incentives, not full replication.
> 3. **Model supply chain** — open weights must be fetched and pinned. Mitigation: signed model manifests and cached weights per provider.

**Open source commitment**

> Protocol specification, verification schema, provider daemon and client SDK will be MIT licensed. Hosted routing, reputation scoring and the commercial gateway remain proprietary.

---

## 4. Colosseum Eternal

Реєстрація: `colosseum.org/eternal`. 4-тижневий спринт, щотижневі апдейти обовʼязкові.

**Inspiration field**

> MBIQ predates the brief. We arrived at a verified inference marketplace independently and treat the request as external validation of the problem. The verification gap is the part most teams skip, and it is the only part that makes an inference marketplace different from a reseller.

**What we will ship in 4 weeks**

> End-to-end slice: request, quote, payment channel, job, provider execution on an open model, signed attestation, escrow settlement, protocol fee. One provider, code generation workload, devnet. Public repo and demo video from week 2.

---

## 5. Чек-лист перед натисканням submit

- [ ] Публічний GitHub-репо з README, у якому перший рядок — посилання на бриф
- [ ] `docs/rfs-response.md` — one-pager у структурі з `request-for-startups.md`
- [ ] 90-секундне відео наскрізного циклу (або хоча б каркас, якщо подаємось раніше)
- [ ] Акаунт в X з 3+ постами про проєкт
- [ ] Заповнені всі `{{...}}`
- [ ] Перевірено: жодного слова «token», «backed by Solana», «official»
- [ ] Дата першого коміту в git — сьогодні або раніше
