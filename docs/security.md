# Security Overview

This document summarizes the security posture of the **MLOps Full Lifecycle Platform**.

## Defense-in-Depth

The platform applies multiple layers of security controls:

### Identity & Access (IAM)

- Least-privilege IAM roles for all SageMaker components
- Separate roles for training, inference, and pipeline execution
- Service-linked roles for Feature Store and Model Registry
- Cross-account access controls for multi-account setups

### Data Protection

- **Training data**: KMS encryption for S3 training datasets
- **Model artifacts**: Encrypted model storage in S3 and Model Registry
- **Feature Store**: Encryption at rest for online and offline stores
- **In transit**: TLS 1.2+ for all API calls and data transfers

### Network Isolation

- VPC deployment for SageMaker training and inference
- Private subnets with no internet access for sensitive workloads
- VPC endpoints for S3, ECR, and SageMaker APIs
- Security groups restricting inter-service communication

### Model Security

- Model signing and verification
- Container image scanning in ECR
- Input validation for inference endpoints
- Model versioning and audit trails

## ML-Specific Security

- Training data lineage tracking
- Experiment reproducibility controls
- A/B testing isolation
- Champion/challenger deployment safeguards

## Compliance Considerations

The architecture supports:

- SOC 2 Type II controls
- GDPR data protection (with appropriate configuration)
- Model governance requirements

> For detailed security configurations, see `SECURITY.md` in the project root.
