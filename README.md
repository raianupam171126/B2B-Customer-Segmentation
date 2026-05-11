# B2B-Customer-Segmentation
B2B customer segmentation framework — RFM, K-Means, Hierarchical, DBSCAN &amp; GMM

Business Problem
Company: TechNova Solutions — a mid-market B2B SaaS company selling an enterprise analytics platform.

Challenge: Marketing and sales teams operate in silos. Marketo captures engagement data (email opens, webinar attendance, content downloads) while Salesforce holds pipeline and revenue data (opportunities, deal size, win rates). Without unifying these, the company can't answer critical questions:

Which accounts are high-value but under-engaged (churn risk)?

Which accounts show strong engagement but low pipeline (conversion opportunity)?

How should marketing prioritize ABM spend across account tiers?

What does a healthy account actually look like across both systems?

This project builds a unified segmentation framework that merges both data sources and applies multiple clustering techniques to identify actionable account segments.
---
Pipeline Overview
```
Step 1:  Environment Setup & Library Installation
Step 2:  Synthetic Data Generation (Salesforce Accounts, Opportunities, Marketo Activities)
Step 3:  Data Validation & Quality Checks (completeness, join-key integrity, data catalog)
Step 4:  Data Merging & Feature Engineering (account-level rollups, unified feature matrix)
Step 5:  Exploratory Data Analysis (distributions, correlations, industry/tier splits)
Step 6:  Advanced Segmentation Techniques
         ├── 6A: RFM Analysis (Recency, Frequency, Monetary)
         ├── 6B: K-Means Clustering (Elbow + Silhouette optimization)
         ├── 6C: Hierarchical Clustering (Ward linkage + Dendrogram)
         ├── 6D: DBSCAN (Density-based anomaly detection)
         └── 6E: Gaussian Mixture Model (Soft/probabilistic clustering)
Step 7:  Model Comparison & Consensus Segmentation (ARI, NMI cross-validation)
Step 8:  Segment Profiling & Business Interpretation (radar charts, heatmaps, naming)
Step 9:  Actionable Recommendations & Export (strategy per segment, executive dashboard)
```
---
Data
Detail	Value
Accounts	2,500 B2B accounts (synthetic, modelled after real Marketo + SFDC patterns)
Opportunities	Multi-stage pipeline data (Prospecting → Closed Won/Lost)
Marketo Activities	Email opens, clicks, webinar attendance, content downloads, form fills
Features Used	9 clustering features spanning firmographic, pipeline, and engagement dimensions
Feature Matrix
Feature	Source	Category
Annual Revenue	Salesforce	Firmographic
Employee Count	Salesforce	Firmographic
Account Tenure	Salesforce	Firmographic
Total Opportunities	Salesforce	Pipeline
Total Pipeline Value	Salesforce	Pipeline
Win Rate	Salesforce	Pipeline
Engagement Score	Marketo	Engagement
Avg Lead Score	Marketo	Engagement
Days Since Last Activity	Marketo	Recency
---
Segmentation Methods
RFM Analysis
Classic Recency-Frequency-Monetary scoring adapted for B2B: Recency = days since last Marketo activity, Frequency = total engagements, Monetary = total pipeline value. Accounts scored 1–5 on each dimension and mapped to segments (Champions, Loyal, At Risk, etc.).

K-Means Clustering
Optimal K selected via Elbow method (KneeLocator) and Silhouette analysis. Features standardized with StandardScaler. Clusters visualized using PCA projection.

Hierarchical Clustering (Agglomerative)
Ward linkage with dendrogram analysis for visual cluster count validation. Provides an alternative grouping to cross-validate K-Means results.

DBSCAN
Density-based method used primarily for anomaly/outlier detection — identifies accounts that don't fit any natural cluster (potential data quality issues or unique high-value accounts).

Gaussian Mixture Model (GMM)
Soft clustering that assigns probability of membership to each cluster rather than hard assignments. Model selection via BIC/AIC minimization.

Consensus Segmentation
Cross-method comparison using Adjusted Rand Index (ARI) and Normalized Mutual Information (NMI) to validate that segments are robust across methods, not artifacts of a single algorithm.
---
Key Results
Segments Identified
Segment	Profile	Strategy
🏆 Tier 1 — Strategic Champions	High revenue, high engagement, strong pipeline	ABM campaigns, executive events, custom content
🌟 Tier 2 — Growth Accounts	Mid-market, rising engagement, expanding pipeline	Nurture sequences, case studies, upsell plays
🔄 Tier 3 — Nurture Pipeline	Active engagement but low conversion	Sales enablement, demo offers, ROI calculators
⚠️ Tier 4 — At-Risk / Dormant	Previously active, declining engagement	Re-engagement campaigns, win-back offers
🌱 Tier 5 — New / Emerging	Early-stage, limited data	Onboarding sequences, educational content
Visualizations
The notebook includes 20+ publication-quality charts:
Feature distributions and correlation heatmaps
RFM segment treemap and scatter plots
Elbow curve, Silhouette scores, and Calinski-Harabasz index
PCA cluster projections (K-Means, Hierarchical, GMM)
DBSCAN anomaly detection plot
Dendrogram for hierarchical clustering
Radar charts for segment comparison
Segment × Industry heatmap
Executive dashboard (pipeline, engagement, revenue by segment)

