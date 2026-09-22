# Lab 3 – Container Image Build, Optimization, Tagging, Push and Vulnerability Scanning

## Aim

To build, optimize, tag and push an OCI-compliant container image using Docker and scan the image for security vulnerabilities.

## Technologies Used

* Docker
* Docker Hub
* Docker Scout
* Python
* Flask

## Project Structure

```text
lab3/
├── app.py
├── requirements.txt
├── Dockerfile
└── README.md
```

## 1. Build the Docker Image

The application was containerized using the following command:

```bash
docker build -t lab3-app:v1 .
```

The image was verified using:

```bash
docker images
```

## 2. Run the Container

The container was run using:

```bash
docker run -d -p 5001:5000 --name lab3-container lab3-app:v1
```

The application was tested at:

```text
http://localhost:5001
```

The application displayed:

```text
Lab 3 Docker Container is running!
```

## 3. Image Optimization

The Dockerfile uses:

```dockerfile
FROM python:3.11-slim
```

instead of the full Python image to reduce the image size.

The following command was also used:

```dockerfile
RUN pip install --no-cache-dir -r requirements.txt
```

This prevents pip's package cache from being stored in the image.

The Dockerfile also copies `requirements.txt` before the application source so that the dependency layer can be reused when only application code changes.

## 4. Image Tagging

The image was tagged with a version:

```bash
docker tag lab3-app:v1 eersay/lab3-app:v1
```

A `latest` tag was also created:

```bash
docker tag lab3-app:v1 eersay/lab3-app:latest
```

## 5. Push to Docker Hub

After logging in to Docker Hub:

```bash
docker login
```

the image was pushed using:

```bash
docker push eersay/lab3-app:v1
```

and:

```bash
docker push eersay/lab3-app:latest
```

## 6. Vulnerability Scanning

The container image was scanned using Docker Scout:

```bash
docker scout cves lab3-app:v1
```

The scan identified vulnerabilities in packages associated with the container image.

The vulnerability report was reviewed based on severity levels such as:

* Critical
* High
* Medium
* Low

The scan results were recorded as part of the security verification of the container image.

## Result

A Docker/OCI-compliant container image was successfully built and optimized. The image was tagged with version information, pushed to Docker Hub, and scanned for known vulnerabilities using Docker Scout.

## Conclusion

The experiment demonstrated the container image lifecycle:

```text
Application
     ↓
Dockerfile
     ↓
Build Image
     ↓
Optimize Image
     ↓
Tag Image
     ↓
Push to Docker Hub
     ↓
Vulnerability Scan
```
