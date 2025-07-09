# n8n Cloud Build Example

This repository contains a sample setup for running the [n8n](https://n8n.io) automation platform on Google Cloud Build and Cloud Run.

## Files

- **Dockerfile** – uses the official n8n Docker image.
- **cloudbuild.yaml** – Cloud Build configuration that builds the image, pushes it to Artifact Registry and deploys to Cloud Run.

## Prerequisites

1. Create a PostgreSQL instance (for example via Cloud SQL) named `n8n-pg`.
2. Store the database password and the n8n encryption key in Secret Manager using the names `n8n_db_password` and `n8n_encryption_key`.
3. Update the `substitutions` section in `cloudbuild.yaml` with your desired region, repository and service name.

## Build and Deploy

Run Cloud Build using the provided configuration:

```bash
gcloud builds submit --config cloudbuild.yaml .
```

The pipeline builds the container, pushes it to Artifact Registry and then deploys it to Cloud Run with the necessary environment variables.

## Local development

To test locally you can build and run the image:

```bash
docker build -t n8n-local .
docker run -p 5678:5678 n8n-local
```

The service will be available on `http://localhost:5678`.
