# Troubleshooting

Common issues and resolutions for the **MLOps Full Lifecycle Platform**.

## Training Issues

### 1. Training Job Fails to Start

**Symptom:** Training job stuck in "Creating" or fails immediately.

**Resolution:**
- Check IAM role has `sagemaker:CreateTrainingJob` permission
- Verify VPC subnet has available IPs
- Check security group allows outbound to S3/ECR
- Verify training image exists in ECR

### 2. Out of Memory During Training

**Symptom:** Training job fails with OOM error.

**Resolution:**
- Increase instance type (e.g., ml.p3.2xlarge → ml.p3.8xlarge)
- Reduce batch size in hyperparameters
- Enable gradient checkpointing
- Use distributed training across multiple instances

### 3. Slow Training Performance

**Symptom:** Training takes longer than expected.

**Resolution:**
- Check data loading bottleneck – use SageMaker Pipe mode
- Verify GPU utilization – check for CPU-bound preprocessing
- Enable mixed precision training
- Use SageMaker Data Parallelism library

## Inference Issues

### 4. High Inference Latency

**Symptom:** Endpoint response time exceeds SLA.

**Resolution:**
- Check model size – consider quantization
- Verify instance type is appropriate
- Enable inference caching for repeated inputs
- Use SageMaker Neo for model optimization

### 5. Endpoint Scaling Issues

**Symptom:** Endpoint not scaling with traffic.

**Resolution:**
- Review auto-scaling policy thresholds
- Check CloudWatch alarms are triggering
- Verify max instance count is sufficient
- Consider provisioned concurrency for Lambda inference

## Pipeline Issues

### 6. Step Functions Timeout

**Symptom:** Pipeline execution times out.

**Resolution:**
- Increase state machine timeout
- Break long-running steps into smaller tasks
- Add heartbeat for long training jobs
- Check for stuck SageMaker jobs

### 7. Feature Store Sync Failures

**Symptom:** Features not appearing in online store.

**Resolution:**
- Check Feature Group status
- Verify IAM permissions for Feature Store
- Check data format matches feature definitions
- Review CloudWatch logs for ingestion errors

## Cost Issues

### 8. Unexpected High Costs

**Symptom:** Monthly bill higher than estimates.

**Resolution:**
- Check for orphaned endpoints – delete unused
- Review training job instance types
- Enable spot training for non-critical jobs
- Implement endpoint auto-scaling

> For architecture details, see `ARCHITECTURE.md`.
