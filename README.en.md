<div align="center">

# Legal Reference Skills

**Two on-demand skills for contract review, data compliance, and structured analysis**

[简体中文](README.md) · English

[Skills](#skills) · [Install](#install) · [Usage](#usage) · [How it works](#how-it-works) · [Sources and limits](#sources)

</div>

Structured reading notes from two legal reference books: decision steps, conditions and exceptions, evidence prompts, source page references, and chapter navigation. Use them to frame a question, then verify the applicable official rules.

<a id="skills"></a>
## Skills

| Skill | Coverage | Structure |
|---|---|---|
| [`civil-code-contracts`](skills/civil-code-contracts/SKILL.md) | Formation, validity, performance, termination, remedies, and specific contract types | Introduction plus 29 chapters: 30 files |
| [`cyber-data-law`](skills/cyber-data-law/SKILL.md) | Network security, data processing, personal information, appendix rules, and cross-topic analysis | 28 modules |

Each skill contains `SKILL.md`, `chapters/`, `glossary.md`, `patterns.md`, `cheatsheet.md`, `sources.md`, and a public `coverage.json` inventory. The skills refer to one another for data-processing agreements, technical outsourcing, and related questions.

The skill bodies are written in Simplified Mandarin. Bilingual READMEs do not imply that all chapters have been translated.

<a id="install"></a>
## Installation

### Hermes Agent

Copy both directories under `skills/` into the **active profile's** `${HERMES_HOME}/skills/law/`. If `HERMES_HOME` is unset, the default is `~/.hermes/skills/law/`. Back up or compare an existing skill with the same name before replacing it.

```text
<HERMES_HOME>/skills/law/
├── civil-code-contracts/
│   ├── SKILL.md
│   └── ...
└── cyber-data-law/
    ├── SKILL.md
    └── ...
```

The following Bash commands stop if a destination already exists:

```bash
git clone https://github.com/aspiration-Gh/legal-reference-skills.git
python - <<'PY'
import os
import shutil
from pathlib import Path

source = Path('legal-reference-skills/skills')
home = Path(os.environ.get('HERMES_HOME', str(Path.home() / '.hermes')))
target = home / 'skills' / 'law'
names = ('civil-code-contracts', 'cyber-data-law')
for name in names:
    if (target / name).exists():
        raise SystemExit(f'Already exists: {target / name}')
for name in names:
    shutil.copytree(source / name, target / name)
print('Installed both skills.')
PY
```

On Windows, copying through the file manager is also sufficient. In a new session, ask the assistant to list the `law` skills and load a chapter to verify discovery and access.

### Other skill hosts

Copy each complete skill directory into a supported skill location, preserving relative paths. The entry point is `SKILL.md`; discovery depends on the host. Compatibility has not been individually tested on every host.

<a id="usage"></a>
## Usage examples

```text
Use civil-code-contracts to review this service agreement.
Identify missing facts, then examine acceptance, termination, and remedies.
Distinguish book commentary from verified applicable rules.
```

```text
Use cyber-data-law to analyze this SDK collection scenario.
Map the parties, purposes, fields, recipients, and retention periods,
then identify the facts needed for a conditional assessment.
```

```text
Use both skills to review this data-processing agreement.
Analyze contractual responsibility separately from the lawfulness
of the processing activity; contractual permission alone is insufficient.
```

Provide the jurisdiction, key dates, party roles, clauses, and relevant facts. Remove unnecessary personal information before sharing. Without official-source verification, the assistant should label the result as conditional book-based analysis.

<a id="how-it-works"></a>
## How it works

```mermaid
flowchart LR
    A[Question and facts] --> B[Skill entry point and topic routing]
    B --> C[Load relevant chapters and supporting files]
    C --> D[Separate rules, commentary, and applied reasoning]
    D --> E[Verify applicable official texts]
    E --> F[Conditional findings, evidence gaps, and next steps]
```

| Benefit | Mechanism | Current limit |
|---|---|---|
| Topic-oriented reference | Chapter index, glossary, and decision tables | Depends on assistant behavior; not a standalone search service |
| Cross-topic analysis | Reciprocal skill references | Both skills must be discoverable by the host |
| Source traceability | Chapters and source PDF page numbers | Books are not distributed; pagination may differ by edition |
| Historical-rule awareness | Date-sensitive official verification instructions | A workflow requirement, not an automatically updated database |

There is no background service, account binding, or API-key configuration. Official-source research depends on the host's browsing tools; the skills do not call external APIs themselves. The material was built using the [book-to-skill](https://github.com/virgiliojr94/book-to-skill) workflow, with additional distinctions between legal sources, exceptions, and verification limits.

## Validation

Public-copy checks cover file completeness, relative links, an inventory of 58 chapters/modules, public-file hashes, privacy-pattern screening, entry-point format, and known injection-pattern scanning. Discovery and supporting-file loading were verified for the original installed skills in Hermes; the public copy changes the identifiers and source documentation.

These checks do not certify exhaustive OCR accuracy or legal correctness. Internal production logs, installation records, machine paths, credentials, and extracted source texts are not distributed.

<a id="sources"></a>
## Sources and limits

- 《民法典合同编理解与适用》 (abbreviated title; a reference on the Civil Code contract provisions): People's Court Press; postscript dated 2020-07-15, exact edition unconfirmed. See [contract sources](skills/civil-code-contracts/sources.md).
- 《网络安全法、数据安全法、个人信息保护法一本通》 (a reference on network security, data security, and personal information rules): first edition, October 2021; ISBN `978-7-5216-2233-1`. See [data-compliance sources](skills/cyber-data-law/sources.md).

**Neither source-book PDF is uploaded or provided here.** Obtain a lawful edition through a bookstore or library. This public copy uses abbreviated titles and institution names and omits country names. This does not change the territorial scope of the original rules or make them universally applicable. Confirm full titles, editions, and jurisdiction before citation or practical use.

Historical rules, interpretive disagreements, and OCR uncertainties remain marked. This is not a comprehensive update to current law. For real matters, verify applicable legislation, judicial interpretations, effective dates, repeals, and transitional arrangements. The material is not individualized legal advice.

Public availability does not grant a redistribution license for the books or third-party material. No additional open-source license is specified in this release. See [RIGHTS.md](RIGHTS.md).
