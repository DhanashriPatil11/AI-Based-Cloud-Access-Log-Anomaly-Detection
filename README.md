# AI-Based-Cloud-Access-Log-Anomaly-Detection
 
### 🚀 Real-time Threat Detection using Isolation Forest & FastAPI

This project implements an **AI-driven anomaly detection system** for identifying unusual login behaviors in cloud environments — such as **insider threats, data exfiltration, or off-hour logins**.  
The solution leverages **Machine Learning (Isolation Forest)**, **FastAPI for deployment**, and **Ngrok for public API access** — built and tested in **Google Colab**.

---

## 📊 Project Overview

- **Goal:** Detect abnormal access patterns in real-time cloud or network log data.  
- **Approach:** Train an Isolation Forest model on normal login activity and predict anomalies on unseen data.  
- **Tech Stack:**  
  - 🐍 Python, Scikit-learn, Pandas, NumPy  
  - ⚙️ FastAPI (REST API deployment)  
  - 🌐 Ngrok (public API tunneling for Colab)  
  - 📈 Kaggle Dataset: [`dasgroup/rba-dataset`](https://www.kaggle.com/datasets/dasgroup/rba-dataset)

---

## 📁 Dataset Used
**Source:** [RBA Dataset – Kaggle](https://www.kaggle.com/datasets/dasgroup/rba-dataset)

The dataset contains anonymized login events with fields such as:
- `User ID`, `IP Address`, `Country`, `Region`, `Timestamp`
- `Login Successful`, `Is Attack IP`, `Is Account Takeover`

Each record represents a login attempt with detailed context for anomaly detection and risk scoring.

---

## ⚙️ Workflow

### **1. Data Preprocessing**
- Load and clean the RBA dataset.
- Encode categorical features (`User ID`, `IP Address`, etc.).
- Extract temporal features (`Hour`, `Day of Week`).

### **2. Model Training**
- Use **Isolation Forest** to learn normal user behavior.
- Detect outliers representing anomalous logins.

### **3. Evaluation**
- Visualize normal vs anomalous events.
- Identify unusual login times, IPs, or users.

### **4. Deployment**
- Deploy trained model using **FastAPI**.
- Serve predictions via a REST API endpoint `/predict`.
- Expose API publicly with **Ngrok** for demo in Google Colab.

---

## 🧩 Example API Usage

### **Endpoint:**  
`POST /predict`

### **Request:**
```json
{
  "ip_encoded": 45,
  "user_encoded": 100,
  "hour": 2,
  "day_of_week": 6
}

---

**Response:**
{
  "prediction": "Anomaly"
}

---
