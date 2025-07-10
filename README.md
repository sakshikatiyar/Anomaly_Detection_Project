# 🛡️ Access Log Anomaly Detection Using Isolation Forest

This project uses **unsupervised machine learning** to detect anomalies in system access logs — helping identify suspicious activities such as failed login attempts, unusual IP behavior, or access outside working hours. The model used is **Isolation Forest**, which is well-suited for detecting outliers in high-dimensional datasets without requiring labeled training data.

---

## 📁 Dataset Description

The dataset contains simulated system access logs with the following fields:

| Column         | Description                                    |
|----------------|------------------------------------------------|
| `timestamp`    | Date and time of the access attempt            |
| `ip_address`   | IP address of the user/system making the request |
| `action`       | Type of action (login, upload, download, etc.) |
| `resource`     | What was accessed (portal, file, admin page)   |
| `status_code`  | HTTP-like response code (e.g., 200, 403)       |
| `anomaly_label`| Ground truth label (0 = normal, 1 = anomaly)   |

---

## 🧠 Methodology

1. **Data Preprocessing**
   - Parsed timestamps into features: `hour` and `day_of_week`
   - Encoded categorical fields: `action`, `resource`, and `ip_address`

2. **Feature Engineering**
   - Selected 6 features for modeling:
     - `hour`, `day_of_week`, `action_encoded`, `resource_encoded`, `ip_encoded`, `status_code`

3. **Modeling**
   - Used **Isolation Forest** (`sklearn.ensemble.IsolationForest`)
   - Parameters:
     - `n_estimators=100`
     - `contamination=0.2` (estimated 20% of logs as anomalies)

4. **Output**
   - Generated `predicted_anomaly` column (1 = anomaly, 0 = normal)
   - Results exported to Excel: `access_log_anomaly_detected.xlsx`

---

## 📊 Visualizations

Included in the Jupyter Notebook:
- Anomaly count bar chart (`seaborn.countplot`)
- Exploratory data views
- IPs/actions most commonly associated with anomalies

---

## 🌍 Real-World Applications

| Domain           | Use Case                                                |
|------------------|---------------------------------------------------------|
| **Cybersecurity**| Detecting brute force login attempts and IP scanning    |
| **Cloud Services** | Identifying overuse or bot-like API activity          |
| **Banking**      | Flagging unusual user sessions or file access           |
| **Healthcare**   | Monitoring for unauthorized access to patient records   |
| **EdTech/Corp IT** | Finding misuse of learning portals or internal systems|

---

## 📂 Files Included

| File                                 | Purpose                                 |
|--------------------------------------|-----------------------------------------|
| `sample_access_log_anomaly_dataset.xlsx` | Simulated access logs (input)           |
| `access_log_anomaly_detected.xlsx`   | Output file with predicted anomalies    |
| `anomaly_detection_access_logs.ipynb`| Jupyter Notebook with full implementation|
| `README.md`                          | Project documentation (this file)       |

---

## 🛠️ Requirements

To run the notebook, install the following Python libraries:

```bash
pip install pandas scikit-learn matplotlib seaborn openpyxl
