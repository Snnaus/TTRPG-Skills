# dm_pdf_ingest.md — PDF Rulebook Ingestion
# Referenced by dm_setup.md. Load when a player provides a PDF rulebook.
# Requires: pdf-reading skill at /mnt/skills/public/pdf-reading/SKILL.md

---

## Purpose

This sub-skill handles extracting usable rules content from a PDF rulebook
file so that dm_setup.md can parse it into mechanics.md and generate sub-skills.
It bridges the gap between a raw PDF upload and the structured text the setup
phase expects.

The output of this process is extracted rules text — the same thing the DM
would receive if the player pasted their rulebook manually. Once extraction
is complete, dm_setup.md step 3 (parsing into mechanics.md) proceeds normally.

---

## When to Use

Use this sub-skill when:
- The player uploads a `.pdf` file as their rulebook during setup (dm_setup.md step 2)
- The player references a PDF they have already uploaded and asks the DM to
  read it for rules

Do NOT use this sub-skill for:
- Non-PDF files (text, pasted content, described-from-memory rules) — those
  go directly to dm_setup.md step 3
- PDFs that are not rulebooks (character sheets, adventure modules, maps) —
  handle those with the general pdf-reading skill as needed during play

---

## Extraction Procedure

### Step 1 — Content Inventory

Before extracting anything, diagnose what kind of PDF this is.
Run the following against the uploaded file:

```bash
pdfinfo /mnt/user-data/uploads/[filename].pdf
pdftotext -f 1 -l 1 /mnt/user-data/uploads/[filename].pdf - | head -30
```

This tells you:
- **Page count** — how large is the rulebook?
- **Text extractability** — does `pdftotext` return readable text, or is
  it empty (scanned) or garbled (broken encoding)?

Based on the results, choose one of three paths:

| Diagnosis | Path |
|---|---|
| `pdftotext` returns clean, readable text | **Text extraction path** (Step 2a) |
| `pdftotext` returns empty or near-empty output | **Scanned PDF path** (Step 2b) |
| `pdftotext` returns garbled/mojibake text | **Font encoding issue** — try rasterize path (Step 2b) |

### Step 2a — Text Extraction Path (text-based PDFs)

Most rulebook PDFs are text-based. Extract the full text:

```python
from pypdf import PdfReader

reader = PdfReader("/mnt/user-data/uploads/[filename].pdf")
total_pages = len(reader.pages)

text = ""
for page in reader.pages:
    page_text = page.extract_text()
    if page_text:
        text += page_text + "\n\n"
```

If the rulebook is large (100+ pages), extract in chunks and focus on the
sections that matter for mechanics.md. The DM needs:

1. **Core stats / attributes** — usually in a "Character Creation" or
   "Abilities" chapter
2. **Resolution mechanic** — "How to Play", "Making Checks", "Core Mechanic"
3. **Combat rules** — "Combat", "Fighting", "Conflict"
4. **Advancement** — "Leveling Up", "Experience", "Advancement"
5. **Unique mechanics** — any system-specific chapters (magic, sanity, stress, etc.)

For large books, use a two-pass approach:

**Pass 1 — Table of contents scan.** Extract the first 5–10 pages to find
the table of contents. Identify which page ranges contain the sections above.

**Pass 2 — Targeted extraction.** Extract only the identified page ranges:

```python
# Extract specific page range (0-indexed)
target_text = ""
for i in range(start_page, end_page + 1):
    page_text = reader.pages[i].extract_text()
    if page_text:
        target_text += page_text + "\n\n"
```

### Step 2b — Scanned PDF / Font Issue Path

If text extraction fails, rasterize key pages and read them visually:

```bash
# Rasterize a page range at 150 DPI
pdftoppm -jpeg -r 150 -f [start] -l [end] /mnt/user-data/uploads/[filename].pdf /tmp/rulebook-page
ls /tmp/rulebook-page-*.jpg
```

Then read the resulting images to extract rules content. This is
token-expensive (~1,600 tokens per page), so prioritize:
1. Table of contents page(s) first — to identify where rules live
2. Core mechanic / resolution pages
3. Combat rules pages
4. Character creation / stats pages
5. Advancement pages

For scanned PDFs longer than ~30 pages, warn the player that full extraction
will be slow and suggest they identify the most important chapters.

### Step 3 — Table and Chart Extraction

Rulebooks often encode critical information in tables (stat modifiers,
difficulty scales, level progression, equipment lists). If the text extraction
from Step 2a produces garbled or misaligned tables:

```python
import pdfplumber

with pdfplumber.open("/mnt/user-data/uploads/[filename].pdf") as pdf:
    page = pdf.pages[page_number]  # 0-indexed
    tables = page.extract_tables()
    for table in tables:
        for row in table:
            print(row)
```

If `pdfplumber` also struggles with a table, rasterize that specific page
and read it visually:

```bash
pdftoppm -jpeg -r 200 -f [page] -l [page] /mnt/user-data/uploads/[filename].pdf /tmp/table-page
```

### Step 4 — Assemble and Present to Player

Once extraction is complete, the DM has raw rules text. Before parsing into
mechanics.md, present a summary to the player for confirmation:

```
"I've read through [rulebook name] ([page count] pages). Here's what I found:

- Stat system: [brief summary — e.g. "6 attributes, 3–18 scale"]
- Core mechanic: [brief summary — e.g. "d20 + modifier vs. difficulty class"]
- Combat: [brief summary — e.g. "initiative-based rounds, action economy"]
- Advancement: [brief summary — e.g. "XP-based leveling, 20 levels"]
- Unique mechanics: [brief summary — e.g. "spell slot system, death saves"]

Does this look right? Is there anything I missed or got wrong?"
```

Wait for player confirmation before proceeding. The player may want to
correct a misread rule or add house rules on top of the extracted content.

### Step 5 — Hand Off to dm_setup.md

After confirmation, the extracted and confirmed rules text becomes the input
for dm_setup.md step 3 (parsing into mechanics.md). From this point forward,
the process is identical to a player who pasted their rules manually.

---

## Edge Cases

**Encrypted or password-protected PDFs:**
If `pdfinfo` reports the PDF is encrypted, tell the player:
"This PDF appears to be password-protected. I can't extract text from it
directly. Could you paste the key rules sections instead, or provide an
unprotected version?"

**PDFs with mixed content (text + scanned pages):**
Some rulebooks have text-based body pages but scanned artwork or handwritten
notes. Extract text where available, rasterize pages where text extraction
returns empty.

**Very large rulebooks (300+ pages):**
Do not attempt to extract the entire book. Use the two-pass approach from
Step 2a. If the table of contents is not extractable, ask the player which
chapters contain the core rules.

**Multiple PDF files:**
If the player uploads multiple PDFs (e.g. core rules + supplement), process
each one separately using the same procedure. Combine the extracted text
before handing off to dm_setup.md step 3. Note which content came from which
file in case of conflicts.

**Content the DM cannot extract:**
If key rules sections are unreadable after both text extraction and rasterization
attempts, tell the player which sections failed and ask them to paste those
sections manually. Do not guess at rules content that could not be read.

---

## Token Budget Awareness

PDF extraction can consume significant context. Keep these costs in mind:

| Method | Approximate cost |
|---|---|
| Text extraction | ~200–400 tokens per page |
| Rasterized page (150 DPI) | ~1,600 tokens per page |
| Both together | ~2,000–2,400 tokens per page |

For a typical rulebook (50–200 pages), targeted extraction of rules-relevant
chapters (usually 30–60 pages of actual mechanics) should cost 6,000–24,000
tokens — manageable. Extracting the entire book at full fidelity is rarely
necessary and should be avoided.

The goal is to extract enough to populate mechanics.md accurately, not to
reproduce the entire rulebook.
