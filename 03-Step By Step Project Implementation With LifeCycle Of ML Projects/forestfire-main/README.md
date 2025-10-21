# 🔥 Algerian Forest Fire Prediction System

A complete end-to-end machine learning project that predicts the **Fire Weather Index (FWI)** for Algerian forest fires using meteorological and environmental data. This project demonstrates the full ML lifecycle from data exploration to model deployment via a Flask web application.

---

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Dataset Description](#dataset-description)
- [Project Architecture](#project-architecture)
- [Technologies Used](#technologies-used)
- [Installation & Setup](#installation--setup)
- [How to Run](#how-to-run)
- [Model Performance](#model-performance)
- [Future Use Cases](#future-use-cases)
- [Project Structure](#project-structure)
- [Contributing](#contributing)

---

## 🎯 Project Overview

This project predicts the **Fire Weather Index (FWI)**, a critical metric used by forest services to assess fire danger levels. The system uses meteorological data (temperature, humidity, wind speed, rainfall) and fire indices (FFMC, DMC, ISI, BUI) to predict FWI values.

### Key Features:
- ✅ Complete ML pipeline: EDA → Feature Engineering → Model Training → Deployment
- ✅ Multiple regression models tested (Linear, Ridge, Lasso, ElasticNet)
- ✅ **Ridge Regression** selected as final model
- ✅ Interactive web interface for real-time predictions
- ✅ Scalable Flask application ready for deployment

---

## 📊 Dataset Description

**Source:** Algerian Forest Fires Dataset  
**Records:** 244 instances  
**Regions:** 2 (Bejaia and Sidi Bel-Abbes)  
**Time Period:** June-September 2012

### Features:
| Feature | Description | Type |
|---------|-------------|------|
| **Temperature** | Temperature in Celsius | Numeric |
| **RH** | Relative Humidity (%) | Numeric |
| **Ws** | Wind Speed (km/h) | Numeric |
| **Rain** | Rainfall (mm) | Numeric |
| **FFMC** | Fine Fuel Moisture Code | Numeric |
| **DMC** | Duff Moisture Code | Numeric |
| **ISI** | Initial Spread Index | Numeric |
| **Classes** | Fire/Not Fire | Categorical |
| **Region** | Bejaia (0) / Sidi Bel-Abbes (1) | Categorical |
| **FWI** | Fire Weather Index (Target) | Numeric |

---

## 🏗️ Project Architecture

```
Data Collection → EDA → Feature Engineering → Model Training → Evaluation → Deployment
```

### Workflow:
1. **EDA & Data Cleaning** (`2.0-EDA And FE Algerian Forest Fires.ipynb`)
   - Handle missing values
   - Remove duplicates
   - Encode categorical variables
   - Feature scaling using StandardScaler

2. **Model Training** (`3.0-Model Training.ipynb`)
   - Train multiple regression models:
     - Linear Regression
     - Ridge Regression (α = 0.1)
     - Lasso Regression (α = 0.1)
     - ElasticNet (α = 0.1, l1_ratio = 0.5)
   - Cross-validation (5-fold)
   - Model evaluation using R², MAE, RMSE

3. **Model Selection**
   - **Ridge Regression** chosen based on:
     - Best R² score: ~0.98
     - Low RMSE and MAE
     - Handles multicollinearity
     - Prevents overfitting

4. **Deployment**
   - Flask web application
   - Pickled model (`ridge.pkl`) and scaler (`scaler.pkl`)
   - HTML templates for user interface

---

## 🛠️ Technologies Used

### Libraries & Frameworks:
- **Python 3.x**
- **NumPy** - Numerical computations
- **Pandas** - Data manipulation
- **Scikit-learn** - Machine learning models
  - `LinearRegression`, `Ridge`, `Lasso`, `ElasticNet`
  - `StandardScaler` for feature scaling
  - `train_test_split` for data splitting
  - `cross_val_score` for model validation
- **Flask** - Web framework for deployment
- **Pickle** - Model serialization

### Regression Models:
1. **Ridge Regression (L2 Regularization)**
   - Formula: $\min_w \|Xw - y\|_2^2 + \alpha \|w\|_2^2$
   - Prevents overfitting by penalizing large coefficients
   
2. **Lasso Regression (L1 Regularization)**
   - Formula: $\min_w \frac{1}{2n} \|Xw - y\|_2^2 + \alpha \|w\|_1$
   - Feature selection via coefficient shrinkage

3. **ElasticNet (L1 + L2)**
   - Formula: $\min_w \frac{1}{2n} \|Xw - y\|_2^2 + \alpha \rho \|w\|_1 + \frac{\alpha(1-\rho)}{2} \|w\|_2^2$
   - Combines Ridge and Lasso benefits

---

## 📦 Installation & Setup

### Prerequisites:
- Python 3.7 or higher
- pip package manager

### Steps:

1. **Clone the repository**
```bash
git clone <repository-url>
cd forestfire-main
```

2. **Create virtual environment (recommended)**
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

---

## 🚀 How to Run

### Option 1: Run Flask Application

```bash
python application.py
```

Then open your browser and navigate to:
```
http://localhost:5000/
```

### Option 2: Run Notebooks (for training)

1. **Exploratory Data Analysis:**
   ```bash
   jupyter notebook notebooks/2.0-EDA\ And\ FE\ Algerian\ Forest\ Fires.ipynb
   ```

2. **Model Training:**
   ```bash
   jupyter notebook notebooks/3.0-Model\ Training.ipynb
   ```

### Input Parameters for Prediction:
When using the web interface, provide:
- Temperature (°C)
- Relative Humidity (%)
- Wind Speed (km/h)
- Rainfall (mm)
- FFMC
- DMC
- ISI
- Classes (0 = Not Fire, 1 = Fire)
- Region (0 = Bejaia, 1 = Sidi Bel-Abbes)

---

## 📈 Model Performance

| Model | R² Score | MAE | RMSE | Cross-Val Score |
|-------|----------|-----|------|-----------------|
| Linear Regression | 0.9786 | 0.5234 | 0.7821 | 0.9756 |
| **Ridge Regression** | **0.9812** | **0.4987** | **0.7341** | **0.9798** ✅ |
| Lasso Regression | 0.9791 | 0.5123 | 0.7652 | 0.9768 |
| ElasticNet | 0.9785 | 0.5201 | 0.7789 | 0.9761 |

**Selected Model:** Ridge Regression (α = 0.1)

---

## 🔮 Future Use Cases

### Immediate Applications:
1. **Real-time Fire Risk Monitoring**
   - Integrate with weather APIs for live predictions
   - Alert systems for forest departments

2. **Mobile Application**
   - Deploy as Android/iOS app for field officers
   - Offline prediction capability

3. **Dashboard & Analytics**
   - Historical trend analysis
   - Seasonal fire risk patterns
   - Regional comparison visualizations

### Advanced Enhancements:
1. **Deep Learning Models**
   - LSTM for time-series forecasting
   - CNN for satellite imagery integration

2. **Multi-region Expansion**
   - Extend to other geographical regions
   - Transfer learning for new datasets

3. **IoT Integration**
   - Real-time sensor data ingestion
   - Automated drone monitoring systems

4. **Cloud Deployment**
   - AWS/Azure/GCP hosting
   - Auto-scaling for high traffic
   - CI/CD pipeline integration

5. **Explainable AI**
   - SHAP/LIME for model interpretability
   - Feature importance visualization

---

## ☁️ AWS Deployment Guide

### AWS Services Used

This project can be deployed on AWS using the following services:

| AWS Service | Purpose | Cost Tier |
|-------------|---------|-----------|
| **AWS Elastic Beanstalk** | Application hosting & auto-scaling | Free tier available |
| **Amazon S3** | Model storage & static assets | Free tier: 5GB |
| **Amazon EC2** | Compute instances (via Beanstalk) | Free tier: 750 hrs/month |
| **AWS CodePipeline** | CI/CD automation | Free tier: 1 pipeline |
| **Amazon CloudWatch** | Monitoring & logging | Free tier available |
| **AWS IAM** | Access management | Always free |
| **Amazon RDS** (Optional) | Database for prediction logs | Free tier: 750 hrs |
| **Amazon API Gateway** (Optional) | RESTful API endpoints | Free tier: 1M requests |

---

### 🚀 AWS Deployment Methods

#### **Method 1: AWS Elastic Beanstalk (Recommended for Beginners)**

Elastic Beanstalk automatically handles deployment, capacity provisioning, load balancing, and auto-scaling.

##### **Step 1: Prepare Application Files**

Create `.ebextensions/python.config`:
```yaml
option_settings:
  aws:elasticbeanstalk:container:python:
    WSGIPath: application:app
```

##### **Step 2: Install AWS CLI & EB CLI**

```powershell
# Install AWS CLI
pip install awscli --upgrade

# Configure AWS credentials
aws configure
# Enter: Access Key ID, Secret Access Key, Region (e.g., us-east-1), Output format (json)

# Install Elastic Beanstalk CLI
pip install awsebcli --upgrade
```

##### **Step 3: Initialize Elastic Beanstalk**

```powershell
# Navigate to project directory
cd forestfire-main

# Initialize EB application
eb init -p python-3.9 forest-fire-predictor --region us-east-1

# Create environment and deploy
eb create forest-fire-env

# Open application in browser
eb open
```

##### **Step 4: Update Application**

```powershell
# After making changes
eb deploy

# Check status
eb status

# View logs
eb logs
```

##### **Step 5: Configure Environment Variables**

```powershell
# Set environment variables
eb setenv FLASK_ENV=production SECRET_KEY=your-secret-key

# Or via AWS Console: Configuration > Software > Environment properties
```

---

#### **Method 2: AWS EC2 with Manual Setup**

For complete control over the environment.

##### **Step 1: Launch EC2 Instance**

1. **AWS Console** → EC2 → Launch Instance
2. **AMI:** Ubuntu Server 22.04 LTS
3. **Instance Type:** t2.micro (free tier)
4. **Security Group:** Allow HTTP (80), HTTPS (443), SSH (22)
5. **Key Pair:** Create/download `.pem` file

##### **Step 2: Connect to EC2**

```powershell
# Convert .pem to .ppk if using PuTTY, or use WSL/Git Bash
ssh -i "your-key.pem" ubuntu@ec2-xx-xx-xx-xx.compute.amazonaws.com
```

##### **Step 3: Setup Application on EC2**

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Python and dependencies
sudo apt install python3-pip python3-venv nginx -y

# Clone repository
git clone <your-repo-url>
cd forestfire-main

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
pip install gunicorn

# Test application
gunicorn -b 0.0.0.0:8000 application:app
```

##### **Step 4: Configure Gunicorn as Systemd Service**

Create `/etc/systemd/system/forestfire.service`:
```ini
[Unit]
Description=Gunicorn instance for Forest Fire Prediction
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/forestfire-main
Environment="PATH=/home/ubuntu/forestfire-main/venv/bin"
ExecStart=/home/ubuntu/forestfire-main/venv/bin/gunicorn -w 4 -b 127.0.0.1:8000 application:app

[Install]
WantedBy=multi-user.target
```

```bash
# Enable and start service
sudo systemctl daemon-reload
sudo systemctl start forestfire
sudo systemctl enable forestfire
sudo systemctl status forestfire
```

##### **Step 5: Configure Nginx Reverse Proxy**

Create `/etc/nginx/sites-available/forestfire`:
```nginx
server {
    listen 80;
    server_name your-domain.com;  # or EC2 public IP

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    location /static {
        alias /home/ubuntu/forestfire-main/static;
    }
}
```

```bash
# Enable site
sudo ln -s /etc/nginx/sites-available/forestfire /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

---

#### **Method 3: AWS Lambda + API Gateway (Serverless)**

For cost-effective, event-driven architecture.

##### **Step 1: Create Lambda Function**

Create `lambda_function.py`:
```python
import json
import pickle
import numpy as np

# Load models (stored in Lambda layer or S3)
ridge_model = pickle.load(open('/tmp/ridge.pkl', 'rb'))
scaler = pickle.load(open('/tmp/scaler.pkl', 'rb'))

def lambda_handler(event, context):
    try:
        body = json.loads(event['body'])
        
        features = [[
            body['Temperature'], body['RH'], body['Ws'],
            body['Rain'], body['FFMC'], body['DMC'],
            body['ISI'], body['Classes'], body['Region']
        ]]
        
        scaled_features = scaler.transform(features)
        prediction = ridge_model.predict(scaled_features)
        
        return {
            'statusCode': 200,
            'headers': {'Content-Type': 'application/json'},
            'body': json.dumps({'FWI_prediction': float(prediction[0])})
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'error': str(e)})
        }
```

##### **Step 2: Package Dependencies**

```powershell
# Create deployment package
mkdir lambda_package
pip install -t lambda_package numpy pandas scikit-learn
cd lambda_package
# Copy lambda_function.py and model files
# Zip everything
Compress-Archive -Path * -DestinationPath ../lambda_deployment.zip
```

##### **Step 3: Deploy to Lambda**

```powershell
# Create Lambda function
aws lambda create-function `
    --function-name forest-fire-predictor `
    --runtime python3.9 `
    --role arn:aws:iam::YOUR_ACCOUNT_ID:role/lambda-execution-role `
    --handler lambda_function.lambda_handler `
    --zip-file fileb://lambda_deployment.zip `
    --timeout 30 `
    --memory-size 512
```

##### **Step 4: Create API Gateway**

1. **AWS Console** → API Gateway → Create REST API
2. Create resource `/predict` with POST method
3. Link to Lambda function
4. Deploy API to stage (e.g., `prod`)
5. Get endpoint URL: `https://xxxxxx.execute-api.us-east-1.amazonaws.com/prod/predict`

---

#### **Method 4: AWS ECS with Docker (Production-Grade)**

##### **Step 1: Create Dockerfile**

Create `Dockerfile`:
```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["gunicorn", "-b", "0.0.0.0:5000", "-w", "4", "application:app"]
```

##### **Step 2: Build and Push to Amazon ECR**

```powershell
# Authenticate Docker to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin YOUR_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com

# Create ECR repository
aws ecr create-repository --repository-name forest-fire-predictor

# Build Docker image
docker build -t forest-fire-predictor .

# Tag image
docker tag forest-fire-predictor:latest YOUR_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/forest-fire-predictor:latest

# Push to ECR
docker push YOUR_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/forest-fire-predictor:latest
```

##### **Step 3: Deploy to ECS**

1. **Create ECS Cluster** (Fargate or EC2)
2. **Create Task Definition** with your ECR image
3. **Create Service** with desired count
4. **Configure Load Balancer** (Application Load Balancer)
5. Access via ALB DNS name

---

### 🔐 AWS Security Best Practices

```powershell
# 1. Never hardcode credentials - use IAM roles
# 2. Store sensitive data in AWS Secrets Manager
aws secretsmanager create-secret --name forest-fire/db-credentials --secret-string '{"username":"admin","password":"xxxxx"}'

# 3. Enable CloudWatch logging
# 4. Use HTTPS with AWS Certificate Manager (ACM)
# 5. Implement WAF for API protection
# 6. Enable VPC for network isolation
```

---

### 📊 AWS Monitoring & Logging

```powershell
# CloudWatch Logs - View application logs
aws logs tail /aws/elasticbeanstalk/forest-fire-env/var/log/eb-activity.log --follow

# CloudWatch Metrics - Monitor application performance
# CPU Utilization, Request Count, Latency, Error Rate

# Set up alarms
aws cloudwatch put-metric-alarm `
    --alarm-name high-cpu-usage `
    --metric-name CPUUtilization `
    --namespace AWS/EC2 `
    --statistic Average `
    --period 300 `
    --threshold 80 `
    --comparison-operator GreaterThanThreshold
```

---

### 💰 Cost Optimization

| Strategy | Implementation | Savings |
|----------|----------------|---------|
| **Use Free Tier** | t2.micro EC2, 750 hrs/month | 100% for 1 year |
| **Auto-scaling** | Scale down during low traffic | 30-50% |
| **Reserved Instances** | 1-year commitment | 40% |
| **Lambda for APIs** | Pay per request | 60% vs EC2 |
| **S3 Lifecycle Policies** | Move old logs to Glacier | 70% |

---

### 🔄 CI/CD Pipeline with AWS CodePipeline

**Setup GitHub → AWS CodePipeline → Elastic Beanstalk:**

```yaml
# buildspec.yml (for CodeBuild)
version: 0.2

phases:
  install:
    runtime-versions:
      python: 3.9
  pre_build:
    commands:
      - echo Installing dependencies...
      - pip install -r requirements.txt
  build:
    commands:
      - echo Build started on `date`
      - python -m pytest tests/  # Run tests
  post_build:
    commands:
      - echo Build completed on `date`

artifacts:
  files:
    - '**/*'
```

**Pipeline Flow:**
1. Push code to GitHub
2. CodePipeline detects changes
3. CodeBuild runs tests
4. Auto-deploy to Elastic Beanstalk
5. CloudWatch monitors deployment

---

### 📱 Access Deployed Application

After deployment, your app will be available at:

- **Elastic Beanstalk:** `http://forest-fire-env.us-east-1.elasticbeanstalk.com`
- **EC2:** `http://ec2-xx-xx-xx-xx.compute.amazonaws.com`
- **API Gateway:** `https://xxxxxx.execute-api.us-east-1.amazonaws.com/prod/predict`
- **Custom Domain:** `https://forestfire.yourdomain.com` (via Route 53)

---

### 🛠️ Troubleshooting AWS Deployment

```powershell
# Elastic Beanstalk logs
eb logs --all

# EC2 instance logs
ssh -i key.pem ubuntu@ec2-ip
tail -f /var/log/nginx/error.log
sudo journalctl -u forestfire -f

# Lambda logs
aws logs tail /aws/lambda/forest-fire-predictor --follow

# Check deployment status
eb health
eb status
```

---

### 📚 AWS Resources & Documentation

- [AWS Free Tier](https://aws.amazon.com/free/)
- [Elastic Beanstalk Documentation](https://docs.aws.amazon.com/elasticbeanstalk/)
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/)
- [Amazon ECS Documentation](https://docs.aws.amazon.com/ecs/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

---

## 📁 Project Structure

```
forestfire-main/
│
├── application.py              # Flask application entry point
├── requirements.txt            # Python dependencies
├── README.md                   # Project documentation
│
├── dataset/
│   └── Algerian_forest_fires_cleaned_dataset.csv
│
├── models/
│   ├── ridge.pkl              # Trained Ridge model
│   └── scaler.pkl             # StandardScaler object
│
├── notebooks/
│   ├── 2.0-EDA And FE Algerian Forest Fires.ipynb
│   └── 3.0-Model Training.ipynb
│
└── templates/
    ├── index.html             # Landing page
    └── home.html              # Prediction interface
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is open-source and available for educational purposes.

---

## 👨‍💻 Author

**Anshul Parkar**  
GitHub: [@AnshulParkar](https://github.com/AnshulParkar)

---

## 📧 Contact

For questions or feedback, please open an issue or reach out via GitHub.

---

**⭐ If you find this project helpful, please give it a star!**
