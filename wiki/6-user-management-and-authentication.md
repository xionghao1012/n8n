Relevant source files
*   [packages/cli/src/controllers/__tests__/me.controller.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/__tests__/me.controller.test.ts)
*   [packages/cli/src/controllers/auth.controller.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts)
*   [packages/cli/src/controllers/invitation.controller.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts)
*   [packages/cli/src/controllers/me.controller.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts)
*   [packages/cli/src/controllers/owner.controller.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/owner.controller.ts)
*   [packages/cli/src/controllers/users.controller.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts)
*   [packages/cli/src/requests.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/requests.ts)
*   [packages/cli/src/services/user.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/user.service.ts)
*   [packages/cli/test/integration/auth.api.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.api.test.ts)
*   [packages/cli/test/integration/auth.mw.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.mw.test.ts)
*   [packages/cli/test/integration/me.api.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/me.api.test.ts)
*   [packages/cli/test/integration/owner.api.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/owner.api.test.ts)
*   [packages/cli/test/integration/shared/random.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/shared/random.ts)
*   [packages/cli/test/integration/users.api.test.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts)

This document covers the user management and authentication system in n8n, including user roles, authentication mechanisms, user lifecycle, and API endpoints. It details how users are created, authenticated, authorized, and managed throughout their lifecycle in the platform.

For information about project-based permissions and resource sharing, see [Project Management and Sharing](https://deepwiki.com/n8n-io/n8n/4.5-project-management-and-sharing). For configuration and deployment aspects, see [Configuration and Deployment](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment).

Authentication System Architecture
----------------------------------

The n8n authentication system is built around JWT-based session management with cookie storage, supporting multiple authentication methods including email/password, LDAP, SAML, and OIDC.

### Core Authentication Flow

Sources: [packages/cli/src/controllers/auth.controller.ts 1-187](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L1-L187)[packages/cli/src/auth/auth.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/auth/auth.service.ts)

### Request Authentication Types

The system defines several request types to handle different authentication states:

Sources: [packages/cli/src/requests.ts 11-38](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/requests.ts#L11-L38)[packages/cli/test/integration/auth.mw.test.ts 16-26](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.mw.test.ts#L16-L26)

Role-Based Access Control
------------------------

n8n implements a role-based access control system with three primary global roles and project-specific roles.

### Global Role Hierarchy

| Role | Scope | Capabilities |
| --- | --- | --- |
| `global:owner` | Instance-wide | Full system access, user management, system configuration |
| `global:admin` | Instance-wide | User management, advanced features (requires license) |
| `global:member` | Instance-wide | Basic workflow access, project participation |

### Role-Based Endpoint Protection

Sources: [packages/cli/src/controllers/users.controller.ts 95-332](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L95-L332)[packages/cli/test/integration/users.api.test.ts 625-656](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L625-L656)

User Lifecycle Management
-------------------------

The user lifecycle in n8n follows a structured flow from invitation through activation to ongoing management.

### User Creation and Invitation Flow

Sources: [packages/cli/src/controllers/invitation.controller.ts 40-88](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L40-L88)[packages/cli/src/controllers/invitation.controller.ts 93-148](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L93-L148)[packages/cli/src/services/user.service.ts 189-236](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/user.service.ts#L189-L236)

### User Deletion and Resource Transfer

Sources: [packages/cli/src/controllers/users.controller.ts 170-287](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L170-L287)[packages/cli/test/integration/users.api.test.ts 669-1108](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L669-L1108)

User Profile and Settings Management
------------------------------------

The `/me` endpoints handle current user operations including profile updates, password changes, and settings management.

### Profile Management API

Sources: [packages/cli/src/controllers/me.controller.ts 48-257](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L48-L257)[packages/cli/test/integration/me.api.test.ts 34-237](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/me.api.test.ts#L34-L237)

Multi-Factor Authentication (MFA)
---------------------------------

n8n supports TOTP-based multi-factor authentication for enhanced security.

### MFA Integration Points

| Operation | MFA Requirement | Implementation |
| --- | --- | --- |
| Login | Required if enabled | `MfaService.validateMfa()` in `AuthController.login()` |
| Email Change | Required if enabled | MFA validation in `MeController.updateCurrentUser()` |
| Password Change | Required if enabled | MFA validation in `MeController.updatePassword()` |

### MFA Request Types

Sources: [packages/cli/src/requests.ts 166-177](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/requests.ts#L166-L177)[packages/cli/test/integration/auth.api.test.ts 83-124](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.api.test.ts#L83-L124)

API Endpoints Reference
-----------------------

### User Management Endpoints

| Method | Endpoint | Controller Method | Permission Scope | Purpose |
| --- | --- | --- | --- | --- |
| GET | `/users` | `UsersController.listUsers()` | `user:list` | List all users with filtering |
| DELETE | `/users/:id` | `UsersController.deleteUser()` | `user:delete` | Delete user with optional transfer |
| PATCH | `/users/:id/role` | `UsersController.changeGlobalRole()` | `user:changeRole` | Change user's global role |
| GET | `/users/:id/password-reset-link` | `UsersController.getUserPasswordResetLink()` | `user:resetPassword` | Generate password reset link |
| PATCH | `/users/:id/settings` | `UsersController.updateUserSettings()` | `user:update` | Update user settings |

### Authentication Endpoints

| Method | Endpoint | Controller Method | Auth Required | Purpose |
| --- | --- | --- | --- | --- |
| POST | `/login` | `AuthController.login()` | No | Authenticate user |
| GET | `/login` | `AuthController.currentUser()` | Yes | Get current user info |
| POST | `/logout` | `AuthController.logout()` | Yes | Logout user |
| GET | `/resolve-signup-token` | `AuthController.resolveSignupToken()` | No | Validate invitation token |

### Personal Account Endpoints

| Method | Endpoint | Controller Method | Purpose |
| --- | --- | --- | --- |
| PATCH | `/me` | `MeController.updateCurrentUser()` | Update profile |
| PATCH | `/me/password` | `MeController.updatePassword()` | Change password |
| PATCH | `/me/settings` | `MeController.updateCurrentUserSettings()` | Update user preferences |
| POST | `/me/survey` | `MeController.storeSurveyAnswers()` | Store personalization survey |

### Invitation Endpoints

| Method | Endpoint | Controller Method | Permission Scope | Purpose |
| --- | --- | --- | --- | --- |
| POST | `/invitations` | `InvitationController.inviteUser()` | `user:create` | Send user invitations |
| POST | `/invitations/:id/accept` | `InvitationController.acceptInvitation()` | No | Accept invitation and activate account |

Sources: [packages/cli/src/controllers/users.controller.ts 95-332](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L95-L332)[packages/cli/src/controllers/auth.controller.ts 41-187](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L41-L187)[packages/cli/src/controllers/me.controller.ts 48-257](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L48-L257)[packages/cli/src/controllers/invitation.controller.ts 40-148](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L40-L148)

SSO Integration
---------------

n8n supports multiple SSO providers with conditional authentication logic.

### SSO Authentication Methods

Sources: [packages/cli/src/controllers/auth.controller.ts 52-82](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L52-L82)[packages/cli/src/controllers/me.controller.ts 67-93](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L67-L93)[packages/cli/src/controllers/me.controller.ts 144-152](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L144-L152)

Testing Infrastructure
----------------------

The authentication system includes comprehensive test coverage across integration and unit tests.

### Test Categories

| Test File | Coverage Area | Key Test Cases |
| --- | --- | --- |
| `auth.api.test.ts` | Authentication endpoints | Login, logout, token validation, MFA |
| `users.api.test.ts` | User management API | User CRUD, role changes, deletion with transfer |
| `me.api.test.ts` | Personal account operations | Profile updates, password changes, settings |
| `invitation.controller.test.ts` | User invitation flow | Invitation creation, acceptance, validation |
| `auth.mw.test.ts` | Authentication middleware | Route protection, role-based access |

### Test Helper Infrastructure

Sources: [packages/cli/test/integration/auth.api.test.ts 17-27](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.api.test.ts#L17-L27)[packages/cli/test/integration/users.api.test.ts 37-40](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L37-L40)[packages/cli/test/integration/shared/random.ts 14-38](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/shared/random.ts#L14-L38)