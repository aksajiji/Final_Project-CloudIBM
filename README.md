⚡ Final_Project-CloudIBM
Power System Fault Detection and Classification

📌 The Challenge
Design and implement a machine learning model to detect and classify different types of faults in a power distribution system.

Using electrical measurement data (e.g., voltage and current phasors), the model should distinguish between:

Normal operating conditions

Fault types:

Line-to-Ground

Line-to-Line

Three-Phase

Objective: Enable rapid and accurate fault identification to maintain power grid stability and reliability.

📂 Dataset
Source: Kaggle – Power System Faults Dataset
Kaggle dataset link – https://www.kaggle.com/datasets/ziya07/power-systemfaults-dataset
Contains fault and non-fault conditions recorded with electrical parameters.

🛠️ Tools & Technologies
IBM Watsonx.ai Studio – AutoAI model training & deployment

IBM Cloud Lite – Hosting & REST API deployment (mandatory)

Python – Auto-generated code for scoring

AutoAI – Feature engineering, algorithm selection & hyperparameter tuning

Libraries: scikit-learn, pandas, numpy, requests

🚀 How to Run / Import the Project
1️⃣ Clone this repository
git clone https://github.com/aksajiji/Final_Project-CloudIBM
cd Final_Project-CloudIBM
2️⃣ Open in IBM Watsonx.ai Studio
Log into IBM Watsonx.ai Studio.

Create a new project.

Import:

fault_data.csv (dataset)

.ipynb notebook (AutoAI-generated or custom)

(Optional) Import the full exported project:

/Power-System-Fault-Detection-and-Classification/ folder

Or Power-System-Fault-Detection-and-Classification.zip

3️⃣ Train & Deploy the Model
Open AutoAI inside Watsonx.ai.

Train the model on the dataset.

Random Forest was the top-performing algorithm.

Deploy the model to an IBM Cloud deployment space.

4️⃣ Access the Deployed Model

import requests
import json

# Get authentication token
API_KEY = "<your IBM Cloud API key>"
token_response = requests.post(
    'https://iam.cloud.ibm.com/identity/token',
    data={"apikey": API_KEY, "grant_type": 'urn:ibm:params:oauth:grant-type:apikey'}
)
mltoken = token_response.json()["access_token"]

# Prepare headers
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + mltoken
}

# Define input payload
payload_scoring = {
    "input_data": [
        {
            "fields": ["Voltage", "Current", "Phase_Angle", "Frequency"],
            "values": [[230, 5.2, 30, 50]]
        }
    ]
}

# Send scoring request
response_scoring = requests.post(
    'https://private.eu-gb.ml.cloud.ibm.com/ml/v4/deployments/<deployment-id>/predictions?version=2021-05-01',
    json=payload_scoring,
    headers=headers
)

print("Scoring response:", response_scoring.json())

📊 Model Performance
Accuracy: ~99% (Random Forest)

Fault Types Detected:

Line-to-Ground

Line-to-Line

Three-Phase

Benefit: Enables real-time power system fault detection.