\# ⚠️ Manthan Core — Constraints



This document defines the \*\*non-negotiable constraints\*\* of Manthan Core (v0.6).



These constraints preserve:



\- determinism

\- replay integrity

\- system trust



\---



\## 🔒 Core Rule



```text

Core must be pure, deterministic, and side-effect free

📦 Constraint Categories

Evaluation Constraints

Data Constraints

Replay Constraints

Config Constraints

Store Constraints

⚙️ 1. Evaluation Constraints

MUST:

be pure function

depend only on contract + config

be synchronous

MUST NOT:

perform IO

use async

use Date / time

use randomness

access environment variables

❌ Forbidden

Date.now()

Math.random()

fetch()

process.env

💾 2. Data Constraints

contract must be immutable

config must be explicit input

result must be derived only from inputs

❌ Forbidden

modifying contract during evaluation

injecting hidden fields

🔁 3. Replay Constraints

replay must use stored contract + config

replay must not fetch external data

replay must not use fallback logic

❌ Forbidden

getRepoConfig(repo) // during replay

⚙️ 4. Config Constraints

config must be loaded before evaluation

config must be stored with decision

config must not change mid-execution

💾 5. Store Constraints

append-only behavior

no updates

no deletes

no partial entries

🔁 6. Idempotency Constraints

same contract.id → processed once

duplicates must return stored result

🧠 7. Determinism Constraints

Same input → same output (always)

🚫 Anti-Violations

❌ Hidden dependency

reading external state during evaluation

❌ Time dependency

using timestamps in logic

❌ Non-deterministic logic

random branching

🔐 Enforcement



Violations cause:



replay mismatch

system inconsistency

loss of trust

🧭 Design Principle

Strict constraints → guaranteed trust

🧭 Version



Manthan Core v0.6 — Constraints Locked



🏁 Summary



Constraints ensure:



purity

predictability

auditability

🔐 Identity



Every decision is traceable, auditable, and built for trust.

