# Quick Start: Using OpenClaw Testing Requirements with AI Agents

This guide helps you quickly integrate the OpenClaw Testing Requirements extension into your AI-assisted development workflow.

## TL;DR

Add this to your AI agent's system prompt:

```
You must follow the AI Constitution (v1.0) and OpenClaw Testing Requirements extension (v1.0).

Critical paths require 90% test coverage. Security code requires 100% coverage.
Always identify critical paths before making changes and ensure adequate test coverage.
```

## 5-Minute Setup

### Step 1: Add to AI Agent Configuration

**For GitHub Copilot or similar:**
```markdown
# .github/copilot-instructions.md

This project follows the AI Constitution with OpenClaw Testing Requirements.

Before making code changes:
1. Identify if the change affects a critical path (auth, payments, data processing, etc.)
2. Check existing test coverage for affected code
3. Create or update tests BEFORE implementing changes
4. Ensure critical paths maintain ≥90% coverage, security code has 100%
5. Run tests and report results

See: https://github.com/drewdeal/AI-Constitution/tree/main/extensions
```

**For Custom AI Agents:**
```python
system_prompt = """
You are a software development assistant bound by:
- AI Constitution v1.0
- OpenClaw Testing Requirements Extension v1.0

Key rules:
- Critical paths: auth, payments, core business logic, data changes
- Coverage: 90% minimum for critical paths, 100% for security
- Workflow: Identify → Test → Implement → Verify
- Never remove tests without approval
- Report coverage with every change
"""
```

### Step 2: Define Your Critical Paths

Create `CRITICAL_PATHS.md` in your project root:

```markdown
# Critical Paths for [Your Project]

Per OpenClaw Testing Requirements Extension:

## Authentication & Authorization
- `src/auth/` - All authentication logic (100% coverage required)
- `src/middleware/auth.py` - Authorization checks (100% coverage)

## Payment Processing  
- `src/payments/` - Transaction handling (90% coverage minimum)
- `src/billing/` - Invoice generation (90% coverage)

## Data Management
- `src/models/user.py` - User data operations (90% coverage)
- `src/api/data.py` - Data modification endpoints (90% coverage)

## System Configuration
- `src/config/` - System configuration (90% coverage)
```

### Step 3: Configure CI/CD Check

Add to `.github/workflows/test.yml`:

```yaml
name: Tests (Constitution Compliant)

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run tests with coverage
        run: |
          pytest --cov=src --cov-report=term-missing --cov-report=json
          
      - name: Check critical path coverage
        run: |
          # Check that critical paths meet OpenClaw requirements
          coverage json -o coverage.json
          python .github/scripts/check_coverage.py
          
      - name: Comment PR with coverage
        if: github.event_name == 'pull_request'
        uses: actions/github-script@v6
        with:
          script: |
            const fs = require('fs');
            const coverage = JSON.parse(fs.readFileSync('coverage.json'));
            const summary = `## Test Coverage (OpenClaw Requirements)
            
            Critical Paths Coverage: ${coverage.totals.percent_covered}%
            Required: 90% minimum
            
            ${coverage.totals.percent_covered >= 90 ? '✅' : '❌'} Coverage requirement met`;
            
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: summary
            });
```

### Step 4: First Use Example

**Ask your AI agent:**
```
I need to add a password reset feature. Follow the OpenClaw Testing Requirements extension.
```

**AI Agent Response:**
```
I'll implement password reset following OpenClaw Testing Requirements.

Critical Path Assessment:
- Feature: User authentication (CRITICAL PATH)
- Required coverage: 100% (security-sensitive code)
- Current auth module coverage: 94%

Test-First Approach:
1. First, I'll create tests:
   - test_password_reset_request_valid()
   - test_password_reset_request_invalid_email()
   - test_password_reset_token_expiration()
   - test_password_reset_token_security()
   - test_password_reset_complete_flow()

2. Then implement the feature to pass these tests

3. Finally, verify coverage meets 100% requirement

Proceeding with test creation...
```

## Common Usage Patterns

### Pattern 1: Code Review Request

```
"Review this PR following OpenClaw Testing Requirements"
```

AI will check:
- ✓ Critical paths identified?
- ✓ Tests included?
- ✓ Coverage maintained?
- ✓ Test quality standards met?

### Pattern 2: Legacy Code Improvement

```
"I need to modify [old module]. Help me add tests per OpenClaw requirements first."
```

AI will:
1. Analyze module for critical paths
2. Assess current coverage
3. Recommend tests to add
4. Help create tests before changes

### Pattern 3: New Feature Development

```
"Create [new feature] following TDD and OpenClaw requirements"
```

AI will:
1. Design feature
2. Write tests first
3. Implement to pass tests
4. Verify coverage standards met

## Verification Checklist

Use this checklist to verify your setup:

- [ ] AI agent knows about OpenClaw Testing Requirements
- [ ] Critical paths documented for your project
- [ ] CI/CD checks coverage thresholds
- [ ] Team understands the workflow
- [ ] First feature developed with extension guidance
- [ ] Coverage reports generated and reviewed

## Quick Reference Card

Print this and keep it handy:

```
╔════════════════════════════════════════════════════════════╗
║        OpenClaw Testing Requirements Quick Reference        ║
╠════════════════════════════════════════════════════════════╣
║ CRITICAL PATHS:                                            ║
║  • Authentication/Authorization                            ║
║  • Payment/Financial transactions                          ║
║  • Data modification operations                            ║
║  • Core business logic                                     ║
║  • Configuration changes                                   ║
║                                                            ║
║ COVERAGE REQUIREMENTS:                                     ║
║  • Critical paths: ≥90% line & branch coverage            ║
║  • Security code: 100% coverage                           ║
║  • Error handling: All paths tested                       ║
║                                                            ║
║ WORKFLOW:                                                  ║
║  1. Identify critical paths in scope                      ║
║  2. Check existing test coverage                          ║
║  3. Write tests FIRST (TDD)                               ║
║  4. Implement changes                                     ║
║  5. Verify coverage meets thresholds                      ║
║  6. Run all tests before committing                       ║
║                                                            ║
║ AI AGENT MUST:                                            ║
║  ✓ Report coverage before and after                       ║
║  ✓ Create tests for new critical code                     ║
║  ✓ Never remove tests without approval                    ║
║  ✓ Document coverage gaps                                 ║
╚════════════════════════════════════════════════════════════╝
```

## Troubleshooting

### "AI isn't following the requirements"

Make sure the extension is explicitly mentioned in the system prompt or instructions file.

### "Coverage requirements seem too strict"

You can customize thresholds in your project's config:
```yaml
# .openclaw-config.yaml
coverage_thresholds:
  critical_paths: 85  # Relaxed from 90%
  security_code: 100  # Keep this high!
```

### "Legacy code has low coverage"

Use the testing debt approach:
1. Document current state
2. Set incremental goals
3. Prioritize critical paths
4. Increase coverage over time

## Next Steps

1. Review full extension: `extensions/openclaw-testing-requirements.md`
2. See more examples: `extensions/openclaw-implementation-guide.md`
3. Understand extensions: `extensions/README.md`
4. Read base Constitution: `constitution.md`

## Support

- Extension Issues: https://github.com/drewdeal/AI-Constitution/issues
- Full Documentation: https://github.com/drewdeal/AI-Constitution
- Base Constitution: CC0 Public Domain - use freely!
