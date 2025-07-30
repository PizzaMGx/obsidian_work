---
weight: 4
title: Working with MinIO and Boto3. A Drop-in S3 Alternative for Local Development
date: 2025-07-30
draft: false
author: Vincent
description: Working with MinIO and Boto3. A Drop-in S3 Alternative for Local Development
tags:
  - IT
categories:
  - IT
---

---

In many Django projects, you'll eventually need to store user-uploaded files like images or documents. Services like Amazon S3 are commonly used in production, but for local development or CI environments, a self-hosted solution like **MinIO** is fast, lightweight, and 100% S3-compatible.

In this post, I’ll show how to:
- Set up **MinIO** using Docker Compose
- Connect it to a **Django** app using `boto3`
- Upload files via Django models using `ImageField`

---

## 🐳 Step 1: Docker Compose Setup for MinIO

Create a `docker-compose.yml` to run MinIO locally:

```yaml
version: '3.8'

services:
  minio:
    image: minio/minio
    container_name: minio
    ports:
      - "9000:9000"   # S3 API
      - "9001:9001"   # MinIO Web UI
    volumes:
      - minio_data:/data
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
    command: server --console-address ":9001" /data

volumes:
  minio_data:
```

Start it up:

```
docker compose up -d
```

Visit [http://localhost:9001](http://localhost:9001) to log in (user: `minioadmin`, password: `minioadmin`).

👉 **Create a bucket** in the UI called: `media`

## 🐍 Step 2: Install `boto3` and Storage Dependencies in Django

Install the necessary packages:

```
pip install boto3 django-storages
```


Update `settings.py`:

```
INSTALLED_APPS += ["storages"]

DEFAULT_FILE_STORAGE = "storages.backends.s3boto3.S3Boto3Storage"

AWS_ACCESS_KEY_ID = "minioadmin"
AWS_SECRET_ACCESS_KEY = "minioadmin"
AWS_STORAGE_BUCKET_NAME = "media"
AWS_S3_ENDPOINT_URL = "http://localhost:9000"
AWS_S3_REGION_NAME = "us-east-1"
AWS_S3_SIGNATURE_VERSION = "s3v4"
AWS_S3_FILE_OVERWRITE = False
AWS_DEFAULT_ACL = None
```

Step 3: Create a Django Model with an `ImageField`:

```
from django.db import models

class UserProfile(models.Model):
    name = models.CharField(max_length=100)
    avatar = models.ImageField(upload_to='avatars/')

    def __str__(self):
        return self.name

```

Then run migrations and test uploading via Django admin or DRF if you're using it.

## 🧰 Step 4: Test File Upload and Access

When you upload an image, it will be stored in MinIO under the `media` bucket in the `avatars/` folder.

You can browse the files via:

- The MinIO Console at [http://localhost:9001](http://localhost:9001)
    
- Or access the files via S3-compatible URLs, e.g.:

```
http://localhost:9000/media/avatars/example.jpg
```

But this is not ideal, we want to make signed URLs to access our images, so we are going to create a script for it.

```
Insert Script From STL for this please
```
## 💡 Why Use MinIO for Local Dev?

- 💻 Works offline, fast and portable
    
- 🧪 Great for testing integrations with S3 APIs
    
- 🔁 Mimics production without needing to upload to AWS
    
- 🔐 Keeps secrets out of the cloud while developing
    

---

## ✅ Final Thoughts

MinIO is a fantastic drop-in S3 replacement for local or even private cloud setups. By integrating it with Django and `boto3`, you get all the benefits of object storage with full control.

Let me know if you'd like a follow-up guide on:

- Uploading via DRF endpoints
    
- Generating pre-signed S3 URLs
    
- Hosting MinIO behind a reverse proxy with HTTPS
