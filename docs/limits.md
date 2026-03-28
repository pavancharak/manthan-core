\# ⚠️ Manthan Core — Limits \& Boundaries



This document defines the operational limits of Manthan Core (v0.6).



These limits are essential to preserve:



\- determinism

\- replay integrity

\- system trust



\---



\## 🧠 Purpose



Understanding limits ensures:



\- safe development

\- predictable behavior

\- strict boundary enforcement



\---



\## 🔒 Core Constraint



```text

Core is computation only — nothing else

📦 System Limits

1\. No External Dependencies in Evaluation

no APIs

no DB calls

no network

⚙️ 2. No Async in Evaluation

evaluate() must be synchronous

⏱️ 3. No Time Dependency

no Date.now()

no timestamps affecting logic

🎲 4. No Randomness

no Math.random()

no probabilistic behavior

💾 5. No Partial Decisions

contract + config + result must always be stored together

🔁 6. Replay Dependency Limit

replay depends ONLY on stored data

no external fetch during replay

⚙️ 7. Config Limit

config must be passed explicitly

no implicit config access

🔐 8. Immutability Limit

contract must not change

config must not change

result must not be modified after computation

🔁 9. Idempotency Limit

same contract ID → processed once

duplicates must return stored result

📊 10. Performance Limits

evaluation must be fast (pure computation)

no heavy processing

no long loops

🌐 11. Environment Limit

evaluate() must not access process.env

🧠 12. Type Safety Limit

all inputs must conform to defined types

no dynamic structure affecting logic

🚫 Unsupported Features

real-time decision updates

streaming evaluation

partial evaluation

incremental recomputation

🔒 Hard Limits



These must NEVER be violated:



purity of evaluate()

replay using stored data only

no mutation of stored decisions

no hidden dependencies

🧭 Design Principle

Strict limits → guaranteed determinism

🧭 Version



Manthan Core v0.6 — Limits Locked



🏁 Summary



Limits ensure:



pure computation

predictable outcomes

reliable replay

🔐 Identity



Every decision is traceable, auditable, and built for trust.

