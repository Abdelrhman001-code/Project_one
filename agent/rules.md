Development Rules
This document defines the practical coding and implementation standards for this project. It explains how code should be designed, written, modified, and verified.

AGENTS.md defines the agent's general operating instructions, task boundaries, and required workflow. This document complements those instructions; it does not replace or repeat them.
1. Code Quality
1.1 Readability and maintainability
- Write code that is clear, predictable, and easy for another developer or agent to understand.
- Prefer straightforward solutions over clever, unnecessarily abstract, or overly complicated implementations.
- Keep functions, components, and modules focused on a clear responsibility.
- Break up large functions or components when doing so improves clarity, reuse, or testability. Do not split code into tiny units without a practical benefit.
- Use consistent formatting and follow the conventions already established in the relevant part of the codebase.
1.2 Naming
- Use descriptive, meaningful names for files, folders, variables, functions, components, types, and props.
- Component names should clearly describe the UI element or responsibility they represent.
- Function and variable names should communicate their purpose.
- Avoid vague names such as data, item, value, or temp when a more meaningful name is available. Short generic names are acceptable when their meaning is obvious from a small local context.
- Follow the naming style already used by the project and the language or framework.
1.3 Types and interfaces
- Prefer explicit, accurate types for component props, function parameters, return values, and shared data structures.
- Reuse existing types and interfaces when they accurately represent the required data.
- Keep types aligned with actual runtime behavior.
- Do not use any, unsafe casts, non-null assertions, or type suppression simply to silence a TypeScript error. Use them only when genuinely necessary, keep their scope narrow, and explain non-obvious cases.
- When changing a shared type or interface, identify and update all affected usages within the task's dependency scope.
1.4 Avoid unnecessary complexity
- Do not introduce design patterns, abstractions, configuration layers, or helper utilities without a concrete benefit.
- Do not optimize code prematurely.
- Prefer the simplest implementation that satisfies the requirements while remaining maintainable and consistent with the existing architecture.
2. Project Structure
2.1 Follow the established structure
- Place files in the locations that match their responsibility and the existing project conventions.
- Keep page-specific components and logic close to the page or feature that owns them when that is consistent with the current architecture.
- Place genuinely reusable components, hooks, utilities, types, and other shared resources in the project's established shared locations.
- Do not create new top-level folders, extra nesting levels, or alternative organizational patterns without a clear need.
- Do not move or reorganize existing files as a cleanup activity unrelated to the assigned implementation.
2.2 Responsibility and ownership
- A file should have a clear purpose and an appropriate location.
- Avoid placing unrelated responsibilities in the same file when separating them would make the code materially easier to understand or maintain.
- Avoid creating separate files for trivial code when doing so adds navigation overhead without a meaningful benefit.
- Follow the architecture already present in the relevant feature instead of imposing a different structure.
2.3 Documentation accuracy
- When a code change adds, removes, renames, or moves project files or folders, update agent/structure.md as required by AGENTS.md.
- Keep descriptions factual and aligned with the actual codebase.
3. Components Management
3.1 Component responsibility
- Each component should have a clear, cohesive responsibility.
- Keep components focused. Extract a subcomponent when it has a meaningful independent responsibility, is reused, or its extraction substantially improves readability or maintainability.
- Do not create components solely to wrap a few lines of markup when the wrapper provides no meaningful value.
- Avoid components that combine unrelated UI, data, and business responsibilities.
3.2 Props and component interfaces
- Define clear and appropriately typed props.
- Keep component APIs as small and understandable as practical.
- Use sensible defaults only when they represent valid and intentional behavior.
- Avoid unnecessary props, unclear boolean combinations, and overly configurable components.
- When changing a component's props, parameters, events, or return contract, inspect all usages that may be affected and update the relevant call sites.
3.3 Existing components first
- Before creating a component, inspect whether an existing component already provides the required behavior or can be extended safely.
- Prefer extending an existing component when the new behavior belongs to its responsibility and the extension will not make its API confusing.
- Create a new component when it has a distinct responsibility or when forcing the behavior into an existing component would make that component harder to maintain.
- Do not duplicate an existing component under a different name to avoid understanding or adapting the original.
4. Component Relationships and Dependencies
4.1 Understand dependencies before changing contracts
Before making a change that may affect other code, identify the relevant relationships, including:
- Parent and child components.
- Components that import or render the component being changed.
- Props, parameters, callback functions, and events passed between components.
- Shared hooks, utilities, constants, types, and interfaces.
- Data structures or state used by the affected components.
- Relevant styling, variants, and responsive behavior.
Inspect the relevant dependency chain far enough to understand the impact of the proposed change. Do not scan unrelated areas of the project.
4.2 Keep dependent code compatible
- If a component's props, parameters, exported members, types, or behavior change, update every affected usage within the scope of that dependency change.
- Do not update only the file where the change originated while leaving dependent call sites with obsolete props, parameters, types, or assumptions.
- Check imports, exports, call sites, and related types after changing a shared contract.
- Preserve backward compatibility where practical. If a breaking change is genuinely required, update all affected usages in the relevant dependency scope and verify them.
- Do not change unrelated behavior in dependent components merely because they use the same component or utility.
4.3 Trace the impact
- Follow the dependency chain in both directions where relevant: from the changed component to its consumers, and from the task's entry point to the shared resources it relies on.
- Consider indirect effects, not only direct imports, when shared types, hooks, styles, or state are involved.
- Verify that the affected parts continue to work together after the change.
5. Shared Components and Compatibility
Shared components require special care because a change can affect multiple pages or features.
5.1 When shared changes are allowed
- A shared component or shared resource may be modified when the change is necessary to complete the assigned task correctly.
- A necessary shared change is considered part of the task even if the shared component is also used by other pages or features.
- Do not avoid a necessary shared change if doing so would create duplicated code, an inconsistent implementation, or an incomplete task.
- Do not modify a shared component merely to perform an optional improvement unrelated to the task.
5.2 Update affected consumers
When modifying a shared component, hook, utility, type, interface, or other shared resource:
1. Identify the relevant consumers and usages.
2. Determine which usages are affected by the change.
3. Update those affected usages so they remain compatible.
4. Preserve the existing behavior and appearance of unaffected usages.
5. Verify the affected consumers after the change.
For example, if a shared button's prop name or accepted variant changes, update the relevant usages in Customers, Orders, Dashboard, and any other affected feature. Do not leave old prop names or incompatible values that cause errors.
5.3 The boundary of related changes
- Make the changes required to keep the task and its affected dependencies correct and compatible.
- A page or feature is not automatically in scope just because it uses the same shared component.
- Update another page only to the extent that it is affected by the necessary shared change.
- Do not redesign, refactor, optimize, or fix independent issues in those pages.
- If an unrelated issue is discovered, leave it unchanged and report it separately.
- If a shared change would require broad architectural changes or create substantial risk beyond the task's reasonable scope, explain the impact and request direction before proceeding.
6. Code Reusability and Duplication
6.1 Reuse appropriately
- Reuse existing components, hooks, utilities, functions, and types when they genuinely fit the required behavior.
- Prefer one well-defined implementation of shared behavior over copying the same logic into multiple places.
- Before adding new code, check whether an existing implementation can be reused or safely extended.
6.2 Avoid harmful duplication
- Do not copy and paste substantial blocks of logic or markup when a suitable reusable solution is practical.
- If the same behavior is implemented in multiple places, consider extracting it only when the behavior is genuinely shared and the abstraction improves maintainability.
- Keep feature-specific behavior local when it is not truly shared.
- Do not force unrelated components into one abstraction just because their markup looks similar.
- Do not create generic frameworks or highly configurable components to eliminate small or harmless repetitions.
6.3 Keep abstractions practical
- An abstraction should make code easier to understand, maintain, or reuse.
- Avoid unnecessary layers of wrappers, helpers, hooks, or configuration.
- Prefer clear, explicit code over indirection that makes behavior difficult to trace.
7. UI/UX Development
7.1 Design consistency
- Follow agent/styles.md as the source of truth for the project's visual system.
- Reuse established design tokens, colors, typography, spacing, borders, shadows, radii, and component patterns.
- Maintain a consistent visual language across pages and shared components.
- Do not introduce arbitrary colors, styling values, visual patterns, or design systems when an established project convention exists.
- Do not make visual changes outside the task's relevant UI or necessary dependency scope.
7.2 Responsive behavior
- Build and maintain layouts that work across the screen sizes relevant to the application.
- Avoid fixed dimensions when they cause overflow, clipping, or unusable layouts on smaller screens.
- Check relevant breakpoints after changing layout, spacing, navigation, or component dimensions.
- Ensure content remains readable and controls remain usable on smaller screens.
7.3 States and feedback
Where relevant to the feature, implement and maintain appropriate:
- Loading states.
- Empty states.
- Error states.
- Disabled states.
- Success or confirmation feedback.
- Pending or in-progress states.
These states should be understandable, consistent with the design system, and appropriate to the actual operation. Do not show misleading success feedback or leave users without feedback during meaningful operations.
7.4 Interaction and accessibility
- Interactive elements must perform the action their UI communicates.
- Use appropriate semantic elements and accessible names.
- Ensure controls can be operated in an accessible way, including keyboard interaction where applicable.
- Provide visible focus states consistent with the design system.
- Use suitable labels and descriptions for form controls.
- Do not use a non-interactive element as an interactive control when a semantic interactive element is appropriate.
7.5 Preserve existing experience
- When changing a shared UI component, preserve existing consumers' appearance and behavior unless the task explicitly requires a change.
- New variants or options should not silently alter the default behavior of existing usages.
- Avoid changing unrelated page layouts or interactions.
8. Code Changes and Modification Safety
8.1 Make focused changes
- Modify only the files necessary to implement the task and maintain the compatibility of affected dependencies.
- Prefer small, targeted edits over rewriting entire files.
- Preserve existing code and behavior that are not part of the required change.
- Do not perform unrelated cleanup, formatting sweeps, refactoring, renaming, or architectural changes.
- Do not remove code simply because it appears unused or unnecessary without verifying its role and the task's requirements.
8.2 Preserve existing work
- Treat existing code and uncommitted changes as potentially important work belonging to the user or another agent.
- Inspect the relevant current code before editing it.
- Do not overwrite, revert, discard, or replace existing changes that are not part of the task.
- Avoid whole-file replacement when a targeted edit is sufficient.
- Do not assume that unfamiliar code or code not created by the current agent can be removed.
8.3 Concurrent and overlapping changes
- Be alert to changes made by other agents or developers in files related to the task.
- Preserve unrelated edits when modifying a file that also contains other work.
- Integrate changes carefully rather than replacing the file with an older or independently reconstructed version.
- If concurrent changes conflict with the task, do not silently choose a destructive resolution. Explain the conflict and request direction when safe integration is unclear.
- Do not claim that a conflict was resolved unless the resulting code has been inspected and verified.
8.4 Avoid scope expansion
- A necessary change to a shared dependency and its affected consumers is allowed as described in Sections 4 and 5.
- An independent issue, optional enhancement, or unrelated refactor remains outside the task, even if discovered while working.
- Record unrelated findings for the completion report instead of fixing them without authorization.
9. Error Handling
9.1 Fix causes, not symptoms
- Handle errors at the appropriate layer and address their underlying cause whenever possible.
- Do not hide, suppress, or bypass errors merely to make the code compile or appear to work.
- Do not use empty catch blocks or silently discard failures.
- Do not return fabricated success values or misleading default data after an operation fails.
- Do not add broad fallback behavior unless it is intentional, safe, and appropriate for the feature.
9.2 Use meaningful error handling
- Handle expected failure cases explicitly.
- Provide useful, appropriate feedback to the user when an operation fails.
- Preserve enough error information for debugging without exposing secrets or sensitive internal details to users.
- Keep error handling specific to the operation and avoid swallowing errors that should be handled by a higher layer.
- Avoid logging sensitive information, credentials, tokens, or private customer data.
9.3 Do not bypass quality checks
- Do not use any, @ts-ignore, @ts-nocheck, broad lint-disable comments, or unsafe casts merely to bypass an error.
- Do not weaken validation, remove checks, or change compiler or lint configuration just to make a task pass.
- If a suppression or exception is genuinely necessary, keep it as narrow as possible and document why it is safe.
- Do not treat a warning or error as resolved until its cause has been addressed or its intentional handling has been justified.
9.4 Scope of fixes
- Fix errors introduced by the current changes.
- Fix pre-existing errors when they directly prevent the assigned task from being completed or make the affected task-related code incorrect.
- Do not fix independent errors in unrelated features. Record and report them instead.
- If a required fix extends into a shared dependency, follow the shared-component and dependency rules in Sections 4 and 5.
10. Testing and Verification
10.1 Verify the implementation
After making changes, perform checks appropriate to the task and the project, such as:
- TypeScript type checking.
- Linting.
- Build verification.
- Relevant unit or integration tests.
- Manual UI or interaction checks where available.
- Checking responsive behavior for affected layouts.
Use the project's existing scripts and tooling. Do not invent commands or assume a check exists without inspecting the project configuration.
10.2 Test the affected dependency scope
- Verify the feature or component directly changed by the task.
- When a shared component, prop, type, hook, utility, or interface changes, verify the affected consumers as well.
- Check that existing usages still compile and that their relevant behavior remains intact.
- Test important success, loading, empty, and error paths when they are relevant to the change.
- Focus verification on the task and its affected dependencies, not unrelated parts of the application.
10.3 Report verification accurately
- Run the relevant checks when the environment and available tooling allow it.
- Never claim that a test, lint check, type check, or build passed unless it was actually run and passed.
- Clearly distinguish checks that passed, checks that failed, and checks that could not be run.
- If a check fails, determine whether the failure was caused by the current changes. Fix task-related failures; report unrelated pre-existing failures without expanding the task unnecessarily.
Final Implementation Standard
A task is not complete merely because the requested code has been written. The implementation should:
- Meet the task requirements.
- Follow the project's established conventions and design system.
- Preserve existing functionality.
- Keep shared components and affected consumers compatible.
- Handle relevant errors correctly rather than hiding them.
- Avoid unnecessary duplication and complexity.
- Pass the relevant verification checks, or clearly report why they could not be completed.
These rules govern implementation quality and safe code changes. The task's scope remains limited to the requested work and the related changes necessary to complete it correctly.