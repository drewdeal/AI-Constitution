# OpenClaw Testing Requirements - Implementation Guide

## Overview

This guide demonstrates how to integrate the OpenClaw Testing Requirements extension with the AI Constitution in practical development scenarios.

## Example 1: AI Agent Reviewing Code Changes

### Scenario
An AI agent is asked to add a new user authentication feature to OpenClaw.

### Application of Constitution + Extension

#### Step 1: Critical Path Identification (Pre-Change Assessment)
```
AI Agent: I'm analyzing the request to add a new authentication feature.

According to the OpenClaw Testing Requirements Extension:
- This is a CRITICAL PATH (handles user authentication)
- Requires minimum 90% coverage for critical paths
- Requires 100% coverage for authentication/authorization logic
- Must include security tests

Current test coverage assessment:
- Authentication module: 85% line coverage, 78% branch coverage
- Gaps identified: OAuth flow error handling, token refresh logic
```

#### Step 2: Test-First Approach (Test-First Modifications)
```
AI Agent: Before implementing the new authentication feature, I will:

1. Create unit tests for new authentication methods:
   - test_oauth_login_success()
   - test_oauth_login_invalid_credentials()
   - test_oauth_login_network_failure()
   - test_token_refresh_success()
   - test_token_refresh_expired_token()

2. Create integration tests:
   - test_complete_oauth_flow()
   - test_authentication_with_existing_session()

3. Create security tests:
   - test_prevents_sql_injection_in_login()
   - test_rate_limiting_on_failed_attempts()
   - test_secure_token_storage()
```

#### Step 3: Implementation with Coverage Validation
```
AI Agent: Implementation complete. Running test suite...

Test Results:
✓ 12 new tests added
✓ All tests passing
✓ Authentication module coverage: 96% line, 94% branch
✓ Meets OpenClaw requirement: >90% for critical paths
✓ Security tests verify authorization logic: 100% coverage

Remaining gap:
- Legacy authentication fallback has 82% coverage
- Recommendation: Add tests for edge cases before next release
```

## Example 2: Code Review by AI Agent

### Scenario
A human developer submits a pull request that modifies critical payment processing logic.

### Application of Constitution + Extension

```
AI Agent Code Review:

I'm reviewing PR #123: "Optimize payment processing performance"

⚠️ Critical Path Alert:
This PR modifies payment transaction processing (CRITICAL PATH per OpenClaw extension).

Test Coverage Analysis:
✓ Unit tests added for optimized calculation logic
✓ Performance benchmarks included
✗ MISSING: Integration tests for transaction rollback scenarios
✗ MISSING: Edge case tests for currency conversion errors
✗ Coverage decreased: 94% → 88% for payment processor module

Recommendations per OpenClaw Testing Requirements:
1. Add integration test: test_transaction_rollback_on_payment_failure()
2. Add edge case test: test_currency_conversion_with_invalid_rates()
3. Add regression test: test_maintains_transaction_atomicity()

Risk Assessment:
- HIGH RISK: Untested rollback logic could lead to data inconsistency
- MEDIUM RISK: Uncovered error paths in production could cause financial errors

Action: Requesting changes before approval. Per autonomy constraints,
I cannot approve PRs with decreased coverage on critical paths.
```

## Example 3: Bootstrapping Tests for Legacy Code

### Scenario
OpenClaw project has legacy code with minimal test coverage.

### Application of Constitution + Extension

```
AI Agent: Analyzing request to add feature to legacy module with no tests.

Error Handling Assessment (per Extension):
1. ASSESS: No test infrastructure detected for legacy_payments module
2. GUIDE: Recommend pytest + pytest-cov for Python-based payment module
3. PRIORITIZE: Focus on critical paths first

Proposed Action Plan:
1. Set up testing infrastructure:
   - Install pytest, pytest-cov, pytest-mock
   - Create tests/legacy_payments/ directory
   - Configure coverage reporting

2. Prioritize critical path coverage:
   - Process payment transactions (most critical)
   - Refund processing (medium critical)
   - Report generation (low critical)

3. Implement characterization tests first:
   - Capture current behavior before changes
   - Ensure refactoring doesn't break existing functionality

4. Add feature with tests:
   - Implement new feature with TDD approach
   - Aim for 90% coverage on new code
   
Testing Debt Documentation:
- Legacy module has 15% coverage
- Goal: Increase to 50% this quarter, 90% within 6 months
- Priority: Critical payment paths first
```

## Example 4: Continuous Integration Integration

### Scenario
Setting up CI pipeline for OpenClaw with Constitution-based requirements.

### CI Configuration Example

```yaml
# .github/workflows/openclaw-tests.yml
name: OpenClaw Testing (Constitution Compliance)

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Run Tests
        run: |
          pytest --cov=src --cov-report=term --cov-report=xml
          
      - name: Check Critical Path Coverage
        run: |
          # OpenClaw Extension: Critical paths require 90% coverage
          python scripts/check_critical_coverage.py \
            --min-coverage 90 \
            --critical-paths "auth,payments,data_processing"
            
      - name: Security Test Validation
        run: |
          # OpenClaw Extension: Security code requires 100% coverage
          python scripts/check_security_coverage.py \
            --min-coverage 100 \
            --security-modules "auth"
            
      - name: Report Coverage
        run: |
          echo "## Test Coverage Report" >> $GITHUB_STEP_SUMMARY
          echo "Per OpenClaw Testing Requirements Extension:" >> $GITHUB_STEP_SUMMARY
          coverage report --show-missing >> $GITHUB_STEP_SUMMARY
```

### CI Check Script Example

```python
# scripts/check_critical_coverage.py
"""
Validates test coverage meets OpenClaw Testing Requirements Extension standards.
Aligned with AI Constitution Section 8: Autonomy Constraints.
"""

import sys
import json
from coverage import Coverage

CRITICAL_PATHS = {
    'auth': 100,  # Authentication requires 100% per security-sensitive code rule
    'payments': 90,  # Financial transactions require 90% per critical path rule
    'data_processing': 90,  # Core business logic requires 90%
}

def check_coverage(cov_file, critical_paths):
    """Check if critical paths meet coverage thresholds."""
    failures = []
    
    for module, required_coverage in critical_paths.items():
        actual_coverage = get_module_coverage(cov_file, module)
        
        if actual_coverage < required_coverage:
            failures.append(
                f"❌ {module}: {actual_coverage}% coverage "
                f"(required: {required_coverage}%)"
            )
        else:
            print(f"✓ {module}: {actual_coverage}% coverage (meets requirement)")
    
    if failures:
        print("\nOpenClaw Testing Requirements NOT MET:")
        for failure in failures:
            print(failure)
        print("\nPer AI Constitution Extension: Critical paths must maintain coverage thresholds.")
        sys.exit(1)
    else:
        print("\n✓ All critical paths meet OpenClaw coverage requirements!")
        sys.exit(0)

if __name__ == "__main__":
    check_coverage("coverage.xml", CRITICAL_PATHS)
```

## Example 5: Agent Reporting Template

### Completion Report Format

```markdown
# AI Agent Work Summary

## Task
Implement user password reset functionality

## Constitution Compliance Report

### Critical Path Identification
- Feature Type: Authentication (CRITICAL PATH)
- Required Coverage: 100% (security-sensitive code)

### Test Coverage
- **Before:** 94% line, 91% branch
- **After:** 97% line, 95% branch
- **Delta:** +3% line, +4% branch ✓

### Tests Added
1. `test_password_reset_request_valid_email()` - Unit test
2. `test_password_reset_request_invalid_email()` - Edge case
3. `test_password_reset_token_expiration()` - Security test
4. `test_password_reset_complete_flow()` - Integration test
5. `test_password_reset_rate_limiting()` - Security test

### Coverage Gaps
None identified for new functionality.

Legacy gap remains:
- Account recovery flow: 82% coverage
- Recommendation: Address in future sprint

### Risk Assessment
✓ LOW RISK: All critical paths for new feature are adequately tested
✓ All security-sensitive logic has 100% coverage
✓ Integration tests verify complete workflow
✓ Rate limiting prevents abuse

### Recommendations
1. Consider adding fuzzing tests for password validation
2. Add monitoring for reset request patterns
3. Document password reset flow in security runbook
```

## Key Takeaways

1. **Pre-Change Assessment**: Always identify critical paths before making changes
2. **Test-First Development**: Create tests before implementing features
3. **Coverage Monitoring**: Track and report coverage metrics for critical paths
4. **Risk Communication**: Clearly communicate testing gaps and their implications
5. **Continuous Improvement**: Use testing debt tracking for incremental improvements

## Integration Checklist

- [ ] Add OpenClaw extension to AI agent configuration
- [ ] Define critical paths for your specific codebase
- [ ] Set up coverage tracking infrastructure
- [ ] Configure CI/CD to enforce coverage requirements
- [ ] Train team on Constitution-based development practices
- [ ] Create project-specific coverage thresholds
- [ ] Document testing debt and remediation plans
- [ ] Schedule regular reviews of coverage metrics
