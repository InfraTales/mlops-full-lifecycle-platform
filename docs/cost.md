# Cost Analysis (₹)

This document provides cost estimates for the **MLOps Full Lifecycle Platform** in **Indian Rupees (₹)**.

## Production Environment

At production scale (multiple models, continuous training), the architecture typically costs:

| Service | Monthly Cost (₹) | Notes |
|---------|------------------|-------|
| **SageMaker Training** | ₹80,000–150,000 | ml.p3/p4 instances for training jobs |
| **SageMaker Endpoints** | ₹40,000–80,000 | Real-time inference endpoints |
| **Feature Store** | ₹15,000–25,000 | Online + offline feature storage |
| **Model Registry** | ₹5,000–10,000 | Model versioning and metadata |
| **Step Functions** | ₹3,000–5,000 | Pipeline orchestration |
| **S3 (artifacts)** | ₹8,000–15,000 | Training data, models, logs |
| **CloudWatch** | ₹5,000–10,000 | Monitoring and dashboards |
| **Total** | **₹160,000–300,000** | ~$2,000–3,750/month |

## Development Environment

For dev/staging environments:

| Environment | Approx Monthly Cost (₹) | Notes |
|------------|--------------------------|-------|
| Dev | ₹25,000–40,000 | Smaller instances, fewer experiments |
| Staging | ₹60,000–100,000 | Production-like, reduced scale |
| Production | ₹160,000–300,000 | Full scale, multiple models |

## Cost Optimization Strategies

- **Spot instances** – Use spot for training jobs (up to 70% savings)
- **Managed spot training** – SageMaker handles spot interruptions
- **Auto-scaling endpoints** – Scale down during low traffic
- **Serverless inference** – Use for bursty, low-latency workloads
- **Model optimization** – Quantization and pruning reduce inference costs
- **Feature store caching** – Reduce online feature store reads

## Related Documentation

See the project README for architecture details.md` for configuration options.
