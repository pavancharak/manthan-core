\# 🛠️ Manthan Core — Troubleshooting Guide



This document helps diagnose and fix issues in Manthan Core (v0.6).



\---



\## 🧠 Purpose



Resolve issues related to:



\- evaluation errors

\- determinism violations

\- replay failures

\- database issues



\---



\## 🔍 1. TypeScript Import Errors



\### ❌ Problem



```text id="ts\_import\_error"

Module has no default export

Cause



Mismatch between:



default export

named export

Fix

import { supabase } from "../../services/supabase"

🔍 2. Supabase Key Error

❌ Problem

supabaseKey is required

Cause

missing environment variable

Fix

SUPABASE\_URL=...

SUPABASE\_SERVICE\_ROLE\_KEY=...

🔍 3. Determinism Violation

❌ Problem

Determinism violated at entry X

Causes

config not stored

config changed

evaluation logic changed

fallback used during replay

Fix

ensure config stored in DB

ensure replay uses stored config

avoid fallback in replay

🔍 4. Missing Config Column

❌ Problem

Could not find 'config' column

Cause

DB schema missing config field

Fix

ALTER TABLE decisions ADD COLUMN config JSONB;

🔍 5. Replay Using Fallback

❌ Problem

Missing config at entry X

Cause

old entries without config

Fix

update DB to include config

avoid fallback in replay logic

🔍 6. Inconsistent Results (ALLOW vs SKIP)

❌ Problem



Different results for same contract



Cause

idempotency logic incorrect

returning wrong structure

Fix

if (existing) return existing.result

🔍 7. Unhandled Promise Rejection

❌ Problem

ERR\_UNHANDLED\_REJECTION

Cause

missing try/catch in async code

Fix

try {

&#x20; await runDecision(...)

} catch (err) {

&#x20; console.error(err)

}

🔍 8. Supabase Insert Error

❌ Problem



Insert fails



Causes

missing column

schema mismatch

Fix

verify table schema

ensure fields match insert payload

🔍 9. Replay Always Failing

❌ Problem



Replay fails for all entries



Causes

evaluation logic changed

stored config missing

Fix

ensure backward compatibility

use stored config only

🔍 10. Webhook Error (GitHub Adapter)

❌ Problem

Cannot read properties of undefined (reading 'login')

Cause

missing payload fields

Fix



Ensure payload includes:



"user": { "login": "username" }

🧠 Debug Workflow

Identify error

Check logs

Verify inputs (contract + config)

Inspect DB

Re-run replay

🔒 Constraints

do not modify stored decisions

do not bypass evaluation

do not inject fallback in replay

🧭 Version



Manthan Core v0.6 — Troubleshooting Locked



🏁 Summary



This guide ensures:



fast debugging

stable execution

consistent replay

🔐 Identity



Every decision is traceable, auditable, and built for trust.

