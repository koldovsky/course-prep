# Moodle GIFT Format Reference

GIFT (General Import Format Technology) is Moodle's native text-based quiz import format. It's simple, human-readable, and widely supported.

## Basic Syntax

Each question is separated by a blank line. The general pattern is:

```
::Question Title:: Question text {answer specification}
```

## Question Types

### Multiple Choice

```gift
::Capital of France:: What is the capital of France? {
  =Paris
  ~London
  ~Berlin
  ~Madrid
}
```

- `=` marks the correct answer
- `~` marks wrong answers
- You can add feedback after `#`: `=Paris#Correct! Paris has been the capital since...`

### Multiple Choice with Weighted Answers

```gift
::Web Technologies:: Which are front-end technologies? {
  ~%50%HTML
  ~%50%CSS
  ~%-50%Node.js
  ~%-50%PostgreSQL
}
```

- `%50%` means 50% credit for selecting this option
- Negative weights penalize wrong selections

### True/False

```gift
::HTTP Stateless:: HTTP is a stateless protocol. {TRUE}
```

or

```gift
::TCP Connectionless:: TCP is a connectionless protocol. {FALSE#TCP is connection-oriented. UDP is connectionless.}
```

### Short Answer

```gift
::Git Command:: What git command creates a new branch? {
  =git branch
  =git checkout -b
}
```

- Multiple correct answers allowed (each prefixed with `=`)

### Numerical

```gift
::Binary Value:: What is the decimal value of binary 1010? {#10:0}
```

- `#10:0` means the answer is 10 with tolerance of 0

### Matching

```gift
::HTTP Methods:: Match the HTTP method with its purpose. {
  =GET -> Retrieve a resource
  =POST -> Create a resource
  =PUT -> Update a resource
  =DELETE -> Remove a resource
}
```

### Essay (Manual Grading)

```gift
::Design Patterns:: Explain the difference between the Factory and Abstract Factory patterns. {}
```

- Empty braces `{}` indicate an essay question

### Fill in the Blank (Embedded)

```gift
::Variable Types:: In Python, the keyword {=def} is used to define a function.
```

## Special Characters

These characters have special meaning and must be escaped with `\` when used literally in question text:

- `~` `=` `#` `{` `}` `:`

```gift
::Escape Example:: What does the \= operator do in JavaScript? {=assignment}
```

## Comments

Lines starting with `//` are comments:

```gift
// Module 1: Introduction to Python
// These questions cover basic syntax

::First Question:: ...
```

## Category Organization

```gift
$CATEGORY: Module 1/Basic Concepts

::Q1:: First question... {=answer}

$CATEGORY: Module 1/Advanced Topics

::Q2:: Second question... {=answer}
```

## Conversion from Markdown Quiz

When converting from the course's `quiz.md` format:

1. Parse each question from the markdown
2. Determine the question type (MC, T/F, short answer, etc.)
3. Format according to GIFT syntax above
4. Add category headers matching the module structure
5. Escape special characters in question text
6. Save as `.gift.txt` file (plain text with .gift.txt extension)

## Import Instructions for Users

1. Go to Moodle course → Question bank → Import
2. Select "GIFT format"
3. Upload the `.gift.txt` file
4. Review imported questions
5. Add questions to a quiz activity
