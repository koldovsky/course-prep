# Moodle XML Format Reference

Moodle XML is the most feature-rich quiz import format. It supports all question types, embedded media, feedback, and detailed scoring.

## Basic Structure

```xml
<?xml version="1.0" encoding="UTF-8"?>
<quiz>
  <question type="category">
    <category><text>$course$/Module 1: Introduction</text></category>
  </question>

  <!-- Questions go here -->
</quiz>
```

## Question Types

### Multiple Choice

```xml
<question type="multichoice">
  <name><text>Capital of France</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>What is the capital of France?</p>]]></text>
  </questiontext>
  <defaultgrade>1</defaultgrade>
  <penalty>0.3333333</penalty>
  <single>true</single>
  <shuffleanswers>true</shuffleanswers>
  <answer fraction="100" format="html">
    <text><![CDATA[<p>Paris</p>]]></text>
    <feedback format="html">
      <text><![CDATA[<p>Correct!</p>]]></text>
    </feedback>
  </answer>
  <answer fraction="0" format="html">
    <text><![CDATA[<p>London</p>]]></text>
    <feedback format="html">
      <text><![CDATA[<p>London is the capital of the United Kingdom.</p>]]></text>
    </feedback>
  </answer>
  <answer fraction="0" format="html">
    <text><![CDATA[<p>Berlin</p>]]></text>
  </answer>
</question>
```

- `fraction="100"` = correct answer (100% credit)
- `fraction="0"` = wrong answer
- `<single>true</single>` = single answer; `false` = multiple answers allowed
- `<shuffleanswers>true</shuffleanswers>` = randomize answer order

### True/False

```xml
<question type="truefalse">
  <name><text>HTTP Stateless</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>HTTP is a stateless protocol.</p>]]></text>
  </questiontext>
  <defaultgrade>1</defaultgrade>
  <answer fraction="100" format="plain_text">
    <text>true</text>
    <feedback format="html">
      <text><![CDATA[<p>Correct! Each HTTP request is independent.</p>]]></text>
    </feedback>
  </answer>
  <answer fraction="0" format="plain_text">
    <text>false</text>
    <feedback format="html">
      <text><![CDATA[<p>HTTP is indeed stateless by design.</p>]]></text>
    </feedback>
  </answer>
</question>
```

### Short Answer

```xml
<question type="shortanswer">
  <name><text>Git Branch Command</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>What git command creates a new branch?</p>]]></text>
  </questiontext>
  <defaultgrade>1</defaultgrade>
  <usecase>0</usecase>
  <answer fraction="100" format="plain_text">
    <text>git branch</text>
  </answer>
  <answer fraction="100" format="plain_text">
    <text>git checkout -b</text>
  </answer>
  <answer fraction="50" format="plain_text">
    <text>branch</text>
  </answer>
</question>
```

- `<usecase>0</usecase>` = case-insensitive matching

### Essay

```xml
<question type="essay">
  <name><text>Design Patterns</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>Explain the difference between Factory and Abstract Factory patterns. Provide code examples.</p>]]></text>
  </questiontext>
  <defaultgrade>10</defaultgrade>
  <responseformat>editor</responseformat>
  <responserequired>1</responserequired>
  <responsefieldlines>15</responsefieldlines>
  <graderinfo format="html">
    <text><![CDATA[<p>Look for: clear distinction between the two patterns, correct UML or code, real-world use case.</p>]]></text>
  </graderinfo>
</question>
```

### Matching

```xml
<question type="matching">
  <name><text>HTTP Methods</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>Match each HTTP method with its purpose.</p>]]></text>
  </questiontext>
  <defaultgrade>1</defaultgrade>
  <shuffleanswers>true</shuffleanswers>
  <subquestion format="html">
    <text><![CDATA[<p>GET</p>]]></text>
    <answer><text>Retrieve a resource</text></answer>
  </subquestion>
  <subquestion format="html">
    <text><![CDATA[<p>POST</p>]]></text>
    <answer><text>Create a resource</text></answer>
  </subquestion>
  <subquestion format="html">
    <text><![CDATA[<p>DELETE</p>]]></text>
    <answer><text>Remove a resource</text></answer>
  </subquestion>
</question>
```

### Numerical

```xml
<question type="numerical">
  <name><text>Binary Conversion</text></name>
  <questiontext format="html">
    <text><![CDATA[<p>What is the decimal value of binary 1010?</p>]]></text>
  </questiontext>
  <defaultgrade>1</defaultgrade>
  <answer fraction="100">
    <text>10</text>
    <tolerance>0</tolerance>
  </answer>
</question>
```

### Cloze (Embedded Answers)

```xml
<question type="cloze">
  <name><text>Python Basics</text></name>
  <questiontext format="html">
    <text><![CDATA[
      <p>In Python, the {1:SHORTANSWER:=def} keyword is used to define a function.
      A function that returns nothing implicitly returns {1:MULTICHOICE:=None~True~False~0}.</p>
    ]]></text>
  </questiontext>
  <defaultgrade>2</defaultgrade>
</question>
```

## Embedding Code in Questions

For programming courses, use `<pre><code>` blocks inside CDATA:

```xml
<questiontext format="html">
  <text><![CDATA[
    <p>What will the following code output?</p>
    <pre><code class="language-python">
x = [1, 2, 3]
y = x
y.append(4)
print(len(x))
    </code></pre>
  ]]></text>
</questiontext>
```

## Categories

Use category questions to organize by module:

```xml
<question type="category">
  <category><text>$course$/Module 1: Python Basics/Variables</text></category>
  <info format="html"><text></text></info>
</question>
```

Nested categories use `/` as separator.

## Conversion from Markdown Quiz

When converting from the course's `quiz.md`:

1. Parse the markdown to identify question types and answers
2. Wrap all text content in `<![CDATA[...]]>` to handle special characters
3. Use `format="html"` for rich text (code blocks, formatting)
4. Set appropriate `defaultgrade` values
5. Add feedback where available from the answer explanations
6. Organize into categories matching the module structure
7. Save as `.xml` file

## Import Instructions for Users

1. Go to Moodle course → Question bank → Import
2. Select "Moodle XML format"
3. Upload the `.xml` file
4. Review imported questions and categories
5. Create a quiz activity and add questions from the bank
