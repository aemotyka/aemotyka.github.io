# LOTUS: Internal Auction Ingestion and Search Platform

!!! note "Sanitized case study"
    LOTUS is an internal system. This writeup intentionally omits private repository links, vendor lists, account IDs, ARNs, secrets, schema details, and business-sensitive implementation details.

## Summary

LOTUS v1 launched as an internal auction ingestion and search platform.

The system gives users a way to search upcoming auction inventory that has been discovered, scraped, extracted, stored, indexed, and exposed through an internal API/UI. My work focused on the production engineering around that system: infrastructure, deployment, environment management, queues, storage, service configuration, IAM, logging, and launch-readiness debugging.

This was not a demo app. The hard part was turning a messy external-data workflow into something that could be deployed, operated, inspected, and fixed.

## What I worked on

| Area | Work |
| --- | --- |
| Infrastructure | Terraform-managed AWS resources for LOTUS environments and production components |
| Runtime | ECS/Fargate task definitions and services for scraper, extractor, indexer, API, UI, and DDL components |
| Deployment | GitHub Actions workflows that build images, push to ECR, render ECS task definitions, and update services |
| Data flow | SQS queues and DLQs for auction and lot discovery/extraction stages |
| Storage | S3 paths for raw HTML, indexes, model/extractor output, logs, and search traces |
| Persistence | RDS PostgreSQL integration for normalized auction/lot data and DDL-managed schema changes |
| State/cache | DynamoDB tables for seen-state and query/cache use cases; Valkey/Redis for API search context |
| Operations | CloudWatch logs, S3 logs, task env management, ECS Exec support, queue/DLQ cleanup, launch debugging |

## Architecture

~~~mermaid
flowchart LR
    SCRAPER[Scraper tasks] --> RAW[S3 raw HTML]
    SCRAPER --> DISCOVER[SQS discovery queues]
    SCRAPER --> SEEN[DynamoDB/RDS seen state]

    DISCOVER --> EXTRACTOR[Extractor services]
    EXTRACTOR --> RAW
    EXTRACTOR --> RDS[(RDS PostgreSQL)]
    EXTRACTOR --> DLQ[SQS DLQs]

    RDS --> INDEXER[Indexer task]
    INDEXER --> INDEX[S3 search indexes]
    INDEXER --> API[API service]

    INDEX --> API
    RDS --> API
    API --> CACHE[Valkey/Redis cache]
    API --> UI[Internal UI]

    SCRAPER --> LOGS[CloudWatch / S3 logs]
    EXTRACTOR --> LOGS
    INDEXER --> LOGS
    API --> LOGS
    UI --> LOGS
~~~

## Why the system is structured this way

LOTUS deals with external auction data, which means source pages change, disappear, redirect, duplicate, or fail. A simple one-shot scraper would be hard to trust and harder to debug.

The production design separates the work into stages:

1. discover auction and lot pages
2. save raw source artifacts
3. hand off work through queues
4. extract structured records
5. store normalized data
6. build search indexes
7. serve search through an internal API/UI

That separation makes the system easier to inspect. If a lot does not show up in search, the failure can be traced stage by stage instead of guessed at.

## Infrastructure and deployment

LOTUS is deployed through AWS and Terraform.

The production environment includes ECS/Fargate task definitions and services for the main application components, SQS queues and DLQs for pipeline handoff, S3 buckets/prefixes for raw artifacts and search outputs, RDS PostgreSQL for persisted records, DynamoDB for state/cache tables, Valkey/Redis for API search context, CloudWatch logging, and IAM roles/policies scoped to each component.

Deployment is handled through GitHub Actions workflows. Application repos build Docker images, push them to ECR, render updated ECS task definitions, and update the correct ECS service when deployment is enabled for that environment.

The important part is not that these services exist. The important part is that they are wired together in a repeatable way, with environment-specific config, deployment gates, tagged task definitions, and operational hooks for debugging.

## Queueing and failure handling

The ingestion pipeline uses SQS queues to decouple crawling from extraction.

That design lets scraper runs hand off work without waiting for extraction to complete. It also creates a cleaner failure boundary: failed messages can be retried, inspected, or parked in DLQs without rerunning the entire crawl.

A major operational concern was parent/child ordering. Lot extraction often depends on auction context already existing. The system therefore has to handle dependency waits, retries, and terminal failure states deliberately instead of treating every missing parent as the same kind of failure.

## Search path

The search path is intentionally downstream from ingestion.

Scraper and extractor components populate durable storage. The indexer builds search artifacts from persisted data. The API reads the active index and database-backed detail paths. The UI gives users a usable internal search surface without requiring direct AWS or database access.

That keeps the user-facing layer separate from crawl/extraction logic and makes the search index rebuildable.

## Launch work

The v1 launch work was mostly practical production engineering:

- clean up prod bootstrap/task-definition drift
- keep Terraform from fighting legitimate service deploy state
- confirm ECS service/task behavior across environments
- harden API/UI deployment workflows
- configure secrets, IAM, logs, queues, and task envs
- debug DLQs and failed extractor handoffs
- validate active search/index behavior before launch
- document and communicate user-facing rollout steps

This is the kind of work that does not look flashy in a screenshot but determines whether the system is actually usable.

## Result

LOTUS v1 launched internally as a searchable auction-ingestion platform.

The system now has a production path across scraper, extractor, indexer, API, UI, and DDL components, with Terraform-managed AWS infrastructure, GitHub Actions deployments, queue-based processing, persisted data, search artifacts, and operational debugging paths.

## What I learned

The hard part of production scraping is not fetching pages. It is identity, state, retries, parent-child relationships, source drift, partial failure, observability, and keeping infrastructure aligned with how the application actually runs.

LOTUS was useful experience because it forced the work out of notebook/demo territory and into production application delivery.
