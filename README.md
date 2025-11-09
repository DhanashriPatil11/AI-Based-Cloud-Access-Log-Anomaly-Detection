# AI-Based Cloud Access Log Anomaly Detection

## 🚀 Real-Time Threat Detection with Isolation Forest & FastAPI

This project is an **AI-powered anomaly detection system** that identifies suspicious logins and potential security threats in cloud environments. It’s designed to spot **insider threats, data exfiltration attempts, off-hour account access, and other abnormal login behaviors**.

The pipeline combines **Machine Learning** (Isolation Forest), **FastAPI** for serving models via REST APIs, and **Ngrok** for public endpoint exposure – making the solution easy to demo, even in notebooks like **Google Colab**.

---

## 📊 Project Overview

- **Goal:** Instantly detect unusual access patterns within cloud/network authentication logs.
- **Method:** Train an Isolation Forest to establish a baseline of normal logins; flag statistically rare/outlier events as anomalies.
- **Tech Stack:**
  - **Python:** Data processing & ML
  - **Scikit-learn:** Machine learning (Isolation Forest)
  - **Pandas, NumPy:** Data transformation
  - **FastAPI:** Lightweight API server for model inference
  - **Ngrok:** Easy public API creation, e.g. for Colab demos
  - **Dataset:** [Kaggle RBA Dataset](https://www.kaggle.com/datasets/dasgroup/rba-dataset)

---

## 📁 Dataset Description

**Source:** [RBA Dataset · Kaggle](https://www.kaggle.com/datasets/dasgroup/rba-dataset)

Features include:
- `User ID`, `IP Address`, `Country`, `Region`
- `Timestamp`, user/session temporal features
- Annotations: `Login Successful`, `Is Attack IP`, `Is Account Takeover`

Each row records a login attempt, providing comprehensive context for anomaly identification and risk assessment.

---

## ⚙️ Workflow

### 1. Data Preprocessing
- Import & clean login event data from CSV
- Encode categorical features (`User ID`, `IP Address`) numerically
- Extract time-based features (`hour` of login, `day_of_week`, etc.)
- Handle missing values, standardize feature scales

### 2. Model Training (Isolation Forest)
- Fit Isolation Forest using only *normal* login data for unsupervised anomaly detection
- Model learns common behavior, so rare/outlier patterns (potential attacks) stand out

### 3. Evaluation
- Visualize the distribution of normal vs anomalous events (e.g., with seaborn or matplotlib)
- Analyze flagged events: unusual login times, odd user-IP combos, suspicious geographies

### 4. Deployment
- Serialize and serve the model using **FastAPI**
- REST endpoint (`POST /predict`) receives new login events, predicts anomaly likelihood in real time
- Expose your API to the internet using **Ngrok** (e.g., for easy Colab demos or mobile test clients)

---

## 🧩 API Demo

### **Endpoint:**  
`POST /predict`

**Sample Request:**
```json
{
  "ip_encoded": 45,
  "user_encoded": 100,
  "hour": 2,
  "day_of_week": 6
}
```

**Sample Response:**
```json
{
  "prediction": "Anomaly"
}
```

---

## 📝 Why Use This Approach?

- **Unsupervised anomaly detection** catches *unknown* or evolving attack patterns with no need for labeled attack data.
- **Real-time REST API** integration = plug into cloud SIEMs, dashboards, or alerting systems.
- **Easy demos & testing:** Deploy anywhere, even from a Jupyter or Colab notebook!

---

## 💡 Extensions

- Add geolocation/IP reputation enrichment for better risk scoring
- Integrate user-agent analysis
- Online learning or periodic retraining to adapt to shifting behaviors
- Alerting & dashboard integration (e.g., Slack, Grafana)

---

**Feel free to [fork ⭐](#) and adapt for your own cloud threat use-case!**
