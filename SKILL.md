---
name: swiss-federal-writing-guidelines
version: "1.0"
updated: "2026-03-13"
description: >
  Apply the official typographic and editorial rules of the Swiss Confederation
  when drafting, correcting, or reviewing any official federal text.
  Trigger this skill whenever a text mentions the Confederation, a federal department,
  a federal act, or whenever the user asks to write or correct a text described as
  "official", "federal", or "according to the Federal Chancellery guidelines".
  Covers French, German, Italian and English.
---

# Rechtschreibung – Swiss Confederation Editorial Rules

This skill ensures compliance of official federal texts with Federal Chancellery directives.

## Reasoning approach

Before correcting anything, think carefully through each potential error — verify it against the reference file before flagging it. Prioritise precision over speed: a missed error is better than a wrong or invented citation.

## Procedure

1. **Identify the language** of the text (fr / de / it / en). Apply **Swiss conventions** for French, German, and Italian (e.g. no `ß` in German; no narrow non-breaking spaces before `?`, `;`, `!` in French — the Swiss convention uses a regular non-breaking space). For English, apply British English conventions by default unless the text specifies American English.
2. **Read the corresponding reference file** (see table below). **Use the Table of Contents at the top of the file** to quickly locate relevant sections and minimize context usage.
3. **Pass A — Standard grammar.** Before checking BK/CaF rules, perform a full grammatical review using the standard grammar authority for the language:
   - German: Duden Grammatik — check declension (Genitiv, Dativ), case government of verbs and prepositions, agreement, and spelling.
   - French: grammaire française standard (Grevisse/Bescherelle) — check agreements (participe passé, adjectifs), mode/temps, and orthographe.
   - Italian: grammatica italiana standard — check agreement, congiuntivo, use of article.
   - English: standard British English grammar — check subject-verb agreement, tense, article use.
   Grammar errors do **not** require a Rz. For the **Reference** field, cite the standard rule (e.g. "Duden Grammatik — bedürfen régit le génitif").
4. **Pass B — BK/CaF editorial rules.** Apply the Federal Chancellery rules in order: capitalisation → numbers → abbreviations → typography. **Verify each potential error against the reference file before reporting it.** Do not flag an error unless you can locate the exact Rz. (Randziffer) or rule section. If no exact reference is found, do not report the error.
5. **Report corrections** using the mandatory format below. Add a **Type** field to every error to distinguish the two passes: `Grammar` or `BK/CaF`.
6. **Iterative Review Recommendation:** If the text is long (e.g., > 5 pages) or if the number of errors found is high (e.g., > 10-15), explicitly recommend that the user applies the corrections and resubmits the text for a second pass. This ensures that subtle errors aren't missed due to the density of initial issues.

## Mandatory error reporting format

Each reported error **must** be presented as a block of 6 distinct lines (use double newlines or `<br>` to ensure they appear as separate lines in the PDF):

1. **Type:** `Grammar` or `BK/CaF` — identifies which pass found the error.
2. **Location:** Where the error is found (e.g., section title, page number).
3. **Context:** The full sentence containing the error.
4. **Original:** The incorrect passage, wrapped in a red background: `<span style="background-color: #f8d7da; padding: 2px;">[incorrect text]</span>`.
5. **Correction:** The corrected version of that specific passage, with the change highlighted in **bold**.
6. **Reference:** Rule citation and a **brief one-sentence explanation**. For `BK/CaF` errors: exact Rz. number(s). For `Grammar` errors: standard authority (e.g. Duden, Grevisse).

Example (Grammar error):
> **Type:** Grammar
> **Location:** Abschnitt 5 «Vision», Aufzählung
> **Context:** Vision des vertrauenswürdigen und interoperablen Datenökosystem Schweiz
> **Original:** <span style="background-color: #f8d7da; padding: 2px;">Datenökosystem Schweiz</span>
> **Correction:** **Datenökosystems Schweiz**
> **Reference:** Duden Grammatik — Genitiv-s bei Substantiven im Genitiv Singular Neutrum obligatorisch.

Example (BK/CaF error):
> **Type:** BK/CaF
> **Location:** Abschnitt «Einleitung», Seite 2
> **Context:** Der Bundesrat hat heute über die "Corona-Massnahmen" gesprochen.
> **Original:** <span style="background-color: #f8d7da; padding: 2px;">"Corona-Massnahmen"</span>
> **Correction:** **«Corona-Massnahmen»**
> **Reference:** Rz. 202 (Anführungszeichen) — In amtlichen Texten sind die typografischen Anführungszeichen « » zu verwenden.

**Note on High Error Density:** After the report, if many errors were found, add:
> 💡 **Recommendation:** Due to the high number of corrections, it is recommended to apply these changes and resubmit the text for a final verification. This ensures maximum precision by clearing "noise" and allowing a more focused second pass.

⚠️ **BK/CaF errors: if you cannot find the exact Rz., do not report the error.**
⚠️ **Grammar errors: cite the standard grammar authority; do not invent rules.**

## Reference files by language

| Language | File | Note |
|----------|------|------|
| Français | `references/fr.md` | Swiss French (CaF rules) |
| Deutsch  | `references/de.md` | Swiss German (BK Schreibweisungen) |
| Italiano | `references/it.md` | Swiss Italian (Istruzioni CaF) |
| English  | `references/en.md` | British English |

→ **Always read the reference file for the relevant language before processing the text.**

## PDF report generation

After reporting all errors in the chat, generate a PDF correction report:

1. **Create a temporary Markdown file** named `correction_report.md` with this structure (ensure blank lines between each field to force new lines in PDF):

```markdown
# Correction report — [filename] — [date]

---

**Location:** [Section/Page]

**Context:** [Full sentence]

**Original:** <span style="background-color: #f8d7da; padding: 2px;">[Incorrect text]</span>

**Correction:** [Corrected text with **bold fix**]

**Reference:** [Rz. number — Rule name] — [Brief explanation]

---
(Repeat for each error)
```

2. **Convert to PDF** by running:

```bash
pandoc correction_report.md -o correction_report.pdf --pdf-engine=wkhtmltopdf -V geometry:margin=2cm -V lang:[language code]
```

   Replace `[language code]` with `fr`, `de`, `it`, or `en` to match the document language.

3. **Confirm** to the user that `correction_report.pdf` has been created and where it is located. If the PDF conversion fails, leave `correction_report.md` in place and inform the user.

## Rules common to all languages

- Use non-breaking spaces between a number and its unit
- Currency abbreviations follow ISO 4217 (CHF, EUR, USD)
- Introduce any custom abbreviation in parentheses at its first occurrence
