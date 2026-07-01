---
name: prd
description: "Generate a Product Requirements Document (PRD) for a new project, tool, or feature. Use when planning a feature, starting a new project, or when asked to create a PRD. Triggers on: create a prd, write prd for, plan this feature, requirements for, spec out."
user-invocable: true
---

# PRD Generator

Create detailed Product Requirements Documents that are clear, actionable, and suitable for implementation.

---

## The Job

1. Receive a project/tool feature description OR a detailed spec document from the user
2. IF a detailed spec document is NOT provided (only a description of the new item) then FIRST use the grill-me skill to create a comprehensive spec document and save it as a markdown file artifact before proceeding
3. ELSE proceed to step 4
4. Ask critical clarifying questions about the provided or created spec document with a few lettered options to choose the answer (or accept a user provided answer)
4. Generate a structured PRD based on the spec document and answers to the clarifying questions
5. Save to `prd-[project- OR tool- OR feature-name].md`

**Important:** Do NOT start implementing. Just create the PRD.

---

## Step 1: Clarifying Questions

When a spec document is provided OR after you have worked with the user to create one using grill-me, then ask only critical questions where the spec document is ambiguous as to a requirement. Focus on:

- **Problem/Goal:** What problem does this solve?
- **Core Functionality:** What are the key actions?
- **Scope/Boundaries:** What should it NOT do?
- **Success Criteria:** How do we know it's done?

### Format Questions Like This:

```
1. What is the primary goal of this feature?
   A. Improve user onboarding experience
   B. Increase user retention
   C. Reduce support burden
   D. Other: [please specify]

2. Who is the target user?
   A. New users only
   B. Existing users only
   C. All users
   D. Admin users only

3. What is the scope?
   A. Minimal viable version
   B. Full-featured implementation
   C. Just the backend/API
   D. Just the UI
```

This lets users respond with "1A, 2C, 3B" for quick iteration.

---

## Step 2: PRD Structure

Generate the PRD with these sections:

### 1. Introduction/Overview

Brief description of the feature and the problem it solves.

### 2. Goals

Specific, measurable objectives (bullet list).

### 3. Spikes

IF the description or spec document implies a need to research, explore, or experiment to better understand the problem, a Spike is a unit of work to be completed before relevant stories to eliminate unknowns.

Each spike needs:

- **Title:** Short descriptive name
- **Description:** "Investigate [specific_unknown] to understand how to approach implementing [story/stories]"
- **Acceptance Criteria:** Verifiable checklist of the research questions to be answered

Each spike should be small enough to implement in one focused session.

If the project does not already have unit/functional testing capabilities, consider creating a spike to set up the needed framework before starting implementation stories.

**Format:**

```markdown
### SP-001: [Title]

**Description:** Investigate [specific_unknown] to understand how to approach implementing [story/stories].

**Acceptance Criteria:**

- [ ] Specific verifiable research question to answer
  - ADD SUPPORTING INFORMATION/DETAIL/EXPLANATION HERE WHEN COMPLETED
    ...
- [ ] Another related research question
  - ADD SUPPORTING INFORMATION/DETAIL/EXPLANATION HERE WHEN COMPLETED
    ...
```

**Important:**

- Acceptance criteria must be specific, verifiable, research questions, not vague. "Will work" is bad. "Third-party URL structure is consistent, so scraping can be handled via regular expressions" is good.

### 3. User Stories

Each story needs:

- **Title:** Short descriptive name
- **Description:** "As a [user], I want [feature] so that [benefit]"
- **Acceptance Criteria:** Verifiable checklist of what "done" means

Each story should be small enough to implement in one focused session.

**Format:**

```markdown
### US-001: [Title]

**Description:** As a [user], I want [feature] so that [benefit].

**Acceptance Criteria:**

- [ ] Specific verifiable criterion
- [ ] Another criterion
- [ ] Typecheck/lint passes
(If this story involves new or changed code, specify the test type and what it should verify, e.g., `- [ ] Unit test for priority sorting logic passes`)
- [ ] **[Stories with code changes]** Automated tests are added/updated and pass (unit, integration, or e2e as appropriate)
- [ ] **[UI stories only]** Verify in browser using playwright-cli skill
- [ ] **[CLI or terminal stories only]** Verify by running command using bash
```

**Important:**

- Acceptance criteria must be verifiable, not vague. "Works correctly" is bad. "Button shows confirmation dialog before deleting" is good.
- **For any story with UI changes:** Always include "Verify in browser using playwright-cli skill" as acceptance criteria. This ensures visual verification of frontend work.
- **For any story with CLI or terminal changes:** Always include "Verify by running command in shell" as acceptance criteria. This ensures verification of running code.

### 4. Functional Requirements

Numbered list of specific functionalities:

- "FR-1: The system must allow users to..."
- "FR-2: When a user clicks X, the system must..."

Be explicit and unambiguous.

### 5. Non-Goals (Out of Scope)

What this feature will NOT include. Critical for managing scope.

### 6. Design Considerations (Optional)

- UI/UX requirements
- Link to mockups if available
- Relevant existing components to reuse

### 7. Technical Considerations (Optional)

- Known constraints or dependencies
- Integration points with existing systems
- Performance requirements

### 8. Testing Strategy  

High-level plan for automated tests that will validate this feature:

- Unit tests for core logic (functions, utilities, hooks)
- Component tests for UI elements (if applicable)
- Integration/API tests for backend endpoints or services
- End-to-end tests for critical user flows

List the key scenarios that must be covered.

Example:

- Unit test: `priority` field defaults to `'medium'`
- Integration test: endpoint `PATCH /tasks/:id` correctly updates priority
- E2E test: user can filter by priority and see filtered list

### 9. Success Metrics

How will success be measured?

- "Reduce time to complete X by 50%"
- "Increase conversion rate by 10%"

### 10. Open Questions

Remaining questions or areas needing clarification.

---

## Writing for Junior Developers

The PRD reader may be a junior developer or AI agent. Therefore:

- Be explicit and unambiguous
- Avoid jargon or explain it
- Provide enough detail to understand purpose and core logic
- Number requirements for easy reference
- Use concrete examples where helpful

---

## Output

- **Format:** Markdown (`.md`)
- **Filename:** `prd-[feature-name].md` (kebab-case)

---

## Example PRD

```markdown
# PRD: Task Priority System

## Introduction

Add priority levels to tasks so users can focus on what matters most. Tasks can be marked as high, medium, or low priority, with visual indicators and filtering to help users manage their workload effectively.

## Goals

- Allow assigning priority (high/medium/low) to any task
- Provide clear visual differentiation between priority levels
- Enable filtering and sorting by priority
- Default new tasks to medium priority

## User Stories

### US-001: Add priority field to database

**Description:** As a developer, I need to store task priority so it persists across sessions.

**Acceptance Criteria:**

- [ ] Add priority column to tasks table: 'high' | 'medium' | 'low' (default 'medium')
- [ ] Generate and run migration successfully
- [ ] Typecheck passes
- [ ] Unit test verifies default value is 'medium'

### US-002: Display priority indicator on task cards

**Description:** As a user, I want to see task priority at a glance so I know what needs attention first.

**Acceptance Criteria:**

- [ ] Each task card shows colored priority badge (red=high, yellow=medium, gray=low)
- [ ] Priority visible without hovering or clicking
- [ ] Typecheck passes
- [ ] Verify in browser using playwright-cli skill

### US-003: Add priority selector to task edit

**Description:** As a user, I want to change a task's priority when editing it.

**Acceptance Criteria:**

- [ ] Priority dropdown in task edit modal
- [ ] Shows current priority as selected
- [ ] Saves immediately on selection change
- [ ] Typecheck passes
- [ ] Verify in browser using playwright-cli skill

### US-004: Filter tasks by priority

**Description:** As a user, I want to filter the task list to see only high-priority items when I'm focused.

**Acceptance Criteria:**

- [ ] Filter dropdown with options: All | High | Medium | Low
- [ ] Filter persists in URL params
- [ ] Empty state message when no tasks match filter
- [ ] Typecheck passes
- [ ] Verify in browser using playwright-cli skill

## Functional Requirements

- FR-1: Add `priority` field to tasks table ('high' | 'medium' | 'low', default 'medium')
- FR-2: Display colored priority badge on each task card
- FR-3: Include priority selector in task edit modal
- FR-4: Add priority filter dropdown to task list header
- FR-5: Sort by priority within each status column (high to medium to low)

## Non-Goals

- No priority-based notifications or reminders
- No automatic priority assignment based on due date
- No priority inheritance for subtasks

## Technical Considerations

- Reuse existing badge component with color variants
- Filter state managed via URL search params
- Priority stored in database, not computed

## Success Metrics

- Users can change priority in under 2 clicks
- High-priority tasks immediately visible at top of lists
- No regression in task list performance

## Open Questions

- Should priority affect task ordering within a column?
- Should we add keyboard shortcuts for priority changes?
```

---

## Checklist

Before saving the PRD:

- [ ] Asked clarifying questions with lettered options OR verified sufficiently detailed spec was provided
- [ ] Incorporated user's answers, if applicable
- [ ] User stories and spikes are all small and specific
- [ ] Functional requirements are numbered and unambiguous
- [ ] Non-goals section defines clear boundaries
- [ ] Saved to `prd-[feature-name].md`
