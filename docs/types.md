\# 🧾 Manthan Core — Types \& Interfaces



This document defines all core types used in Manthan Core (v0.6).



These types ensure:



\- consistency

\- determinism

\- contract integrity



\---



\## 🔒 Core Principle



```text

Types define the boundaries of truth

📦 Location

core/types/decision.ts

🧩 1. DecisionContract

export type DecisionContract = {

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

✅ 2. DecisionResult

export type DecisionResult = {

&#x20; action: "ALLOW" | "DENY" | "SKIP"

&#x20; reason: string

&#x20; contract\_id: string

}

⚙️ 3. DecisionEntry (Stored Record)

export type DecisionEntry = {

&#x20; id: string

&#x20; contract: DecisionContract

&#x20; result: DecisionResult

&#x20; config: Record<string, any>

&#x20; created\_at?: string

}

🔁 4. ReplayResult (Optional)

export type ReplayResult = {

&#x20; index: number

&#x20; status: "OK" | "VIOLATION"

}

🧠 5. Config Type

export type RepoConfig = {

&#x20; min\_description\_length: number

&#x20; block\_wip: boolean

&#x20; require\_title: boolean

}

🧩 Relationships

DecisionContract + RepoConfig

&#x20;           ↓

&#x20;       evaluate()

&#x20;           ↓

&#x20;     DecisionResult

&#x20;           ↓

&#x20;     DecisionEntry (stored)

🔐 Type Constraints

all types must be serializable

no functions inside types

no dynamic structures affecting determinism

⚠️ Strict Rules

contract must include metadata.repo

result.contract\_id must match contract.id

config must be stored with entry

🚫 Forbidden

optional contract fields that affect logic

dynamic typing in evaluation

mutation of typed objects

🧠 Design Principle

Types enforce structure → structure ensures determinism

🧭 Version



Manthan Core v0.6 — Types Locked



🏁 Summary



Types ensure:



consistency across system

safe evaluation

reliable replay

🔐 Identity



Every decision is traceable, auditable, and built for trust.

