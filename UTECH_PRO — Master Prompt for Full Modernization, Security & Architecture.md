# UTECH_PRO — FULL PROJECT MODERNIZATION MASTER PROMPT

You are working on my existing project **UTECH_PRO**.

Repository:
https://github.com/jonibak2/UTECH_PRO

Your job is NOT simply to rewrite the existing HTML into React.

Your job is to act as a **senior software architect, security engineer, frontend engineer, backend/database engineer, UX/UI designer, and DevOps engineer** and help me transform this project into a properly engineered production-quality application.

---

# 1. PROJECT CONTEXT

UTECH_PRO is an internal web application used by a small company called UTECH.

The application is used by employees to manage and mark tasks as completed.

Important usage model:

- The company is small.
- Employees primarily access the application from their phones.
- Users need to see tasks.
- Users can currently see tasks belonging to other employees.
- Users can currently mark tasks belonging to other employees.
- There is also an administrative interface.
- Historically, the application has treated someone accessing it from a computer as an administrator.
- I am not certain whether there is any real authentication or server-side authorization.
- I suspect that some of the current "admin" logic may simply be client-side JavaScript logic.
- The current database is **Firebase Realtime Database**.
- I want to continue using Firebase unless you find a compelling architectural reason that makes this impossible or unsafe.
- The project is currently local and does not need to be deployed immediately.
- I want the freedom to completely redesign the application.
- I want the final result to be substantially more secure, maintainable, scalable, and professional than the current implementation.

The current repository is primarily a traditional HTML/CSS/JavaScript application.

Do NOT assume that the existing architecture is good.

Do NOT preserve bad architecture simply because it already exists.

Do NOT blindly convert every existing file into a React component.

First understand the system.

---

# 2. ABSOLUTE RULE: AUDIT FIRST, CODE LATER

DO NOT immediately start rewriting the project.

Before changing code, perform a comprehensive audit of the entire repository.

You must inspect:

- every source file
- every HTML page
- every JavaScript file
- every CSS file
- Firebase configuration
- Firebase Realtime Database rules
- all client-side database operations
- all authentication-related logic
- all admin-related logic
- all forms
- all user input
- all URLs/routes
- all localStorage/sessionStorage usage
- all external dependencies
- all API calls
- all secrets/configuration
- all data structures
- all CRUD operations
- all assumptions about users
- all assumptions about administrators
- all mobile/desktop behavior

Do not rely on filenames alone.

Trace how the application actually works.

Build a mental model of the current system before proposing the new architecture.

---

# 3. SECURITY AUDIT

Perform a serious security audit.

Treat the application as if it will eventually contain real company data.

Do NOT give me vague advice such as:

"Use authentication."

Instead, determine exactly:

- what is currently authenticated
- what is not authenticated
- how Firebase identifies requests
- whether anonymous users can read data
- whether anonymous users can write data
- whether users can impersonate administrators
- whether users can modify arbitrary records
- whether users can modify other users' tasks
- whether users can modify metadata
- whether users can bypass UI restrictions
- whether users can directly call Firebase APIs
- whether client-side restrictions can be bypassed
- whether Firebase Rules actually enforce the intended permissions
- whether an attacker can modify data without using the UI
- whether an attacker can read data without using the UI

Explicitly distinguish:

CLIENT-SIDE SECURITY
from
SERVER/DATABASE-ENFORCED SECURITY.

Assume that anything shipped to the browser can be inspected and modified by the user.

---

# 4. FIREBASE SECURITY

Firebase Realtime Database must be audited extremely carefully.

Review:

- database.rules.json
- database structure
- read permissions
- write permissions
- validation rules
- authentication requirements
- role enforcement
- data validation
- path-level permissions
- privilege escalation possibilities
- race conditions
- unauthorized writes
- unauthorized reads

The current repository contains Firebase rules that appear to allow unrestricted read/write access to important database paths.

Verify this yourself from the actual repository rather than blindly trusting this description.

If this is still true, explain the exact consequences.

Then design secure Firebase Rules for the new architecture.

Do not simply say "make the database private."

Define the actual permission model.

---

# 5. AUTHENTICATION & AUTHORIZATION

Design a proper authentication system.

The current "computer = administrator" concept must NOT automatically be considered secure.

Determine whether it should be removed completely.

I want you to design a real permission system.

Consider:

- Firebase Authentication
- administrator role
- regular employee role
- custom claims if appropriate
- authenticated user identity
- role-based authorization
- database-enforced authorization
- secure session handling

The final architecture must ensure that:

> A user cannot become an administrator simply by modifying JavaScript, HTML, localStorage, browser settings, or requests.

The database must enforce authorization independently of the UI.

---

# 6. USER MODEL

Propose a proper user model.

For example, potentially:

User
- uid
- displayName
- role
- active
- createdAt
- updatedAt

But do NOT blindly use this example.

Design the model based on the actual application.

Explain:

- how employees are identified
- how administrators are identified
- how accounts are created
- how accounts are disabled
- how roles are changed
- who can change roles
- what happens when a user's role changes
- how deleted/deactivated users behave

---

# 7. APPLICATION PERMISSIONS

Create a clear permission matrix.

For example:

| Action | Employee | Admin |
|---|---|---|
| View tasks | ? | ? |
| Mark task complete | ? | ? |
| Edit task | ? | ? |
| Delete task | ? | ? |
| Create task | ? | ? |
| Manage employees | ? | ? |
| Manage configuration | ? | ? |
| View administrative data | ? | ? |

Do not assume the answers.

Infer the intended behavior from the existing application and clearly identify anything that requires my confirmation.

Remember:

All employees currently need to be able to see tasks belonging to everyone and mark tasks belonging to everyone.

If you believe this should change for security reasons, explain why and propose alternatives, but do not silently change the business requirement.

---

# 8. DATA MODEL

Analyze the current Firebase database structure.

Document:

- every major node
- what each node represents
- what writes to it
- what reads from it
- which users should access it
- relationships between nodes
- duplicated data
- unnecessary data
- unsafe data
- inconsistent data structures

Then propose a clean Firebase Realtime Database schema.

Explain why your schema is better.

Optimize it for:

- mobile performance
- minimal reads
- minimal writes
- maintainability
- Firebase security rules
- predictable permissions
- future expansion

Do not migrate data blindly.

Include a migration strategy.

---

# 9. TECHNOLOGY MIGRATION

I want to modernize the frontend.

React is my preferred direction, but do NOT assume React is automatically the best answer.

Evaluate the project and determine whether something such as:

- React + Vite
- React + TypeScript + Vite
- Next.js
- another appropriate frontend architecture

would make sense.

Because this is primarily an application rather than a content website, consider the trade-offs carefully.

My default preference is:

React + TypeScript + Vite

unless you have a strong reason to choose something else.

Explain your decision.

---

# 10. TYPESCRIPT

Strongly consider TypeScript.

If you recommend it, explain how it will improve this particular project.

Use types for:

- users
- tasks
- database objects
- forms
- API/database responses
- application state
- configuration
- permissions

Avoid using `any` unless there is a legitimate reason.

---

# 11. ARCHITECTURE

Design a clean application architecture.

Do not create a giant `App.jsx`.

Separate concerns appropriately.

For example, consider structures such as:

src/
  components/
  pages/
  layouts/
  hooks/
  services/
  firebase/
  types/
  utils/
  constants/
  features/

But do NOT blindly copy this structure.

Design the architecture around the actual application.

Explain:

- component boundaries
- state management
- Firebase access layer
- authentication layer
- authorization layer
- reusable UI
- form handling
- validation
- error handling
- loading states
- notifications
- routing

---

# 12. UI / UX REDESIGN

You have permission to completely redesign the application.

Do not merely make the existing interface slightly prettier.

Analyze the current UX and determine what should be improved.

The application is heavily used on phones.

Mobile UX should therefore be treated as a primary design target rather than an afterthought.

Design for:

- touch interaction
- large tap targets
- fast task completion
- clear hierarchy
- minimal unnecessary navigation
- readable typography
- responsive layouts
- loading states
- empty states
- error states
- confirmation states
- success feedback
- accessibility
- RTL where appropriate
- Hebrew-language usage

Also consider desktop usage for administrators.

The desktop experience should feel intentional rather than simply being a stretched mobile layout.

---

# 13. DESIGN SYSTEM

Create a coherent design system.

Define:

- typography
- spacing
- colors
- borders
- radii
- shadows
- buttons
- inputs
- cards
- tables
- modals
- dialogs
- notifications
- loading indicators
- empty states
- error states

Avoid random styling differences between pages.

Create reusable components.

The final application should feel like one coherent product.

---

# 14. ACCESSIBILITY

Audit and improve:

- keyboard navigation
- focus states
- semantic HTML
- contrast
- screen-reader labels
- form labels
- error messages
- touch target sizes
- reduced-motion behavior

Do not treat accessibility as optional polish.

---

# 15. SECURITY AGAINST CLIENT MANIPULATION

Assume the user can:

- edit JavaScript
- edit HTML
- edit CSS
- modify localStorage
- modify sessionStorage
- inspect network requests
- call Firebase directly
- replay requests
- manipulate form values
- bypass disabled buttons
- modify hidden fields
- invoke internal functions from the browser console

The application must remain secure despite this.

Anything important must be enforced by Firebase/backend authorization rather than UI logic.

---

# 16. INPUT VALIDATION

Audit every user-controlled value.

Consider:

- task names
- employee names
- notes
- IDs
- dates
- numeric values
- JSON
- query parameters
- URL parameters
- form fields

Use appropriate validation.

Do not trust client-side validation alone.

---

# 17. XSS / INJECTION

Search the entire project for unsafe DOM operations such as:

- innerHTML
- insertAdjacentHTML
- document.write
- eval
- dynamic script injection
- unsafe URL construction

Determine whether each usage is actually exploitable.

Do not simply replace everything blindly.

Also examine:

- HTML injection
- stored XSS
- reflected XSS
- DOM XSS
- malicious database content
- unsafe rendering of user-controlled strings

---

# 18. SECRETS

Search the repository for:

- API keys
- service account credentials
- private keys
- passwords
- tokens
- credentials
- secrets

Distinguish between:

PUBLIC CONFIGURATION
and
REAL SECRET CREDENTIALS.

Do not incorrectly claim that every Firebase client configuration value is a secret.

Explain what is safe to expose and what is not.

---

# 19. DEPENDENCIES

When rebuilding the project:

- minimize dependencies
- avoid unnecessary libraries
- use maintained packages
- check package security
- avoid abandoned libraries
- avoid dependency bloat

Explain why every major dependency exists.

---

# 20. PERFORMANCE

Optimize for real mobile users.

Consider:

- bundle size
- code splitting
- lazy loading
- Firebase reads
- Firebase listeners
- unnecessary re-renders
- caching
- image optimization
- network requests
- loading states
- offline behavior where useful

Do not optimize prematurely.

Identify actual bottlenecks first.

---

# 21. ERROR HANDLING

Create a consistent error-handling system.

The application should gracefully handle:

- Firebase unavailable
- network failure
- permission denied
- invalid data
- authentication failure
- expired sessions
- malformed data
- unexpected exceptions

Never silently swallow important errors.

Give users understandable messages while keeping technical details available for debugging.

---

# 22. LOGGING / AUDIT TRAIL

Consider whether important actions should be logged.

Especially:

- administrator actions
- task modifications
- task deletion
- user creation
- role changes
- configuration changes

If useful, design an audit-log system.

Explain its storage requirements and security implications.

---

# 23. DATA INTEGRITY

Think about malicious or accidental database writes.

Determine whether Firebase Rules can enforce:

- required fields
- data types
- allowed values
- timestamps
- immutable fields
- valid IDs
- valid user references

Use Firebase validation rules wherever appropriate.

---

# 24. BACKUPS & RECOVERY

Design a practical backup/recovery strategy for Firebase.

Consider:

- accidental deletion
- malicious modification
- database corruption
- restoring previous data
- backup frequency
- retention
- administrator access

Do not over-engineer this for a small company.

Give me a realistic solution.

---

# 25. TESTING

Design a testing strategy.

At minimum consider:

- unit tests
- component tests
- integration tests
- Firebase Rules tests
- authentication tests
- authorization tests
- mobile UI tests
- regression tests

Security tests are especially important.

Create explicit tests such as:

> Anonymous user attempts to read tasks → must fail.

> Normal employee attempts to modify admin-only data → must fail.

> Normal employee attempts to grant themselves admin role → must fail.

> User modifies frontend JavaScript to expose admin UI → database still rejects unauthorized operation.

Do not rely on visual hiding for security.

---

# 26. MIGRATION STRATEGY

Do NOT recommend destroying the current project and rebuilding everything blindly.

Create a migration strategy.

Explain:

1. what should be backed up
2. what should remain temporarily
3. what should be rewritten
4. what can be reused
5. how Firebase data should migrate
6. how the new authentication system should be introduced
7. how old users should be migrated
8. how old URLs/pages should be handled
9. how to test the new version
10. how to roll back if something goes wrong

---

# 27. DEVELOPMENT ENVIRONMENT

Design a proper local development environment.

Include:

- Node.js
- package manager
- environment variables
- Firebase configuration
- Firebase Emulator Suite where appropriate
- linting
- formatting
- TypeScript
- testing
- development scripts
- production build

Prefer reproducible setup.

Document the setup so another developer can clone the repository and run it.

---

# 28. ENVIRONMENT SEPARATION

Consider separate:

- development
- testing
- production

Firebase environments/projects if appropriate.

Do not allow development testing to accidentally destroy production data.

---

# 29. DEPLOYMENT

I am currently keeping the project local.

Do NOT force me to deploy immediately.

However, design the project so that it can later be deployed easily.

Evaluate appropriate options such as:

- Firebase Hosting
- Vercel
- Cloudflare
- other suitable static/frontend hosting

Because Firebase is already used, consider Firebase Hosting, but do not automatically select it without comparing the trade-offs.

---

# 30. DOCUMENTATION

The final project should have proper documentation.

Create/update:

README.md

It should explain:

- what UTECH_PRO is
- architecture
- tech stack
- local setup
- environment variables
- Firebase setup
- authentication
- database structure
- security model
- development commands
- testing
- deployment
- backup/recovery
- troubleshooting

A future developer should be able to understand the project without asking me basic questions.

---

# 31. DO NOT OVERENGINEER

This is a small company's internal application.

Do not turn it into a giant enterprise platform unnecessarily.

Every architectural decision should balance:

- security
- maintainability
- simplicity
- cost
- performance
- developer experience

Use the simplest architecture that properly solves the problem.

---

# 32. IMPORTANT: VERIFY EVERYTHING

Do not make assumptions about the current implementation.

If something is unclear:

1. inspect the repository
2. inspect the relevant code
3. trace the behavior
4. explain what you found
5. distinguish facts from assumptions

Never say something is secure without verifying how it is enforced.

Never say something is vulnerable without identifying the actual attack path or evidence.

If you cannot verify something, explicitly say:

"I cannot confirm this from the available code."

---

# 33. REQUIRED FIRST RESPONSE

Your FIRST response after receiving this prompt must NOT modify the project.

Instead, produce a complete technical audit.

Structure it approximately as:

## Executive Summary

## Current Architecture

## Current Data Flow

## Current Authentication Model

## Current Authorization Model

## Firebase Security Audit

## Critical Security Findings

## High-Risk Findings

## Medium/Low-Risk Findings

## Current UI/UX Assessment

## Current Code Quality

## Current Performance

## Current Maintainability

## Technical Debt

## Recommended Target Architecture

## Recommended Technology Stack

## Proposed Firebase Data Model

## Proposed Authentication & Authorization

## Proposed Permission Matrix

## Proposed UI/UX Direction

## Migration Strategy

## Testing Strategy

## Deployment Strategy

## Backup/Recovery Strategy

## Phased Implementation Plan

## Questions / Decisions Required From Me

For every finding, include:

- severity
- affected area/file
- what is happening
- why it matters
- how it can be exploited or cause problems
- recommended fix
- whether the fix is mandatory or optional

---

# 34. DO NOT START IMPLEMENTATION UNTIL THE AUDIT IS COMPLETE

After the audit, wait for my confirmation before beginning the actual migration.

When I approve the architecture, proceed incrementally.

Do not attempt to generate an enormous amount of code in one response.

Work in logical phases.

After each major phase:

- explain what changed
- list changed files
- explain important decisions
- explain how to test it
- identify remaining risks

---

# 35. PRIORITY ORDER

Use this priority order:

1. Data security
2. Authentication
3. Authorization
4. Data integrity
5. Reliability
6. Correctness
7. Maintainability
8. Mobile UX
9. Desktop UX
10. Performance
11. Visual polish

Do not sacrifice security for convenience.

Do not sacrifice correctness for visual improvements.

---

# 36. FINAL GOAL

The end result should no longer feel like a collection of HTML files connected to Firebase.

It should feel like a properly engineered internal business application.

The final system should have:

- modern frontend architecture
- real authentication
- real authorization
- Firebase-enforced security
- clean database structure
- strong input validation
- secure admin functionality
- professional responsive UI
- excellent mobile experience
- maintainable code
- useful tests
- documentation
- reliable error handling
- sensible backups
- straightforward future deployment

Most importantly:

**Never confuse "the user cannot see the button" with "the user cannot perform the action."**

Security must be enforced at the actual authorization boundary.

Start by auditing the repository.
Do not write implementation code yet.