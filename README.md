# Amazon S3 Integration with Spring Boot 🚀

A robust Spring Boot RESTful API application demonstrating integration with **Amazon Web Services (AWS) Simple Storage Service (S3)** for cloud-based file management, including file uploading, downloading, and deletion.

---

## 📌 Features

- **Upload Files**: Upload multipart files to an Amazon S3 bucket with automated timestamp prefixing to prevent naming collisions.
- **Download Files**: Retrieve and download stored files directly from AWS S3 as an attachment stream (`application/octet-stream`).
- **Delete Files**: Remove unwanted objects from the target S3 bucket via REST endpoint.
- **Configurable Limits**: Configured multipart file upload thresholds and size limits.

---

## 🛠️ Tech Stack & Dependencies

- **Java**: `1.8+`
- **Spring Boot**: `2.7.1`
- **Spring Cloud AWS**: `2.3.0` (`spring-cloud-starter-aws-messaging`, AWS S3 SDK)
- **Lombok**: Boilerplate reduction (logging & annotations)
- **Build Tool**: Maven

---

## 📁 Project Structure

```text
S3Bucket-Spring-Boot-App
│
├── src/main/java/com/owais/s3bucket
│   ├── S3bucketApplication.java         # Spring Boot Application Entry Point
│   ├── config
│   │   └── StorageConfig.java          # AWS S3 Client Bean Configuration
│   ├── controller
│   │   └── StorageController.java      # REST Endpoints (/file/*)
│   └── service
│       └── StorageService.java         # Business Logic & AWS S3 Operations
│
├── src/main/resources
│   ├── application.properties
│   └── application.yml                 # AWS Credentials & Server Configuration
│
└── pom.xml                             # Project Dependencies & Build Plugins
```

---

## ⚙️ Prerequisites & Setup

### 1. AWS Configuration
1. Create an **AWS Account** and sign in to the AWS Management Console.
2. Create an **Amazon S3 Bucket** (e.g., `your-bucket-name`).
3. Create an **IAM User** with permissions for S3 (`AmazonS3FullAccess` or a custom policy for PutObject, GetObject, DeleteObject).
4. Generate and copy your **Access Key ID** and **Secret Access Key**.

### 2. Application Configuration
Update `src/main/resources/application.yml` with your AWS credentials, bucket name, and region:

```yaml
cloud:
  aws:
    credentials:
      access-key: YOUR_AWS_ACCESS_KEY
      secret-key: YOUR_AWS_SECRET_KEY
    region:
      static: us-west-2
    stack:
      auto: false

application:
  bucket:
    name: YOUR_S3_BUCKET_NAME

spring:
  servlet:
    multipart:
      enabled: true
      file-size-threshold: 2MB
      max-file-size: 5MB
      max-request-size: 10MB

server:
  port: 9090
```

> ⚠️ **Security Tip**: Avoid pushing your sensitive AWS credentials (`access-key` and `secret-key`) to public version control. Consider using environment variables or AWS IAM roles.

---

## 🚀 Running the Application

### Using Maven Wrapper

**Windows (PowerShell / CMD):**
```bash
./mvnw.cmd spring-boot:run
```

**Linux / macOS:**
```bash
./mvnw spring-boot:run
```

The application will start on port `9090` (Base URL: `http://localhost:9090`).

---

## 📡 REST API Endpoints

Base URL: `http://localhost:9090/file`

| Method | Endpoint | Description | Request Body / Params | Response |
| :--- | :--- | :--- | :--- | :--- |
| `POST` | `/upload` | Upload a file to S3 | `form-data` with key `file` (`MultipartFile`) | Success message with generated file name |
| `GET` | `/download/{fileName}` | Download a file from S3 | Path variable: `fileName` | File stream (`application/octet-stream`) |
| `DELETE` | `/delete/{fileName}` | Delete a file from S3 | Path variable: `fileName` | Confirmation message |

---

### 🧪 API Usage Examples

#### 1. Upload File
```bash
curl -X POST http://localhost:9090/file/upload \
  -F "file=@/path/to/your/sample.txt"
```
**Response:**
```text
File Uploaded: 1657178492100_sample.txt
```

#### 2. Download File
```bash
curl -X GET http://localhost:9090/file/download/1657178492100_sample.txt \
  --output sample.txt
```

#### 3. Delete File
```bash
curl -X DELETE http://localhost:9090/file/delete/1657178492100_sample.txt
```
**Response:**
```text
1657178492100_sample.txt removed...
```
