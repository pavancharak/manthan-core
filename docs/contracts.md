\# 📜 Manthan Core — Decision Contracts



This document defines the Decision Contract used in Manthan Core (v0.6).



The contract is the \*\*only input\*\* to the decision engine.



\---



\## 🧠 Core Principle



```text

Decision = f(contract, config)

📦 Contract Schema

type DecisionContract = {

&#x20; id: string

&#x20; intent: string

&#x20; inputs: Record<string, any>

&#x20; outputs: Record<string, any>

&#x20; behavior: string

&#x20; determinism: "strict"

&#x20; boundaries: any\[]

&#x20; metadata: {

&#x20;   created\_at: string

&#x20;   version: string

&#x20;   repo: string

&#x20; }

}

🧩 Field Definitions

id

unique identifier

used for idempotency

intent

describes decision purpose

inputs

raw data used in evaluation

outputs

reserved (future use)

behavior

execution mode (currently "noop")

determinism

must always be "strict"

boundaries

reserved for constraints

metadata

{

&#x20; "created\_at": "...",

&#x20; "version": "v1",

&#x20; "repo": "owner/repo"

}

🔁 Contract Lifecycle

created (adapter)

passed to core

evaluated

stored

replayed

🔐 Contract Properties

immutable

serializable

complete input definition

⚠️ Determinism Risk

Example

created\_at uses runtime timestamp

Constraint

Stored contract must be reused exactly during replay

🚫 Forbidden

modifying contract after creation

missing required fields

dynamic mutation during execution

🔁 Replay Dependency



Replay uses:



stored contract

stored config



No regeneration allowed.



🧠 Design Principle

Contract defines WHAT decision is being made

🧭 Versioning

metadata.version = "v1"

🧪 Validation Rules

required fields present

valid structure

deterministic metadata

🏁 Summary



Contract is:



the foundation of decision-making

the unit of determinism

the source of replay

🔐 Identity



Every decision is traceable, auditable, and built for trust.

