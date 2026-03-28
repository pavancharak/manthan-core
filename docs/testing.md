\# 🧪 Manthan Core — Testing Strategy



This document defines how Manthan Core (v0.6) is tested.



Testing ensures:



\- determinism

\- correctness

\- replay integrity



\---



\## 🧠 Testing Philosophy



```text

Test that decisions are correct AND reproducible

🔒 Core Principle

Same input → same output (always)

📦 Testing Layers

Evaluation Tests

Idempotency Tests

Replay Tests

Store Tests

⚙️ 1. Evaluation Tests

Goal



Verify decision logic



Test Case

const result = evaluate(contract, config)



expect(result.action).toBe("ALLOW")

Scenarios

valid input → ALLOW

missing title → DENY

short description → DENY

🔁 2. Idempotency Tests

Goal



Ensure duplicate contracts are not reprocessed



Test

const first = await runDecision(contract, repo)

const second = await runDecision(contract, repo)



expect(second.action).toBe("SKIP")

🔁 3. Replay Tests

Goal



Ensure recomputed decisions match stored results



Test

await replayAndVerify()

// expect no mismatch

Expected Output

All decisions verified. System is consistent.

💾 4. Store Tests

Goal



Ensure data is stored correctly



Test

contract stored

result stored

config stored

Constraint

Stored entry must be sufficient for replay

⚠️ Failure Tests

Missing Config

expect replay failure

Modified Logic

expect determinism violation

🧠 Determinism Test

const r1 = evaluate(contract, config)

const r2 = evaluate(contract, config)



expect(r1).toEqual(r2)

🚫 Forbidden Testing

mocking evaluation randomness

bypassing config

altering contract mid-test

🔐 Test Constraints

tests must use real inputs

no hidden dependencies

no external state

🧭 Test Execution

npx ts-node core/test.ts

🧠 Design Principle

If it cannot be replayed, it cannot be trusted

🧭 Version



Manthan Core v0.6 — Testing Locked



🏁 Summary



Testing ensures:



correctness

determinism

replay safety

🔐 Identity



Every decision is traceable, auditable, and built for trust.

