\# ⚙️ Manthan Core — Evaluation Engine



This document defines the evaluation engine in Manthan Core (v0.6).



\---



\## 🧠 Overview



The evaluation engine is the \*\*heart of the system\*\*.



It computes:



```text

Decision = f(contract, config)

🔒 Core Principle

Evaluation must be pure

📦 Location

core/engine/evaluate.ts

⚙️ Function Signature

export function evaluate(

&#x20; contract: DecisionContract,

&#x20; config: any

): DecisionResult

📊 Output

type DecisionResult = {

&#x20; action: "ALLOW" | "DENY"

&#x20; reason: string

&#x20; contract\_id: string

}

🔁 Execution Rules

synchronous

deterministic

side-effect free

🧠 Example Logic

if (config.require\_title \&\& !contract.inputs.title) {

&#x20; return {

&#x20;   action: "DENY",

&#x20;   reason: "Title is required",

&#x20;   contract\_id: contract.id

&#x20; }

}



if (config.block\_wip \&\& contract.inputs.title?.includes("WIP")) {

&#x20; return {

&#x20;   action: "DENY",

&#x20;   reason: "WIP PRs are not allowed",

&#x20;   contract\_id: contract.id

&#x20; }

}



if (

&#x20; contract.inputs.body?.length < config.min\_description\_length

) {

&#x20; return {

&#x20;   action: "DENY",

&#x20;   reason: "Description must be at least X characters",

&#x20;   contract\_id: contract.id

&#x20; }

}



return {

&#x20; action: "ALLOW",

&#x20; reason: "All checks passed",

&#x20; contract\_id: contract.id

}

🔐 Constraints

MUST NOT:

perform IO

use async operations

access environment variables

use Date / time

use randomness

MUST:

rely only on contract + config

produce same output for same input

⚠️ Determinism Violations

❌ Example

if (Date.now() > threshold)

❌ Example

Math.random()

🔁 Replay Dependency



Replay calls:



evaluate(contract, config)



Result must match stored result.



🧠 Design Principle

Pure logic → predictable decisions

🔒 Evaluation Boundary

Allowed	Forbidden

condition checks	API calls

config usage	DB access

contract usage	time/random

🧭 Version



Manthan Core v0.6 — Evaluation Locked



🏁 Summary



Evaluation engine ensures:



deterministic decisions

reproducibility

trust

🔐 Identity



Every decision is traceable, auditable, and built for trust.

