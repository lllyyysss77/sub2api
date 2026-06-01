```markdown
# sub2api Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns, coding conventions, and workflows for contributing to the `sub2api` project. The repository is primarily written in Go for the backend and TypeScript/Vue for the frontend, with a strong emphasis on conventional commits, modular code organization, and robust testing. The documented workflows cover common tasks such as database migrations, API endpoint development, fullstack feature delivery, UI flows, admin dashboard updates, OAuth and payment flows, and spec writing.

## Coding Conventions

### File Naming

- **Go files:** Use `snake_case` (e.g., `user_service.go`)
- **TypeScript files:** Use `camelCase` or `PascalCase` as appropriate (e.g., `apiClient.ts`, `PaymentFlow.vue`)
- **Test files:** Suffix with `.spec.ts` for frontend tests and `_test.go` for Go tests

### Import Style

- **Go:** Mixed imports (standard library, third-party, and local packages grouped)
    ```go
    import (
        "context"
        "fmt"

        "github.com/gin-gonic/gin"
        "sub2api/backend/internal/service"
    )
    ```

### Export Style

- **Go:** Named exports for structs, functions, and interfaces
    ```go
    type UserService struct { ... }

    func (s *UserService) CreateUser(ctx context.Context, req *CreateUserRequest) error { ... }
    ```

- **TypeScript:** Named exports for functions and types
    ```ts
    export function fetchUser(id: string): Promise<User> { ... }
    export type PaymentStatus = 'pending' | 'completed';
    ```

### Commit Patterns

- **Conventional Commits:** Use prefixes such as `fix:`, `feat:`, `refactor:`, `docs:`, `test:`
    ```
    feat: add user profile endpoint
    fix: correct payment status update logic
    ```

## Workflows

### Add or Modify Database Table with Migration

**Trigger:** When introducing a new entity or modifying an existing one in the database  
**Command:** `/new-table`

1. Edit or add schema files in `backend/ent/schema/*.go`
2. Run ent codegen to update `backend/ent/*` (models, queries, etc.)
    ```bash
    go run entgo.io/ent/cmd/ent generate ./ent/schema
    ```
3. Add or update migration SQL in `backend/migrations/*.sql`
4. Update `backend/ent/migrate/schema.go` and related runtime files
5. Update relevant service and repository logic in `backend/internal/service/*` and `backend/internal/repository/*`

### Add or Update API Endpoint

**Trigger:** When exposing new backend functionality via HTTP API  
**Command:** `/new-endpoint`

1. Add or update handler logic in `backend/internal/handler/*.go`
2. Register the route in `backend/internal/server/routes/*.go`
3. Define request/response DTOs in `backend/internal/handler/dto/*.go`
4. Write or update tests in `backend/internal/handler/*_test.go`

### Feature Development Fullstack

**Trigger:** When delivering a new user-facing capability end-to-end  
**Command:** `/new-feature`

1. **Backend:**
    - Implement handler, service, and repository logic
    - Update or add API endpoints and tests
2. **Frontend:**
    - Add or update API calls in `src/api/*.ts`
    - Implement or update Vue components and views
    - Add or update tests (`*.spec.ts`)
    - Update types and i18n as needed

### Add or Update Frontend UI Flow

**Trigger:** When adding or updating a user-facing UI flow or panel  
**Command:** `/new-ui-flow`

1. Add or update Vue components in `frontend/src/components/**/*.vue`
2. Add or update views in `frontend/src/views/**/*.vue`
3. Update router in `frontend/src/router/index.ts` if navigation changes
4. Update types and i18n as needed
5. Write or update tests in `frontend/src/components/**/*.spec.ts` or `frontend/src/views/**/*.spec.ts`

### Add or Update Admin Dashboard View

**Trigger:** When exposing new admin functionality or reports  
**Command:** `/new-admin-view`

1. Add or update admin views in `frontend/src/views/admin/*.vue`
2. Update or add admin API in `frontend/src/api/admin/*.ts`
3. Add or update tests in `frontend/src/views/admin/__tests__/*.spec.ts`
4. Update backend handler in `backend/internal/handler/admin/*.go`
5. Update admin routes in `backend/internal/server/routes/admin.go`

### Add or Update Auth OAuth Flow

**Trigger:** When adding or refining OAuth login, binding, or callback flows  
**Command:** `/new-oauth-flow`

1. Update backend OAuth handlers in `backend/internal/handler/auth_*_oauth.go` and tests
2. Update backend OAuth service logic in `backend/internal/service/auth_*.go` and tests
3. Update routes in `backend/internal/server/routes/auth.go`
4. Update frontend API in `frontend/src/api/auth.ts`
5. Update frontend callback views in `frontend/src/views/auth/*CallbackView.vue` and tests

### Add or Update Payment Flow

**Trigger:** When supporting new payment providers, flows, or UI  
**Command:** `/new-payment-flow`

1. Update backend payment service in `backend/internal/service/payment_*.go` and tests
2. Update backend payment handler in `backend/internal/handler/payment_*.go`
3. Update or add payment schema in `backend/ent/schema/payment_*.go` and run codegen
4. Add or update migration SQL in `backend/migrations/*.sql`
5. Update frontend payment components in `frontend/src/components/payment/*.vue` and tests
6. Update payment views in `frontend/src/views/user/Payment*.vue` and tests
7. Update payment types in `frontend/src/types/payment.ts`

### Add or Update Spec and Implementation Plan

**Trigger:** When documenting and planning a new major system or feature  
**Command:** `/new-spec`

1. Add or update design specs in `docs/superpowers/specs/*.md`
2. Add or update implementation plans in `docs/superpowers/plans/*.md`
3. Iterate on both as the design evolves

## Testing Patterns

- **Frontend:** Uses [Vitest](https://vitest.dev/) for unit and component testing.
    - Test files are named `*.spec.ts` and placed alongside or in `__tests__` directories.
    - Example:
        ```ts
        // frontend/src/components/MyComponent.spec.ts
        import { describe, it, expect } from 'vitest';
        import MyComponent from './MyComponent.vue';

        describe('MyComponent', () => {
          it('renders correctly', () => {
            // mount and assert
          });
        });
        ```
- **Backend:** Go tests use the standard testing package.
    - Test files are named with `_test.go` suffix.
    - Example:
        ```go
        // backend/internal/service/user_service_test.go
        func TestCreateUser(t *testing.T) {
            // test logic
        }
        ```

## Commands

| Command           | Purpose                                                           |
|-------------------|-------------------------------------------------------------------|
| /new-table        | Add or modify a database table with migration                     |
| /new-endpoint     | Add or update an API endpoint                                     |
| /new-feature      | Implement a new fullstack feature                                 |
| /new-ui-flow      | Add or update a frontend UI flow                                  |
| /new-admin-view   | Add or update an admin dashboard view                             |
| /new-oauth-flow   | Add or update an OAuth authentication flow                        |
| /new-payment-flow | Add or update payment processing logic and UI                     |
| /new-spec         | Add or update a design spec and implementation plan               |
```
