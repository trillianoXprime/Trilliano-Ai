# Trilliano AI Deployment Guide

## Overview

This guide provides comprehensive instructions for deploying Trilliano AI to various cloud providers, including scaling considerations, cost analysis, and monitoring setup.

## Prerequisites

- Docker and Docker Compose installed
- Cloud provider account (AWS, GCP, Azure, or DigitalOcean)
- Domain name (optional but recommended)
- SSL certificate (Let's Encrypt recommended)

## Quick Start - Local Development

```bash
# Clone and setup
git clone <repository-url>
cd trilliano-ai
cp .env.example .env

# Configure environment variables
nano .env

# Start services
docker-compose up -d

# Access the application
# Backend: http://localhost:8000
# Frontend: http://localhost:3000
```

## Cloud Provider Deployment

### AWS Deployment

#### Option 1: EC2 with Docker Compose

**Instance Requirements:**
- Instance Type: t3.large (2 vCPU, 8GB RAM) minimum
- Storage: 50GB EBS volume
- Security Groups: Allow ports 80, 443, 8000, 3000

**Setup Steps:**

```bash
# 1. Launch EC2 instance with Ubuntu 22.04
# 2. Install Docker and Docker Compose
sudo apt update
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker ubuntu

# 3. Clone repository and configure
git clone <repository-url>
cd trilliano-ai
cp .env.production.example .env

# 4. Configure environment variables
sudo nano .env

# 5. Deploy with production compose
docker-compose -f docker-compose.prod.yml up -d

# 6. Setup reverse proxy (Nginx)
sudo apt install -y nginx certbot python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com
```

**Cost Estimate (Monthly):**
- t3.large EC2: ~$60
- 50GB EBS: ~$5
- Data transfer: ~$10-50
- **Total: ~$75-115/month**

#### Option 2: ECS with Fargate

**Setup with AWS CLI:**

```bash
# 1. Create ECS cluster
aws ecs create-cluster --cluster-name trilliano-cluster

# 2. Create task definition
aws ecs register-task-definition --cli-input-json file://aws/task-definition.json

# 3. Create service
aws ecs create-service \
  --cluster trilliano-cluster \
  --service-name trilliano-service \
  --task-definition trilliano-task \
  --desired-count 1 \
  --launch-type FARGATE \
  --network-configuration "awsvpcConfiguration={subnets=[subnet-xxx],securityGroups=[sg-xxx],assignPublicIp=ENABLED}"
```

**Cost Estimate (Monthly):**
- Fargate (1 vCPU, 2GB): ~$30
- Application Load Balancer: ~$20
- Data transfer: ~$10-30
- **Total: ~$60-80/month**

### Google Cloud Platform (GCP)

#### Cloud Run Deployment

**Setup Steps:**

```bash
# 1. Build and push container images
gcloud builds submit --tag gcr.io/PROJECT_ID/trilliano-backend backend/
gcloud builds submit --tag gcr.io/PROJECT_ID/trilliano-frontend frontend/

# 2. Deploy backend service
gcloud run deploy trilliano-backend \
  --image gcr.io/PROJECT_ID/trilliano-backend \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --memory 2Gi \
  --cpu 1

# 3. Deploy frontend service
gcloud run deploy trilliano-frontend \
  --image gcr.io/PROJECT_ID/trilliano-frontend \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --memory 1Gi \
  --cpu 1
```

**Cost Estimate (Monthly):**
- Cloud Run (backend): ~$25-40
- Cloud Run (frontend): ~$15-25
- Cloud SQL (optional): ~$25
- **Total: ~$65-90/month**

### Microsoft Azure

#### Container Instances Deployment

```bash
# 1. Create resource group
az group create --name trilliano-rg --location eastus

# 2. Create container group
az container create \
  --resource-group trilliano-rg \
  --name trilliano-app \
  --image your-registry/trilliano:latest \
  --cpu 2 \
  --memory 4 \
  --ports 80 443 \
  --environment-variables \
    DATABASE_URL=sqlite:///data/trilliano.db \
    OPENAI_API_KEY=your-key

# 3. Setup Application Gateway for SSL termination
az network application-gateway create \
  --name trilliano-gateway \
  --resource-group trilliano-rg \
  --capacity 2 \
  --sku Standard_v2
```

**Cost Estimate (Monthly):**
- Container Instances: ~$50-70
- Application Gateway: ~$25
- Storage: ~$5
- **Total: ~$80-100/month**

### DigitalOcean

#### Droplet Deployment

```bash
# 1. Create droplet (4GB RAM, 2 vCPUs)
doctl compute droplet create trilliano-app \
  --size s-2vcpu-4gb \
  --image ubuntu-22-04-x64 \
  --region nyc1 \
  --ssh-keys your-ssh-key-id

# 2. Setup application
ssh root@droplet-ip
apt update && apt install -y docker.io docker-compose
git clone <repository-url>
cd trilliano-ai
cp .env.production.example .env
docker-compose -f docker-compose.prod.yml up -d
```

**Cost Estimate (Monthly):**
- 4GB Droplet: ~$24
- Load Balancer: ~$12
- Managed Database: ~$15
- **Total: ~$51/month**

## Scaling Considerations

### Horizontal Scaling

#### Load Balancer Configuration

**Nginx Load Balancer:**

```nginx
upstream backend {
    server backend-1:8000;
    server backend-2:8000;
    server backend-3:8000;
}

upstream frontend {
    server frontend-1:3000;
    server frontend-2:3000;
}

server {
    listen 80;
    server_name yourdomain.com;

    location /api/ {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location / {
        proxy_pass http://frontend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

#### Auto-scaling Configuration

**Docker Swarm:**

```yaml
# docker-compose.swarm.yml
version: '3.8'
services:
  backend:
    image: trilliano/backend:latest
    deploy:
      replicas: 3
      update_config:
        parallelism: 1
        delay: 10s
      restart_policy:
        condition: on-failure
      resources:
        limits:
          memory: 2G
        reservations:
          memory: 1G
    networks:
      - trilliano-network

  frontend:
    image: trilliano/frontend:latest
    deploy:
      replicas: 2
      update_config:
        parallelism: 1
        delay: 10s
      restart_policy:
        condition: on-failure
    networks:
      - trilliano-network
```

**Kubernetes Deployment:**

```yaml
# k8s/backend-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: trilliano-backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: trilliano-backend
  template:
    metadata:
      labels:
        app: trilliano-backend
    spec:
      containers:
      - name: backend
        image: trilliano/backend:latest
        ports:
        - containerPort: 8000
        resources:
          requests:
            memory: "1Gi"
            cpu: "500m"
          limits:
            memory: "2Gi"
            cpu: "1000m"
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: trilliano-secrets
              key: database-url
---
apiVersion: v1
kind: Service
metadata:
  name: trilliano-backend-service
spec:
  selector:
    app: trilliano-backend
  ports:
  - port: 8000
    targetPort: 8000
  type: ClusterIP
```

### Vertical Scaling

#### Resource Requirements by Load

**Light Load (< 100 concurrent users):**
- CPU: 2 cores
- RAM: 4GB
- Storage: 50GB
- Estimated cost: $50-75/month

**Medium Load (100-1000 concurrent users):**
- CPU: 4-8 cores
- RAM: 8-16GB
- Storage: 100GB
- Estimated cost: $150-300/month

**Heavy Load (1000+ concurrent users):**
- CPU: 16+ cores
- RAM: 32+ GB
- Storage: 500GB+
- Estimated cost: $500-1000+/month

### Database Scaling

#### SQLite Limitations and Migration

**When to migrate from SQLite:**
- > 1000 concurrent users
- > 100GB database size
- Need for high availability

**PostgreSQL Migration:**

```python
# backend/models/database.py
import os
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Support both SQLite and PostgreSQL
DATABASE_URL = os.getenv("DATABASE_URL", "sqlite:///./trilliano.db")

if DATABASE_URL.startswith("postgresql"):
    engine = create_engine(DATABASE_URL, pool_size=20, max_overflow=0)
else:
    engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()
```

## Cost Analysis

### Cost Breakdown by Component

#### Infrastructure Costs

| Component | Small | Medium | Large |
|-----------|-------|--------|-------|
| Compute | $30-50 | $100-200 | $300-500 |
| Database | $0-25 | $25-100 | $100-300 |
| Storage | $5-10 | $20-50 | $100-200 |
| Network | $10-20 | $50-100 | $200-500 |
| **Total** | **$45-105** | **$195-450** | **$700-1500** |

#### API Costs (Monthly)

| Provider | Light Usage | Medium Usage | Heavy Usage |
|----------|-------------|--------------|-------------|
| OpenAI GPT-4 | $50-100 | $200-500 | $1000-2000 |
| Anthropic Claude | $40-80 | $150-400 | $800-1500 |
| Replicate (Images) | $20-50 | $100-200 | $500-1000 |
| **Total APIs** | **$110-230** | **$450-1100** | **$2300-4500** |

#### Total Cost Estimates

**Startup/Development:**
- Infrastructure: $50-100/month
- APIs: $100-200/month
- **Total: $150-300/month**

**Small Business:**
- Infrastructure: $200-400/month
- APIs: $500-1000/month
- **Total: $700-1400/month**

**Enterprise:**
- Infrastructure: $1000-2000/month
- APIs: $2000-5000/month
- **Total: $3000-7000/month**

### Cost Optimization Strategies

#### 1. Model Selection Optimization

```python
# backend/adapters/llm.py - Cost-aware model selection
class CostOptimizedLLMAdapter:
    def __init__(self):
        self.model_costs = {
            "gpt-4": 0.03,  # per 1K tokens
            "gpt-3.5-turbo": 0.002,
            "claude-3-sonnet": 0.015,
            "local-llama": 0.0  # Only compute costs
        }
    
    async def select_optimal_model(self, complexity_score: float, budget_limit: float):
        if budget_limit < 0.01:
            return "local-llama"
        elif complexity_score < 0.5:
            return "gpt-3.5-turbo"
        else:
            return "gpt-4"
```

#### 2. Caching Strategy

```python
# backend/services/cache.py
import redis
from typing import Optional

class ResponseCache:
    def __init__(self):
        self.redis_client = redis.Redis(host='localhost', port=6379, db=0)
        self.cache_ttl = 3600  # 1 hour
    
    async def get_cached_response(self, prompt_hash: str) -> Optional[str]:
        return self.redis_client.get(f"response:{prompt_hash}")
    
    async def cache_response(self, prompt_hash: str, response: str):
        self.redis_client.setex(f"response:{prompt_hash}", self.cache_ttl, response)
```

#### 3. Resource Scheduling

```yaml
# k8s/hpa.yaml - Horizontal Pod Autoscaler
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: trilliano-backend-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: trilliano-backend
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
```

## Monitoring and Alerting

### Monitoring Stack Setup

#### Prometheus + Grafana

**Docker Compose Monitoring Stack:**

```yaml
# monitoring/docker-compose.monitoring.yml
version: '3.8'
services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3001:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana_data:/var/lib/grafana
      - ./grafana/dashboards:/etc/grafana/provisioning/dashboards
      - ./grafana/datasources:/etc/grafana/provisioning/datasources

  node-exporter:
    image: prom/node-exporter:latest
    ports:
      - "9100:9100"
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.ignored-mount-points=^/(sys|proc|dev|host|etc)($$|/)'

volumes:
  prometheus_data:
  grafana_data:
```

**Prometheus Configuration:**

```yaml
# monitoring/prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'trilliano-backend'
    static_configs:
      - targets: ['backend:8000']
    metrics_path: '/metrics'
    scrape_interval: 5s

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']

  - job_name: 'postgres'
    static_configs:
      - targets: ['postgres-exporter:9187']

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - alertmanager:9093
```

#### Application Metrics

**Backend Metrics Integration:**

```python
# backend/app/metrics.py
from prometheus_client import Counter, Histogram, Gauge, generate_latest
from fastapi import Response
import time

# Metrics definitions
REQUEST_COUNT = Counter('http_requests_total', 'Total HTTP requests', ['method', 'endpoint', 'status'])
REQUEST_DURATION = Histogram('http_request_duration_seconds', 'HTTP request duration')
ACTIVE_SESSIONS = Gauge('active_sessions_total', 'Number of active sessions')
MODEL_INFERENCE_TIME = Histogram('model_inference_duration_seconds', 'Model inference time', ['model_type'])
API_COSTS = Counter('api_costs_total', 'Total API costs in USD', ['provider'])

class MetricsMiddleware:
    def __init__(self, app):
        self.app = app
    
    async def __call__(self, scope, receive, send):
        if scope["type"] == "http":
            start_time = time.time()
            
            # Process request
            await self.app(scope, receive, send)
            
            # Record metrics
            duration = time.time() - start_time
            REQUEST_DURATION.observe(duration)
            REQUEST_COUNT.labels(
                method=scope["method"],
                endpoint=scope["path"],
                status="200"  # Simplified
            ).inc()

@app.get("/metrics")
async def metrics():
    return Response(generate_latest(), media_type="text/plain")
```

### Alert Rules

**Prometheus Alert Rules:**

```yaml
# monitoring/alert_rules.yml
groups:
  - name: trilliano_alerts
    rules:
      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value }} errors per second"

      - alert: HighResponseTime
        expr: histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m])) > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High response time detected"
          description: "95th percentile response time is {{ $value }} seconds"

      - alert: HighMemoryUsage
        expr: (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes > 0.9
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High memory usage"
          description: "Memory usage is {{ $value | humanizePercentage }}"

      - alert: HighCPUUsage
        expr: 100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage"
          description: "CPU usage is {{ $value }}%"

      - alert: DatabaseConnectionFailure
        expr: up{job="postgres"} == 0
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "Database connection failure"
          description: "Cannot connect to database"

      - alert: HighAPICosts
        expr: increase(api_costs_total[1h]) > 100
        for: 0m
        labels:
          severity: warning
        annotations:
          summary: "High API costs detected"
          description: "API costs in the last hour: ${{ $value }}"
```

### Grafana Dashboards

**Main Application Dashboard:**

```json
{
  "dashboard": {
    "title": "Trilliano AI Monitoring",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])",
            "legendFormat": "{{method}} {{endpoint}}"
          }
        ]
      },
      {
        "title": "Response Time",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          },
          {
            "expr": "histogram_quantile(0.50, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "50th percentile"
          }
        ]
      },
      {
        "title": "Active Sessions",
        "type": "singlestat",
        "targets": [
          {
            "expr": "active_sessions_total"
          }
        ]
      },
      {
        "title": "API Costs (Hourly)",
        "type": "graph",
        "targets": [
          {
            "expr": "increase(api_costs_total[1h])",
            "legendFormat": "{{provider}}"
          }
        ]
      }
    ]
  }
}
```

### Log Management

#### Centralized Logging with ELK Stack

**Logstash Configuration:**

```yaml
# logging/logstash.conf
input {
  beats {
    port => 5044
  }
}

filter {
  if [fields][service] == "trilliano-backend" {
    grok {
      match => { "message" => "%{TIMESTAMP_ISO8601:timestamp} %{LOGLEVEL:level} %{GREEDYDATA:message}" }
    }
    
    if [level] == "ERROR" {
      mutate {
        add_tag => ["error"]
      }
    }
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "trilliano-%{+YYYY.MM.dd}"
  }
}
```

**Application Logging Configuration:**

```python
# backend/app/logging_config.py
import logging
import json
from datetime import datetime

class JSONFormatter(logging.Formatter):
    def format(self, record):
        log_entry = {
            "timestamp": datetime.utcnow().isoformat(),
            "level": record.levelname,
            "message": record.getMessage(),
            "module": record.module,
            "function": record.funcName,
            "line": record.lineno
        }
        
        if hasattr(record, 'session_id'):
            log_entry["session_id"] = record.session_id
        
        if hasattr(record, 'user_id'):
            log_entry["user_id"] = record.user_id
            
        return json.dumps(log_entry)

# Configure logging
logging.basicConfig(
    level=logging.INFO,
    handlers=[
        logging.StreamHandler(),
        logging.FileHandler('/var/log/trilliano/app.log')
    ]
)

# Set JSON formatter for structured logging
for handler in logging.root.handlers:
    handler.setFormatter(JSONFormatter())
```

### Health Checks

**Comprehensive Health Check Endpoint:**

```python
# backend/api/health.py
from fastapi import APIRouter, HTTPException
from sqlalchemy import text
from backend.models.database import SessionLocal
from backend.adapters.llm_factory import LLMFactory
import asyncio
import time

router = APIRouter()

@router.get("/health")
async def health_check():
    checks = {
        "database": await check_database(),
        "llm_models": await check_llm_models(),
        "disk_space": await check_disk_space(),
        "memory": await check_memory_usage()
    }
    
    overall_status = "healthy" if all(check["status"] == "healthy" for check in checks.values()) else "unhealthy"
    
    return {
        "status": overall_status,
        "timestamp": time.time(),
        "checks": checks
    }

async def check_database():
    try:
        db = SessionLocal()
        db.execute(text("SELECT 1"))
        db.close()
        return {"status": "healthy", "response_time": "< 100ms"}
    except Exception as e:
        return {"status": "unhealthy", "error": str(e)}

async def check_llm_models():
    try:
        llm_factory = LLMFactory()
        adapter = await llm_factory.get_adapter("default")
        # Quick test inference
        response = await adapter.generate_text("test", {"max_tokens": 1})
        return {"status": "healthy", "models_available": True}
    except Exception as e:
        return {"status": "unhealthy", "error": str(e)}
```

## Security Considerations

### SSL/TLS Configuration

**Let's Encrypt with Certbot:**

```bash
# Install certbot
sudo apt install certbot python3-certbot-nginx

# Obtain certificate
sudo certbot --nginx -d yourdomain.com -d api.yourdomain.com

# Auto-renewal
sudo crontab -e
# Add: 0 12 * * * /usr/bin/certbot renew --quiet
```

### Firewall Configuration

**UFW Setup:**

```bash
# Enable UFW
sudo ufw enable

# Allow SSH
sudo ufw allow ssh

# Allow HTTP/HTTPS
sudo ufw allow 80
sudo ufw allow 443

# Allow application ports (if needed)
sudo ufw allow 8000
sudo ufw allow 3000

# Deny all other incoming
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### Environment Security

**Secrets Management:**

```bash
# Use Docker secrets for production
echo "your-secret-key" | docker secret create openai_api_key -
echo "your-db-password" | docker secret create db_password -
```

```yaml
# docker-compose.prod.yml with secrets
version: '3.8'
services:
  backend:
    image: trilliano/backend:latest
    secrets:
      - openai_api_key
      - db_password
    environment:
      - OPENAI_API_KEY_FILE=/run/secrets/openai_api_key
      - DB_PASSWORD_FILE=/run/secrets/db_password

secrets:
  openai_api_key:
    external: true
  db_password:
    external: true
```

## Backup and Disaster Recovery

### Database Backup Strategy

**Automated Backup Script:**

```bash
#!/bin/bash
# scripts/backup-database.sh

BACKUP_DIR="/backups"
DATE=$(date +%Y%m%d_%H%M%S)
DB_FILE="/data/trilliano.db"

# Create backup directory
mkdir -p $BACKUP_DIR

# SQLite backup
sqlite3 $DB_FILE ".backup $BACKUP_DIR/trilliano_$DATE.db"

# Compress backup
gzip "$BACKUP_DIR/trilliano_$DATE.db"

# Upload to cloud storage (AWS S3 example)
aws s3 cp "$BACKUP_DIR/trilliano_$DATE.db.gz" s3://your-backup-bucket/database/

# Clean up old local backups (keep last 7 days)
find $BACKUP_DIR -name "trilliano_*.db.gz" -mtime +7 -delete

echo "Backup completed: trilliano_$DATE.db.gz"
```

**Cron Job Setup:**

```bash
# Add to crontab
0 2 * * * /path/to/scripts/backup-database.sh >> /var/log/backup.log 2>&1
```

### Application State Backup

**Configuration and Data Backup:**

```bash
#!/bin/bash
# scripts/backup-application.sh

BACKUP_DIR="/backups/app"
DATE=$(date +%Y%m%d_%H%M%S)

# Create backup directory
mkdir -p $BACKUP_DIR

# Backup configuration files
tar -czf "$BACKUP_DIR/config_$DATE.tar.gz" \
  .env \
  docker-compose.prod.yml \
  nginx.conf \
  /etc/letsencrypt/

# Backup user uploads and generated content
tar -czf "$BACKUP_DIR/data_$DATE.tar.gz" \
  /data/uploads/ \
  /data/generated_images/ \
  /data/logs/

# Upload to cloud storage
aws s3 sync $BACKUP_DIR s3://your-backup-bucket/application/

echo "Application backup completed: $DATE"
```

## Troubleshooting Guide

### Common Issues and Solutions

#### 1. High Memory Usage

**Symptoms:**
- Application becomes slow or unresponsive
- Out of memory errors in logs

**Solutions:**
```bash
# Check memory usage
free -h
docker stats

# Restart services to clear memory leaks
docker-compose restart backend

# Increase swap space
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

#### 2. Database Connection Issues

**Symptoms:**
- "Database connection failed" errors
- Slow query responses

**Solutions:**
```bash
# Check database file permissions
ls -la /data/trilliano.db

# Check disk space
df -h

# Restart database container
docker-compose restart database

# Check database integrity
sqlite3 /data/trilliano.db "PRAGMA integrity_check;"
```

#### 3. API Rate Limiting

**Symptoms:**
- "Rate limit exceeded" errors
- Slow API responses

**Solutions:**
```python
# Implement exponential backoff
import asyncio
import random

async def api_call_with_backoff(func, max_retries=3):
    for attempt in range(max_retries):
        try:
            return await func()
        except RateLimitError:
            if attempt == max_retries - 1:
                raise
            wait_time = (2 ** attempt) + random.uniform(0, 1)
            await asyncio.sleep(wait_time)
```

#### 4. SSL Certificate Issues

**Symptoms:**
- "SSL certificate expired" errors
- Browser security warnings

**Solutions:**
```bash
# Check certificate expiration
sudo certbot certificates

# Renew certificates
sudo certbot renew

# Test renewal process
sudo certbot renew --dry-run

# Restart nginx
sudo systemctl restart nginx
```

### Performance Optimization

#### 1. Database Optimization

```sql
-- Add indexes for common queries
CREATE INDEX idx_conversations_session_timestamp 
ON conversations(session_id, timestamp);

CREATE INDEX idx_moderation_logs_timestamp 
ON moderation_logs(timestamp);

-- Analyze query performance
EXPLAIN QUERY PLAN SELECT * FROM conversations WHERE session_id = ?;
```

#### 2. Caching Implementation

```python
# Redis caching for expensive operations
import redis
import json
import hashlib

class CacheManager:
    def __init__(self):
        self.redis_client = redis.Redis(host='redis', port=6379, db=0)
    
    def cache_key(self, prefix: str, data: dict) -> str:
        data_str = json.dumps(data, sort_keys=True)
        hash_obj = hashlib.md5(data_str.encode())
        return f"{prefix}:{hash_obj.hexdigest()}"
    
    async def get_or_set(self, key: str, func, ttl: int = 3600):
        cached = self.redis_client.get(key)
        if cached:
            return json.loads(cached)
        
        result = await func()
        self.redis_client.setex(key, ttl, json.dumps(result))
        return result
```

## Maintenance Procedures

### Regular Maintenance Tasks

#### Daily Tasks
- Check application logs for errors
- Monitor resource usage (CPU, memory, disk)
- Verify backup completion
- Check SSL certificate status

#### Weekly Tasks
- Review performance metrics
- Update security patches
- Clean up old log files
- Test disaster recovery procedures

#### Monthly Tasks
- Review and optimize database performance
- Update dependencies and security patches
- Analyze cost reports and optimize resources
- Review and update monitoring alerts

### Update Procedures

**Application Updates:**

```bash
#!/bin/bash
# scripts/update-application.sh

# Pull latest images
docker-compose pull

# Create backup before update
./scripts/backup-application.sh

# Update services with zero downtime
docker-compose up -d --no-deps backend
sleep 30
docker-compose up -d --no-deps frontend

# Verify deployment
curl -f http://localhost:8000/health || exit 1

echo "Update completed successfully"
```

**Security Updates:**

```bash
#!/bin/bash
# scripts/security-update.sh

# Update system packages
sudo apt update && sudo apt upgrade -y

# Update Docker images
docker-compose pull

# Restart services
docker-compose down && docker-compose up -d

# Check for vulnerabilities
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
  aquasec/trivy image trilliano/backend:latest
```

This comprehensive deployment guide provides everything needed to successfully deploy, scale, monitor, and maintain Trilliano AI in production environments.