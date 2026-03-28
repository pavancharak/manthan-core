\# ❌ Manthan Core — Anti-Patterns



This document defines what MUST NEVER be done in Manthan Core (v0.6).



Violating these patterns breaks:



\- determinism

\- replay integrity

\- system trust



\---



\## 🔒 Core Rule



```text

If evaluation is not pure, the system is broken

🚫 1. Using Time in Evaluation

❌ Anti-Pattern

if (Date.now() > deadline)

Why it's wrong

output changes over time

replay will fail

🚫 2. Using Randomness

❌ Anti-Pattern

if (Math.random() > 0.5)

Why it's wrong

non-deterministic output

cannot reproduce decision

🚫 3. Performing IO in evaluate()

❌ Anti-Pattern

await fetch("...")

Why it's wrong

introduces external dependency

breaks purity

🚫 4. Fetching Config Inside Evaluation

❌ Anti-Pattern

const config = await getRepoConfig(repo)

Why it's wrong

hidden dependency

replay inconsistency

🚫 5. Mutating Contract

❌ Anti-Pattern

contract.inputs.title = "changed"

Why it's wrong

alters input mid-execution

breaks replay

🚫 6. Modifying Config During Evaluation

❌ Anti-Pattern

config.min\_description\_length = 5

Why it's wrong

changes logic dynamically

breaks determinism

🚫 7. Partial Storage of Decisions

❌ Anti-Pattern

store({ contract, result }) // missing config

Why it's wrong

replay cannot reconstruct decision

🚫 8. Recomputing Config During Replay

❌ Anti-Pattern

const config = await getRepoConfig(repo)

Why it's wrong

config may have changed

replay mismatch

🚫 9. Ignoring Idempotency

❌ Anti-Pattern

runDecision(contract) // without checking hasDecision

Why it's wrong

duplicate decisions

inconsistent logs

🚫 10. Silent Error Handling

❌ Anti-Pattern

catch (e) {}

Why it's wrong

hides failures

breaks auditability

🚫 11. Hidden Dependencies

❌ Anti-Pattern

reading environment variables in evaluate

using global state

Why it's wrong

implicit inputs

non-reproducible behavior

🚫 12. Changing Evaluation Logic Without Versioning

❌ Anti-Pattern

modifying rules without tracking version

Why it's wrong

replay mismatch for historical decisions

🧠 Summary Rule

Every input must be explicit, every output must be reproducible

🔒 Enforcement



Violations result in:



determinism failure

replay inconsistency

system distrust

🧭 Version



Manthan Core v0.6 — Anti-Patterns Locked



🏁 Summary



Avoiding anti-patterns ensures:



pure evaluation

consistent replay

reliable system behavior

🔐 Identity



Every decision is traceable, auditable, and built for trust.

