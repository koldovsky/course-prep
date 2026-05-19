---
name: course-prep
description: "Comprehensive course preparation skill for creating full training courses with all materials — syllabi, lecture notes, slides, code samples, projects, quizzes, tasks, and assessments. Works in two phases: first builds Obsidian-compatible markdown source files, then compiles them into output formats (PPTX, PDF, Moodle GIFT/XML, standalone code projects). Especially strong for IT and programming courses but works for any subject. Use this skill whenever the user mentions: course, training, workshop, bootcamp, curriculum, syllabus, lecture, lesson plan, teaching materials, course outline, learning objectives, module, educational content, training program, coding exercises, programming course, tech workshop, or any request to prepare educational/training content. Also trigger when the user wants to create quizzes, assignments, or assessments as part of a structured learning program."
---

# Course Preparation Skill

This skill creates complete, professional training courses through a structured, validated workflow. It produces Obsidian-compatible markdown as the source of truth, then compiles to any requested output format.

## Core Philosophy

Every piece of content must be **traceable and verifiable**. No hallucinated APIs, no invented library methods, no fake URLs. When in doubt, search and confirm. The course creator acts as both author and fact-checker.

## Three-Stage Content Pipeline

The skill organizes every course into **three numbered folders** that make the data flow direction unmistakable:

```
course-name/
├── 00-raw/      ← Original inputs: client briefs, research notes, reference PDFs,
│                  transcripts, screenshots — anything that informed the course.
│                  Preserved verbatim for traceability.
│
├── 01-source/   ← Obsidian-compatible markdown — the single source of truth.
│                  Human-editable. This is where the actual course lives:
│                  lectures, tasks, quizzes, code samples, assets.
│
└── 02-dist/     ← Compiled deliverables: .pptx, .pdf, Moodle imports,
                   zipped code projects. ALWAYS regenerated from 01-source/ —
                   never edit these by hand.
```

**Why numbered folders?** The numbers encode the pipeline direction: raw materials flow into source, source compiles into dist. Anyone opening the course — instructor, student, future you — immediately understands the architecture.

**The cardinal rule:** `01-source/` is the single source of truth. If you want to change the course, edit the source. Outputs in `02-dist/` are disposable — they get rebuilt.

---

## Milestone-Based Workflow

The skill works through milestones. After completing each milestone, **stop and present results to the user for approval** before moving to the next one. Never rush ahead — the user drives the pace.

### Milestone 1: Course Blueprint

**Goal:** Understand what course to build and produce a structured plan.

**Steps:**
1. Create the course folder scaffold immediately — `course-name/00-raw/`, `course-name/01-source/`, `course-name/02-dist/` — and save the user's original request verbatim into `00-raw/original-outline.md` before doing anything else. This preserves the brief exactly as received.

2. Interview the user to gather requirements:
   - Topic and scope (e.g., "Python for beginners", "Advanced React patterns")
   - Target audience and their prerequisites
   - Desired duration (hours/days/weeks) and session length
   - Preferred depth: overview vs. deep-dive
   - Any specific technologies, versions, or frameworks to cover
   - Any existing materials to incorporate
   - Preferred language for the course materials

3. Research the topic using web search to:
   - Find the current stable versions of technologies involved
   - Identify official documentation URLs
   - Understand the standard learning path for this topic
   - Find commonly recommended resources and references
   - Save distilled findings into `00-raw/research-notes.md` with source URLs and the date researched

4. Produce the **Course Blueprint** (`01-source/_blueprint.md`):
   - Course title and description
   - Target audience profile
   - Prerequisites
   - Learning objectives (what students will be able to do after the course)
   - Module breakdown with topics and time allocation
   - Technology stack with exact versions
   - Key references and official docs (verified URLs)

**Approval gate:** Present the blueprint. User reviews module structure, scope, and pacing. Adjust until approved.

---

### Milestone 2: Detailed Module Outlines

**Goal:** For each module, create a detailed outline of content, exercises, and assessments.

**Steps:**
1. For each module, create an outline that includes:
   - Learning objectives for this specific module
   - Key concepts to cover (ordered by teaching sequence)
   - Code demonstrations planned
   - Hands-on exercises / tasks
   - Quiz questions (topics, not yet full text)
   - Estimated timing per section

2. Validate the teaching sequence — concepts should build on each other logically. A student should never encounter a term or technique that wasn't introduced earlier.

3. Cross-check: search official docs to confirm that APIs, methods, and patterns you plan to teach actually exist in the specified version.

**Approval gate:** Present all module outlines. User reviews scope, ordering, and exercise ideas. Adjust until approved.

---

### Milestone 3: Source Content Creation

**Goal:** Write the actual course materials as Obsidian-compatible markdown inside `01-source/`. Each module gets its own folder: `01-source/module-NN-topic-slug/`.

This is the largest milestone. Work through it **one module at a time**, presenting each completed module for review before moving to the next.

**For each module, create:**

1. **Lecture notes** (`lecture.md`) — the main teaching content:
   - Clear explanations with analogies where helpful
   - Code snippets embedded as fenced code blocks with language tags
   - Diagrams described in Mermaid syntax (Obsidian renders these natively)
   - Callout blocks for tips, warnings, and important notes using Obsidian syntax: `> [!tip]`, `> [!warning]`, `> [!info]`
   - Internal links between modules using `[[wikilink]]` syntax
   - All external links verified via web search
   - Speaker/instructor notes in blockquotes or a separate section

2. **Code samples** (`code/` subfolder):
   - Standalone, runnable files — not fragments
   - Include comments explaining what each section does
   - Provide a `README.md` with setup/run instructions
   - If it's a full project, include dependency files (`package.json`, `requirements.txt`, etc.)
   - **Validation:** Write the code, then verify key APIs/methods exist by searching official docs. For critical samples, describe how to test them.

3. **Tasks and exercises** (`tasks/` subfolder):
   - Each task in its own markdown file
   - Clear problem statement, expected outcome, hints
   - Starter code if applicable (as a separate file or embedded)
   - Solution in a collapsible section or separate `_solution` file
   - Difficulty level indicated (beginner / intermediate / advanced)

4. **Quiz** (`quiz.md`):
   - Multiple choice, true/false, short answer, and code-completion questions
   - Answers in a separate collapsible section or `_answers.md` file
   - Questions should test understanding, not memorization
   - Include at least one question that requires applying concepts to a new scenario

**Obsidian formatting conventions:**
- Use YAML frontmatter for metadata: `title`, `module`, `duration`, `objectives`
- Use `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!example]` callout syntax
- Use `\`\`\`language` fenced code blocks
- Use `\`\`\`mermaid` for diagrams
- Use `![[image.png]]` for embedded images and `[[other-file]]` for internal links
- Use `---` horizontal rules to separate major sections

**Validation checklist for each module:**
- [ ] All external URLs verified (search to confirm they resolve)
- [ ] All API/method names confirmed against official docs for the specified version
- [ ] Code samples include correct imports and dependencies
- [ ] No placeholder or invented content — everything is real and specific
- [ ] Teaching sequence is logical — no forward references to unexplained concepts

**Approval gate:** Present each completed module for review. User may request changes before you proceed to the next module.

---

### Milestone 4: Cross-Module Review and Supplementary Materials

**Goal:** Ensure the course is cohesive and complete.

**Steps:**
1. Create a **course README** (`01-source/README.md`) — the main entry point:
   - Course overview and objectives
   - How to navigate the materials
   - Setup instructions (tools, environment)
   - Module index with links

2. Create a **references document** (`01-source/_references.md`):
   - All external links used throughout the course, organized by module
   - Official documentation links
   - Recommended further reading
   - Each link annotated with what it covers and when it was last verified

3. Create a **glossary** (`01-source/_glossary.md`) if the course introduces significant terminology.

4. Review the full course for:
   - Consistent terminology across modules
   - No gaps in the learning path
   - Balanced pacing (no module drastically longer than others without reason)
   - Progressive difficulty curve

**Approval gate:** Present the complete source package. User does a final review of the full course structure.

---

### Milestone 5: Output Compilation (On Request)

**Goal:** Compile the markdown source in `01-source/` into requested output formats, writing results into `02-dist/`.

This milestone is **only executed when the user requests specific outputs**. The source markdown is always the primary deliverable. Never edit files in `02-dist/` by hand — regenerate them from `01-source/`.

**Available output formats:**

| Format | How | Notes |
|--------|-----|-------|
| **PPTX** | Use the `pptx` skill | Output → `02-dist/slides/`. Read pptx SKILL.md first. |
| **PDF** | Use the `pdf` skill | Output → `02-dist/pdf/`. Read pdf SKILL.md first. |
| **DOCX** | Use the `docx` skill | Output → `02-dist/docx/`. Read docx SKILL.md first. |
| **Moodle Quiz (GIFT)** | Convert each `quiz.md` → GIFT | Output → `02-dist/moodle/`. See `references/moodle-gift.md` |
| **Moodle Quiz (XML)** | Convert each `quiz.md` → Moodle XML | Output → `02-dist/moodle/`. See `references/moodle-xml.md` |
| **Code Projects** | Package `code/` folders | Output → `02-dist/projects/` as ZIPs with README |
| **XLSX** | Use the `xlsx` skill | Output → `02-dist/` for gradebooks, schedules, rubrics |

**When compiling to PPTX or PDF, always read the corresponding skill's SKILL.md first** — those skills have specific best practices that significantly improve output quality.

**Compilation rules:**
- Always generate from the current source — never from cached/stale content
- Preserve all code formatting and syntax highlighting where the format supports it
- Include speaker notes in PPTX from the lecture notes' instructor annotations
- Moodle outputs must be tested by describing how to import them

**Approval gate:** Present compiled outputs for review. User verifies formatting and completeness.

---

## Folder Structure

Every course uses the three-stage pipeline layout. The numbered prefixes make the data flow direction unmistakable (raw → source → dist).

```
course-name/
├── README.md                       # Top-level overview + how the three folders relate
│
├── 00-raw/                         # Original inputs — preserved verbatim for traceability
│   ├── README.md                   # What belongs here, what doesn't
│   ├── original-outline.md         # Client brief / user request as received
│   ├── research-notes.md           # Raw findings from web research, with sources
│   ├── references/                 # Reference PDFs, papers, screenshots
│   └── transcripts/                # Interview transcripts, planning call notes
│
├── 01-source/                      # The course itself — Obsidian-compatible markdown
│   ├── README.md                   # Course overview, navigation, setup instructions
│   ├── _blueprint.md               # Course plan (Milestone 1 output)
│   ├── _references.md              # All verified external links used in the course
│   ├── _glossary.md                # Term definitions (if needed)
│   │
│   ├── module-01-topic-name/
│   │   ├── lecture.md              # Main teaching content
│   │   ├── quiz.md                 # Assessment questions
│   │   ├── _quiz-answers.md        # Quiz answers (separate for student version)
│   │   ├── code/
│   │   │   ├── README.md           # Setup and run instructions
│   │   │   ├── example-01.py       # Standalone demos
│   │   │   └── project/            # Full project if applicable
│   │   │       ├── package.json
│   │   │       └── src/
│   │   ├── tasks/
│   │   │   ├── task-01.md          # Exercise with problem statement
│   │   │   └── task-01-solution.md # Solution
│   │   └── assets/
│   │       └── diagram.png         # Generated or referenced images
│   │
│   └── module-02-topic-name/       # Same structure per module
│       └── ...
│
└── 02-dist/                        # Compiled deliverables — always regenerated from source
    ├── README.md                   # Build conventions, never-edit rule
    ├── slides/                     # .pptx decks
    ├── pdf/                        # Printable handouts, reading packets
    ├── docx/                       # Editable Word versions
    ├── moodle/                     # .gift.txt, .xml quiz imports, SCORM packages
    └── projects/                   # Zipped code projects ready for students
```

### When to use each folder

| Folder | Contains | Edit by hand? | Purpose |
|--------|----------|---------------|---------|
| `00-raw/` | Original inputs | Only to add new raw materials | Traceability — "where did that fact come from?" |
| `01-source/` | The course content | **Yes — this is the working document** | The single source of truth |
| `02-dist/` | Compiled outputs | **Never** — always regenerate | Shippable deliverables |

### Pipeline direction

```
00-raw/ ──(inform)──▶ 01-source/ ──(compile)──▶ 02-dist/
```

When the source changes, dist is rebuilt. When the topic shifts (new library version, deprecated API), you re-research into raw, then update source, then rebuild dist. The raw folder is the audit trail; source is the working document; dist is the shipping product.

---

## Validation Strategy

Validation is not optional — it is built into every step. The goal is zero hallucinations in the final materials.

### What to Validate

1. **Technology facts**: Version numbers, API signatures, method names, default behaviors. Always search official documentation before writing about a specific API or feature. If you can't verify it, say so explicitly and mark it with `> [!warning] Unverified` in the source.

2. **URLs and links**: Every external URL must be checked. Use web search to confirm the page exists and contains what you expect. If a link is dead or redirects unexpectedly, find an alternative or note it.

3. **Code samples**: Ensure imports are correct, method signatures match the documented API, and the code would run given the stated dependencies and versions. Describe the expected output. For critical samples, provide test commands.

4. **Conceptual accuracy**: Cross-reference explanations with multiple authoritative sources (official docs, well-known textbooks or references). If sources disagree, note the discrepancy.

5. **Completeness**: Every concept mentioned in a quiz or task must be covered in the lecture content. Every code sample must have its dependencies listed.

### Validation Markers

Use these markers in source files to track verification status:

- `<!-- VERIFIED: description of what was checked, source URL, date -->` — confirmed fact
- `<!-- NEEDS-VERIFICATION: what needs checking -->` — flagged for review
- `> [!warning] Unverified` — visible callout when something couldn't be confirmed

Before presenting any milestone for approval, search for all `NEEDS-VERIFICATION` markers and resolve them.

---

## Handling Different Course Types

### Programming / IT Courses (Primary Focus)
- Emphasize runnable code — every concept should have a working example
- Include environment setup instructions (IDE, runtime, packages)
- Provide both "follow along" snippets in lectures and standalone project files
- Tasks should be coding exercises with clear acceptance criteria
- Use Mermaid diagrams for architecture, flow, and class diagrams

### Conceptual / Theory Courses
- Emphasize diagrams, analogies, and real-world examples
- Tasks focus on analysis, comparison, and design rather than coding
- Quizzes test understanding of principles and tradeoffs

### Mixed Courses (Theory + Practice)
- Balance lecture content between explanation and demonstration
- Tasks progress from conceptual (explain, compare) to practical (implement, debug)

---

## Tips for Quality

- **Teach in order of dependency.** If concept B requires understanding concept A, module A must come first. Verify this during Milestone 2.
- **Use progressive complexity.** Start each module with the simplest useful example, then build complexity. Don't start with the most general/abstract case.
- **Make tasks authentic.** Instead of "write a function that adds two numbers," create scenarios that feel like real problems a developer would face.
- **Include common mistakes.** In lecture notes, mention pitfalls and debugging tips — students learn enormously from "what goes wrong" sections.
- **Keep code DRY across modules.** If later modules build on earlier code, reference it explicitly rather than duplicating it. Use Obsidian wikilinks for this.

---

## Quick Start

When the user asks to create a course, follow this sequence:

1. Create the `00-raw/`, `01-source/`, `02-dist/` scaffold and save the user's brief verbatim into `00-raw/original-outline.md`
2. Ask what they want to teach (topic, audience, duration, depth)
3. Research the topic and save findings into `00-raw/research-notes.md`
4. Present the Course Blueprint (`01-source/_blueprint.md`) → **wait for approval**
5. Create detailed module outlines → **wait for approval**
6. Write source content module by module in `01-source/` → **wait for approval after each module**
7. Cross-module review and supplementary materials in `01-source/` → **wait for approval**
8. Compile to requested output formats into `02-dist/` → **wait for approval**

If the user already has a partial course or specific materials, adapt — skip completed steps, incorporate existing content, and pick up from wherever they are.
