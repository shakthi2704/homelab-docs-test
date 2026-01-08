# CI/CD – Drone (Baseline Documentation)

## Purpose

Document the presence, role, and operational boundaries of the CI/CD systemdeployed on the core-services LXC.

This document exists to **describe deployed reality**, not future automation.

## Scope

In scope:

- Drone CI/CD server deployment

- Drone Docker runner deployment

- Integration with Gitea repositories

- Manual pipeline triggering

Out of scope:

- Production-grade CI/CD pipelines

- Application build, test, or release workflows

- Secrets automation

- Infrastructure-as-code execution

- Multi-runner or distributed CI/CD

## Architecture Overview

Node: core-services (LXC)

Services:

- Drone Server

- Drone Docker Runner

Integration:

- Gitea (self-hosted Git service)

Execution Model:

- Docker-in-Docker via mounted Docker socket

- Pipelines run only when explicitly triggered

## Deployed Components

### Drone Server

Purpose:

- Provides CI/CD control plane

- Integrates with Gitea for repository events

- Exposes web UI for visibility and control

Characteristics:

- Docker container

- Persistent data stored in Docker volume

- Accessible via LXC_IP:8080

- No reverse proxy or TLS termination

### Drone Docker Runner

Purpose:

- Executes CI/CD pipelines as Docker containers

Characteristics:

- Docker container

- Docker socket mounted from host LXC

- Limited runner capacity

- No privileged escalation beyond Docker access

## Gitea Integration

- Drone is connected to the Gitea instance running on core-services

- Repositories must be manually activated in Drone

- Only selected repositories participate in CI/CD

Activated repositories:

- docker-stacks

- home-lab-config

No organization-wide automation is enabled.

## Pipeline Usage Model

Current usage intent:

- Pipelines are **optional**

- Pipelines are **manually triggered**

- Pipelines are **minimal by design**

There is **no requirement** for all repositories to contain a .drone.yml.

## Example Minimal Pipeline (Reference Only)

This example exists **only to validate Drone functionality**.

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`kind: pipeline  type: docker  name: validation  steps:    - name: test      image: alpine      commands:        - echo "CI/CD system validated"`

Notes:

- This pipeline performs no real work

- It does not modify infrastructure

- It is safe to remove at any time

## Operational Rules

- CI/CD must not deploy services automatically

- CI/CD must not manage secrets

- CI/CD must not mutate LXC configuration

- All automation must be explicitly documented before use

## Validation Status

- Drone server running

- Drone runner connected

- Gitea integration verified

- Manual pipeline execution validated

CI/CD is considered **available but intentionally limited**.

## Notes

- This document reflects **current deployed state only**

- Expansion requires explicit scope approval and documentation update
