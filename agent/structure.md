
This document will serve as the central reference for the project's current file structure, target architecture, and file organization conventions.

Understand their responsibilities and avoid duplicating their content.

## 2. Inspect the Actual Project Structure

Document only files and folders that actually exist.

Do not assume that a file or directory exists simply because it is mentioned in another document.

## 3. Create agent/structure.md

Organize the document into three main sections.

### Part 1: Current Project Structure

Document the actual project structure as it exists at the time of inspection.

Project/
│
├── AGENTS.md
│
└── agent/
    ├── rules.md
    ├── project.md
    ├── structure.md
    └── styles.md


This section must be updated whenever project files or directories are added, removed, renamed, or moved.

Never include planned or nonexistent files in this section.

### Part 2: Target Project Architecture

Define the intended organizational architecture for future development.

The architecture must follow these principles:

**A. Feature-Based Frontend Architecture**

- Organize application features independently.
- Each feature should own its relevant UI components.
- Keep feature-specific components inside their respective feature directories.
- Organize feature-specific hooks and types close to the feature that owns them.
- Avoid mixing unrelated features.
- Extract genuinely reusable components into shared locations.

**B. Component Organization**

- Each component should have a clear and independent responsibility.
- Keep components focused and maintainable.
- Separate meaningful subcomponents when appropriate.
- Avoid unnecessary component splitting.
- Distinguish between feature-specific components and globally shared components.

**C. Frontend and Backend Separation**

The frontend is strictly responsible for presentation and user interaction.

It must not directly implement:

- Database operations.
- Business logic.
- Backend processing.
- Data manipulation that belongs to backend business rules.
- Direct database access.

The frontend communicates with backend functionality through the approved backend interfaces.

**D. Centralized Backend Ownership**

The Supervisor Agent is the sole owner of backend development and implementation.

Its responsibilities include:

- Database schema and architecture.
- Database migrations.
- Supabase Edge Functions.
- Backend business logic.
- CRUD operations.
- Authentication and authorization.
- Data validation and security.
- Row Level Security (RLS).
- Storage operations.
- External integrations.
- Backend-related shared utilities and types.

Other agents must not independently create or modify backend implementations.

The backend architecture should be organized around Supabase and its Edge Functions without introducing unnecessary architectural layers or duplicate backend locations.

**E. Supabase Organization**

Account for the project's Supabase infrastructure, including:

- Edge Functions.
- Database migrations.
- Database-related configuration.
- Shared backend functionality where appropriate.

Keep Supabase-related files in their appropriate locations and follow the established Supabase conventions.

Do not invent additional infrastructure or duplicate Supabase functionality.

### Part 3: Structure Organization Rules

Define practical rules governing how all agents must organize future files.

Include rules covering:

1. Where new pages and routes should be created.
2. Where feature-specific components belong.
3. Where shared UI components belong.
4. How feature-specific hooks and types should be organized.
5. How backend files are organized and who owns them.
6. How Supabase Edge Functions and migrations are organized.
7. When a component should be extracted into an independent component.
8. When shared components should be reused.
9. How to avoid unnecessary folders and excessive nesting.
10. How to maintain consistency with the target architecture.

## 4. Important Architectural Rules

The following rules are mandatory:

- Current Project Structure represents reality, not future plans.