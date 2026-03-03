# Testing Guide for JSON Field Extractor Task

## Prerequisites

Before running the tests, ensure you have the following installed:

1. **Docker**: Download from [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. **uv**: Install using:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   For Windows (PowerShell):
   ```powershell
   powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

3. **Git**: Should already be installed

## Setup

1. Navigate to the repository:
```bash
cd Harbor-Task
```

2. Install Harbor dependencies:
```bash
uv sync
```

## Running Validation Tests

### 1. Oracle Test (Expected Result: 1.0)

This test verifies that the reference solution works correctly.

```bash
uv run harbor run --agent oracle --path harbor_tasks/json-field-extractor --job-name test-oracle
```

**Expected Output**: Score should be **1.0** (100% pass rate)

### 2. NOP Test (Expected Result: 0.0)

This test verifies that the task doesn't auto-pass without a proper solution.

```bash
uv run harbor run --agent nop --path harbor_tasks/json-field-extractor --job-name test-nop
```

**Expected Output**: Score should be **0.0** (0% pass rate)

### 3. Linting Check

Run Ruff linter to check code quality:

```bash
uvx ruff check harbor_tasks/json-field-extractor
```

**Expected Output**: No errors or warnings

## Understanding Test Results

### Oracle Test (1.0 = Success)
- Tests all functionality with the reference solution
- Validates that:
  - Output file is created at `/app/output.json`
  - Output is valid JSON
  - Correct number of records are extracted
  - Only `name` and `email` fields are present
  - Values match the input data

### NOP Test (0.0 = Success)
- Runs without executing any solution
- Ensures the task doesn't pass by default
- Confirms that output validation is working

## Test Cases

The task includes 7 comprehensive test cases:

1. **test_output_file_exists**: Verifies output file creation
2. **test_output_is_valid_json**: Validates JSON format
3. **test_output_has_correct_number_of_records**: Checks record count
4. **test_output_has_only_name_and_email_fields**: Validates field extraction
5. **test_output_preserves_correct_values**: Ensures data accuracy
6. **test_first_record_values**: Validates first record
7. **test_last_record_values**: Validates last record

## Troubleshooting

### Docker Issues
- Ensure Docker Desktop is running
- Check Docker version: `docker --version`
- Try restarting Docker Desktop

### UV Issues
- Verify installation: `uv --version`
- Reinstall if needed using the installation command above

### Harbor Not Found
- Make sure you ran `uv sync` first
- Check that you're in the correct directory

## Manual Testing

You can also manually test the solution:

1. Build the Docker container:
```bash
cd harbor_tasks/json-field-extractor/environment
docker build -t json-extractor-test .
```

2. Run the solution:
```bash
docker run -v $(pwd)/../solution:/solution json-extractor-test bash /solution/solve.sh
```

3. Check the output:
```bash
docker run json-extractor-test cat /app/output.json
```

## Submission Checklist

Before submitting, ensure:

- [ ] Oracle test returns 1.0
- [ ] NOP test returns 0.0
- [ ] Ruff linting passes with no errors
- [ ] Screenshots of test outputs are captured
- [ ] Pull request is created on GitHub
- [ ] Test outputs are included in PR description

## Next Steps

1. Take screenshots of Oracle and NOP test results
2. Create a pull request on GitHub
3. Include test output screenshots in the PR description
4. Submit to: jyoti.sharma@xelron.in & founder@xelron.in

## Support

If you encounter any issues:
- Check the Harbor documentation: [GitHub - laude-institute/harbor](https://github.com/laude-institute/harbor)
- Review existing tasks in the `harbor_tasks/` folder
- Ensure all file paths use absolute paths (`/app/...`)
