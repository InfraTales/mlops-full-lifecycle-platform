# Runbook

Operational guide for deploying, operating, and maintaining the **MLOps Full Lifecycle Platform**.

## 1. Deployment

### Prerequisites

- AWS CLI configured with appropriate credentials
- Node.js 18+ and npm installed
- AWS CDK CLI installed (`npm install -g aws-cdk`)
- Docker installed (for custom containers)

### Deploy Steps

```bash
# Install dependencies
npm install

# Bootstrap CDK (first time only)
cdk bootstrap

# Deploy to dev
cdk deploy --context environment=dev

# Deploy to production
cdk deploy --context environment=prod
```

## 2. Training Pipelines

### Trigger Training Job

```bash
# Start training pipeline
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:region:account:stateMachine:mlops-training \
  --input '{"model_name": "my-model", "hyperparameters": {...}}'
```

### Monitor Training

- Check SageMaker Training Jobs console
- View CloudWatch logs for training metrics
- Monitor Step Functions execution

## 3. Model Deployment

### Deploy New Model Version

```bash
# Register model in Model Registry
aws sagemaker create-model-package ...

# Update endpoint with new model
aws sagemaker update-endpoint --endpoint-name prod-endpoint \
  --endpoint-config-name new-config
```

### A/B Testing

- Configure traffic splitting in endpoint config
- Monitor metrics for each variant
- Promote winner via pipeline

## 4. Monitoring

### Key Metrics to Watch

- **Training**: Job duration, loss curves, resource utilization
- **Inference**: Latency, throughput, error rates
- **Feature Store**: Feature freshness, serving latency
- **Data drift**: Input distribution changes

### Dashboards

Pre-configured dashboards for:

- Model performance overview
- Training pipeline status
- Inference endpoint health
- Feature store metrics

## 5. Maintenance

### Regular Tasks

- Review model performance weekly
- Retrain models on schedule or drift detection
- Archive old model versions
- Update container images quarterly

### Teardown

```bash
cdk destroy --context environment=dev
```

> For troubleshooting common issues, see `docs/troubleshooting.md`.
