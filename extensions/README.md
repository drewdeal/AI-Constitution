# AI Constitution Extensions

This directory contains domain-specific extensions to the AI Constitution. Extensions provide additional rules, constraints, and guidelines for specific use cases while maintaining alignment with the core Constitution's values and principles.

## Available Extensions

### OpenClaw Testing Requirements

**Files:**
- `openclaw-testing-requirements.md` - Complete testing requirements specification
- `openclaw-testing-requirements.yaml` - Machine-readable version
- `openclaw-implementation-guide.md` - Practical examples and integration guide

**Purpose:**
Ensures AI agents working with OpenClaw development workflows maintain adequate test coverage for critical code paths. This extension applies the Constitution's core values (competence, security, honesty) to software testing practices.

**Key Features:**
- Defines critical path criteria
- Specifies coverage thresholds (90% for critical paths, 100% for security code)
- Provides behavioral directives for AI agents
- Includes test quality standards
- Offers integration guidance for CI/CD pipelines

**When to Use:**
- AI agents performing code changes or reviews
- Autonomous coding systems
- CI/CD pipeline enforcement
- Code quality gates
- Developer assistance tools

## Using Extensions

### 1. Choose Relevant Extensions

Select extensions that match your domain and use case:
- Software development → OpenClaw Testing Requirements
- (Future: Healthcare → Medical AI Guidelines)
- (Future: Finance → Financial Services Compliance)

### 2. Integration Approach

Extensions can be integrated in several ways:

**A. System Prompt Integration**
```
You are an AI assistant governed by the AI Constitution v1.0.

Additionally, you must comply with the following extensions:
- OpenClaw Testing Requirements v1.0 (for development tasks)

Core principles:
- Competence: Validate critical functionality is tested
- Security: Untested critical paths are security risks
- Honesty: Report coverage gaps accurately
```

**B. Configuration File**
```yaml
# ai-agent-config.yaml
constitution:
  version: "1.0"
  source: "https://github.com/drewdeal/AI-Constitution"
  
extensions:
  - name: "openclaw-testing-requirements"
    version: "1.0"
    enabled: true
    config:
      critical_path_coverage: 90
      security_code_coverage: 100
      enforce_test_first: true
```

**C. Policy Layer**
```python
from ai_constitution import Constitution, Extension

# Load base constitution
constitution = Constitution.load("constitution.yaml")

# Add extensions
openclaw_testing = Extension.load("extensions/openclaw-testing-requirements.yaml")
constitution.add_extension(openclaw_testing)

# Apply to AI agent
agent = AIAgent(constitution=constitution)
```

### 3. Customization

Extensions are templates. Customize them for your needs:

```yaml
# my-project-openclaw-testing.yaml
extends: "openclaw-testing-requirements.yaml"

# Override thresholds for your project
coverage_thresholds:
  critical_paths:
    minimum_line_coverage: 95  # Stricter than default 90
    minimum_branch_coverage: 95
  
# Add project-specific critical paths
critical_path_definition:
  additional_criteria:
    - "Handles PII data processing"
    - "Integrates with external payment APIs"
```

### 4. Validation

Ensure extensions are properly applied:

1. **Test AI Agent Behavior**: Verify the agent follows extension rules
2. **Monitor Compliance**: Track adherence to extension requirements
3. **Review Outputs**: Check that agents report as specified in extensions
4. **Audit Decisions**: Ensure extension rules influence agent decisions

## Creating New Extensions

To create a new extension:

1. **Follow the Template Structure**:
   - Purpose statement
   - Core principles (aligned with Constitution values)
   - Definitions
   - Requirements and directives
   - Error handling guidance
   - Autonomy constraints
   - Reporting requirements
   - Integration guidelines
   - Version and governance

2. **Align with Constitution**:
   - Reference relevant Constitution sections
   - Maintain consistency with core values
   - Don't contradict red lines or prohibitions
   - Extend, don't replace, core principles

3. **Provide Both Formats**:
   - Markdown (.md) for human readability
   - YAML (.yaml) for machine processing

4. **Include Examples**:
   - Create implementation guides
   - Show practical usage scenarios
   - Provide integration code samples

5. **Document Governance**:
   - Version number
   - Review frequency
   - Change management process
   - Alignment with industry standards

## Extension Principles

All extensions should:

- ✓ **Complement** the base Constitution, not contradict it
- ✓ **Specify** domain-specific requirements clearly
- ✓ **Maintain** alignment with core values
- ✓ **Provide** actionable directives for AI agents
- ✓ **Include** both human and machine-readable formats
- ✓ **Document** rationale and governance

## Examples by Domain

### Software Development (Available)
- OpenClaw Testing Requirements - Ensures adequate test coverage

### Healthcare (Future)
- Medical AI Guidelines - HIPAA compliance, patient safety, clinical decision support

### Finance (Future)
- Financial Services Compliance - Regulatory requirements, risk management, audit trails

### Customer Service (Future)
- Customer Interaction Standards - Privacy, escalation, sentiment handling

### Research (Future)
- Research Ethics Guidelines - Data handling, citation, reproducibility

## Contributing Extensions

To contribute a new extension:

1. Create both .md and .yaml versions
2. Follow the template structure from existing extensions
3. Include an implementation guide with examples
4. Submit a pull request with clear documentation
5. Note: All contributions fall under CC0 Public Domain

## Version Compatibility

Extensions specify which Constitution versions they're compatible with:

```yaml
applies_to_constitution_version: "1.0+"
```

Ensure your Constitution version matches the extension requirements.

## License

All extensions are released under CC0 Public Domain Dedication, matching the base Constitution. Use freely in any project.
