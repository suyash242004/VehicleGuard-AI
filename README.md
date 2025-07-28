# VehicleGuard-AI: End-to-End Vehicle Insurance Prediction MLOps Pipeline

[![Python 3.10](https://img.shields.io/badge/python-3.10-blue.svg)](https://www.python.org/downloads/release/python-3100/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green.svg)](https://www.mongodb.com/cloud/atlas)
[![AWS](https://img.shields.io/badge/AWS-Cloud-orange.svg)](https://aws.amazon.com/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-blue.svg)](https://www.docker.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-brightgreen.svg)](https://github.com/features/actions)

## 🚗 Project Overview

VehicleGuard-AI is a comprehensive end-to-end MLOps solution for predicting vehicle insurance claims and risk assessment. This project leverages machine learning algorithms to analyze customer data and vehicle characteristics to predict insurance claim likelihood, helping insurance companies make data-driven decisions on pricing and risk assessment.

## 🎯 Business Problem

Insurance companies need accurate forecasting of insurance claims as the evolution of claims determines cash outflows, pricing, and profitability of insurance coverage. Machine learning can consider various variables such as automobile brand and model, driver's age and experience, and location to make highly accurate predictions.

## ✨ Key Features

- **End-to-End MLOps Pipeline**: Complete automation from data ingestion to model deployment
- **Real-time Predictions**: Web application for instant insurance risk assessment
- **Scalable Architecture**: Cloud-native design with AWS integration
- **Model Monitoring**: Continuous model evaluation and retraining capabilities
- **CI/CD Integration**: Automated deployment pipeline using GitHub Actions
- **Data Validation**: Robust data quality checks and schema validation

## 🏗️ Architecture

```
├── Data Ingestion (MongoDB Atlas)
├── Data Validation & Quality Checks
├── Data Transformation & Feature Engineering
├── Model Training & Evaluation
├── Model Registry (AWS S3)
├── Model Deployment (AWS EC2)
└── Monitoring & Logging
```

## 🛠️ Technology Stack

- **Programming Language**: Python 3.10
- **Database**: MongoDB Atlas
- **Cloud Services**: AWS (EC2, S3, ECR)
- **Containerization**: Docker
- **Web Framework**: FastAPI
- **ML Libraries**: Scikit-learn, Pandas, NumPy
- **CI/CD**: GitHub Actions
- **Monitoring**: Custom logging system

## 📋 Prerequisites

Before setting up the project, ensure you have:

- Python 3.10 installed
- MongoDB Atlas account
- AWS account with appropriate permissions
- Docker installed (for deployment)
- Git installed

## 🚀 Quick Start

### 1. Project Setup

```bash
# Clone the repository
git clone https://github.com/suyash242004/VehicleGuard-AI.git
cd MLOPS-Proj1

# Create project template
python template.py
```

### 2. Environment Setup

```bash
# Create and activate virtual environment
conda create -n vehicle python=3.10 -y
conda activate vehicle

# Install requirements
pip install -r requirements.txt

# Verify local packages installation
pip list
```

### 3. Database Configuration

#### MongoDB Atlas Setup:

1. Sign up to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new project
3. Create M0 cluster (free tier)
4. Setup database user credentials
5. Configure network access (0.0.0.0/0 for development)
6. Get connection string

#### Set Environment Variables:

**For Bash/Linux/Mac:**

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/"
echo $MONGODB_URL
```

**For Windows PowerShell:**

```powershell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster.mongodb.net/"
echo $env:MONGODB_URL
```

### 4. AWS Configuration

#### AWS Account Setup:

1. Create IAM user with AdministratorAccess policy
2. Generate Access Keys
3. Create S3 bucket: `my-model-mlopsproj` (region: us-east-1)
4. Set up ECR repository for Docker images

#### Set AWS Environment Variables:

```bash
# Bash/Linux/Mac
export AWS_ACCESS_KEY_ID="your_access_key"
export AWS_SECRET_ACCESS_KEY="your_secret_key"

# Windows PowerShell
$env:AWS_ACCESS_KEY_ID="your_access_key"
$env:AWS_SECRET_ACCESS_KEY="your_secret_key"
```

## 📁 Project Structure

```
├── artifacts/                 # Generated artifacts (ignored in git)
├── notebooks/                 # Jupyter notebooks for EDA
│   ├── mongoDB_demo.ipynb
│   └── EDA_Feature_Engineering.ipynb
├── src/
│   ├── components/            # ML pipeline components
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   ├── configuration/         # Configuration files
│   │   ├── mongo_db_connections.py
│   │   └── aws_connection.py
│   ├── entity/               # Data classes and entities
│   │   ├── config_entity.py
│   │   ├── artifact_entity.py
│   │   ├── estimator.py
│   │   └── s3_estimator.py
│   ├── pipeline/             # Training and prediction pipelines
│   ├── utils/                # Utility functions
│   ├── logger/               # Logging configuration
│   └── exception/            # Custom exception handling
├── static/                   # Static files for web app
├── templates/                # HTML templates
├── .github/workflows/        # CI/CD configuration
├── config/
│   └── schema.yaml          # Data schema validation
├── app.py                   # Flask web application
├── demo.py                  # Testing script
├── requirements.txt         # Python dependencies
├── Dockerfile              # Docker configuration
└── README.md               # Project documentation
```

## 🔄 MLOps Pipeline Workflow

### 1. Data Ingestion

- Connects to MongoDB Atlas
- Fetches data in key-value format
- Transforms to pandas DataFrame
- Validates data integrity

### 2. Data Validation

- Schema validation using `config/schema.yaml`
- Data quality checks
- Missing value analysis
- Outlier detection

### 3. Data Transformation

- Feature engineering
- Data preprocessing
- Encoding categorical variables
- Scaling numerical features

### 4. Model Training

- Multiple algorithm comparison
- Hyperparameter tuning
- Cross-validation
- Model selection based on performance metrics

### 5. Model Evaluation

- Performance metrics calculation
- Model comparison with baseline
- Threshold-based model acceptance
- Model versioning

### 6. Model Deployment

- Model registry in AWS S3
- Containerized deployment
- Real-time prediction API
- Health monitoring

## 🌐 Web Application

The project includes a Flask web application that provides:

- **Home Page**: User-friendly interface for insurance prediction
- **Prediction Form**: Input form for customer and vehicle details
- **Results Page**: Prediction results with confidence scores
- **Training Endpoint**: `/training` route for model retraining

### Running the Application Locally

```bash
python app.py
```

Access the application at `http://localhost:5000`

## 🐳 Docker Deployment

### Build Docker Image

```bash
docker build -t vehicle-insurance-app .
```

### Run Container

```bash
docker run -p 5000:5000 vehicle-insurance-app
```

## ☁️ Cloud Deployment

### AWS EC2 Deployment

1. **Launch EC2 Instance:**

   - AMI: Ubuntu Server 24.04
   - Instance Type: t2.medium
   - Storage: 30GB
   - Security Group: Allow HTTP, HTTPS, and custom TCP (5080)

2. **Setup Docker on EC2:**

   ```bash
   sudo apt-get update -y
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```

3. **Configure GitHub Self-Hosted Runner:**
   - Go to Repository Settings → Actions → Runners
   - Follow setup instructions for Linux
   - Configure runner on EC2 instance

### CI/CD Pipeline

The project uses GitHub Actions for automated deployment:

#### Required Secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_DEFAULT_REGION`
- `ECR_REPO`

#### Deployment Trigger:

- Automatic deployment on push to main branch
- Docker image building and pushing to ECR
- EC2 instance deployment

## 📊 Model Performance

The model evaluation includes:

- **Accuracy Metrics**: Precision, Recall, F1-score
- **ROC-AUC**: Area under the ROC curve
- **Confusion Matrix**: Classification performance visualization
- **Feature Importance**: Key factors influencing predictions

## 🔍 Monitoring & Logging

- **Custom Logger**: Structured logging throughout the pipeline
- **Exception Handling**: Comprehensive error tracking
- **Model Drift Detection**: Monitoring for data and model drift
- **Performance Tracking**: Real-time model performance metrics

## 🧪 Testing

```bash
# Run data ingestion test
python demo.py

# Test MongoDB connection
jupyter notebook notebooks/mongoDB_demo.ipynb

# Explore data
jupyter notebook notebooks/EDA_Feature_Engineering.ipynb
```

## 📝 Configuration

### Key Configuration Files:

- **`constants/__init__.py`**: Project constants and thresholds
- **`config/schema.yaml`**: Data validation schema
- **`requirements.txt`**: Python dependencies

### Environment Variables:

```bash
MONGODB_URL=mongodb+srv://username:password@cluster.mongodb.net/
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_DEFAULT_REGION=us-east-1
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Team

- **Developer**: [Suyash](https://github.com/suyash242004)
- **Project Type**: End-to-End MLOps Implementation

## 🙏 Acknowledgments

- MongoDB Atlas for database services
- AWS for cloud infrastructure
- Open-source ML libraries and tools
- Insurance industry datasets and research

## 📞 Support

For support and questions:

- Create an [Issue](https://github.com/suyash242004/VehicleGuard-AI/issues)
- Contact: suyashmatade007@gmail.com

---

⭐ **If you find this project helpful, please give it a star!** ⭐
