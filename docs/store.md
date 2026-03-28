\# 💾 Manthan Core — Decision Store



This document defines the persistence layer in Manthan Core (v0.6).



\---



\## 🧠 Overview



The store layer is responsible for:



\- saving decisions

\- retrieving decisions

\- enforcing idempotency



\---



\## 🔒 Core Principle



```text

Store data exactly as produced — no transformation

📦 Location

core/store/decision.store.ts

🧩 Responsibilities

1\. Idempotency Check

hasDecision(contractId: string): Promise<boolean>

Behavior

checks if decision already exists

prevents duplicate processing

💾 2. Append Decision

appendDecision(entry)

Stored Fields

{

&#x20; id: string,

&#x20; contract: object,

&#x20; result: object,

&#x20; config: object

}

Constraint

Everything needed for replay must be stored

📖 3. Read Log

getLog(): Promise<any\[]>

Purpose

used for replay

used for inspection

🧠 Storage Backend

Supabase (Postgres)

📊 Table Schema

decisions (

&#x20; id TEXT PRIMARY KEY,

&#x20; contract JSONB,

&#x20; result JSONB,

&#x20; config JSONB,

&#x20; created\_at TIMESTAMP DEFAULT NOW()

)

⚠️ Constraints

no mutation after insert

append-only behavior

no partial writes

🚫 Forbidden

updating existing decisions

deleting decision records

storing incomplete entries

🔁 Idempotency Flow

hasDecision(id)

&#x20;  ↓

exists → skip

not exists → evaluate + store

🧠 Error Handling

DB errors must throw

no silent failures

🔐 Guarantees

each contract processed once

decision log is consistent

replay has full data

🧭 Design Principle

Store once, trust forever

🧭 Version



Manthan Core v0.6 — Store Locked



🏁 Summary



Store ensures:



persistence

idempotency

replay integrity

🔐 Identity



Every decision is traceable, auditable, and built for trust.

