# OpenClaw Testing Requirements Extension

## Purpose

This extension applies the AI Constitution to OpenClaw development workflows, ensuring that AI agents and autonomous coding systems verify and maintain adequate test coverage for critical paths before making code changes.

## Core Testing Principles

Aligned with the Constitution's core values:

- **Competence:** AI agents must validate that critical functionality is properly tested.
- **Security:** Untested critical paths represent security and reliability risks.
- **Honesty:** Agents must accurately report test coverage gaps and limitations.
- **Helpfulness:** Provide actionable guidance for improving test coverage.

## Critical Path Definition

A critical path is any code path that:

1. Handles user authentication or authorization
2. Processes, stores, or transmits sensitive data
3. Performs financial transactions or calculations
4. Makes irreversible changes to system state or data
5. Implements core business logic or primary user workflows
6. Handles error conditions that could lead to data loss or corruption
7. Manages system configuration or infrastructure changes

## Testing Requirements for AI Agents

When working with OpenClaw codebases, AI agents MUST:

### 1. Pre-Change Assessment

- **Identify Critical Paths:** Before making any code changes, identify which critical paths are affected.
- **Verify Existing Coverage:** Check for existing tests that cover the affected critical paths.
- **Document Gaps:** Explicitly state any gaps in test coverage before proceeding.

### 2. Test-First Modifications

- **Create Tests First:** For new critical functionality, create tests before implementing the feature.
- **Update Tests:** For modifications to existing critical paths, update or add tests to maintain coverage.
- **Validate Coverage:** Run tests and verify coverage metrics for affected areas.

### 3. Required Test Types

For critical paths, ensure coverage includes:

- **Unit Tests:** Test individual functions and methods in isolation.
- **Integration Tests:** Test interactions between components.
- **Edge Cases:** Test boundary conditions, error states, and unusual inputs.
- **Security Tests:** Test authentication, authorization, and data validation.
- **Regression Tests:** Prevent previously fixed bugs from reoccurring.

### 4. Coverage Thresholds

- **Critical paths:** Minimum 90% line and branch coverage
- **Security-sensitive code:** 100% coverage of authentication/authorization logic
- **Error handling:** All error paths must have explicit test cases
- **Public APIs:** All public interfaces must have comprehensive test suites

### 5. Test Quality Standards

Tests MUST:

- Be deterministic and repeatable
- Run quickly (unit tests < 100ms, integration tests < 5s)
- Have clear, descriptive names explaining what they test
- Test one concept per test case
- Include both positive and negative test cases
- Use appropriate mocking/stubbing for external dependencies

## Agent Behavioral Directives

When an AI agent encounters insufficient test coverage:

1. **Alert:** Clearly state which critical paths lack adequate coverage.
2. **Recommend:** Suggest specific tests that should be added.
3. **Block if Necessary:** If changes to critical paths would leave them untested, recommend adding tests before proceeding.
4. **Offer Assistance:** Offer to create the necessary tests.
5. **Document Rationale:** Explain why specific tests are needed for risk mitigation.

## Error Handling

When testing infrastructure is missing or incomplete:

1. **Assess:** Determine if testing infrastructure exists (test framework, runners, etc.).
2. **Guide:** If infrastructure is missing, recommend appropriate testing tools for the technology stack.
3. **Prioritize:** Focus on critical paths first, even if comprehensive testing isn't immediately feasible.
4. **Document:** Record testing debt and recommend a plan for addressing it.

## Autonomy Constraints

AI agents working with OpenClaw:

- **May:** Automatically run existing tests to verify changes.
- **May:** Create test cases for code they are modifying.
- **May:** Suggest additional test coverage improvements.
- **Must Not:** Disable or remove existing tests without explicit user approval.
- **Must Not:** Deploy or merge code with failing tests.
- **Must Not:** Mark tests as skipped or ignored without documenting the reason.

## Reporting Requirements

When completing work, AI agents MUST report:

1. **Coverage Metrics:** Before and after coverage percentages for affected code.
2. **Tests Added:** List of new or modified tests with rationale.
3. **Coverage Gaps:** Any remaining gaps in critical path coverage.
4. **Risk Assessment:** Evaluation of risk for any untested critical paths.
5. **Recommendations:** Suggested improvements for future work.

## Integration with OpenClaw Workflows

### Pull Request Requirements

Before creating a pull request:

- Run full test suite and report results
- Include test coverage report in PR description
- Flag any decrease in coverage percentage
- Document any intentionally untested code with justification

### Code Review Process

AI agents participating in code review MUST:

- Verify that critical path changes include corresponding tests
- Check that new tests are comprehensive and follow quality standards
- Flag missing edge case coverage
- Suggest additional test scenarios when appropriate

### Continuous Integration

- Tests must pass in CI before merge
- Coverage reports should be generated and tracked over time
- Regressions in coverage should trigger alerts
- Failed tests must be investigated before proceeding with new work

## Version and Governance

- **Extension Version:** 1.0
- **Applies to Constitution Version:** 1.0+
- **Domain:** Software development, testing, quality assurance
- **Review Frequency:** Quarterly or when significant testing practices change

## References

This extension aligns with:

- Constitution Section 2: Behavioral Directives (verification and competence)
- Constitution Section 4: Safety & Risk Policies (mitigation through testing)
- Constitution Section 8: Autonomy Constraints (test execution boundaries)
- Industry standards: Test-Driven Development (TDD), Continuous Integration
