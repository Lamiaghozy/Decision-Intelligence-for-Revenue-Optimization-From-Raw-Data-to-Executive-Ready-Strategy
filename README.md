Decision-Grade Data Infrastructure for Large-Scale Infrastructure Operations

Cloudera Big Data Specialist | Hive & Impala | Distributed SQL

Author: Lamia Ghozy
Focus: Business Intelligence & Decision Intelligence
Context: Large-scale infrastructure operations analytics

1. Why This Project Exists 

Large infrastructure programs generate massive operational telemetry across multiple machines, vendors, and teams. The real risk is not lack of data — it’s decision latency caused by fragmented, unreliable, and inconsistent data.

This project addresses a core executive problem:

How do we transform heterogeneous machine data into a single, decision-ready source of truth that leaders can trust for operational, financial, and risk decisions — at scale?

The work deliberately focuses on data foundations that enable decisions, not dashboards or reports.

2. Business Problem Being Solved
The Real Problem (Not the Technical One)

Three tunnel boring machines (TBMs) produce high-volume operational data:

Different formats

Different conventions

Different data quality assumptions

Before this work:

Analysts could not query the data holistically

Comparisons across machines were unreliable

Any operational insight requires manual, error-prone reconciliation

Leadership lacked confidence in metrics derived from the data

This blocked decisions around:

Operational performance benchmarking

Risk detection and anomaly analysis

Long-term cost and productivity optimization

Strategic planning over a 10-year construction horizon

3. Why This Problem Matters Now

At a small scale, inconsistency is inconvenient.
At the infrastructure scale, inconsistency is expensive.

As data volume grows:

Manual reconciliation collapses

Inconsistent schemas become silent risk multipliers

Decision cycles slow down precisely when speed matters most

This project establishes early discipline so the system remains trustworthy as data grows from hourly to near-real-time granularity.

4. Decision That Was Blocked (Before)

Before consolidation:

❌ “Which TBM is underperforming relative to distance drilled?”

❌ “Are location anomalies operational issues or data artifacts?”

❌ “Can we compare performance month-over-month across machines?”

These questions were unanswerable with confidence.

5. What Changed After This Work

After implementation:

✅ One canonical, analytics-ready table

✅ Consistent schema, null handling, and formats

✅ Hive + Impala compatibility for broad access

✅ Storage optimised for scale and query performance

Most importantly:

Decision-makers gained a single, trusted operational lens.

6. Architecture Overview (Decision-Oriented)
High-Level Architecture
        ┌────────────────────┐
        │  TBM Telemetry     │
        │  (3 Vendors)       │
        └────────┬───────────┘
                 │
                 ▼
        ┌────────────────────┐
        │ Amazon S3 (Raw)    │
        │ Heterogeneous Data │
        └────────┬───────────┘
                 │
                 ▼
   ┌──────────────────────────────┐
   │ Staging Layer (Normalization)│
   │ - Delimiters standardized   │
   │ - Headers handled           │
   │ - Missing values resolved   │
   └────────┬────────────────────┘
            │
            ▼
   ┌──────────────────────────────┐
   │ Canonical Analytics Table    │
   │ dig.tbm_sf_la (Parquet)      │
   │ - Hive + Impala compatible   │
   │ - Decision-grade schema      │
   └──────────────────────────────┘

7. Design Decisions (What I Chose — and Why)
7.1 Staging Tables (Intentional Trade-off)

Decision: Introduce TBM-specific staging tables
Why:

Preserves raw semantics

Makes data quality handling explicit

Avoids silent corruption during ingestion

I chose clarity and auditability over speed of ingestion.

7.2 Parquet for Final Table

Decision: Store final table as Parquet
Why:

Columnar storage for analytical workloads

Compression without sacrificing precision

Faster scans at scale

7.3 Data Types (Precision Over Convenience)

DECIMAL is used intentionally for distance and coordinates

Avoided floating-point ambiguity

Ensures analytical correctness over long time horizons

8. Conscious Trade-Offs I Accepted

I prioritised data trust over ingestion speed

I accepted additional complexity (staging layer) to reduce long-term risk

I optimised for analytical scalability, not ad-hoc querying convenience

This mirrors how high-stakes data systems are built in production environments.

9. Validation Outputs (Trust Signals)
Row Counts by TBM
SELECT tbm, COUNT(*) AS num_rows
FROM dig.tbm_sf_la
GROUP BY tbm
ORDER BY tbm;

TBM	Rows
Bertha II	91,619
Diggy McDigface	93,163
Shai-Hulud	94,237
Schema (Canonical)
DESCRIBE dig.tbm_sf_la;

10. If Constraints Changed…
If I Had 2 More Weeks

Partitioning by year/month

Bucketing by tbm

Incremental ingestion strategy

Data quality metrics (freshness, completeness)

If I Had Less Data

Same architecture

Less urgency — but same discipline

If Stakeholders Were Hostile

Start with the cost of bad data

Quantify decision delays

Anchor on operational risk, not tooling

#DecisionIntelligence  
#BusinessIntelligence  
#DataDrivenStrategy  
#RevenueOptimization  
#AnalyticsLeadership  
#DataForDecisionMaking  
#ExecutiveAnalytics  
#AIinBusiness
