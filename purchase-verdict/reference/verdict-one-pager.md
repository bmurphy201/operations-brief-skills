# Purchase verdict, one page

One page. Every number names the record it came from. Names are role labels; real names stay in
the manifest.

---

## 1. Case

| Field | Value |
|---|---|
| Case ID | |
| Date | |
| Process owner (role) | |
| Proposed purchase, and who requested it | |
| Expected state | |
| Actual state | |
| Time window | |

## 2. Observed failure

| | Statement | Record that shows it |
|---|---|---|
| Expected | | |
| Actual | | |

## 3. Existence or visibility

Result: `exists` / `not found in the system of record` / `visible only under a filter or
permission`

What hid it, if visibility: ____________________

## 4. Records this verdict rests on

Three to six. Each one has a source system, an identifier, and a timestamp.

| # | Record | Source system | Identifier | Timestamp | What it establishes |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

## 5. Comparison window

| Scope | Days | N examined | M showing the divergence |
|---|---|---|---|
| | | | |

Reading: `M = 1 of N, data condition` / `M = N, systematic, configuration or mapping` /
`1 < M < N, process or handoff condition` / `window too small to distinguish`

If 1 < M < N, what separates the affected rows from the clean rows: ____________________

## 6. Four branches

Every row carries a status. No blanks. `untested` is a finding and is written as `untested`.

| Branch | Status | Evidence, by record number from section 4 |
|---|---|---|
| Handoff or process | supported / contradicted / untested | |
| Wrong or missing data | supported / contradicted / untested | |
| Feature of the system we own, needing configuration | supported / contradicted / untested | |
| Genuinely missing capability | supported / contradicted / untested | |

## 7. Verdict, or competing branches

Use **7a** only when exactly one branch is supported **and** no remaining branch is untested on a
test that could change the result. Otherwise use **7b**. Delete the one you do not use.

### 7a. Verdict

The evidence supports: ____________________

Branches ruled out, and by which record: ____________________

### 7b. Competing branches, not settled

| Competing branch | Why it is still live |
|---|---|
| | |
| | |

**One discriminating test.** The cheapest test that separates them. One, not a list.

| Field | Value |
|---|---|
| The test | |
| What each outcome would mean | |
| Owner (role) | |
| Date due | |

## 8. Next action

| Field | Value |
|---|---|
| Action | |
| Owner (role) | |
| Date | |
| If the action is a test-environment replay: configuration and master-data parity with production as of the failure confirmed by | |

## 9. How we will know it worked

| Field | Value |
|---|---|
| The observable change | |
| Environment it will be observed in | |
| Who checks, and when | |

## 10. Backlog of already-affected records

Separate from the fix. Correcting a setting or a mapping fixes the forward flow and repairs nothing
that already failed.

| Field | Value |
|---|---|
| Records already affected (count) | |
| How that count was derived (record or extract) | |
| Remediation owner (role) | |
| Remediation date | |

## 11. Capability claim

| Field | Value |
|---|---|
| The claim | |
| Source document and date | |
| Installed version | |
| Licensed edition | |
| Status | PROVEN / `UNVERIFIED - owed by <role>, needed before sign-off` |

## 12. Indicators

| | Indicator | Baseline | Source | Review date |
|---|---|---|---|---|
| Leading | | | | |
| Lagging | | | | |

Either row with no baseline reads `UNVERIFIED - owed by <role>, needed before sign-off`. Never
omitted, never inferred.

## 13. Sign-off

No change, correction, or purchase proceeds until all three sign. This document is a
recommendation until then.

| Role | Name | Signature | Date |
|---|---|---|---|
| Process owner | | | |
| System owner or administrator | | | |
| Budget approver | | | |

## 14. Open evidence gaps

| Missing artifact | System of record | Owner | Retrieval deadline | Branch it would change |
|---|---|---|---|---|
| | | | | |
