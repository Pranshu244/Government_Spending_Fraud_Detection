# Government_Spending_Fraud_Detection
AI-based fraud and anomaly detection prototype for government spending using graph neural networks and hybrid risk scoring to flag high-risk transactions for early investigation and improved transparency.

## Overview
This repository presents a prototype **AI-driven fraud and anomaly detection system** designed to monitor public spending across government procurement, welfare schemes, and contractual payments.
The system combines **unsupervised anomaly detection, graph-based deep learning, and rule-based risk aggregation** to identify suspicious transactions and flag high-risk cases for early investigation.
This project was developed as part of a civic-tech hackathon and focuses on explainability, scalability, and real-world deployability.

## Problem Statement
Government spending systems handle large volumes of transactions, making manual auditing inefficient and reactive. Fraud, irregularities, and anomalies—such as inflated payments, repeated beneficiaries, and suspicious vendors—often go undetected until significant financial leakage occurs.
There is a need for an automated, data-driven system that can proactively detect such risks and support transparent governance.

## Solution Summary


The proposed system:
1. Automatically screens large-scale transaction data
2. Detects anomalous and irregular behavior using machine learning
3. Models transactional relationships using graphs
4. Assigns risk scores and flags high-risk cases
5. Presents results through a dashboard for early investigation


## System Architecture
The solution follows a three-stage fraud detection pipeline, supported by a modular ML workflow suitable for real-world deployment.

## Fraud Detection Pipeline
### Stage 1: Statistical Anomaly Detection (Isolation Forest)

1. Input transaction features are standardized using a scaler
2. An Isolation Forest model detects transactions that deviate from normal behavior
3. Each transaction is assigned an anomaly score
4. This stage captures global statistical irregularities such as unusual amounts or spending patterns
   
**Output:** Anomaly score per transaction

### Stage 2: Graph-Based Anomaly Detection (GNN Autoencoder)

1. Transactions are modeled as nodes in a graph
2. Relationships (shared vendors, accounts, beneficiaries, etc.) form edges
3. A Graph Neural Network Autoencoder (GNN-AE) is trained to reconstruct node features
4. High reconstruction error indicates structurally abnormal behavior within the transaction network
   
**Why Autoencoder?**
The model learns normal graph patterns and flags deviations without labeled fraud data.

**Output:** GNN reconstruction error score per transaction

### Adaptive Thresholding

1. Percentile-based thresholds are applied to:
     1. Isolation Forest anomaly scores
     2. GNN reconstruction scores
2. Transactions exceeding either threshold are flagged for further risk evaluation

### Stage 3: Rule-Based Risk Aggregation
This stage incorporates domain knowledge to strengthen decision-making:
1. High transaction amounts
2. Repeated vendor interactions
3. Shared bank accounts across multiple vendors
Each rule contributes to a risk score, and transactions are finally classified as high-risk based on combined ML and rule-based signals.

**Final Output:** Binary fraud flag and aggregated risk score

## Model Details
### GNN Autoencoder Architecture
1. Framework: PyTorch + PyTorch Geometric
2. Layers:
   1. GCNConv (input → 32)
   2. GCNConv (32 → input)
3. Loss Function: Mean Squared Error (MSE)
4. Optimizer: Adam
The autoencoder reconstructs node features and uses reconstruction error as an anomaly signal.

## Evaluation Snapshot
1. Real fraud cases: 215
2. High-risk cases detected: 121
3. Recall: ~0.56
This reflects a prototype-level model prioritizing recall for early risk detection rather than final legal classification.

## Technology Stack
### Machine Learning
1. Python
2. Scikit-learn (Isolation Forest, preprocessing)
3. PyTorch
4. PyTorch Geometric (Graph Neural Networks)

### Data & Visualization
1. Pandas
2. NumPy

### Frontend
1. Streamlit

## Prototype Demo (Frontend)
A lightweight Streamlit-based frontend has been added to demonstrate the end-to-end fraud detection pipeline in action.  
The frontend integrates all trained components—encoder, scaler, Isolation Forest, and GNN Autoencoder—into a single interactive web interface.
### The interface allows:

- Uploading trained models (encoder, scaler, Isolation Forest, GNN Autoencoder)
- Uploading transaction CSV data in raw (non-encoded) form
- Automatically applying preprocessing, encoding, and scaling
- Running the complete multi-stage fraud detection pipeline
- Visualizing flagged high-risk transactions and summary statistics for quick inspection

## Steps to Run the Frontend (Colab)
1. Open the folder **`Website_Code`** in this repository.
2. Click on **`Government_Fraud_Detection_App.ipynb`**.
3. Click **“Open in Colab”** (top of the notebook).
4. Create a free ngrok account and obtain your authentication token from:  
   https://dashboard.ngrok.com/get-started/your-authtoken
5. Replace the placeholder with your token in the notebook:
   ```python
   ngrok.set_auth_token("YOUR_NGROK_AUTH_TOKEN")
6. Run all cells using **Runtime → Run all**.
7. Once execution completes, a public ngrok URL will be generated.
8. Open the generated URL in a browser (desktop or mobile).
9. Upload model files and a transaction CSV to run the fraud detection pipeline.


## Pictures
![image alt](https://github.com/Pranshu244/Government_Spending_Fraud_Detection/blob/5b116849dbf38d915c29d921a36aafcf02fe78b1/Pictures/PIC_1.png)

![image alt](https://github.com/Pranshu244/Government_Spending_Fraud_Detection/blob/5b116849dbf38d915c29d921a36aafcf02fe78b1/Pictures/PIC_2.png)

![image alt](https://github.com/Pranshu244/Government_Spending_Fraud_Detection/blob/5b116849dbf38d915c29d921a36aafcf02fe78b1/Pictures/PIC_3.png)
