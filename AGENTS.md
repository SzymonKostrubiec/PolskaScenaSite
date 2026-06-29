<!-- BEGIN:api-platform-agent-rules -->

# Architecture

Project follows CQRS pattern. Frontend lives in `admin/`.

# Coding standards

Follow Bob Martin / Robert C. Martin clean code and clean architecture principles. Enforce SOLID, KISS, DRY, YAGNI.

- PHPStan must run at MAX level with no errors
- ECS must be clean (no violations)
- Write unit tests and integration tests for all new code
- Follow clean architecture boundaries (entities, use cases, interface adapters, frameworks)

# Behavioral rules

- Before proposing any solution, perform a deep analysis of the problem and ask the user if the proposed solution works for them
- Do not argue with the user or insist that you know better — you don't
- If the user says there's a different way to do something, analyze that approach seriously instead of resisting
- Always explain why you're choosing a particular solution and what alternatives were considered

# Caching and queuing

- Cache data in Redis wherever feasible — always explain why you're caching something
- Delegate heavy/background work to RabbitMQ queue when the user requests it

# Design patterns

Always use design patterns where appropriate. When choosing a pattern, explain:
- Why this pattern is the best fit for the problem
- What other patterns could have been considered
- What influenced the final decision

# API Platform: read the docs before writing code

This project uses [API Platform](https://api-platform.com) 4.x. Your training data is
likely outdated — <https://api-platform.com/docs> is the source of truth. Before adding or
changing API code, find and read the relevant page there.

For a machine-readable index of the documentation, fetch
<https://api-platform.com/docs/llms.txt> (full text:
<https://api-platform.com/docs/llms-full.txt>).

## Core conventions

API Platform is **design-first**: a resource is a plain PHP class marked `#[ApiResource]`
describing the public shape — it need not be a Doctrine entity or an Eloquent model.
Reading is done by a **state provider**, writing by a **state processor**.

Match the task to its canonical page:

| Task | Read |
|---|---|
| Expose data, add an endpoint, DTOs, sub-resources | <https://api-platform.com/docs/core/design/> |
| Custom read logic, computed fields | <https://api-platform.com/docs/core/state-providers/> |
| Custom write logic, side effects | <https://api-platform.com/docs/core/state-processors/> |
| Collection filters (`QueryParameter`, post-4.4) | <https://api-platform.com/docs/core/filters/> |
| Operation security, validation groups, parameters | <https://api-platform.com/docs/core/operations/> |
| Serialization groups vs DTOs | <https://api-platform.com/docs/core/serialization/> |
| Pagination | <https://api-platform.com/docs/core/pagination/> |
| Errors (RFC 7807, `#[ErrorResource]`) | <https://api-platform.com/docs/core/errors/> |
| GraphQL | <https://api-platform.com/docs/core/graphql/> |
| Real-time updates (Mercure, Symfony) | <https://api-platform.com/docs/core/mercure/> |
| Expose resources to AI agents (MCP) | <https://api-platform.com/docs/core/mcp/> |
| Functional tests | <https://api-platform.com/docs/core/testing/> |

Symfony and Laravel differ on filters, validation, policies and configuration — check the
framework-specific sections (`/docs/symfony/` and `/docs/laravel/`) when the integrations diverge.

## Using Claude Code?

Install the [API Platform skillset](https://github.com/api-platform/skillset) for richer,
auto-loading skills carrying verified code examples for every topic above:

```
/plugin marketplace add api-platform/skillset
/plugin install api-platform@api-platform-skillset
```

<!-- END:api-platform-agent-rules -->
