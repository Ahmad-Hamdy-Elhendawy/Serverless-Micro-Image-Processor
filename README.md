# Serverless-Micro-Image-Processor

# Serverless-Micro-Image-Processor

## Overview
This project implements a fully serverless image processing pipeline on AWS. It allows users to upload an image, automatically processes it (resize + watermark), and returns a secure URL to access the final image.

The system is event-driven, scalable, and requires no server management.

---

## Architecture

![Architecture](architecture.png)

---

## Tech Stack
- AWS Lambda  
- AWS Step Functions  
- Amazon S3  
- API Gateway  
- Bash (client script)

---

## Workflow

1. Client requests a presigned upload URL via API Gateway  
2. Image is uploaded directly to S3  
3. S3 triggers a Lambda function  
4. Lambda starts a Step Functions workflow  
5. Step Functions executes:
   - Resize image  
   - Add watermark  
6. Processed image is stored in a separate S3 bucket  
7. Client requests a presigned URL to access the processed image  

---

## Project Structure
image-processing-pipeline/
│
├── README.md
├── architecture.png
├── demo.mp4
│
├── lambdas/
│ ├── upload-url/
│ ├── resize/
│ ├── watermark/
│ └── return-image/
│
├── step-functions/
│ └── state-machine.json
│
├── scripts/
│ └── client.sh
│
└── docs/
└── notes.md

---

## How to Run

1. Clone the repository:
git clone https://github.com/Ahmad-Hamdy-Elhendawy/Serverless-Micro-Image-Processor
cd image-processing-pipeline


2. Make the script executable:
3. chmod +x upload-image.sh
4. Enter your image's full path when prompted

---

## Example Output
[OK] Upload successful
[INFO] Waiting for processing...
[OK] Processed image URL:
https://<url>


---

## Key Features
- Fully serverless architecture  
- Event-driven processing using S3 triggers  
- Workflow orchestration with Step Functions  
- Secure uploads and downloads using presigned URLs  
- Decoupled and scalable design  

---

## Future Improvements
- Replace polling with event-based notifications (SQS/SNS)  
- Use DynamoDB for job status tracking  
- Add error handling (DLQ, retries, failure states)  

---

## Outcome
This project demonstrates a complete serverless pipeline using AWS services, covering event-driven architecture, workflow orchestration, and secure file handling.
