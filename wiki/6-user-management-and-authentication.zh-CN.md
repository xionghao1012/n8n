相关源文件
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

本文档介绍n8n中的用户管理和认证系统，包括用户角色、认证机制、用户生命周期和API端点。它详细说明了用户在平台中的创建、认证、授权和整个生命周期的管理方式。

有关基于项目的权限和资源共享的信息，请参见[项目管理与共享](https://deepwiki.com/n8n-io/n8n/4.5-project-management-and-sharing)。有关配置和部署方面的信息，请参见[配置与部署](https://deepwiki.com/n8n-io/n8n/5-configuration-and-deployment)。

认证系统架构
----------------------------------

n8n认证系统围绕基于JWT的会话管理和Cookie存储构建，支持多种认证方法，包括电子邮件/密码、LDAP、SAML和OIDC。

### 核心认证流程

来源：[packages/cli/src/controllers/auth.controller.ts 1-187](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L1-L187)[packages/cli/src/auth/auth.service.ts](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/auth/auth.service.ts)

### 请求认证类型

系统定义了几种请求类型来处理不同的认证状态：

来源：[packages/cli/src/requests.ts 11-38](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/requests.ts#L11-L38)[packages/cli/test/integration/auth.mw.test.ts 16-26](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.mw.test.ts#L16-L26)

基于角色的访问控制
------------------------

n8n实现了基于角色的访问控制系统，具有三个主要全局角色和项目特定角色。

### 全局角色层次结构

| 角色 | 范围 | 功能 |
| --- | --- | --- |
| `global:owner` | 实例范围 | 完整系统访问权限、用户管理、系统配置 |
| `global:admin` | 实例范围 | 用户管理、高级功能（需要许可证） |
| `global:member` | 实例范围 | 基本工作流访问权限、项目参与 |

### 基于角色的端点保护

来源：[packages/cli/src/controllers/users.controller.ts 95-332](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L95-L332)[packages/cli/test/integration/users.api.test.ts 625-656](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L625-L656)

用户生命周期管理
-------------------------

n8n中的用户生命周期遵循从邀请、激活到持续管理的结构化流程。

### 用户创建和邀请流程

来源：[packages/cli/src/controllers/invitation.controller.ts 40-88](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L40-L88)[packages/cli/src/controllers/invitation.controller.ts 93-148](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L93-L148)[packages/cli/src/services/user.service.ts 189-236](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/services/user.service.ts#L189-L236)

### 用户删除和资源转移

来源：[packages/cli/src/controllers/users.controller.ts 170-287](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L170-L287)[packages/cli/test/integration/users.api.test.ts 669-1108](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L669-L1108)

用户资料和设置管理
------------------------------------

`/me`端点处理当前用户操作，包括资料更新、密码更改和设置管理。

### 资料管理API

来源：[packages/cli/src/controllers/me.controller.ts 48-257](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L48-L257)[packages/cli/test/integration/me.api.test.ts 34-237](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/me.api.test.ts#L34-L237)

多因素认证（MFA）
---------------------------------

n8n支持基于TOTP的多因素认证，以增强安全性。

### MFA集成点

| 操作 | MFA要求 | 实现 |
| --- | --- | --- |
| 登录 | 启用时需要 | `AuthController.login()`中的`MfaService.validateMfa()` |
| 电子邮件更改 | 启用时需要 | `MeController.updateCurrentUser()`中的MFA验证 |
| 密码更改 | 启用时需要 | `MeController.updatePassword()`中的MFA验证 |

### MFA请求类型

来源：[packages/cli/src/requests.ts 166-177](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/requests.ts#L166-L177)[packages/cli/test/integration/auth.api.test.ts 83-124](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.api.test.ts#L83-L124)

API端点参考
-----------------------

### 用户管理端点

| 方法 | 端点 | 控制器方法 | 权限范围 | 用途 |
| --- | --- | --- | --- | --- |
| GET | `/users` | `UsersController.listUsers()` | `user:list` | 列出所有用户（带过滤） |
| DELETE | `/users/:id` | `UsersController.deleteUser()` | `user:delete` | 删除用户（可选转移资源） |
| PATCH | `/users/:id/role` | `UsersController.changeGlobalRole()` | `user:changeRole` | 更改用户全局角色 |
| GET | `/users/:id/password-reset-link` | `UsersController.getUserPasswordResetLink()` | `user:resetPassword` | 生成密码重置链接 |
| PATCH | `/users/:id/settings` | `UsersController.updateUserSettings()` | `user:update` | 更新用户设置 |

### 认证端点

| 方法 | 端点 | 控制器方法 | 是否需要认证 | 用途 |
| --- | --- | --- | --- | --- |
| POST | `/login` | `AuthController.login()` | 否 | 用户认证 |
| GET | `/login` | `AuthController.currentUser()` | 是 | 获取当前用户信息 |
| POST | `/logout` | `AuthController.logout()` | 是 | 用户登出 |
| GET | `/resolve-signup-token` | `AuthController.resolveSignupToken()` | 否 | 验证邀请令牌 |

### 个人账户端点

| 方法 | 端点 | 控制器方法 | 用途 |
| --- | --- | --- | --- |
| PATCH | `/me` | `MeController.updateCurrentUser()` | 更新个人资料 |
| PATCH | `/me/password` | `MeController.updatePassword()` | 更改密码 |
| PATCH | `/me/settings` | `MeController.updateCurrentUserSettings()` | 更新用户偏好设置 |
| POST | `/me/survey` | `MeController.storeSurveyAnswers()` | 存储个性化调查结果 |

### 邀请端点

| 方法 | 端点 | 控制器方法 | 权限范围 | 用途 |
| --- | --- | --- | --- | --- |
| POST | `/invitations` | `InvitationController.inviteUser()` | `user:create` | 发送用户邀请 |
| POST | `/invitations/:id/accept` | `InvitationController.acceptInvitation()` | 否 | 接受邀请并激活账户 |

来源：[packages/cli/src/controllers/users.controller.ts 95-332](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/users.controller.ts#L95-L332)[packages/cli/src/controllers/auth.controller.ts 41-187](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L41-L187)[packages/cli/src/controllers/me.controller.ts 48-257](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L48-L257)[packages/cli/src/controllers/invitation.controller.ts 40-148](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/invitation.controller.ts#L40-L148)

单点登录（SSO）集成
---------------

n8n支持多种SSO提供商，并具有条件认证逻辑。

### SSO认证方法

来源：[packages/cli/src/controllers/auth.controller.ts 52-82](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/auth.controller.ts#L52-L82)[packages/cli/src/controllers/me.controller.ts 67-93](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L67-L93)[packages/cli/src/controllers/me.controller.ts 144-152](https://github.com/xionghao1012/n8n/blob/master/packages/cli/src/controllers/me.controller.ts#L144-L152)

测试基础设施
----------------------

认证系统包括全面的测试覆盖，涵盖集成测试和单元测试。

### 测试类别

| 测试文件 | 覆盖范围 | 关键测试用例 |
| --- | --- | --- |
| `auth.api.test.ts` | 认证端点 | 登录、登出、令牌验证、MFA |
| `users.api.test.ts` | 用户管理API | 用户CRUD、角色更改、带转移的删除 |
| `me.api.test.ts` | 个人账户操作 | 资料更新、密码更改、设置 |
| `invitation.controller.test.ts` | 用户邀请流程 | 邀请创建、接受、验证 |
| `auth.mw.test.ts` | 认证中间件 | 路由保护、基于角色的访问 |

### 测试辅助基础设施

来源：[packages/cli/test/integration/auth.api.test.ts 17-27](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/auth.api.test.ts#L17-L27)[packages/cli/test/integration/users.api.test.ts 37-40](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/users.api.test.ts#L37-L40)[packages/cli/test/integration/shared/random.ts 14-38](https://github.com/xionghao1012/n8n/blob/master/packages/cli/test/integration/shared/random.ts#L14-L38)