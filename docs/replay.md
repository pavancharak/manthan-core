\# 🔁 Manthan Core — Replay Engine



This document defines the replay mechanism in Manthan Core (v0.6).



\---



\## 🧠 Overview



Replay verifies that past decisions remain consistent.



It ensures:



```text

Same contract + same config → same decision

🔒 Core Principle

Replay must recompute exactly — no fallbacks, no external dependencies

📦 Location

core/replay.ts

⚙️ Function

export async function replayAndVerify()

🔁 Replay Flow

Load decisions from DB

&#x20;       ↓

For each entry:

&#x20; use stored contract

&#x20; use stored config

&#x20;       ↓

Recompute using evaluate()

&#x20;       ↓

Compare with stored result

&#x20;       ↓

Match → OK

Mismatch → Determinism violation

📊 Example

Stored Entry

{

&#x20; "contract": { ... },

&#x20; "config": { ... },

&#x20; "result": {

&#x20;   "action": "ALLOW",

&#x20;   "reason": "All checks passed"

&#x20; }

}

Replay Step

const recomputed = evaluate(contract, config)

Comparison

JSON.stringify(recomputed) === JSON.stringify(entry.result)

⚠️ Determinism Violation

Trigger

mismatch between recomputed and stored result

Behavior

Determinism violated at entry X

🚫 Forbidden Behavior

fetching config during replay

regenerating contract

using fallback values

modifying stored data

🔐 Requirements

stored entry must include config

stored entry must include contract

replay must use stored values only

🧠 Failure Cases

Cause	Effect

missing config	mismatch

changed evaluation logic	mismatch

mutated contract	mismatch

🔁 Replay Guarantees

detects drift

ensures integrity

validates system correctness

⚙️ Logging

All decisions verified. System is consistent.

🧠 Design Principle

Trust is proven by recomputation

🧭 Version



Manthan Core v0.6 — Replay Locked



🏁 Summary



Replay ensures:



determinism

auditability

long-term consistency

🔐 Identity



Every decision is traceable, auditable, and built for trust.

