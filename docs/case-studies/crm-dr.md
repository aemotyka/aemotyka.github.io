# CRM-DR: Salesforce disaster-recovery reporting on AWS

!!! note "Draft placeholder"
    This page will become the first polished case study. The final version should be sanitized for public viewing and should not include internal AWS account IDs, bucket names, ARNs, repository links, employee names, or screenshots of internal systems.

## Summary

CRM-DR is an AWS-based disaster-recovery reporting system for Salesforce data. It creates a daily queryable copy of core Salesforce objects, publishes curated reporting snapshots, replicates the reporting layer to a second region, validates freshness and consistency, and exposes Athena tables that recreate key Salesforce reporting behaviors during an outage.

## Planned sections

- Context
- Requirements
- Architecture
- Data flow
- Key design decisions
- SOQL-emulation reporting layer
- Reliability and monitoring
- Security and access control
- Cost profile
- Results
- Lessons learned

## Architecture draft

```mermaid
flowchart LR
    SF[Salesforce] --> AF[AWS AppFlow]
    AF --> RAW[S3 raw landing zone]
    RAW --> SFN[Step Functions snapshot workflow]
    SFN --> CURATED_E1[S3 curated snapshot us-east-1]
    CURATED_E1 --> GLUE_E1[Glue catalog and crawler]
    GLUE_E1 --> ATHENA_E1[Athena reporting workgroup]

    CURATED_E1 --> REPL[S3 cross-region replication]
    REPL --> CURATED_E2[S3 curated snapshot us-east-2]
    CURATED_E2 --> DR_FINAL[DR finalizer workflow]
    DR_FINAL --> GLUE_E2[Glue catalog and crawler]
    GLUE_E2 --> ATHENA_E2[Athena DR reporting workgroup]

    SFN --> DQ[Data-quality checks]
    DR_FINAL --> DQ
    DQ --> CW[CloudWatch alarms]
    CW --> SNS[SNS alerts]
```
