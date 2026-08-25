# AWS Certified Cloud Practitioner (CLF-C02) — Study Guide

Compiled: August 2026. Sources: AWS's official exam guide and docs, cross-checked against multiple 2026 prep sites (see Sources at the end).

---

## 1. Exam Logistics (know these cold)

| Item | Detail |
|---|---|
| Code | CLF-C02 (replaced CLF-C01 in 2023) |
| Level | Foundational |
| Format | 65 questions — multiple choice (1 correct) and multiple response (2+ correct) |
| Scored vs unscored | 50 scored + 15 unscored (unmarked, answer everything as if it counts) |
| Duration | 90 minutes |
| Passing score | 700 / 1000 (scaled score, roughly ~70–72% correct) |
| Cost | $100 USD (+tax where applicable) |
| Delivery | Pearson VUE test centre **or** online proctored from home |
| Validity | 3 years |
| Prerequisites | None — no other cert required |
| Question style | Scenario-based ("A company wants to... which service...") not just definitions |

### Domain weightings

| Domain | Weight |
|---|---|
| 1. Cloud Concepts | 24% |
| 2. Security and Compliance | 30% |
| 3. Cloud Technology and Services | 34% |
| 4. Billing, Pricing, and Support | 12% |

Security (30%) and Technology/Services (34%) together are **64%** of the exam — spend most of your time there.

---

## 2. Domain 1 — Cloud Concepts (24%)

### Value proposition of the cloud
- **Trade capital expense (CapEx) for variable operating expense (OpEx)** — no upfront hardware.
- **Economies of scale** — AWS buys hardware at massive scale, passes savings on.
- **Stop guessing capacity** — scale up/down based on actual demand.
- **Increase speed and agility** — provision resources in minutes.
- **Stop spending on running/maintaining data centers** — focus on differentiating work.
- **Go global in minutes** — deploy in multiple Regions worldwide.

### Well-Architected Framework — 6 pillars
1. **Operational Excellence** — run and monitor systems, continuously improve.
2. **Security** — protect data, systems, and assets.
3. **Reliability** — recover from failures, meet demand.
4. **Performance Efficiency** — use resources efficiently, adapt as needs change.
5. **Cost Optimization** — avoid unneeded costs.
6. **Sustainability** — minimize environmental impact.

### Cloud economics
- **TCO (Total Cost of Ownership)** — AWS Pricing Calculator / TCO Calculator compare on-prem vs AWS cost.
- **Fixed vs variable costs**: on-prem = fixed (buy servers upfront); cloud = variable (pay for usage).
- Cost benefits: no data center costs, reduced staffing overhead, pay-as-you-go.

### Cloud design/migration concepts
- **6 R's of migration**: Rehost ("lift and shift"), Replatform, Repurchase (move to SaaS), Refactor/re-architect, Retire, Retain.
- **AWS Cloud Adoption Framework (CAF)** — 6 perspectives: Business, People, Governance, Platform, Security, Operations.
- Elasticity vs Scalability: elasticity = auto up/down with demand; scalability = ability to grow to handle load (vertical vs horizontal scaling).
- High availability, fault tolerance, disaster recovery vs scalability/elasticity — know the difference.
- **Disaster recovery strategies** (know order of RTO/cost, cheapest → most expensive): Backup & Restore → Pilot Light → Warm Standby → Multi-site Active/Active.

---

## 3. Domain 2 — Security and Compliance (30%)

### AWS Shared Responsibility Model
- **AWS is responsible FOR the cloud**: physical security, hardware, global infrastructure, virtualization layer, managed service internals.
- **Customer is responsible IN the cloud**: guest OS patching (for unmanaged services like EC2), firewall/security group config, IAM, data encryption, network traffic protection.
- Responsibility shifts depending on service type: IaaS (EC2) = customer manages more; managed/serverless (RDS, Lambda, S3) = AWS manages more.

### IAM (Identity and Access Management)
- **Root user** — created with account, has full access; should be locked down (MFA, not used day to day).
- **IAM users** — individual identities with credentials.
- **IAM groups** — collections of users sharing permissions.
- **IAM roles** — temporary credentials assumed by users, services, or federated identities (no long-term keys).
- **IAM policies** — JSON documents granting/denying permissions (identity-based vs resource-based).
- **Principle of least privilege** — grant only what's needed.
- **MFA (Multi-Factor Authentication)** — extra layer beyond password.
- **AWS Organizations** — manage multiple accounts centrally; **Service Control Policies (SCPs)** set permission guardrails across accounts.
- **AWS IAM Identity Center** (formerly AWS SSO) — centralized workforce access across accounts/apps.
- **Amazon Cognito** — identity for customer-facing web/mobile apps (not internal IAM).

### Security, governance & compliance concepts
- **AWS Artifact** — on-demand access to AWS compliance reports (e.g., ISO, PCI, SOC) and agreements.
- **AWS Compliance Programs** — AWS complies with HIPAA, PCI DSS, GDPR, FedRAMP, ISO 27001, SOC 1/2/3, etc.
- **Data residency / sovereignty** — customer chooses Region(s); AWS doesn't move data between Regions unless configured.
- **Encryption**: at rest (S3 SSE, EBS encryption) and in transit (TLS/SSL).
- **AWS Key Management Service (KMS)** — create/manage encryption keys.
- **AWS CloudHSM** — dedicated hardware security module for key storage (customer-managed, higher control than KMS).
- **AWS Secrets Manager** — store/rotate secrets (DB credentials, API keys).
- **AWS Config** — track resource configuration changes/compliance over time.

### Security services (know what each does at a high level)
| Service | Purpose |
|---|---|
| Amazon GuardDuty | Threat detection using ML/anomaly detection on logs |
| AWS Shield (Standard/Advanced) | DDoS protection |
| AWS WAF | Web Application Firewall — filters HTTP(S) traffic (SQLi, XSS rules) |
| AWS Firewall Manager | Centrally manage WAF/Shield/security group rules across accounts |
| Amazon Inspector | Automated security assessments for EC2/containers (vulnerabilities) |
| Amazon Macie | Discovers/protects sensitive data (PII) in S3 using ML |
| AWS Trusted Advisor | Best-practice checks: cost, performance, security, fault tolerance, service limits |
| AWS Security Hub | Aggregates security findings/alerts across services in one dashboard |
| Network ACLs vs Security Groups | NACL = stateless, subnet-level, allow+deny rules; SG = stateful, instance-level, allow rules only |

### DDoS/Network protection layering
- Edge (CloudFront + Shield) → WAF (app layer rules) → Security Groups/NACLs → IAM.

---

## 4. Domain 3 — Cloud Technology and Services (34%, the biggest domain)

### Ways to interact with AWS
- **AWS Management Console** — browser GUI.
- **AWS CLI** — command line.
- **AWS SDKs** — programmatic access in languages (Python/boto3, JS, Java, etc.).
- **AWS CloudShell** — browser-based shell with CLI pre-configured.
- **Infrastructure as Code (IaC)**: **AWS CloudFormation** (AWS-native, JSON/YAML templates) and **Terraform** (3rd-party, multi-cloud) — deploy repeatable, version-controlled infrastructure.
- **AWS Elastic Beanstalk** — PaaS; upload code, AWS handles provisioning/scaling/load balancing.

### Global Infrastructure
- **Region** — a geographic area with multiple, isolated data centers (e.g., eu-west-1).
- **Availability Zone (AZ)** — one or more discrete data centers within a Region, isolated from failures in other AZs but connected via low-latency links. Each Region has ≥3 AZs (design for ≥2 AZs for HA).
- **Edge Locations** — CloudFront/Route 53 endpoints for caching content closer to users (more locations than Regions).
- **Local Zones** — extend a Region closer to large population/industry centers for low-latency needs.
- **Wavelength Zones** — infrastructure embedded in telecom providers' 5G networks for ultra-low latency.
- **AWS Outposts** — AWS hardware/services physically deployed on-premises.
- **Global vs Regional services**: IAM, Route 53, CloudFront, WAF = global; EC2, S3 (bucket created in a Region), RDS, VPC = regional.

### Compute
| Service | What it is |
|---|---|
| **EC2** | Virtual servers (IaaS); choose instance type/family, pay per second/hour |
| EC2 pricing models | On-Demand (pay as you go, no commitment); Reserved Instances (1–3yr commit, cheaper); Savings Plans (flexible $ commitment); Spot Instances (unused capacity, cheapest, can be reclaimed); Dedicated Hosts/Instances (physical isolation) |
| Auto Scaling | Automatically add/remove EC2 instances based on demand |
| Elastic Load Balancing (ELB) | Distributes traffic across multiple targets/AZs (ALB, NLB, GWLB, CLB) |
| **AWS Lambda** | Serverless, event-driven functions; pay per invocation/duration, no server management |
| **Amazon ECS / EKS** | Container orchestration (Docker); ECS = AWS-native, EKS = managed Kubernetes |
| **AWS Fargate** | Serverless compute for containers (no EC2 management) |
| **AWS Batch** | Run batch computing jobs at scale |
| Lightsail | Simplified VPS for simple web apps/small projects |

### Storage
| Service | What it is |
|---|---|
| **Amazon S3** | Object storage; buckets/objects; 11 nines durability; storage classes below |
| S3 Standard | Frequently accessed data |
| S3 Intelligent-Tiering | Auto-moves data between tiers based on access patterns |
| S3 Standard-IA / One Zone-IA | Infrequent access, lower cost, retrieval fee |
| S3 Glacier Instant/Flexible/Deep Archive | Archival, cheapest, slower retrieval (minutes to hours/days) |
| S3 Versioning | Keep multiple versions of an object |
| S3 Lifecycle Policies | Auto-transition/delete objects over time |
| **Amazon EBS** | Block storage volumes attached to a single EC2 instance (like a hard drive) |
| **Amazon EFS** | Managed NFS file storage, shared across multiple EC2 instances/AZs |
| **AWS Storage Gateway** | Hybrid storage — connect on-prem to AWS cloud storage |
| **AWS Snow Family** (Snowcone/Snowball/Snowmobile) | Physical devices for large-scale offline data transfer |

### Databases
| Service | What it is |
|---|---|
| **Amazon RDS** | Managed relational DB (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server) |
| **Amazon Aurora** | AWS-built MySQL/PostgreSQL-compatible DB, higher performance, 5x/3x throughput |
| **Amazon DynamoDB** | Managed NoSQL, key-value, serverless, single-digit ms latency at any scale |
| **Amazon Redshift** | Data warehousing, OLAP, large-scale analytics/BI |
| **Amazon ElastiCache** | In-memory caching (Redis/Memcached) to speed up applications |
| **Amazon DocumentDB** | MongoDB-compatible managed document DB |
| **AWS Database Migration Service (DMS)** | Migrate databases to AWS with minimal downtime |

### Networking & Content Delivery
| Service | What it is |
|---|---|
| **Amazon VPC** | Your isolated virtual network; subnets, route tables, IGW, NAT gateway |
| Subnets | Public (route to Internet Gateway) vs Private (no direct internet route) |
| **Route 53** | DNS service + domain registration + health checks + routing policies |
| **Amazon CloudFront** | CDN — caches content at edge locations for low latency |
| **AWS Direct Connect** | Dedicated private network connection from on-prem to AWS (not over public internet) |
| **AWS VPN (Site-to-Site)** | Encrypted connection over the public internet |
| **AWS Transit Gateway** | Central hub to connect many VPCs and on-prem networks |
| **AWS Global Accelerator** | Improves availability/performance by routing over the AWS global network |

### Other frequently-tested service categories (know the *purpose*, not deep detail)
- **Analytics**: Athena (serverless SQL queries on S3), EMR (big data/Hadoop/Spark), Kinesis (real-time streaming), QuickSight (BI dashboards/visualization), Glue (ETL/data catalog).
- **Machine Learning**: SageMaker (build/train/deploy ML models), Rekognition (image/video analysis), Comprehend (NLP), Polly (text-to-speech), Transcribe (speech-to-text), Translate, Lex (chatbots), Textract (extract text from docs), Bedrock (generative AI foundation models).
- **Application Integration**: SQS (message queuing, decoupling), SNS (pub/sub notifications), EventBridge (event bus), Step Functions (workflow orchestration).
- **Management/Monitoring**: CloudWatch (metrics, logs, alarms, dashboards), CloudTrail (API call/audit logging — "who did what"), AWS Config (config compliance history), Systems Manager (patch/operate fleets), AWS Health Dashboard (service health).
- **Developer tools**: CodeCommit/CodeBuild/CodeDeploy/CodePipeline (CI/CD suite — note CodeCommit is deprecated for new customers).
- **Migration**: Migration Hub, Application Discovery Service, Server Migration Service.

> Exam tip: You will NOT be asked to configure these services — you'll be asked "which service solves this scenario?" Focus on **purpose + 1-2 distinguishing facts** per service, not deep configuration.

---

## 5. Domain 4 — Billing, Pricing, and Support (12%)

### Pricing fundamentals
- **Pay-as-you-go** — no upfront commitment, pay for what you use.
- **Save when you reserve** — commit to usage (Reserved Instances, Savings Plans) for discounts.
- **Pay less by using more** — volume-based tiered discounts (e.g., S3 data transfer).
- **Free Tier** — 12 months free (new accounts) + always-free + short-term trials, varies by service.

### Billing & cost management tools
| Tool | Purpose |
|---|---|
| **AWS Billing Console / Bills** | View invoices, charges by service |
| **AWS Cost Explorer** | Visualize and analyze historical/forecasted spend |
| **AWS Budgets** | Set custom cost/usage thresholds, get alerts |
| **AWS Cost and Usage Report (CUR)** | Most detailed, granular billing data export |
| **AWS Pricing Calculator** | Estimate costs before deploying |
| **Consolidated Billing (via AWS Organizations)** | Single bill for multiple linked accounts, combined usage can unlock volume discounts |
| **AWS Cost Anomaly Detection** | ML-based alerts on unusual spend patterns |
| Resource tagging / Cost allocation tags | Track/attribute costs by project, team, environment |

### AWS Support Plans
| Plan | Key features |
|---|---|
| **Basic** | Free for all; customer service, docs, forums, Trusted Advisor (7 core checks), Personal Health Dashboard |
| **Developer** | Business hours email support via cases; general guidance |
| **Business** | 24/7 phone/chat/email; <1hr response for production system down; full Trusted Advisor checks; access to AWS Support API |
| **Enterprise On-Ramp** | Subset of Enterprise; pool of Technical Account Managers (TAM), <30min critical response |
| **Enterprise** | Dedicated TAM, <15min response for business-critical down, concierge support |

### Other resources
- **AWS Trusted Advisor** — best-practice checks across 5 categories: Cost Optimization, Performance, Security, Fault Tolerance, Service Limits.
- **AWS Knowledge Center, re:Post, Documentation, Whitepapers** — free self-service resources.
- **AWS Marketplace** — buy third-party software that runs on AWS.
- **AWS Professional Services / AWS Partner Network (APN)** — consulting/implementation partners.

---

## 6. High-yield fact cheat sheet

- Shared Responsibility: AWS = **of** the cloud; Customer = **in** the cloud.
- S3 = **object** storage; EBS = **block** storage (single instance); EFS = **file** storage (shared/multiple instances).
- RDS = relational (SQL); DynamoDB = NoSQL (key-value/document).
- Security Group = stateful, instance-level, allow only. NACL = stateless, subnet-level, allow & deny.
- CloudWatch = performance monitoring/metrics. CloudTrail = API activity/audit logging.
- Elasticity = automatic scale to match demand. Scalability = capability to grow (manual or automatic).
- Spot Instances = cheapest but interruptible. Reserved = commitment discount. On-Demand = flexible, most expensive per-hour.
- Global services: IAM, Route 53, CloudFront, WAF. Everything else is generally Region-scoped.
- Minimum 3 AZs per Region typically; design workloads across ≥2 AZs for high availability.
- AWS Organizations → SCPs (guardrails) + Consolidated Billing (volume discounts, one invoice).
- Well-Architected Framework has **6** pillars (Sustainability was added later — often forgotten).
- 6 R's of migration: Rehost, Replatform, Repurchase, Refactor, Retire, Retain.

---

## 7. Suggested 2–3 week study plan

| Week | Focus |
|---|---|
| 1 | Domain 1 (Cloud Concepts) + Domain 2 (Security) — watch course, take notes, do domain-specific quizzes |
| 2 | Domain 3 (Technology & Services) — this is the biggest domain; go service-by-service using the tables above, use AWS Free Tier to click around the console for EC2, S3, IAM, VPC |
| 3 | Domain 4 (Billing) + full-length practice exams daily, review every wrong answer, re-read weak domains, sit the exam |

**Practice exams**: use at least 2–3 full-length timed practice exams before sitting the real one (e.g., Tutorials Dojo/Jon Bonso practice tests, Skillbuilder's official practice question set, and AWS's own official practice exam). Aim to consistently score 80%+ before booking.

---

## 8. About the YouTube video: "AWS Certified Cloud Practitioner Certification Course 2026 (CLF-C02) – Pass the Exam!"

This is the **freeCodeCamp** upload of a course created by **Andrew Brown** (ExamPro), ~13–14 hours long, and it's a legitimate, widely-recommended free resource. Reasons it's worth watching:

- freeCodeCamp/Andrew Brown courses are consistently well-regarded in the AWS cert community and are commonly cited as sufficient (often combined with practice exams) to pass CLF-C02.
- It covers the exact syllabus you need: cloud concepts, global infrastructure, compute/storage/database/networking services, IAM/security, pricing models, Well-Architected Framework, migration, and billing/support — matching all four exam domains.
- It's free and very thorough, which is good for a first pass through the material.

Caveats to keep in mind:
- **CLF-C02 replaced CLF-C01** in 2023, and AWS periodically refreshes exam guides — always double check the video's content against the *current* official exam guide domains/weightings above, since a general "2026" title doesn't guarantee AWS hasn't tweaked emphasis since the video was recorded (e.g., generative AI/Bedrock awareness has been increasingly emphasized in recent exam updates).
- 13+ hours is long — you don't need to absorb every second in one sitting. Use it as your primary content source, then reinforce with **practice questions**, since passing CLF-C02 is much more about recognizing "which service fits this scenario" than reciting facts.
- Supplement it with the **official AWS Skill Builder "AWS Certified Cloud Practitioner Official Practice Question Set"** (free) and one paid/free practice test bank (e.g., Tutorials Dojo) — video + practice questions is the winning combo most people report.

**Verdict: yes, it's a good primary study resource** — pair it with this sheet + practice exams and you should be well prepared.

---

## Sources

- [AWS Certified Cloud Practitioner (CLF-C02) official docs](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02.html)
- [AWS Certified Cloud Practitioner Exam Guide (PDF)](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)
- [Pluralsight — The new AWS Cloud Practitioner (CLF-C02): What to expect](https://www.pluralsight.com/resources/blog/cloud/new-aws-clf-c02-exam0)
- [Tutorials Dojo — AWS Cloud Practitioner CLF-C02 Exam Guide Study Path](https://tutorialsdojo.com/aws-cloud-practitioner-clf-c02-exam-guide/)
- [freeCodeCamp — AWS Certified Cloud Practitioner Study Course](https://www.freecodecamp.org/news/aws-certified-cloud-practitioner-study-course-pass-the-exam-with-this-free-13-hour-course/)
- [Class Central — course listing](https://www.classcentral.com/course/freecodecamp-aws-certified-cloud-practitioner-certification-course-clf-c02-pass-the-exam-273037)
- [K21 Academy — AWS CLF-C02 Exam Guide](https://k21academy.com/aws-cloud/aws-certified-cloud-practitioner-clf-c02-exam/)

*Note: This guide is a study aid, not a replacement for the official AWS exam guide — always cross-check against AWS's current published guide before your exam date, since AWS updates these periodically.*
