# Invergent

**Think wider. Decide better.**

Invergent is an experimental web-based toolkit for exploring and practicing three complementary movements of thinking:

- **Divergent thinking** — expanding the possibility space.
- **Convergent thinking** — narrowing possibilities into a reasoned direction.
- **Switching** — deliberately moving from exploration to selection and back again when needed.

The project is intentionally lightweight, browser-based, and data-driven.

> **Divergence creates possibilities.  
> Convergence creates direction.  
> Invergent connects the two.**

## What is Invergent?

Invergent is built around a simple idea:

> Good problem solving is not only about generating many ideas or choosing quickly. It is also about knowing **when to open the search space and when to close it**.

The project currently has two main experiences.

### Profile

**profile.html**

A short heuristic experiment that explores a user's tendencies across:

- Divergence
- Convergence
- Flexibility across domains
- Switching between exploration and selection

The result is presented as an experimental profile such as **Explorer**, **Optimizer**, **Integrator**, or **Flexible Searcher**.

The profile is **not a clinical diagnosis and is not a validated psychometric instrument**. It is an experimental framework intended for reflection, learning, and further development.

### Learn

**learn.html**

A practice lab for deliberately exercising:

- Divergent thinking
- Convergent thinking
- Switching between the two

The learning session provides prompts, timers, immediate feedback, and a lightweight session summary.

## Data-Driven Architecture

Questions and exercises are **not hard-coded into the HTML pages**.

They live in:

~~~text
data.json
~~~

Both profile.html and learn.html load their content dynamically from this file.

This means you can add, remove, or revise questions without rewriting the application's UI code.

### Repository structure

~~~text
invergent/
├── index.html       # Landing page
├── profile.html     # Heuristic thinking profile
├── learn.html       # Thinking practice lab
├── data.json        # Question and exercise bank
├── README.md        # Project documentation
└── LICENSE          # GNU AGPL v3.0
~~~

## Adding a Profile Question

Add a new object to:

~~~text
data.json
~~~

inside:

~~~json
{
  "profile": {
    "tasks": []
  }
}
~~~

Example:

~~~json
{
  "id": "d7",
  "type": "divergent",
  "seconds": 60,
  "question": "What else could a public library become?",
  "hint": "Generate distinct possibilities.",
  "input": "textarea",
  "placeholder": "One idea per line…",
  "scoring": {
    "method": "divergent_text",
    "dimension": "divergence",
    "maxIdeas": 14
  }
}
~~~

A convergent question can use multiple-choice options:

~~~json
{
  "id": "c7",
  "type": "convergent",
  "seconds": 45,
  "question": "Which option should be tested first?",
  "hint": "Use the stated constraints.",
  "input": "choice",
  "choices": [
    {
      "id": "A",
      "title": "Option A",
      "description": "Description of option A."
    },
    {
      "id": "B",
      "title": "Option B",
      "description": "Description of option B."
    }
  ],
  "answer": "B",
  "scoring": {
    "method": "choice",
    "dimension": "convergence"
  }
}
~~~

### Switching exercises

Switching tasks ask the user to **generate first and choose later**.

Example:

~~~json
{
  "id": "s3",
  "type": "switching",
  "seconds": 90,
  "question": "Generate several ways to reuse an empty building, then choose one to test.",
  "hint": "Explore first. Put your final decision on a new line beginning with “FINAL:”.",
  "input": "textarea",
  "placeholder": "Ideas first…\n\nFINAL: …",
  "scoring": {
    "method": "switch_text",
    "dimension": "switching",
    "maxIdeas": 8,
    "finalMarker": "FINAL:"
  }
}
~~~

## Adding a Learning Exercise

Add an object inside:

~~~json
{
  "learn": {
    "exercises": []
  }
}
~~~

Learning exercises support the same three thinking modes.

### Divergent exercise

~~~json
{
  "id": "d4",
  "type": "divergent",
  "seconds": 60,
  "title": "Change the frame.",
  "hint": "Try several perspectives.",
  "prompt": "How else could this public space be used?",
  "input": "textarea",
  "placeholder": "One idea per line…",
  "chips": [
    "education",
    "art",
    "community",
    "business"
  ],
  "feedback": {
    "low": "Try another perspective.",
    "mid": "Push into a different domain.",
    "high": "Good divergence."
  }
}
~~~

### Convergent exercise

~~~json
{
  "id": "c4",
  "type": "convergent",
  "seconds": 45,
  "title": "Choose under constraints.",
  "hint": "Compare the trade-offs.",
  "prompt": "Which option should be tested first?",
  "input": "choice",
  "choices": [],
  "answer": "B",
  "criteria": [
    ["Value", "What matters most?"],
    ["Risk", "What could fail?"],
    ["Effort", "What can be implemented?"]
  ]
}
~~~

## Design Principles

### 1. Separate exploration from evaluation

During a divergent task, quantity and variety are encouraged before judgment.

During a convergent task, the focus shifts to criteria, evidence, constraints, and trade-offs.

### 2. Make the transition visible

The switching exercises explicitly separate:

~~~text
EXPLORE
   ↓
EXPAND
   ↓
COMPARE
   ↓
SELECT
   ↓
BUILD
~~~

### 3. Keep the system editable

The question bank should be easy to extend without changing application logic.

### 4. Keep the prototype honest

Invergent uses heuristic scoring and should not be presented as a validated psychological or clinical assessment.

## Running Locally

Because the pages load data.json with fetch(), use a local HTTP server rather than opening the HTML files directly with file://.

For example:

~~~bash
python -m http.server 8000
~~~

Then open:

~~~text
http://localhost:8000/
~~~

## GitHub Pages

The project is designed to work as a static site.

Once GitHub Pages is enabled for the repository, the application can run without a backend.

The application stores the question bank in the repository itself, making content updates as simple as updating data.json.

## Roadmap Ideas

Possible future directions include:

- More question categories and difficulty levels
- Domain-specific practice packs
- Randomized question selection
- Multiple languages
- Personal practice history
- Progress tracking
- Question tagging and filtering
- Authoring tools for building question banks
- More sophisticated heuristic scoring
- Research mode for experimenting with alternative scoring models

## Contributing

Contributions are welcome.

The easiest way to contribute is to add or improve questions in data.json, while keeping the existing schema and avoiding claims that imply clinical or psychometric validity.

For code changes, keep the project dependency-light and preserve the static, browser-first architecture where practical.

## License

Invergent is licensed under the **GNU Affero General Public License v3.0**.

See [LICENSE](LICENSE).

## Author

Created by **Angga Conni Saputra**.

---

**Invergent is an experiment in thinking about thinking.**
