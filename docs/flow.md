\# 🔄 Manthan Core — Execution Flow



This document defines how a decision flows through Manthan Core (v0.6).



\---



\## 🧠 Overview



Core execution transforms:



```text

Contract + Config → Decision

🔒 Core Principle

Execution must be deterministic and repeatable

📦 Main Entry Point

runDecision(contract, repo)

🔁 Step-by-Step Flow

1\. Idempotency Check

hasDecision(contract.id)

Behavior

if exists → return stored result

skip evaluation

⚙️ 2. Load Config

getRepoConfig(repo)

Output

deterministic config object

🧠 3. Evaluate Decision

evaluate(contract, config)

Rules

pure function

no side effects

💾 4. Store Decision

appendDecision({

&#x20; contract,

&#x20; result,

&#x20; config

})

Stored Data

contract

result

config

🔁 5. Return Result

return decision

🔄 Full Flow Diagram

runDecision

&#x20;   ↓

hasDecision?

&#x20; /   \\

yes    no

&#x20;↓      ↓

return  getConfig

&#x20;        ↓

&#x20;      evaluate

&#x20;        ↓

&#x20;      store

&#x20;        ↓

&#x20;      return

🔁 Replay Flow

Load stored decisions

&#x20;       ↓

For each:

&#x20; evaluate(contract, config)

&#x20;       ↓

Compare with stored result

&#x20;       ↓

Match → OK

Mismatch → Violation

⚠️ Failure Points

Step	Failure

Idempotency	DB error

Config	missing config

Evaluate	logic bug

Store	DB failure

Replay	mismatch

🔐 Guarantees

no duplicate processing

same input → same output

stored decision = source of truth

🧭 Constraints

no hidden dependencies

no mutation of inputs

no fallback in replay

🧠 Design Principle

Explicit flow → predictable outcomes

🧭 Version



Manthan Core v0.6 — Flow Locked



🏁 Summary



Execution flow ensures:



clarity

determinism

replayability

🔐 Identity



Every decision is traceable, auditable, and built for trust.

