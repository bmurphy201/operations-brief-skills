# Source manifest worksheet

Fill this before any analysis. It is the record of what the verdict is built on, and it is the
only place real names and unmasked money fields are allowed to appear.

**Case folder access list:** ____________________  **Deletion date:** ____________

---

## A. Case header

| Field | Value |
|---|---|
| Case ID | |
| Date opened | |
| Analyst | |
| Process owner | |
| Proposed purchase, and who requested it | |
| Expected state | |
| Actual state | |
| Time window of the case (from / to) | |

---

## B. Step 0, preservation (complete this first)

Retention varies by system, by version, and by local configuration. Ask the administrator of each
system. Do not estimate.

| System | Log or extract to preserve | Retention stated by (name) | Retention period | Export deadline | Exported (y/n) | File stored at |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |

Any row where the export deadline has already passed: write it in section G as an evidence gap and
name the branch it would have changed.

---

## C. Step 1, existence versus visibility

| Question | Answer |
|---|---|
| Identifier searched for | |
| Who searched, and with what access level | |
| Filters, date range, location, company, and status all cleared? (y/n) | |
| Result: found / not found anywhere in the system of record | |
| If found: what hid it (filter, default location, posting status, permission) | |

If found, the condition is visibility. Record it and stop. The purchase question is answered.

---

## D. Exported artifacts

One row per export. Read-only means the account used for the export cannot write to that system.

| # | Source system | Report or extract name | Record IDs included | Fields included | Export date and time | Exported by | Source retention | Read-only? |
|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | |
| 2 | | | | | | | | |
| 3 | | | | | | | | |
| 4 | | | | | | | | |
| 5 | | | | | | | | |
| 6 | | | | | | | | |

### Required set, checked off

- [ ] Transaction records, side A
- [ ] Transaction records, side B
- [ ] Integration, rejection, or error log covering the case window
- [ ] Item or entity master, system 1
- [ ] Item or entity master, system 2 (and any further system involved)
- [ ] Current written procedure for the step that failed
- [ ] Interface configuration or field mapping definition
- [ ] Vendor documentation for the installed version and licensed edition

Any unchecked box is an evidence gap. Write it in section G.

---

## E. Records and claims

Every input goes in exactly one table. A screenshot always goes in the claims table.

### Records (source system, identifier, and timestamp all present)

| # | What it is | Source system | Identifier | Timestamp | Artifact row from section D |
|---|---|---|---|---|---|
| | | | | | |

### Claims (what a person reported)

| # | Claim | Who said it | Date | The export that would turn this into a record | Owner of that export |
|---|---|---|---|---|---|
| | | | | | |

---

## F. Step 3, comparison window

| Field | Value |
|---|---|
| Window scope (same item / partner / location / transaction type) | |
| Window length in days | |
| N, comparable records examined | |
| M, records showing the same divergence | |
| Extract that produced the window (artifact row from section D) | |

If 1 < M < N: what do the affected rows share that the clean rows do not?

| Candidate | Affected rows | Clean rows | Separates? |
|---|---|---|---|
| Person or operator role | | | |
| Shift or time of day | | | |
| Route, channel, or entry method | | | |
| Partner or carrier | | | |
| Item class or location | | | |

---

## G. Evidence gaps

Five columns, every row. A gap with no branch is a gap nobody needs to chase.

| Missing artifact | System of record holding it | Owner who can produce it | Retrieval deadline | Branch it would change |
|---|---|---|---|---|
| | | | | |

---

## H. Join check

Every log line used as evidence must carry an identifier and a timestamp inside the case window. A
line that merely sounds related is not a joined record.

| Log line reference | Identifier it carries | Timestamp | Inside the case window? | Joins to which record |
|---|---|---|---|---|
| | | | | |

---

## I. Capability claim

| Field | Value |
|---|---|
| The claim, verbatim | |
| Who made it | |
| Form of proof offered (documentation section / dated support response / release note / verbal) | |
| Installed version | |
| Licensed edition | |
| Document reference and date | |
| Status: PROVEN or UNVERIFIED | |

Verbal is not proof. If the only form offered is verbal, this row reads UNVERIFIED and the
one-pager carries it as UNVERIFIED.

---

## J. Masking record

| Field class | Present in the exports? | Masked on the one-pager? | If unmasked, the one field the verdict turns on |
|---|---|---|---|
| Unit cost | | | |
| Supplier pricing | | | |
| Margin | | | |
| Contract terms | | | |
| Operator and scanner names | | | |
| Customer or employee personal data | | | |

| Field | Value |
|---|---|
| Third-party AI tool used, if any | |
| Company agreement covering this data class confirmed by (name, date) | |
| If not confirmed: analysis done without a third-party tool (y/n) | |
