# Foresight in EU Impact Assessments - data bundle

162 impact assessments, 368 located "foresight" mentions.
Produced by `pipeline/run_all.py`; method and schemas in the repository's
SPEC.md (https://github.com/monkeymoves/eu-ia-foresight-pipeline).

## The two working surfaces

1. **The review page** - browse the evidence.
   Hosted at https://monkeymoves.github.io/eu-ia-foresight-data/out/review.html (also in this bundle at
   `out/review.html`, which works offline). Search and filters at the top,
   an index of mention-bearing IAs on the left, every mention as a
   highlighted excerpt with a link that opens the source PDF at the exact
   page. Tick mentions as you review them; ticks are stored in your own
   browser only (a personal aid, not shared data).

2. **The spreadsheet** - record the judgements.
   `out/dataset.xlsx`: a single sheet, one row per impact assessment.
   Read the evidence for an IA on the review page (the "Review page" link
   in its row takes you straight there), then record your call in that row.

## Which columns are yours vs AI-drafted

- Yours (the actual dataset): **Topic**, **Kind of foresight (final)**,
  **Other / notes**. Dropdowns are embedded where a fixed list applies
  (kind: embedded, contextual).
- Machine suggestions, clearly named **"AI draft: ..."**: topic, kind,
  methods, material influence, how, notes. Every draft verdict traces to a
  verbatim quote visible on the review page. Confirm or override; never
  treat a draft as a result (see docs/adr/0001 in the repository).
- Deterministic (no AI, but heuristics worth sanity-checking): **Scope**
  (parsed from the title), **Mention pages**, **Related: ...** term counts,
  **Flags** (e.g. register-side download failures).

The "Reference" column links to the official register entry; "Review page"
links to that IA's section of the hosted review page. Both are ordinary
web links, so they work from Excel, Google Sheets, or anywhere else.

## Working in Google Sheets

Upload `dataset.xlsx` to Google Drive and open it with Google Sheets (or
File > Import in an empty Sheet). Links and dropdowns survive the
conversion, and the whole team can then work in one shared Sheet.

## Folder contents

```
manifest.json       one register entry per impact assessment (IA)
mentions.json       every located "foresight" mention, with page refs
ai_drafts.json      the combined AI draft classifications (with evidence)
pdfs/<ref>/partN.pdf
md/<ref>/partN.md   page-marked plain text of each PDF
docx/<ref>/partN.docx   Word versions, for easier reading
out/
  dataset.xlsx      the spreadsheet
  review.html       the review page (self-contained, works offline)
  README.md         this file
```

## Re-running the AI draft step yourself

The AI drafts were produced in Claude sessions (claude.ai / Claude Code)
using the versioned prompt at `prompts/classification-prompt.md` in the
repository - no paid API calls anywhere. To redo or extend them, paste the
prompt plus the relevant excerpts into your own Claude session and copy
the output back into the "AI draft" columns, then review as usual.
