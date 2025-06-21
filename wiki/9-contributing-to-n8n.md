# Contributing to n8n | n8n-io/n8n | DeepWiki

This document covers the development workflow, CI/CD processes, and contribution guidelines for the n8n project. It explains the automated systems that manage code quality, testing, and releases from initial development through production deployment.

## Relevant Source Files

* [.github/scripts/bump-versions.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/bump-versions.mjs)
* [.github/scripts/package.json](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/package.json)
* [.github/scripts/update-changelog.mjs](https://github.com/xionghao1012/n8n/blob/master/.github/scripts/update-changelog.mjs)
* [.github/workflows/check-documentation-urls.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-documentation-urls.yml)
* [.github/workflows/check-pr-title.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-pr-title.yml)
* [.github/workflows/check-run-eligibility.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/check-run-eligibility.yml)
* [.github/workflows/chromatic.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/chromatic.yml)
* [.github/workflows/ci-master.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-master.yml)
* [.github/workflows/ci-postgres-mysql.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-postgres-mysql.yml)
* [.github/workflows/ci-pull-requests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/ci-pull-requests.yml)
* [.github/workflows/docker-base-image.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-base-image.yml)
* [.github/workflows/docker-images-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/docker-images-nightly.yml)
* [.github/workflows/e2e-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-reusable.yml)
* [.github/workflows/e2e-tests-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests-pr.yml)
* [.github/workflows/e2e-tests.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/e2e-tests.yml)
* [.github/workflows/linting-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/linting-reusable.yml)
* [.github/workflows/release-create-pr.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-create-pr.yml)
* [.github/workflows/release-publish.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-publish.yml)
* [.github/workflows/release-push-to-channel.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/release-push-to-channel.yml)
* [.github/workflows/security-trivy-scan-callable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/security-trivy-scan-callable.yml)
* [.github/workflows/test-workflows-nightly.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-nightly.yml)
* [.github/workflows/test-workflows-pr-approved.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-approved.yml)
* [.github/workflows/test-workflows-pr-comment.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/test-workflows-pr-comment.yml)
* [.github/workflows/units-tests-reusable.yml](https://github.com/xionghao1012/n8n/blob/master/.github/workflows/units-tests-reusable.yml)
* [CONTRIBUTING.md](https://github.com/xionghao1012/n8n/blob/master/CONTRIBUTING.md)

## Development Workflow

The n8n project uses a structured development workflow centered around monorepo management, automated testing, and strict quality gates.

### Development Environment Setup

The development setup follows a standard monorepo pattern using `pnpm` workspaces:

| Component | Tool/Technology | Configuration File |
| --- | --- | --- |
| Package Manager | pnpm with corepack | `.packageManagerrc` |
| Node.js Version | 22.x | Multiple workflow files |
| Build System | Turbo | `turbo.json` |
| Linting | ESLint/Prettier | Multiple config files |
| Testing | Jest, Cypress | Test configuration files |

The project enforces strict requirements for community contributions.

## CI/CD Pipeline Architecture

The n8n CI/CD system uses GitHub Actions with multiple interconnected workflows for comprehensive quality assurance and automated deployment.

### Core CI Workflows

The primary CI pipeline includes:
- Pull request validation
- Master branch testing
- Database compatibility testing
- End-to-end testing

### Database Testing Matrix

The project maintains compatibility across multiple database engines through dedicated testing workflows.

### E2E Testing System

End-to-end testing uses Cypress with parallel execution and approval-based triggering.

## Testing Framework Architecture

The testing system encompasses multiple layers and types of testing with comprehensive coverage reporting.

### Test Execution Matrix

The comprehensive testing pipeline includes:
- Unit tests
- Integration tests
- Database tests
- End-to-end tests

### Test Eligibility and Approval System

The project uses an eligibility system to determine when comprehensive tests should run.

## Release Management System

The release system automates version bumping, changelog generation, and multi-channel publishing through GitHub Actions workflows.

### Release Creation Pipeline

The automated release process includes:
- Version bumping
- Changelog generation
- Release PR creation

### Release Publishing Pipeline

The multi-channel release distribution system handles:
- Docker image publishing
- NPM package publishing
- GitHub release creation

### Channel Management System

The project supports multiple release channels with automated tagging.

## Code Quality and Security

The project maintains high code quality through automated checks and security scanning integrated into the CI/CD pipeline.

### Quality Gates System

The code quality enforcement pipeline includes:
- Linting
- Type checking
- Test coverage requirements

### Security Scanning Integration

The security vulnerability detection system includes:
- Dependency scanning
- Container scanning
- Code scanning

## Infrastructure and Deployment

The project uses Docker-based deployment with multi-architecture support and automated nightly builds.

### Docker Build System

The container build and distribution pipeline handles:
- Multi-architecture builds
- Nightly builds
- Release builds

This contributing system ensures code quality, comprehensive testing, and reliable release management through automated CI/CD pipelines that scale from individual contributions to production deployments across multiple distribution channels.