# Worked example: entirely invented

> **Everything below is invented.** The company, the people, the part numbers, the record
> identifiers, the systems, the version numbers, the editions, and the documentation references do
> not exist. No customer, vendor, or product is described here. Product names are written as
> `ERP-A` and `WMS-B` on purpose, so that nothing in this example can be read as a claim about any
> real software's behavior.
>
> It is here to show the shape of a correct output, including the two outputs people skip: a case
> the evidence does not settle, and a case where the evidence is already gone.

The case is deliberately one that **does not** end in a clean verdict. That is the common outcome
in a real purchase question, and a worked example that always resolves teaches the wrong habit.

---

# Case A. The evidence does not settle it

## 1. Case

| Field | Value |
|---|---|
| Case ID | PV-0001 (invented) |
| Date | Day 0 of this example |
| Process owner (role) | Receiving supervisor |
| Proposed purchase, and who requested it | A warehouse module upgrade, requested by the operations manager, on the stated basis that "WMS-B cannot handle our part numbers" |
| Expected state | A scanned receipt in WMS-B posts against the matching purchase order line in ERP-A |
| Actual state | The receipt is rejected at the interface and never posts in ERP-A |
| Time window | Day minus 2 to Day 0 |

## 2. Observed failure

| | Statement | Record that shows it |
|---|---|---|
| Expected | Receipt `R-882` posts against PO line `PO-417-1` for item `A-104` | PO line export, record 1 |
| Actual | `R-882` sits rejected at the interface with an unmatched item identifier | Interface rejection log line, record 3 |

## 3. Existence or visibility

Result: `not found in the system of record`

The receiving supervisor reported the receipt as "missing from ERP-A." A systems administrator
searched ERP-A by receipt identifier with all filters, date ranges, warehouse defaults, company
selector, and posting-status filters cleared, and the record is not present under any of them. So
this is not a visibility condition. It was worth four minutes of checking, because a saved
warehouse filter would have closed the case here and the purchase question would have ended.

What hid it, if visibility: not applicable.

## 4. Records this verdict rests on

| # | Record | Source system | Identifier | Timestamp | What it establishes |
|---|---|---|---|---|---|
| 1 | PO line export | ERP-A | `PO-417-1` | Day minus 2, 08:14 | The PO line exists and expects item `A-104` |
| 2 | Scan transaction export | WMS-B | `SCN-55120` | Day minus 2, 14:02 | The scan happened, and carries item identifier `A104` |
| 3 | Interface rejection log line | Integration layer | `REJ-9931`, references `SCN-55120` | Day minus 2, 14:02:06 | The scan reached the interface and was rejected on an unmatched item identifier, six seconds after the scan |
| 4 | Item master export | ERP-A | item `A-104` | Day 0, 09:30 | ERP-A holds the item as `A-104`, with the hyphen |
| 5 | Item cross-reference export | WMS-B | item `A104` | Day 0, 09:34 | WMS-B holds the same item as `A104`, with no hyphen |

Record 3 carries the identifier of record 2 and a timestamp six seconds after it. That is what
makes it a joined record rather than a log line on a related theme.

## 5. Comparison window

| Scope | Days | N examined | M showing the divergence |
|---|---|---|---|
| Item `A-104` only, all receipts | 30 | 5 | 5 |

Reading: `M = N, systematic`

All five comparable receipts for this item show the identifier arriving without its hyphen. That
rules out a one-off keying error on `R-882`.

It does not finish the job, and this is the point of the example. The window was scoped to **one
item**. A transform that is systematic for one item is consistent with two different causes:

- The interface mapping strips or fails to translate hyphens for **every** item, which is
  configuration.
- This one item's cross-reference record in WMS-B was created without the hyphen, which is data.

The window as drawn cannot tell those apart, because it contains no other hyphenated item.

If 1 < M < N: not applicable, M = N.

## 6. Four branches

| Branch | Status | Evidence, by record number from section 4 |
|---|---|---|
| Handoff or process | contradicted | Records 2 and 3. The scan transmitted and reached the interface six seconds later. There is no manual step and no timing gap. |
| Wrong or missing data | supported | Records 4 and 5. The same item carries two different identifiers in the two systems. |
| Feature of the system we own, needing configuration | supported | Records 2 and 5 plus the window, M = 5 of 5. The divergence is systematic rather than per-transaction, which is the signature of a mapping. |
| Genuinely missing capability | contradicted | `ERP-A 9.2 Standard` and `WMS-B 4.1` both document an item cross-reference table in the installed version and licensed edition. The stated basis for the purchase, that WMS-B cannot handle these part numbers, is contradicted by the documentation for the release in use. |

Two branches are supported, and one of the two is additionally untested at the document level: the
interface mapping definition has not been exported. See section 14.

## 7. Verdict, or competing branches

Section 7a is not available. Two branches are supported and a test that could change the result
has not been run, so a single-branch verdict is not permitted.

### 7b. Competing branches, not settled

| Competing branch | Why it is still live |
|---|---|
| Wrong or missing data | WMS-B's cross-reference record for this one item may simply have been created without the hyphen. Records 4 and 5 are consistent with that and with nothing else being wrong. |
| Feature of the system we own, needing configuration | The divergence is systematic across all 5 in-window receipts, which is what a mapping rule produces. The mapping definition itself has not been read, so this is supported by behavior and untested at the document level. |

**One discriminating test.**

| Field | Value |
|---|---|
| The test | Pull the same 30-day window for three other items whose ERP-A identifier contains a hyphen, and compare the identifier that arrives on the WMS-B side. |
| What each outcome would mean | If the other hyphenated items also arrive without their hyphens, the behavior is a mapping rule and the branch is configuration. If only `A-104` does, the cause is that item's cross-reference record and the branch is data. If no other hyphenated item exists, the test cannot run and the mapping definition must be exported and read instead. |
| Owner (role) | Integration administrator |
| Date due | Day 3 |

One test, not a list. The mapping definition export is also owed, and it appears as an evidence
gap in section 14 rather than as a second test, because the window test is cheaper and either
outcome narrows the question.

## 8. Next action

| Field | Value |
|---|---|
| Action | Run the discriminating test in 7b. Do not change the mapping and do not edit the cross-reference record until it returns. |
| Owner (role) | Integration administrator |
| Date | Day 3 |
| If the action is a test-environment replay: configuration and master-data parity with production as of the failure confirmed by | Not applicable at this step. If a replay follows, the integration administrator confirms that the test environment's mapping and item master match production as of Day minus 2, in writing, before the replay counts as evidence. |

## 9. How we will know it worked

| Field | Value |
|---|---|
| The observable change | A new receipt for the affected item posts to the PO line with no interface rejection |
| Environment it will be observed in | Production, after the fix is signed off. A test-environment pass alone is not the measure, because parity is the open question. |
| Who checks, and when | Receiving supervisor, on the first receipt for this item after the change |

## 10. Backlog of already-affected records

| Field | Value |
|---|---|
| Records already affected (count) | 5 |
| How that count was derived (record or extract) | The 30-day comparison window extract, section 5, M = 5 |
| Remediation owner (role) | Receiving supervisor, with the integration administrator |
| Remediation date | Within 5 days of the fix being signed off |

Correcting a mapping or a cross-reference record fixes the next receipt. It does not repost
`R-882` or the other four. That is a separate task with its own owner, and it is the line most
often left off.

## 11. Capability claim

| Field | Value |
|---|---|
| The claim | "WMS-B cannot handle our part numbers." |
| Source document and date | `WMS-B 4.1` administration documentation, item cross-reference section (invented reference) |
| Installed version | WMS-B 4.1 |
| Licensed edition | Standard |
| Status | Claim CONTRADICTED by the documentation for the installed version. The capability exists in the release in use. |

The claim was made verbally in the purchase request. Verbal is not proof, in either direction. What
settles it here is the documentation for the version actually installed, not the current product
page.

## 12. Indicators

| | Indicator | Baseline | Source | Review date |
|---|---|---|---|---|
| Leading | Interface rejections per week on unmatched item identifiers | `UNVERIFIED - owed by integration administrator, needed before sign-off` | Integration rejection log | Day 10 |
| Lagging | Receipts requiring manual posting per month | `UNVERIFIED - owed by receiving supervisor, needed before sign-off` | ERP-A receipt posting report | Day 30 |

Both baselines are printed as `UNVERIFIED` rather than estimated. Without a baseline there is no
way to tell afterwards whether the change worked, so these are owed before sign-off, not after.

## 13. Sign-off

| Role | Name | Signature | Date |
|---|---|---|---|
| Process owner | | | |
| System owner or administrator | | | |
| Budget approver | | | |

Unsigned. The proposed warehouse module upgrade does not proceed on this document. On the evidence
so far, the stated basis for it is contradicted, and the real cause is one of two fixes that cost
nothing to license.

## 14. Open evidence gaps

| Missing artifact | System of record | Owner | Retrieval deadline | Branch it would change |
|---|---|---|---|---|
| Interface field mapping definition for the item identifier | Integration layer | Integration administrator | Day 3, no retention limit on a configuration export | Configuration branch. Reading it would move that branch from supported-by-behavior to supported-by-document, or contradict it. |
| 30-day window for three other hyphenated items | WMS-B and ERP-A | Integration administrator | Day 3, inside the 30-day transaction window | Separates the data branch from the configuration branch. This is the discriminating test in 7b. |
| Written procedure for receiving a mismatched identifier | Process documentation | Receiving supervisor | No deadline | Handoff branch. Currently contradicted on timing evidence; the procedure would confirm whether operators are instructed to key around the rejection, which would change the backlog count. |

---

# Case B. The same case, where the evidence has already expired

Identical facts, with one change: in this variant the integration layer's rejection log retention
is 7 days, and nobody exported anything until Day 23. Records 3 and the window extract are gone.

## What the output becomes

**EVIDENCE INCOMPLETE.** Not a verdict, and not a softer version of one.

### Four branches in this variant

| Branch | Status | Why |
|---|---|---|
| Handoff or process | untested | The rejection log is gone. Without record 3 there is no timestamp showing the scan reached the interface, so there is no evidence that contradicts a timing gap. In Case A this branch was contradicted. Here it is untested, and those are different findings. |
| Wrong or missing data | untested | The item master exports still exist and show two identifiers, but with no transaction-level log the divergence cannot be tied to the failure of `R-882`. |
| Feature of the system we own, needing configuration | untested | The comparison window cannot be built, so there is no count and no way to distinguish systematic from one-off. |
| Genuinely missing capability | contradicted | The vendor documentation for the installed version and edition does not expire, so this one still resolves. |

### Evidence gaps, five columns each

| Missing artifact | System of record | Owner | Retrieval deadline | Branch it would change |
|---|---|---|---|---|
| Interface rejection log covering Day minus 2 | Integration layer | Integration administrator | **Passed.** 7-day retention; the case was opened on Day 23. | Handoff branch, and the join that ties any branch to this failure |
| 30-day comparison window for item `A-104` | WMS-B and ERP-A | Integration administrator | **Passed** for the original window. A fresh 30-day window from today can be built if the condition is still live. | Separates data from configuration |
| Interface field mapping definition | Integration layer | Integration administrator | No retention limit. Available now. | Configuration branch |

### What goes back to the requester

Three sentences, and no verdict.

1. The purchase cannot be evaluated on this case, because the log that would join the failure to a
   cause was deleted before anyone exported it.
2. Two things are available today and neither needs a purchase: the mapping definition, which has
   no retention limit, and a fresh 30-day comparison window if the condition is still occurring.
3. One finding does survive: the stated basis for the purchase, that WMS-B cannot handle these part
   numbers, is contradicted by the documentation for the version installed. That is enough to stop
   the purchase, and not enough to name the fix.

### The lesson this variant carries

Step 0 is first for this reason. The logs that explain a transaction usually expire long before the
transaction records do. By the time a purchase request reaches a budget approver, the evidence that
would have settled it is often already gone. Preserve first, then analyse.
