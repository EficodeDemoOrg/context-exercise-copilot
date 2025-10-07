---
mode: Initializer
description: "Enhance basic CONSTITUTION.md with comprehensive software engineering practices and standards"
---
Transform the minimal CONSTITUTION.md into a comprehensive project charter with industry best practices.

⚠️ **REQUIRED CONTEXT**: User must attach existing `CONSTITUTION.md`

⚠️ **MANDATORY TOOL**: You MUST use the #todo tool to track the enrichment process through all phases.

**Before starting, create your TODO list:**
```
#todo
- [ ] Phase 1: Analyze existing CONSTITUTION.md
- [ ] Phase 2: Generate comprehensive enhancements (10 sections)
- [ ] Phase 3: Present proposal to user
- [ ] Phase 4: Integrate approved changes
- [ ] Verify enhanced CONSTITUTION.md is complete
```

# PHASE 1: ANALYZE EXISTING CONSTITUTION

Read the current CONSTITUTION.md and extract:
- Primary language and framework
- Database/storage choices
- Architecture pattern
- API approach
- State management
- Testing strategy
- Version control workflow
- CI/CD platform
- Deployment target
- Container strategy
- Monitoring approach

# PHASE 2: GENERATE COMPREHENSIVE ENHANCEMENT

Based on the technical stack, research and apply best practices to create a complete constitution.

## Required Sections to Add:

### 1. Coding Standards
Based on [language] and [framework], define:
- **Naming Conventions**
  - Variables: [camelCase/snake_case/etc.]
  - Functions/Methods: [pattern]
  - Classes/Components: [pattern]
  - Files and directories: [pattern]
  - Constants: [UPPER_SNAKE_CASE/etc.]

- **File Organization**
  ```
  src/
  ├── components/     [UI components]
  ├── features/       [Feature modules]
  ├── services/       [API/external services]
  ├── utils/          [Shared utilities]
  └── types/          [TypeScript definitions]
  ```

- **Import Order**
  1. External dependencies
  2. Internal modules
  3. Local components
  4. Styles
  5. Types

### 2. Error Handling & Logging

- **Error Response Format**
  ```json
  {
    "error": {
      "code": "SPECIFIC_ERROR_CODE",
      "message": "User-friendly message",
      "details": {},
      "timestamp": "ISO-8601"
    }
  }
  ```

- **Logging Levels**
  - ERROR: System failures requiring immediate attention
  - WARN: Recoverable issues, degraded performance
  - INFO: Important business events
  - DEBUG: Detailed diagnostic information

- **Error Boundaries** (for React/similar)
  - Global error boundary at app level
  - Feature-level boundaries for isolation
  
### 3. Security Practices

- **Authentication Pattern**: [JWT/OAuth2/Session-based]
- **Authorization**: Role-based access control (RBAC)
- **Input Validation**: All user inputs validated at entry point
- **Secrets Management**: Environment variables, never in code
- **API Security Headers**: CORS, CSP, rate limiting

### 4. Data Management

- **Database Patterns**
  - Migrations: Version controlled, sequential
  - Query optimization: Indexed foreign keys, pagination
  - Connection pooling: [specific limits]
  
- **State Management Rules** (based on chosen approach)
  - Global state: [What belongs there]
  - Local state: [Component-specific data]
  - Derived state: Computed, not stored

### 5. Testing Standards

- **Test Structure**
  ```
  describe('[Component/Function]', () => {
    it('should [expected behavior]', () => {
      // Arrange
      // Act
      // Assert
    });
  });
  ```

- **Coverage Requirements**
  - Unit tests: Critical business logic
  - Integration tests: API endpoints, data flows
  - E2E tests: Critical user journeys

- **Mocking Strategy**
  - External services: Always mocked in unit tests
  - Database: In-memory for integration tests

### 6. Performance Guidelines

- **Frontend**
  - Bundle size: Max [X]KB initial load
  - Lazy loading: Routes and heavy components
  - Image optimization: WebP with fallbacks
  
- **Backend**
  - Response time: 95th percentile < 500ms
  - Database queries: Maximum N+1 prevention
  - Caching: Redis/in-memory for frequent reads

### 7. Development Workflow

- **Branch Naming**
  - Features: `feature/[ticket-id]-brief-description`
  - Fixes: `fix/[ticket-id]-brief-description`
  - Hotfixes: `hotfix/[severity]-brief-description`

- **Commit Message Format**
  ```
  type(scope): subject
  
  body (optional)
  
  footer (optional)
  ```
  Types: feat, fix, docs, style, refactor, test, chore

- **Pull Request Standards**
  - Template required
  - Minimum 1 reviewer
  - All CI checks must pass
  - Squash merge strategy

### 8. Documentation Requirements

- **Code Documentation**
  - Public APIs: JSDoc/docstrings required
  - Complex logic: Inline comments explaining "why"
  - README per feature module

- **Architecture Decision Records (ADRs)**
  - Significant technical decisions documented
  - Located in `docs/ADR/`
  - Follow provided template

### 9. Operational Standards

- **Monitoring**
  - APM: [Tool based on deployment target]
  - Error tracking: [Sentry/similar]
  - Metrics: Business KPIs + technical health

- **Deployment**
  - Zero-downtime deployments
  - Rollback capability within 5 minutes
  - Feature flags for gradual rollout

### 10. Dependency Management

- **Adding Dependencies**
  - Justify need in PR description
  - Check license compatibility
  - Review security advisories
  - Prefer well-maintained packages (recent updates, many contributors)

- **Update Schedule**
  - Security patches: Immediate
  - Minor updates: Monthly
  - Major updates: Quarterly evaluation

# PHASE 3: PRESENT PROPOSAL

Generate summary:

```markdown
## 📋 CONSTITUTION ENHANCEMENT SUMMARY

I've prepared a comprehensive constitution based on your technical stack:
- **Language**: [extracted]
- **Framework**: [extracted]
- **Architecture**: [extracted]

### Key Additions Proposed:

**Coding Standards**
• [Naming convention choice] for consistency
• [File structure pattern] for organization
• [Import ordering] for readability

**Error Handling**
• Standardized error format across all APIs
• [Logging strategy] with clear levels
• Error boundary implementation

**Security**
• [Auth pattern] implementation
• Input validation at all entry points
• Environment-based secrets management

**Testing**
• [Test structure] for all test types
• Focus on [critical areas]
• [Coverage strategy]

**Performance**
• [Specific metrics] for response times
• [Caching strategy] for optimization
• [Bundle/query optimization]

**Workflow**
• [Branch strategy] with clear naming
• [Commit format] for history clarity
• [PR requirements] for quality

**Documentation**
• ADR process for decisions
• API documentation requirements
• Inline comment standards

### Dependencies I May Introduce:
• [Testing framework] - for test execution
• [Linting tools] - for code quality
• [Type checking] - for type safety
• [Build tools] - for optimization

This enhanced constitution will:
✅ Provide clear guidelines for all developers
✅ Ensure consistency across the codebase
✅ Establish quality gates and standards
✅ Define operational excellence criteria

Would you like me to:
1. Apply ALL enhancements as proposed
2. Modify specific sections (please specify)
3. Remove certain sections (please specify)

Please review and provide your decision.
```

# PHASE 4: HANDLE USER FEEDBACK

## If user says "Apply all" or "1":
- Generate complete enhanced CONSTITUTION.md
- Overwrite existing file
- Confirm: "✅ CONSTITUTION.md enhanced with comprehensive standards"

## If user requests modifications:
- Ask: "Which sections need adjustment and what changes would you like?"
- Wait for specific feedback
- Regenerate those sections
- Present updated summary

## If user wants sections removed:
- Ask: "Which sections should I exclude?"
- Remove specified sections
- Present trimmed version

# PHASE 5: FINALIZE

After applying changes:

```markdown
## ✅ CONSTITUTION ENHANCED

Your CONSTITUTION.md now includes:
- [List of all sections included]

This comprehensive constitution will guide:
• The Architect in design decisions
• The Lead Developer in task creation
• The Implementer in code standards
• All future contributors in project practices

⚠️ **IMPORTANT**: Please review the complete CONSTITUTION.md to ensure it aligns with your project vision. This document will be the foundation for all subsequent development.

The enhanced constitution is ready for use by all downstream agents.
```

# ERROR HANDLERS

## If no CONSTITUTION.md provided:
```
❌ Cannot proceed without existing CONSTITUTION.md
Please first run /init_project to create the basic constitution.
```

## If CONSTITUTION.md is incomplete:
```
⚠️ The provided CONSTITUTION.md appears incomplete.
Missing: [list missing sections]

Should I:
1. Proceed with available information
2. Wait for complete constitution
```