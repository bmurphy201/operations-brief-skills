# Start here

## What this is

A diagnosis you run before you approve operations software. It is a written procedure plus three
worksheets. You can run it with an AI assistant or entirely by hand.

The question it answers: when someone reports that the system failed, is the real problem the
data, the handoff between people and systems, a setting in software you already own, or a
capability your software genuinely does not have? Those four answers lead to four different
actions, and only one of them is a purchase.

## What you give it

Your own records:

1. One failure you can evidence on both sides, with the transaction records that show it.
2. The integration, rejection, or error log covering that window, exported **before it expires**.
3. A handful of comparable records: the same item, partner, location, or transaction type over a
   stated number of days.
4. The item or entity master from every system involved, the written procedure for the step that
   failed, and the field mapping or interface configuration.
5. The vendor documentation for the version and edition you actually run.

## What you get back

A one-page verdict naming which fix the evidence supports, with the records that support it.

When the evidence does not settle it, you get the competing explanations and the single cheapest
test that would separate them, with an owner and a date. That is a result, not a failure, and it
is cheaper than a wrong purchase.

Either way you walk into the vendor conversation with a verdict instead of an impression.

## Route 1: load it as a skill in Claude

Anthropic's support documentation describes this route as: navigate to **Customize > Skills**
(`https://claude.ai/customize/skills`), click the "+" button, then "+ Create skill", then select
"Upload a skill", and "Upload a ZIP file containing your skill folder."

The ZIP in this package is built for that shape: it contains one top-level folder named
`purchase-verdict`, and the skill's own name is `purchase-verdict`. The same documentation lists
"Skill folder name doesn't match the skill name" as a cause of upload failure, so do not rename
the folder. That documentation also lists a ZIP size limit without stating the number; this
package is small plain text, well under any plausible limit.

Reference: https://support.claude.com/en/articles/12512180-use-skills-in-claude

Two honest limits on that paragraph. Colony Spark has not performed this upload on your account,
so treat it as the documented procedure rather than a tested one. And if you do not see **Skills**
under Customize, this route is not available to your account or plan. Use Route 2 instead, which
works anywhere.

## Route 2: paste it into ChatGPT or any other assistant

**This is not a one-click install anywhere except where a platform documents one.** For ChatGPT in
particular, OpenAI's documentation describes workspace skills, local filesystem skills, and
plugins as **separate** installation paths, and states that "ChatGPT workspace skill distribution,
local filesystem skill installation, and surface-specific plugin installation are separate paths"
and that "ChatGPT workspace controls don't install local filesystem skills or plugins." That page
does not document uploading a ZIP of a skill folder inside ChatGPT, so do not expect the Route 1
file to install there.

Reference: https://learn.chatgpt.com/docs/enterprise/skills

What works in any assistant, including ChatGPT, Gemini, Copilot, and a local model:

1. Open `reference/generic-llm-prompt.md`.
2. Paste the whole file into a new conversation.
3. Attach or paste your exports and worksheets when it asks for them, subject to the upload rule
   below.

If your workspace administrator does distribute skills, hand them the folder and let them use
whichever of their documented paths applies. That is their call, not a setting you can change from
a chat window.

## Route 3: no AI at all

The procedure is deterministic. The work that establishes cause is joining records, counting them,
and comparing fields. A spreadsheet and a query tool do all of it. Print `SKILL.md`,
`reference/source-manifest-worksheet.md`, and `reference/verdict-one-pager.md`, and work through
them. An assistant drafts the explanation faster. It does not establish the cause.

## Before you paste anything: the upload rule

Do not put transaction records, supplier pricing, contract terms, employee names, or customer
data into a third-party AI tool unless your company's agreement with that provider covers that
class of data. Check with whoever owns that agreement **before** the first paste. If the answer is
no, Route 3 still gives you the full verdict.

Mask unit cost, supplier pricing, margin, and contract terms unless the verdict turns on money.
Replace people's names with role labels. Scope every export to the case plus the comparison
window, never a full table.

## What this will not do

- It does not connect to your ERP, WMS, or any other system, on any route. It reads only what a
  person gives it.
- It does not read or change a single record in your systems.
- It does not approve or decline a purchase, a configuration change, or a data correction. Three
  named humans sign off: the process owner, the system owner, and the budget approver.
- It is not a substitute for your software partner or your IT group. It gives them a verdict with
  the records attached, so the conversation starts from evidence.

## Read next

`SKILL.md` is the procedure. The worked example in `reference/worked-example-invented.md` is
entirely invented, including every company, person, part number, and document reference. It shows
the shape of a correct output, including a case the evidence does not settle. It is not a customer
story and none of its records exist.
