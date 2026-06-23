# Engineering Case Studies

These are sanitized writeups of production systems I designed, built, operated, or significantly remediated.

The focus is practical engineering: architecture, infrastructure, deployment, reliability, debugging, cost control, and business impact.

---

## Published

### [LOTUS: internal auction ingestion and search platform](lotus.md)

An internal platform for discovering, scraping, extracting, storing, indexing, and searching upcoming auction lots. My work focused on the production cloud path: Terraform-managed AWS infrastructure, ECS/Fargate services, SQS queues and DLQs, S3 artifacts, RDS PostgreSQL integration, DynamoDB state/cache tables, GitHub Actions deployments, scheduled jobs, service secrets, IAM, logging, and launch-readiness debugging.

**Core themes:** AWS infrastructure, Terraform, ECS/Fargate, queue-based processing, production deployments, search indexing, PostgreSQL, operational debugging.

### [CRM-DR: Salesforce disaster-recovery reporting on AWS](crm-dr.md)

A disaster-recovery reporting system that exports Salesforce data into AWS, publishes curated Athena-queryable snapshots, validates freshness and consistency, and provides a documented continuity path during a Salesforce outage.

**Core themes:** disaster recovery, data pipelines, AWS AppFlow, S3, Glue, Athena, Step Functions, Lambda, KMS, monitoring, schema drift handling.

---

## Planned / older writeups

### [Legacy cloud systems recovery](legacy-cloud-systems-recovery.md)

A cloud infrastructure remediation effort focused on investigating unmanaged AWS resources, stabilizing business-critical legacy systems, reducing spend, documenting ownership, and restoring operational control.

### [Jewelry recommendation engine](jewelry-recommendation-engine.md)

Applied ML and data workflow work for surfacing auction jewelry lots using image similarity, keyword matching, active learning, and Salesforce-integrated review paths.
