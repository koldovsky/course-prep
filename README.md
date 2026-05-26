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

The skill works in five milestones. Each milestone runs through a **mandatory independent review gate** before it reaches you for approval:

| Milestone | Output | Review gate target |
|-----------|--------|--------------------|
| 1 — Blueprint | Course plan: modules, objectives, audience, tech stack | `blueprint` |
| 2 — Module outlines | Detailed breakdown of topics, exercises, timing per module | `module-outline` |
| 3 — Source content | Lecture notes, code samples, tasks, and quizzes in `01-source/` | `module` |
| 4 — Cross-module review | Course README, references, glossary, consistency pass | `course-package` |
| 5 — Compile outputs | PPTX / PDF / Moodle / DOCX / XLSX into `02-dist/` | `compiled-output` |

The review gate is the companion [`course-review`](../course-review/) skill — it spawns a clean-context subagent that has not seen the authoring conversation, so it can audit the artifact without bias. Critical findings must be fixed before the milestone is presented to you. See [course-review/README.md](../course-review/README.md) for details.

After the gate passes, Claude stops and presents results (artifact + review verdict) for your approval before continuing.

## Core Philosophy

Every fact, API, and URL is verified before it goes into the course. No hallucinated library methods. No invented endpoints. When in doubt, search and confirm — or mark it explicitly as unverified.

Authoring and reviewing are separate jobs. The agent that writes a lecture cannot reliably audit it — same-context self-review produces motivated reasoning. The companion [`course-review`](../course-review/) skill runs every milestone gate in an independent subagent.

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
