---
name: purchase-verdict
description: Decide whether a reported operations failure calls for a data fix, a process fix, a configuration change in software you already own, or genuinely new software. Use before approving an ERP, WMS, MES, or other operations software purchase, and whenever someone says "our system cannot do that." Tests four explanations against the operator's own records and returns a one-page verdict, or names the single next test when the evidence is not sufficient.
---

# Purchase Verdict

A read-only diagnosis you run before you approve software. You bring one failure you can
evidence and a bounded set of comparable records. The output is a one-page verdict naming which
fix the evidence supports, or a statement of what evidence is missing, who owns it, and the one
test that would settle it.

## What this does, and what it does not do

It does:

- Separate four explanations for the same complaint, and mark each one supported, contradicted,
  or untested against your records.
- Say when the evidence does not settle the question, instead of picking the likely answer.
- Give the buyer a verdict to carry into the vendor conversation.

It does not:

- Connect to your ERP, WMS, database, or any other system. It reads only the files and text a
  person gives it.
- Read or write any record. Everything it sees is an export a human made.
- Approve, authorize, or decline a purchase, a configuration change, or a data correction. Those
  are human decisions with named owners and signatures.
- Replace your software partner, your IT group, or your vendor's support organization. Its output
  is an input to their work.

Run it when a person asks it to run. It has no schedule and no trigger.

## Step 0. Preserve the evidence that expires

Do this before any analysis, including before building the manifest.

Transaction records usually outlive the logs that explain them. Scan logs, integration and
middleware error logs, queue and interface records, and job histories are frequently kept for a
much shorter period, and they are exactly what the four tests depend on. Retention varies by
system, by version, and by local configuration, so do not assume a number. Ask the person who
administers each system what their retention is, and write the answer down.

For each system in scope, record and then act:

| System | What to export | Retention stated by | Retention period | Export deadline | Exported? |
|---|---|---|---|---|---|

Export the case window and the comparison window now, store the files in the case folder, then
continue. If a needed log is already past retention, stop and go to Step 6. Say so at the start.
Discovering it in Step 4 wastes the analysis.

## Step 1. Does the record exist, or is it just not visible?

The cheapest check, and it can close the case outright.

"It is missing from my screen" and "it was never created" are different conditions with the same
complaint. A saved filter, a date range, a default warehouse or location, a company or entity
selector, a posting status, or a role permission all produce the same report from the operator.

Have someone with broad read access query for the record by its identifier, with no filters.

- Found: the condition is visibility. Capture which filter, default, or permission hid it. The
  purchase question is usually answered here and the rest of this procedure is not needed.
- Not found by identifier anywhere in the system of record: the record does not exist. Continue.

Record the result either way. A one-pager that skips this step cannot be trusted, because the
reader cannot tell which condition was diagnosed.

## Step 2. Build the source manifest

Use `reference/source-manifest-worksheet.md`. One row per exported artifact, with the source
system, the report or extract name, the record identifiers included, the fields included, the
export date and time, who exported it, that source's retention, and whether the export was taken
with read-only access.

Keep two classes of input apart, and label every input as one or the other:

- A **record** carries a source system, an identifier, and a timestamp. It can be joined to other
  records.
- A **claim** is what a person reported. It can be true and still is not a record.

A screenshot is a claim. It has no source header, no export time, and no identifier you can join
on. Treat it as a pointer to the export you still need, never as the export.

The minimum set for a purchase question:

- The transaction records on both sides of the suspected divergence.
- The integration, rejection, or error log covering the case window.
- The item or entity master from **each** system involved, not just one.
- The current written procedure for the step that failed.
- The interface configuration or field mapping definition.
- The vendor documentation for the **installed version and licensed edition** you actually run.

## Step 3. The bounded comparison window

One case cannot separate bad data from a system that is configured wrong. A single transaction
shows that a value was wrong. It cannot show whether it was wrong once or whether the system
produces it wrong every time. Those two findings lead to opposite actions, so the input needs two
scopes, not one.

- **The case:** one transaction, fully evidenced, both sides.
- **The comparison window:** the same item, partner, location, or transaction type, over a stated
  number of days, pulled only to count how often the same divergence appears.

State the window's scope, the number of comparable records examined (N), and the number showing
the same divergence (M). Both numbers go on the one-pager. Then:

| What the window shows | What it indicates | What it does not establish |
|---|---|---|
| M = 1 of N | A single record, so a data condition | That the configuration is correct |
| M = N, systematically transformed the same way | Configuration or mapping | Which specific setting, until you read the mapping |
| 1 < M < N | A process or handoff condition | The cause, until you test what separates the affected rows from the clean ones |

An intermittent pattern has a required follow-up: name what the affected rows share that the
clean rows do not. Person, shift, route, partner, entry channel, or item class.

If the window is too small to distinguish these cases, say the window was too small. Do not pick
the nearest branch.

## Step 4. Test all four branches

Mark every branch, every time. Four statuses on every one-pager.

| Branch | What supports it | What contradicts it | The discriminating test |
|---|---|---|---|
| **Handoff or process** | The record exists in system A and never arrives in B; a timing gap at a manual step; the written procedure is silent on this case | The automated path shows the record transferred inside the window | Does the gap appear only when a particular person, shift, route, or entry channel is involved? |
| **Wrong or missing data** | A field value differs across systems; a required field is empty | The value is correct in every system and the case still fails | Is the bad value on **one** record in the window, or on all of them? |
| **A feature of the system you own, needing configuration or integration** | The feature is documented in your installed version and licensed edition, and is switched off, unmapped, or unconfigured | Vendor documentation for the version you actually run shows no such feature | The same count inverted: a systematic transform across every comparable record is configuration, not keying |
| **A genuinely missing capability** | A documented limit in your installed version, or a dated written statement from the vendor or partner | Any one of the three branches above resolves the case | Has anyone read the documentation for the version we run, rather than the current product page? |

Each branch gets a status, not a score:

- **Supported:** named records in the manifest support it.
- **Contradicted:** named records in the manifest argue against it.
- **Untested:** nobody ran the test.

Untested and contradicted are different findings and must never be merged. Recording that you
looked for disconfirming evidence and did not find it is a different claim from not having looked.

## Step 5. Verdict, or competing branches plus one test

A single-branch verdict is permitted **only** when both conditions hold:

1. Exactly one branch is supported, and
2. No remaining branch is untested on a test that could change the result.

Otherwise the output is the competing branches, plus **one** discriminating test: the cheapest
test that separates them, with a named owner and a date. One test, not a list. A list is a
research project and it will not get run.

This rule exists because naming a confident verdict on mixed evidence is worse than returning
competing branches. A wrong verdict gets acted on. Competing branches get tested.

## Step 6. Evidence incomplete

Not a failure. A result, and often the most useful one, because it is returned before money moves.

For every gap, print five things:

1. The missing artifact.
2. The system of record that holds it.
3. The named owner who can produce it.
4. The retrieval deadline, given that source's retention.
5. **Which branch it would change.** Nobody should chase evidence that cannot move the decision.

Anything asserted without evidence is printed on the one-pager as
`UNVERIFIED - owed by <name>, needed before sign-off`. That includes a missing baseline, a missing
lagging measure, and an unproven capability claim. Never omit it and never infer it.

## Step 7. Capability proof

"Our system cannot do that" is a claim, not a record, and it is the single highest-leverage claim
in a purchase decision. Accept it only as one of:

- A section of vendor documentation for the **installed version and licensed edition** you run.
- A dated written response from vendor or partner support, naming your version.
- A documented limit in the release you are on.

Check the documentation for the version installed, not the current product page. Features arrive
in releases you are not running, and are also removed or gated by edition.

A verbal statement is not capability proof. The reason is structural rather than personal: the
person best placed to say "the system cannot do that" is often the same person who would otherwise
have to configure it. Ask for the document, from anyone, every time.

## Step 8. Human sign-off

The one-pager is a recommendation. Three named humans sign before anything changes or is bought:
the process owner, the system owner or administrator, and the budget approver. Any configuration
change, data correction, or purchase requires their signature. This skill never performs or
authorizes any of them.

Add the remediation line separately from the fix. Correcting a mapping or a setting fixes the
forward flow. It does not repair the records that already failed. The verdict needs the count of
already-affected records and the named owner who will remediate them.

If the next action is to reproduce the case in a test environment, check configuration parity
first: the test environment's mapping and master data must match production as of the failure.
Otherwise the replay exercises a different system and proves nothing about yours.

## Data handling rules

- **Enforce read-only at the credential, not in prose.** "This skill does not edit records" is
  only true if the account used for the export cannot write. Use a reporting or extract role.
- Scope every export to the case plus the comparison window. No full-table dumps.
- Mask unit cost, supplier pricing, margin, and contract terms unless the verdict turns on money.
  If it does, name the one field needed and include only that field.
- Replace operator and scanner names with role labels on the one-pager. Real names stay in the
  restricted manifest.
- **Do not upload any record to a third-party AI tool unless your company's agreement with that
  provider covers that class of data.** Check before the first paste, not after. If the agreement
  does not cover it, the joining, counting, and comparing in Steps 1 through 4 are all
  deterministic work you can do in a spreadsheet or a query, with no model involved.
- A model drafts the explanation. It does not establish cause. Cause comes from the records named
  in the manifest.
- Give the case folder a named access list and a deletion date when you create it.

## Output

Fill `reference/verdict-one-pager.md`. Every number on it carries the record that shows it.

## Self-check before this leaves your hands

- [ ] Step 0 ran first, and each system's retention and export deadline are written down.
- [ ] Existence versus visibility is resolved and recorded.
- [ ] Every input is labeled record or claim. No screenshot is doing a record's job.
- [ ] The item or entity master is present from **every** system involved.
- [ ] Each joined log line carries an identifier and a timestamp inside the window. A log line
      that merely sounds related is not a joined record.
- [ ] The comparison window's scope, N, and M are all stated.
- [ ] All four branches carry a status. No branch is blank, and untested is written as untested.
- [ ] If more than one branch is supported, or any branch that could change the result is
      untested, the output is competing branches plus exactly one discriminating test with an
      owner and a date.
- [ ] Every gap prints artifact, system, owner, deadline, and the branch it would change.
- [ ] Any capability claim carries a document, a version, and an edition, or reads `UNVERIFIED`.
- [ ] The remediation line for already-affected records is present and separate from the fix.
- [ ] Money and personal-name fields are masked, or the one field the verdict turns on is named.
- [ ] Three sign-off lines are present and unsigned until the humans sign them.

## Files in this package

- `START-HERE.md` how to install or paste this, and what it is not
- `SKILL.md` this procedure
- `reference/generic-llm-prompt.md` the pasteable version for any assistant
- `reference/source-manifest-worksheet.md` the input worksheet
- `reference/verdict-one-pager.md` the output template
- `reference/worked-example-invented.md` one fully invented example, end to end
- `LICENSE` the MIT license this package is released under
