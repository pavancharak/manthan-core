\# ⚙️ Manthan Core — Config System



This document defines how configuration is handled in Manthan Core (v0.6).



\---



\## 🧠 Overview



Config provides the \*\*rules used during evaluation\*\*.



It is a required input:



```text

Decision = f(contract, config)

🔒 Core Principle

Config must be explicit, deterministic, and stored with the decision

📦 Location

core/config/getConfig.ts

⚙️ Function

export async function getRepoConfig(repo: string)

📊 Output

{

&#x20; min\_description\_length: number,

&#x20; block\_wip: boolean,

&#x20; require\_title: boolean

}

🔁 Flow

Repo

&#x20; ↓

Fetch config (DB)

&#x20; ↓

Return config

&#x20; ↓

Pass into evaluate()

💾 Source

Supabase → repo\_configs table

🧩 Example

{

&#x20; "min\_description\_length": 10,

&#x20; "block\_wip": true,

&#x20; "require\_title": true

}

⚠️ Default Fallback

return data?.rules || {

&#x20; min\_description\_length: 10,

&#x20; block\_wip: true,

&#x20; require\_title: true

}

Constraint

Fallback must be deterministic

🔁 Replay Requirement

config must be stored with decision

replay must NOT fetch config again

🚫 Forbidden

dynamic config during evaluation

fetching config inside evaluate()

modifying config mid-execution

🔐 Determinism Rule

Same contract + same config = same decision

🧠 Failure Cases

Issue	Effect

missing config in DB	fallback used

config not stored	replay failure

config changed after decision	replay mismatch

🔒 Storage Requirement

appendDecision({

&#x20; contract,

&#x20; result,

&#x20; config

})

🧭 Design Principle

Config defines HOW decisions are made

🧭 Version



Manthan Core v0.6 — Config Locked



🏁 Summary



Config ensures:



flexible rules

deterministic execution

replay integrity

🔐 Identity



Every decision is traceable, auditable, and built for trust.

