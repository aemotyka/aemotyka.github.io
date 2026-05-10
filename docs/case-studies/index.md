# Engineering Case Studies

These case studies are sanitized writeups of production systems I designed, built, operated, or significantly remediated.

They focus on the parts of engineering work that are usually hard to see from a resume alone: problem framing, architecture, tradeoffs, reliability, cost control, operational ownership, and business impact.

---

## [CRM-DR: Salesforce disaster-recovery reporting on AWS](crm-dr.md)

A disaster-recovery reporting system that exports core Salesforce data into AWS, publishes curated Athena-queryable snapshots, replicates the reporting layer across regions, validates data freshness and consistency, and provides a documented continuity path during a Salesforce outage.

**Core themes:** disaster recovery, data pipelines, AWS AppFlow, S3, Glue, Athena, Step Functions, Lambda, KMS, cross-region replication, monitoring, schema drift handling, SOQL-emulation.

---

## [LOTUS: Large-scale auction ingestion and search](lotus.md)

An AWS-hosted auction ingestion and search platform for discovering, scraping, extracting, storing, indexing, and searching upcoming auction lots from global auction sources.

**Core themes:** distributed scraping, queue-based processing, structured extraction, duplicate avoidance, RDS PostgreSQL, ECS/Fargate, S3, SQS, Terraform, internal search tooling.

---

## [Jewelry Recommendation Engine](jewelry-recommendation-engine.md)

An applied ML system for surfacing auction jewelry lots of interest to a buying team using image similarity, keyword matching, and active learning, with recommendations integrated into Salesforce.

**Core themes:** image similarity, active learning, Salesforce integration, inherited system remediation, AWS cost reduction, internal product delivery.

---

## [AWS Legacy Cleanup and Ownership Recovery](aws-legacy-cleanup.md)

A cloud infrastructure remediation effort focused on investigating unmanaged AWS resources, retiring zombie systems, stabilizing business-critical legacy applications, reducing spend, and restoring operational ownership.

**Core themes:** AWS auditing, cost optimization, documentation, Terraform migration, legacy application recovery, operational risk reduction.