# course-prep

[![skills.sh](https://skills.sh/b/koldovsky/course-prep)](https://skills.sh/koldovsky/course-prep)

A skill for Claude Code that creates complete, professional training courses — from first brief to student-ready deliverables.

## Install

```bash
npx skills add koldovsky/course-prep
```

Or install globally (available across all projects):

```bash
npx skills add koldovsky/course-prep -g -a claude-code
```

## What It Does

Give Claude a topic, audience, and duration. The skill runs a structured, milestone-based workflow that produces:

- **Obsidian-compatible markdown** as the single source of truth
- **PPTX slide decks** for each module
- **PDF handouts** and reading packets
- **Moodle quizzes** in GIFT and XML format
- **Standalone code projects** zipped and ready for students
- **DOCX** editable Word versions
- **XLSX** gradebooks, rubrics, and schedules

Strong focus on IT and programming courses, but works for any subject.

## Three-Stage Pipeline

Every course is organised into three numbered folders so the data-flow direction is unmistakable:

```
course-name/
├── 00-raw/      ← Original inputs: client briefs, research notes, reference PDFs
├── 01-source/   ← Obsidian-compatible markdown — the single source of truth
└── 02-dist/     ← Compiled deliverables: .pptx, .pdf, Moodle imports, code ZIPs
```

**The cardinal rule:** `01-source/` is the only thing you ever edit by hand. Everything in `02-dist/` is regenerated from source — never touched directly.

## Workflow

The skill works in five milestones, stopping for your approval between each one:

| Milestone | Output |
|-----------|--------|
| 1 — Blueprint | Course plan: modules, objectives, audience, tech stack |
| 2 — Module outlines | Detailed breakdown of topics, exercises, timing per module |
| 3 — Source content | Lecture notes, code samples, tasks, and quizzes in `01-source/` |
| 4 — Cross-module review | Course README, references, glossary, consistency pass |
| 5 — Compile outputs | PPTX / PDF / Moodle / DOCX / XLSX into `02-dist/` |

Claude stops after each milestone and presents results for your review before continuing.

## Core Philosophy

Every fact, API, and URL is verified before it goes into the course. No hallucinated library methods. No invented endpoints. When in doubt, search and confirm — or mark it explicitly as unverified.

## Folder Structure (Full)

```
course-name/
├── README.md
│
├── 00-raw/
│   ├── original-outline.md     # Your brief, preserved verbatim
│   ├── research-notes.md       # Web research with source URLs and dates
│   └── references/             # PDFs, screenshots, transcripts
│
├── 01-source/
│   ├── README.md               # Course overview and navigation
│   ├── _blueprint.md           # Milestone 1 output
│   ├── _references.md          # All verified external links
│   ├── _glossary.md
│   │
│   ├── module-01-topic-name/
│   │   ├── lecture.md          # Main teaching content (Obsidian callouts, Mermaid)
│   │   ├── quiz.md
│   │   ├── _quiz-answers.md
│   │   ├── code/               # Standalone, runnable samples with README
│   │   ├── tasks/              # Exercises with starter code and solutions
│   │   └── assets/
│   │
│   └── module-NN-.../ 
│
└── 02-dist/                    # Never edit — always regenerate from 01-source/
    ├── slides/                 # .pptx
    ├── pdf/
    ├── docx/
    ├── moodle/                 # .gift.txt and .xml quiz imports
    └── projects/               # Zipped code projects
```

## Requirements

- [Claude Code](https://claude.ai/code) with the `skills` CLI
- For PPTX output: the [`pptx` skill](https://skills.sh/anthropics/skills/pptx) (auto-used when compiling slides)
- For PDF output: the [`pdf` skill](https://skills.sh/anthropics/skills/pdf)

## Evals

The `evals/` folder contains test cases for validating skill behaviour. Run them with:

```bash
npx skills eval koldovsky/course-prep
```

## License

MIT
