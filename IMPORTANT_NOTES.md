# ⚠️ IMPORTANT NOTES - READ BEFORE TESTING

## Prerequisites Installation

### 1. Docker Desktop
**MUST BE RUNNING** before executing any Harbor tests.

- Download: https://www.docker.com/products/docker-desktop
- Install and start Docker Desktop
- Verify: `docker --version`

### 2. UV Package Manager
Install using PowerShell (Windows):
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Or using bash (WSL/Linux/Mac):
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify: `uv --version`

### 3. Harbor CLI
Will be installed automatically when you run `uv sync`

---

## ⚠️ Critical Notes

### Before Running Tests:

1. **Docker Must Be Running**
   - Open Docker Desktop application
   - Wait for it to fully start (green icon)
   - If tests fail with "Cannot connect to Docker daemon", restart Docker

2. **Internet Connection Required**
   - Tests download dependencies
   - First run will take longer (building Docker image)

3. **Disk Space**
   - Ensure at least 2GB free space
   - Docker images will be created

4. **Windows Users**
   - Use PowerShell or Command Prompt (not Git Bash for Harbor commands)
   - WSL2 is recommended but not required

---

## 🚀 Quick Start Commands

### Step 1: Navigate to Repository
```bash
cd c:\Users\HP\Downloads\Placement\Assignments\Prashuu\Harbor-Task
```

### Step 2: Install Dependencies
```bash
uv sync
```
**Expected**: Downloads Harbor CLI and dependencies (~1-2 minutes)

### Step 3: Run Oracle Test
```bash
uv run harbor run --agent oracle --path harbor_tasks/json-field-extractor --job-name test-oracle
```
**Expected Output**: 
- Builds Docker image (first time only, ~2-3 minutes)
- Runs tests
- **Final Score: 1.0** ✅

### Step 4: Run NOP Test
```bash
uv run harbor run --agent nop --path harbor_tasks/json-field-extractor --job-name test-nop
```
**Expected Output**:
- Uses existing Docker image (faster)
- Runs tests without solution
- **Final Score: 0.0** ✅

### Step 5: Run Linting
```bash
uvx ruff check harbor_tasks/json-field-extractor
```
**Expected Output**: No errors or warnings ✅

---

## 🐛 Troubleshooting

### Issue: "Cannot connect to Docker daemon"
**Solution**: 
- Start Docker Desktop
- Wait for it to fully initialize
- Try again

### Issue: "harbor: command not found"
**Solution**:
- Run `uv sync` first
- Use `uv run harbor` instead of just `harbor`

### Issue: "uv: command not found"
**Solution**:
- Reinstall UV using the installation command above
- Restart your terminal
- Check PATH environment variable

### Issue: Docker build timeout
**Solution**:
- Check internet connection
- Increase timeout in task.toml (already set to 300 seconds)
- Clear Docker cache: `docker system prune`

### Issue: Tests fail with "pytest not found"
**Solution**:
- This is expected for NOP test (should score 0.0)
- For Oracle test, check that test.sh uses `uvx` (already configured)

### Issue: Permission denied on Linux/Mac
**Solution**:
- Make scripts executable: `chmod +x harbor_tasks/json-field-extractor/solution/solve.sh`
- Make test.sh executable: `chmod +x harbor_tasks/json-field-extractor/tests/test.sh`

---

## 📸 Screenshot Capture

### What to Capture:

1. **Oracle Test Screenshot**
   - Show the full terminal output
   - Ensure the final score "1.0" is visible
   - Include the command you ran

2. **NOP Test Screenshot**
   - Show the full terminal output
   - Ensure the final score "0.0" is visible
   - Include the command you ran

3. **Linting Screenshot** (optional)
   - Show the command and output
   - Should show no errors

### Screenshot Tips:
- Use full terminal window
- Ensure text is readable
- Include timestamp if possible
- Save as PNG or JPG

---

## ⏱️ Expected Timing

| Task | First Run | Subsequent Runs |
|------|-----------|-----------------|
| `uv sync` | 1-2 minutes | Instant |
| Oracle Test | 3-5 minutes | 30-60 seconds |
| NOP Test | 2-3 minutes | 20-40 seconds |
| Linting | 5-10 seconds | 5-10 seconds |

**Total Time**: ~10-15 minutes for first complete run

---

## ✅ Success Indicators

### Oracle Test Success:
```
✓ test_output_file_exists PASSED
✓ test_output_is_valid_json PASSED
✓ test_output_has_correct_number_of_records PASSED
✓ test_output_has_only_name_and_email_fields PASSED
✓ test_output_preserves_correct_values PASSED
✓ test_first_record_values PASSED
✓ test_last_record_values PASSED

Final Score: 1.0
```

### NOP Test Success:
```
✗ test_output_file_exists FAILED
✗ test_output_is_valid_json FAILED
... (all tests fail)

Final Score: 0.0
```

### Linting Success:
```
All checks passed!
```
or no output at all (means success)

---

## 🔄 If You Need to Rebuild

### Clean Docker Images:
```bash
docker system prune -a
```

### Reinstall Dependencies:
```bash
rm -rf .venv
uv sync
```

### Reset Git (if needed):
```bash
git reset --hard HEAD
git clean -fd
```

---

## 📋 Pre-Submission Checklist

Before creating PR and sending email:

- [ ] Docker Desktop is running
- [ ] `uv sync` completed successfully
- [ ] Oracle test returned 1.0
- [ ] NOP test returned 0.0
- [ ] Linting passed with no errors
- [ ] Screenshots captured and saved
- [ ] Screenshots are clear and readable
- [ ] All commands ran without errors

---

## 🆘 Getting Help

If you encounter issues:

1. Check this document first
2. Review TESTING_GUIDE.md
3. Check Harbor documentation: https://github.com/laude-institute/harbor
4. Verify Docker is running
5. Try restarting Docker Desktop
6. Check internet connection

---

## 📞 Support Contacts

**Submission Email**:
- jyoti.sharma@xelron.in
- founder@xelron.in

**Your Information**:
- Name: Kuruva Radhakrishna
- Email: kuruvaradhakrishna@gmail.com
- GitHub: https://github.com/kuruva-radhakrishna

---

## 🎯 Final Reminder

1. ✅ Ensure Docker is running
2. ✅ Run all three validation commands
3. ✅ Capture screenshots showing scores
4. ✅ Create pull request with screenshots
5. ✅ Send email with PR link and screenshots

**You're ready to validate and submit! Good luck! 🚀**
