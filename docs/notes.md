# 📝Project Notes — Serverless Micro Image Processor

---

##  Design Decisions

### S3 Buckets

| Bucket | Purpose |
|---|---|
| `img-raw-<account>-<region>` | Stores raw uploaded images |
| `img-processed-<account>-<region>` | Stores final processed images |

### Step Functions Workflow

- Pipeline order: **Resize → Watermark**
- Triggered by **S3 `ObjectCreated` events** on the raw bucket

### Lambda Layers

- Pillow is bundled as a Lambda Layer to avoid packaging it inside every individual function

---

##  Lessons Learned

- **Presigned URLs** allow secure client uploads without exposing AWS credentials
- **Step Functions** will fail if the payload doesn't match expected keys — `resized_image` must exist before the watermark step runs
- Returning presigned URLs for processed images requires a **separate Lambda route** (`/processed`) with a GET integration in API Gateway

---

##  Tips

- Always set `InputPath` and `OutputPath` carefully in Step Functions to pass the correct payload between states
- Use S3 `ObjectCreated` events to trigger processing Lambdas
- Test presigned URL generation independently before wiring up the client script

---

##  Future Considerations

- [ ] Implement job status tracking with DynamoDB to replace polling
- [ ] Add error handling in Step Functions (DLQ, retries, failure states)
- [ ] Extend the workflow with additional image transformations

