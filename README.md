# Harbor Task: JSON Field Extractor

This repository contains a Harbor task implementation for the new hire assignment.

## Task Description

**Task Name**: JSON Field Extractor  
**Difficulty**: Easy  
**Category**: Data Processing

The task requires an agent to read a JSON file containing user records, extract specific fields (name and email), and write the filtered data to an output file.

## Task Structure

```
harbor_tasks/json-field-extractor/
├── task.toml              # Task metadata
├── instruction.md         # Instructions for the agent
├── environment/
│   ├── Dockerfile         # Container setup
│   └── input.json         # Input data file
├── solution/
│   └── solve.sh           # Reference solution
└── tests/
    ├── test.sh            # Test runner
    └── test_outputs.py    # Test cases
```

## Prerequisites

- Docker
- uv (Python package manager)
- Git

## Installation

1. Clone this repository:
```bash
git clone https://github.com/kuruva-radhakrishna/Harbor-Task.git
cd Harbor-Task
```

2. Install dependencies:
```bash
uv sync
```

## Running Tests

### Oracle Test (Expected: 1.0)
Tests that the reference solution works correctly:
```bash
uv run harbor run --agent oracle --path harbor_tasks/json-field-extractor --job-name test-oracle
```

### NOP Test (Expected: 0.0)
Tests that the task doesn't auto-pass without a solution:
```bash
uv run harbor run --agent nop --path harbor_tasks/json-field-extractor --job-name test-nop
```

### Linting
```bash
uvx ruff check harbor_tasks/json-field-extractor
```

## Task Details

### Input
A JSON file at `/app/input.json` with user records containing fields: id, name, email, age, city.

### Output
A JSON file at `/app/output.json` with only name and email fields extracted from each record.

### Example

**Input:**
```json
[
  {
    "id": 1,
    "name": "Alice Smith",
    "email": "alice@example.com",
    "age": 28,
    "city": "New York"
  }
]
```

**Output:**
```json
[
  {
    "name": "Alice Smith",
    "email": "alice@example.com"
  }
]
```

## Author

- **Name**: Kuruva Radhakrishna
- **Email**: kuruvaradhakrishna@gmail.com

## License

This project is part of the Harbor framework by Laude Institute.
