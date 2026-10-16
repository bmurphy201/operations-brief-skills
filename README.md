# The Operations Brief Skills

Free, open tools from [The Operations Brief](https://theoperationsbrief.com) that you can run with
an AI assistant or entirely by hand. Each one lives in its own folder in this repository and is
released as a downloadable ZIP.

MIT licensed, so you can read it, use it at work, change it, and share it.

| Skill | What it decides | Folder |
| --- | --- | --- |
| Purchase Verdict | Whether a reported system failure needs a data fix, a process fix, a setting change in software you already own, or genuinely new software | [`purchase-verdict/`](purchase-verdict/) |

---

## Purchase Verdict

### Your first step

[**Download purchase-verdict-v1.0.zip**](https://github.com/bmurphy201/operations-brief-skills/releases/download/purchase-verdict-v1.0/purchase-verdict-v1.0.zip),
unzip it, and open `START-HERE.md`. That file is short and tells you which of the three ways to run
it fits your situation.

The full release, including the checksum, is on its
[release page](https://github.com/bmurphy201/operations-brief-skills/releases/tag/purchase-verdict-v1.0).

If you would rather read before you download, every file is browsable right here in
[`purchase-verdict/`](purchase-verdict/).

### What it does

Someone on your team reports that the system failed. A vendor says the fix is a new module. Before
you sign anything, this walks you through four competing explanations for the same complaint:

1. **Data.** A record is wrong, missing, or mismatched between two systems.
2. **Handoff.** A person or a system did not do the step, or did it in the wrong order.
3. **Configuration.** A setting in software you already own is switched the wrong way.
4. **Capability.** Your software genuinely cannot do it.

Only the fourth one is a purchase. The other three are cheaper, and the procedure makes you prove
which one your own records actually support.

### What you need before you start

You do not need a developer, a license, or an account anywhere. You need records:

- One failure you can evidence on both sides, with the transaction records that show it.
- The integration, rejection, or error log covering that window. **Export this first.** These logs
  expire on a retention schedule, and once that window closes the question may be unanswerable.
- A handful of comparable records: the same item, partner, location, or transaction type across a
  stated number of days.
- The item or entity master from every system involved, the written procedure for the step that
  failed, and the field mapping or interface configuration.
- The vendor documentation for the version and edition you actually run, not the current product
  page.

If you cannot get some of these, that is a normal outcome and the procedure handles it. See the
next section.

### What you get back

**One page.** Either a verdict or a next test, never a guess dressed as a verdict.

- **A verdict** names which of the four fixes your evidence supports, lists the records that
  support it, and marks the other three branches contradicted or untested. You walk into the vendor
  conversation with a position instead of an impression.
- **A next test** is what you get when the evidence does not settle it. Instead of picking the
  likely answer, you get the explanations still standing and the single cheapest test that would
  separate them, with a named owner and a date. One test, not a list. This is a result, not a
  failure, and it costs less than a wrong purchase.
- **Evidence incomplete** is what you get when a required source is gone or was never kept. It
  prints each missing item with the system it lives in, who owns it, the deadline to retrieve it,
  and which of the four branches it would change. That list is the thing you hand your IT group.

### Three ways to run it

Pick one. They produce the same procedure.

#### Route 1: load it as a skill in Claude

Anthropic's documentation describes this route as: go to **Customize > Skills** (you have to be
signed in), click **+**, then **+ Create skill**, then **Upload a skill**, then upload a ZIP file
containing your skill folder. The ZIP in the release is built for that shape. It contains one
top-level folder named `purchase-verdict`, matching the skill's own name, because that same
documentation lists a folder name that does not match the skill name as a cause of upload failure.
So do not rename the folder.

Reference: <https://support.claude.com/en/articles/12512180-use-skills-in-claude>

Two honest limits. We have not performed this upload on your account, so treat it as the
documented procedure rather than one we tested for you. And if you do not see **Skills** under
Customize, this route is not available on your account or plan. Use Route 2, which works anywhere.

#### Route 2: paste it into ChatGPT or any other assistant

**This ZIP is not a one-click install everywhere.** It is a ZIP of plain text files, and only a
platform that documents a skill upload will import it. For ChatGPT in particular, OpenAI's
documentation describes workspace skills, local filesystem skills, and plugins as separate
installation paths, and does not document uploading a skill ZIP inside ChatGPT. Do not expect the
Route 1 file to install there.

Reference: <https://learn.chatgpt.com/docs/enterprise/skills>

What does work, in ChatGPT and in any other assistant:

1. Open `reference/generic-llm-prompt.md` from the download.
2. Copy the whole file and paste it into a new conversation.
3. Give it your exports and worksheets when it asks, subject to the privacy rule below.

If your workspace administrator distributes skills for your company, hand them the folder and let
them use whichever of their own documented paths applies.

#### Route 3: no AI at all

The procedure is deterministic. The work that establishes cause is joining records, counting them,
and comparing fields, and a spreadsheet does all of it. Print `SKILL.md`,
`reference/source-manifest-worksheet.md`, and `reference/verdict-one-pager.md` and work through
them. An assistant drafts the write-up faster. It does not establish the cause.

### Privacy and data boundaries

**Read this before your first paste.**

Do not put transaction records, supplier pricing, contract terms, employee names, or customer data
into a third-party AI tool unless your company's agreement with that provider covers that class of
data. Ask whoever owns that agreement first. If the answer is no, Route 3 still gives you the full
verdict with no AI tool involved.

When you are cleared to proceed:

- Mask unit cost, supplier pricing, margin, and contract terms unless the verdict turns on money.
- Replace people's names with role labels.
- Scope every export to the one case plus the comparison window. Never a full table.

Nothing in this repository sends your data anywhere. These are text files. Whatever you paste into
an assistant goes to that assistant under that provider's terms, not ours.

### What this will not do

- It does not connect to your ERP, WMS, or any other system, on any route. It reads only what a
  person hands it.
- It does not read or change a single record in your systems.
- It does not approve or decline a purchase, a configuration change, or a data correction. Three
  named humans sign off: the process owner, the system owner, and the budget approver.
- It does not replace your software partner or your IT group. It gives them a verdict with the
  records attached, so the conversation starts from evidence.

### About the worked example

`reference/worked-example-invented.md` is **entirely invented**, including every company, person,
part number, and document reference. It exists to show the shape of a correct output, including one
case the evidence does not settle. It is not a customer story and none of its records exist.

### Verifying your download

Optional, and only if you care to. The SHA-256 of `purchase-verdict-v1.0.zip` is:

```
422e242b597e66936b843d870e17eb95311175323e1a2b9f184f0116c227f6ae
```

To check your copy against it:

```sh
shasum -a 256 purchase-verdict-v1.0.zip    # macOS
sha256sum purchase-verdict-v1.0.zip        # Linux
```

The ZIP and the [`purchase-verdict/`](purchase-verdict/) folder in this repository are the same six
files.

---

## Where to get help

- **Something is unclear, or the procedure does not fit your case:** open an
  [issue](https://github.com/bmurphy201/operations-brief-skills/issues) and describe your situation.
  Please do not paste real transaction data, supplier pricing, or customer names into a public
  issue.
- **You want the newsletter these come from:** [The Operations Brief](https://theoperationsbrief.com).

To set expectations: this is a published tool, not a support contract. We do not provide
implementation support for your ERP or WMS, and nothing here replaces your software partner or
your IT group.

## License

[MIT](LICENSE). Use it at work, change it, share it, build it into something you sell. The only
condition is that the copyright notice and permission notice travel with it.

## Repository layout

One folder per skill at the root, each self-contained:

```
operations-brief-skills/
  LICENSE                 MIT, covers every skill in this repository
  README.md               this file
  purchase-verdict/       the first skill
    START-HERE.md         what it is, what you need, the three routes
    SKILL.md              the procedure itself
    reference/            the pasteable prompt, worksheets, and the invented example
```

Each skill is released independently, tagged `<skill-name>-v<version>`, with the skill's ZIP
attached as the release asset. Adding a future skill means adding a folder, a row in the table at
the top of this file, and a tag. Existing skills and their download links are unaffected.
