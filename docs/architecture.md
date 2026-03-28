\# 🧩 Manthan Core — Architecture



This document defines the architecture of Manthan Core (v0.6).



\---



\## 🧠 Overview



Manthan Core is a \*\*pure computation layer\*\*.



It takes:



\- contract

\- config



And produces:



\- decision



\---



\## 🔒 Core Principle



```text

Core must remain pure and deterministic

📦 High-Level Structure

Contract + Config

&#x20;       ↓

Evaluate (Pure Function)

&#x20;       ↓

Decision Result

🧩 Components

1\. Orchestrator



File:



core/index.ts

Responsibility

idempotency check

config loading (outside evaluation)

decision execution

persistence trigger

⚙️ 2. Evaluation Engine



File:



core/engine/evaluate.ts

Responsibility

apply rules

compute decision

remain pure

Constraints

no IO

no async

no randomness

no time dependency

🔁 3. Replay Engine



File:



core/replay.ts

Responsibility

recompute decisions

verify consistency

💾 4. Store Layer



File:



core/store/decision.store.ts

Responsibility

persist decisions

read decision log

handle idempotency

⚙️ 5. Config Layer



File:



core/config/getConfig.ts

Responsibility

fetch config before evaluation

provide deterministic input

🧠 Data Flow

Contract

&#x20;  ↓

Load Config

&#x20;  ↓

Evaluate

&#x20;  ↓

Decision

&#x20;  ↓

Store (contract + config + result)

🔐 Boundary Definition

Layer	Allowed	Forbidden

Core	computation	IO

Store	DB access	logic

Config	fetch	mutation

Replay	verify	fallback

🔁 Execution Flow

runDecision()

&#x20;   ↓

hasDecision()

&#x20;   ↓

getRepoConfig()

&#x20;   ↓

evaluate()

&#x20;   ↓

appendDecision()

⚠️ Critical Constraints

evaluation must remain pure

config must be passed explicitly

replay must not fetch external data

🧭 Version



Manthan Core v0.6 — Architecture Locked



🏁 Summary



Core architecture ensures:



strict separation of concerns

deterministic execution

replay safety

🔐 Identity



Every decision is traceable, auditable, and built for trust.

