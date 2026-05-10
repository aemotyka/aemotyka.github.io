# Alex Motyka

I build production AI, data, and cloud systems for messy real-world business problems.

My recent work has focused on AWS infrastructure, applied machine learning systems, Salesforce-integrated workflows, disaster-recovery reporting, search, data pipelines, cost optimization, and legacy system recovery.

I am especially interested in roles where engineering work sits close to business-critical operations: production ML systems, data infrastructure, search/relevance systems, cloud-native applications, and reliability-focused backend platforms.

---

## Selected engineering case studies

### [CRM-DR: Salesforce disaster-recovery reporting on AWS](case-studies/crm-dr.md)

Designed and built a disaster-recovery reporting system that backs up core Salesforce data into AWS, publishes a curated Athena-queryable reporting snapshot, replicates it across regions, validates freshness and consistency, and provides a documented continuity path during a Salesforce outage.

**Focus areas:** AWS AppFlow, S3, Glue, Athena, Step Functions, Lambda, KMS, cross-region replication, CloudWatch alarms, IAM, disaster recovery, schema drift handling.

---

### [LOTUS: large-scale auction ingestion and search platform](case-studies/lotus.md)

Architected an AWS-hosted system for discovering, scraping, extracting, storing, indexing, and searching upcoming auction lots from global auction sources. The system is designed around high-volume ingestion, duplicate avoidance, structured extraction, and internal search access for business users.

**Focus areas:** distributed scraping, SQS, ECS/Fargate, S3, RDS PostgreSQL, Terraform, search indexing, structured extraction, cost-aware AWS design.

---

### [Jewelry recommendation engine](case-studies/jewelry-recommendation-engine.md)

Reworked an inherited auction recommendation system into a lower-cost AWS pipeline that combines image similarity, keyword matching, and active learning to surface jewelry lots of interest to the buying team through Salesforce.

**Focus areas:** applied ML, image similarity, active learning, Salesforce integration, infrastructure remediation, cost reduction.

---

### [AWS legacy cleanup and ownership recovery](case-studies/aws-legacy-cleanup.md)

Investigated, documented, cleaned up, and stabilized years of unmanaged AWS resources and legacy business applications, reducing monthly spend and restoring operational ownership over previously undocumented systems.

**Focus areas:** AWS auditing, cost optimization, Terraform migration, legacy application recovery, documentation, operational risk reduction.

---

## Technical profile

I work primarily across:

- Python, SQL, TypeScript, C
- AWS, Terraform, Docker, GitHub Actions
- S3, ECS/Fargate, SQS, RDS PostgreSQL, Lambda, Step Functions, Glue, Athena, CloudWatch, IAM
- PyTorch, TensorFlow, scikit-learn, Pandas, NumPy
- Salesforce development and Salesforce-integrated AWS systems

---

## Resume

A current resume is available here:

[View resume](resume.md)

---

## Links

- [GitHub](https://github.com/aemotyka)
- [LinkedIn](https://www.linkedin.com/in/alexandermotyka/)