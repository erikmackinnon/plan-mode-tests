## Executive Summary

Build a Chrome extension that adds a context-menu item on LinkedIn posts. When activated it captures post text and author metadata, generates a comedic, Sora 2–formatted prompt to create a short spoof video gently trolling the author, and shows it in a modal where the user can copy, tweak, and save prompts. Include guardrails enforcing playful satire tone, configurable intensity, and a prompt history. Provide guidance and hooks for integrating with Sora 2 APIs in the future. Expected outcomes: quick prompt generation, safe usage guardrails, easy export/integration, and a user-friendly UI for editing and history.

## Core Functionalities

- **Context Menu Integration**: Add a Chrome context menu item visible on LinkedIn posts that triggers data capture of post text and author metadata. (Priority: **High**)
- **Prompt Generation Engine**: Generate comedic, Sora 2–formatted prompts from captured post data with configurable intensity and satire guardrails to prevent harassment. (Priority: **High**)
- **Modal UI with Edit & History**: Display generated prompts in a modal allowing copy, tweak, save to history, and adjust intensity; maintain local history of prompts. (Priority: **High**)
- **Sora 2 Integration Hooks**: Provide clear API integration points and example adapters for sending prompts to Sora 2 and handling responses in future integrations. (Priority: **Medium**)
- **Safety & Configuration**: Implement tone guardrails, profanity filters, opt-out lists, and user settings to control prompt intensity and satire boundaries. (Priority: **High**)

## Tech Stack

- **Extensions**: Chrome Extension Manifest V3
- **Frontend**: JavaScript (ES6+), HTML/CSS, Chrome Context Menus API, Content Scripts, chrome.runtime.sendMessage, DOMPurify, Webpack or Vite, Svelte
- **Frontend/Backend**: TypeScript
- **Backend**: Background Service Worker, Sora 2 API (HTTP/REST)
- **Offline Data Storage**: IndexedDB
- **Auth**: OAuth 2.0 / Chrome Identity API
- **Localization**: i18next
- **Testing**: Jest
- **Quality**: ESLint + Prettier
- **User Authentication**: Clerk
- **AI**: OpenAI GPT / Anthropic Claude

## Development Guidelines & Best Practices

Follow these guidelines while implementing the project:

- **Placeholder Images**: Use [Unsplash](https://unsplash.com) or [Picsum Photos](https://picsum.photos) for placeholder images
  - Example: `https://source.unsplash.com/random/800x600?nature`
  - Example: `https://picsum.photos/800/600`
- **Code Quality**: Write clean, maintainable code with proper comments and documentation
- **Testing**: Test each feature thoroughly before marking it as complete
- **Commit Messages**: Use clear, descriptive commit messages that reference the task/story ID
- **Error Handling**: Implement proper error handling and user-friendly error messages
- **Responsive Design**: Ensure all UI components work across mobile, tablet, and desktop devices
- **Accessibility**: Follow WCAG guidelines for accessible UI components
- **Performance**: Optimize images, minimize bundle sizes, and implement lazy loading where appropriate
- **Security**: Never commit API keys or sensitive credentials; use environment variables
- **API & Model Versions**: Always use the latest available APIs and models unless the user explicitly specifies a different version
- **Progress Updates**: Update task checkboxes in real-time as you work through the plan

## Project Timeline

This plan lays out your roadmap in **Milestones**, **Stories** with acceptance criteria, and **Subtasks**. Follow the plan task by task and update progress on milestones, stories, and subtasks immediately as you work on them based on the legend below.

**Progress Legend:**
- `- [ ]` = To-do (not started)
- `- [~]` = In progress (currently working on)
- `- [x]` = Completed (finished)
- `- [/]` = Skipped (not needed)

Tasks are categorized by complexity to guide time estimations: XS, S, M, L, XL, XXL.

### - [ ] **Milestone 1**: **Project setup: design system, CI/CD, env config, extension scaffolding**

- [ ] **Configure Environment** - (S): As a: DevOps engineer, I want to: configure the project environment (variables, runtime, and tooling) So that: the team has a consistent, reproducible setup for development and CI
  - **Acceptance Criteria:**
    - [ ] Environment variables are defined and stored securely
Local and CI environments have identical configurations
Tooling versions (e.g., Node, Python) are pinned and verifiable
Environment bootstrap completes within 10 minutes
Security best practices are enforced (no secrets in code)
- [ ] **Initialize Repository** - (S): As a: developer, I want to: initialize the repository with standard structure, lint rules, and baseline configuration So that: new contributors can start quickly and code quality is maintained
  - **Acceptance Criteria:**
    - [ ] Git repository initialized with main branch
Lint configuration exists and passes on initial run
Baseline code structure (folders, templates) in place
README and contribution guidelines present
CI config skeleton present
- [ ] **Setup CI Pipeline** - (M): As a: DevOps engineer, I want to: set up a CI pipeline with build, test, and deploy steps So that: code changes are automatically validated and deployed where appropriate
  - **Acceptance Criteria:**
    - [ ] CI pipeline triggers on PRs and pushes
Build step runs with defined cached dependencies
Test suite executes and passes
Artifacts produced and stored
Pipeline includes basic failure notifications
- [ ] **Install Dependencies** - (S): As a: developer, I want to: install project dependencies via package manager So that: the project can be built and run locally
  - **Acceptance Criteria:**
    - [ ] Dependency installation completes without errors
Lockfile updated and verified
Local build succeeds
Vendors resolved for all platforms
Offline install fallback tested
- [ ] **Configure Build Tools** - (M): As a: developer, I want to: configure build tooling (bundler, transpiler, linter, formatter) So that: code is compiled consistently and adheres to standards
  - **Acceptance Criteria:**
    - [ ] Build tool versions pinned
Configs for bundling, linting, and formatting present
Build runs locally and in CI without errors
Cache strategy implemented for faster builds
Documentation updated with build tool usage
- [ ] **Dev Environment Setup** - (M): As a: developer, I want to: set up the local development environment with necessary services and mocks So that: developers can run and test features locally
  - **Acceptance Criteria:**
    - [ ] All required services mocked or available (DB, API, cache)
Dev server starts and serves app
Environment variables for local dev present
Debugging and hot-reload works
Documentation for local dev environment available
- [ ] **Design System Init** - (L): As a: designer/developer, I want to: initialize the design system repository with tokens, components, and guidelines So that: UI consistency is achieved across the product
  - **Acceptance Criteria:**
    - [ ] Design tokens defined and published
Component library initialized and documented
Usage guidelines and contribution process documented
Storybook or component explorer set up
CI checks for design system docs

### - [ ] **Milestone 2**: **Core Chrome extension: context menu on LinkedIn, content capture, prompt generation engine, prompt modal UX**

- [ ] **Prompt Modal: Show generated prompt with copy and tweak options** - (XS): As a: product user, I want to: display the generated prompt with copy and tweak controls, So that: I can quickly reuse or adjust prompts in the modal.
  - **Acceptance Criteria:**
    - [ ] The modal shows the generated prompt text by default.
Copy button copies the prompt to clipboard with a single click.
Tweak options open an editable panel allowing on-the-fly modifications.
Copied prompt appears in a transient confirmation toast within 2 seconds.
- [ ] **Prompt Modal: Save and view prompt history** - (M): As a: user, I want to: save prompts and view history, So that: I can reuse past prompts and track changes.
  - **Acceptance Criteria:**
    - [ ] Prompts are saved to user’s history on demand.
History list shows last N prompts with timestamps.
Selecting a history item loads the prompt into the modal for editing.
History persists across sessions when the user is authenticated.
- [ ] **Prompt Modal: Configure satire intensity and guardrails** - (M): As a: user, I want to: configure satire intensity and guardrails, So that: prompts align with brand voice and safety policies.
  - **Acceptance Criteria:**
    - [ ] Users can set satire level on a scale (0-100).
Guardrails toggle enables/disables content filters.
Changing settings updates prompt generation parameters in real time or on submit.
System prevents level values outside allowed range and saves preferences per user.
- [ ] **Prompt Modal: Validate content to prevent harassment** - (L): As a: user, I want to: validate generated content for harassment, So that: the final prompt respects platform guidelines.
  - **Acceptance Criteria:**
    - [ ] Content validation runs before prompt display/export.
Harassment keywords trigger blocking or redaction.
Admins can override validations with audit trail.
Validation results are shown to users with remediation options.
- [ ] **Prompt Modal: Provide Sora 2 integration hooks and export** - (XL): As a: user, I want to: access Sora 2 integration hooks and export prompts, So that: prompts can be integrated into external workflows.
  - **Acceptance Criteria:**
    - [ ] Sora 2 hooks are exposed in a well-documented API surface.
Export functionality supports multiple formats (JSON, plain text).
Export preserves prompt metadata (timestamp, origin, tweaks).
Errors in export are gracefully handled and reported to user.

### - [ ] **Milestone 3**: **Prompt history, dashboard views, and power-user features**

- [ ] **Save Prompt** - (S): As a: product user, I want to: Save a new prompt I created, So that: I can reuse and access it later in Prompt History
  - **Acceptance Criteria:**
    - [ ] User can save a new prompt with title and content
System stores prompt in history repository with timestamp
Saving duplicates is handled gracefully (warn or overwrite)
- [ ] **View History** - (XS): As a: product user, I want to: View my prompt history, So that: I can review and select previous prompts
  - **Acceptance Criteria:**
    - [ ] User can load a list of prompts in history
Each item shows title, timestamp, and brief preview
Selecting an item populates prompt editor or detail view
- [ ] **Tweak Prompt** - (M): As a: product user, I want to: Tweak a prompt from history, So that: I can refine prompts without recreating from scratch
  - **Acceptance Criteria:**
    - [ ] User can edit title/content of a history item
Edits are saved back to history with revision tracking
Unsaved changes warning on navigate away
- [ ] **Delete Prompt** - (S): As a: product user, I want to: Delete a prompt from history, So that: I can remove unwanted prompts and keep history clean
  - **Acceptance Criteria:**
    - [ ] User can delete a prompt with confirmation
System removes prompt from storage and updates history view
Deletion does not affect other prompts
- [ ] **Export Prompt** - (M): As a: product user, I want to: Export a prompt or prompts, So that: I can share or backup prompts externally
  - **Acceptance Criteria:**
    - [ ] User can export single or multiple prompts
Export format supports JSON/CSV
Export includes all relevant metadata (title, timestamp, content)
Export operation is download-only with progress feedback
- [ ] **Prompt Modal & Copy** - (S): As a: dashboard user, I want to: open a prompt modal and copy the content, So that: I can easily reuse prompts in conversations.
  - **Acceptance Criteria:**
    - [ ] Modal opens from Dashboard with accessible focus
Prompt content is selectable and copyable
Copied content matches on-screen prompt
Modal closes without losing focus or data
- [ ] **Prompt History** - (M): As a: dashboard user, I want to: view prompt history, So that: I can reuse or modify previously created prompts.
  - **Acceptance Criteria:**
    - [ ] History list shows last N prompts
Selecting a prompt loads its content into editor
History persists across sessions
Delete/clear history supported with confirmation
- [ ] **Sora Integration Hooks** - (L): As a: dashboard developer, I want to: hook into Sora integration endpoints, So that: I can trigger Sora actions from the dashboard
  - **Acceptance Criteria:**
    - [ ] Endpoint hooks invoked on prompt actions
Payloads match Sora API contracts
Errors are handled gracefully and surfaced
Integration tests cover end-to-end flow
- [ ] **Generate Sora Prompt** - (S): As a: product user, I want to: generate a Sora prompt, So that: I can quickly craft prompts for Sora interactions within the dashboard.
  - **Acceptance Criteria:**
    - [ ] Prompt can be generated with a single action
Generated prompt conforms to allowed Sora syntax
System stores generated prompt in user history for quick reuse
Edge case: prompt generation handles invalid inputs gracefully
- [ ] **Guardrails & Intensity** - (M): As a: dashboard user, I want to: configure guardrails and intensity for prompts, So that: I can control risk and output style.
  - **Acceptance Criteria:**
    - [ ] Guardrail levels (low/medium/high) selectable
Intensity setting affects prompt generation logic
Invalid configurations are rejected with user-friendly errors
Guardrails persist per user or per session

### - [ ] **Milestone 4**: **Settings panel for intensity, tone guardrails, satire controls, and user preferences**

- [ ] **Prompt Intensity** - (S): As a: product admin, I want to: adjust the prompt intensity setting in the Settings Panel, So that: users receive prompts aligned to desired tone and risk level across the platform.
  - **Acceptance Criteria:**
    - [ ] User can access the Prompt Intensity setting from Settings Panel
Setting accepts integer values between 0 and 100
Changes persist across sessions and reloads
- [ ] **Satire Guardrails** - (M): As a: content moderator, I want to: enable Satire Guardrails in Settings Panel, So that: platform content respects safety and brand guidelines without stifling expression.
  - **Acceptance Criteria:**
    - [ ] Toggle to enable/disable Satire Guardrails
Guardrails apply to generated content in real-time or on save
Audit log records enabling/disabling actions with timestamp
Guardrails default to enabled in MVP
- [ ] **Copy & Tweak Modal** - (S): As a: admin, I want to: copy and tweak modal configurations from the Settings Panel, So that: I can quickly clone and customize settings for new workflows without starting from scratch.
  - **Acceptance Criteria:**
    - [ ] Modal configurations can be cloned with a single action
Cloned configs are editable before saving
Clone preserves essential fields and validation rules
Changes do not affect original config unless saved

### - [ ] **Milestone 5**: **Integration hooks for Sora 2 APIs, developer guidance, and integration flows**

- [ ] **Prompt Modal UI** - (M): 
  - **Acceptance Criteria:**
    - [ ] Story functionality is implemented as specified
User interface is responsive and accessible
Data is properly validated and stored
Error handling provides helpful feedback
- [ ] **Guardrails & Config** - (M): 
  - **Acceptance Criteria:**
    - [ ] Story functionality is implemented as specified
User interface is responsive and accessible
Data is properly validated and stored
Error handling provides helpful feedback

### - [ ] **Milestone 6**: **Documentation and deployment: CI/CD, release process, usage docs**

- [ ] **Release Pipeline** - (L): As a: DevOps engineer, I want to: define and automate the release pipeline for deployments to staging and production, So that: releases are repeatable, traceable, and faster.
  - **Acceptance Criteria:**
    - [ ] Release pipeline definition is version-controlled.
Pipeline deploys to staging with at least two validation steps.
Production deployment requires approval gate and can only trigger with successful staging validation.
Rollbacks are configured and can be triggered with one command.
Pipeline logs are persisted and accessible for auditing
- [ ] **SSL & Domain Setup** - (S): As a: System Administrator, I want to: configure SSL certificates and domain bindings for the deployment environments, So that: traffic is secure and the app is reachable under the correct domains.
  - **Acceptance Criteria:**
    - [ ] SSL certificate is issued and installed for all domains
HTTPS redirection enforced
Domain DNS records updated and propagated
Certificate expiry monitoring in place
No mixed content or insecure resources in deployment pages
- [ ] **Monitoring & Logging** - (M): As a: Site Reliability Engineer, I want to: implement monitoring dashboards and centralized logging for deployment environments, So that: system health is observable and issues can be diagnosed quickly.
  - **Acceptance Criteria:**
    - [ ] Metrics collected for CPU, memory, disk, and network are visible in dashboards
Logs are centralized with correlation IDs for tracing
Alerts are configured for threshold breaches
Retention policy defined for logs and dashboards
Artifacts of monitoring configuration are version-controlled

### - [ ] **Milestone 7**: **Maintenance, monitoring, bug fixes, and ongoing support**

- [ ] **Monitor System Health** - (XS): As a: system administrator, I want to: monitor system health metrics (CPU, memory, disk, service status) in real-time, So that: I can detect issues early and maintain service availability
  - **Acceptance Criteria:**
    - [ ] System dashboards show real-time health metrics for all critical services
Alerts trigger when any metric breaches predefined thresholds
Historical data retained for at least 30 days and retrievable
System can run health checks on schedule without impacting performance
- [ ] **Performance Optimization** - (M): As a: platform engineer, I want to: identify and optimize bottlenecks in code paths and queries, So that: I can improve response times and resource utilization
  - **Acceptance Criteria:**
    - [ ] Baseline performance metrics established
Bottlenecks identified and addressed
Performance improvements measurable by predefined targets
Regression tests confirm no new performance regressions
- [ ] **Security Updates** - (S): As a: security administrator, I want to: apply latest security patches and verify patch effectiveness, So that: I can reduce vulnerability exposure and maintain compliance
  - **Acceptance Criteria:**
    - [ ] All critical and high-severity patches applied
Patch verification confirms successful installation on affected components
Rollback plan tested and available
Compliance reports updated after patching
- [ ] **Backup Configuration** - (S): As a: IT administrator, I want to: configure and verify backups (schedules, retention, and restoration tests), So that: I can ensure data resilience and quick recovery
  - **Acceptance Criteria:**
    - [ ] Backup schedules are in place for all critical data
Backups complete successfully and conformance to retention policy
Restoration tests validated with successful recoveries
Notifications sent on backup success/failure
