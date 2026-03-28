\# 🧠 Manthan Core — Overview



Manthan Core is the \*\*deterministic decision engine\*\* of the Manthan system.



It is the most critical and \*\*non-negotiable layer\*\*.



\---



\## 🔒 Core Identity



```text

Core is pure, deterministic, and immutable

🧠 What Core Does



Manthan Core:



evaluates decisions

ensures determinism

guarantees replay consistency

🚫 What Core Does NOT Do

no IO

no database access

no API calls

no randomness

no time-based logic

📦 Core Function

Decision = f(contract, config)

🧩 Core Responsibilities

evaluate contract using config

return deterministic decision

produce consistent output

🔁 Core Position in System

Adapter → Platform → Core → Decision

🔐 Core Guarantees

same input → same output

no side effects

replay-safe

⚙️ Key Files

core/

├── index.ts

├── engine/evaluate.ts

├── replay.ts

├── store/decision.store.ts

├── config/getConfig.ts

├── types/decision.ts

🧠 Design Philosophy

Make decisions pure, reproducible, and verifiable

🧭 Version



Manthan Core v0.6 — Locked



🏁 Summary



Core is:



the brain of the system

the source of truth for logic

the foundation of trust

🔐 Identity



Every decision is traceable, auditable, and built for trust.

