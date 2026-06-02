# EDA-ECommerce-Shipping-Data

Phase 1: Exploration and Baselines (Matches Modules 1 - 4)

Action: Source our dataset and perform extensive EDA. Set up a robust validation framework (train/val/test splits).

Goal: Train baseline models (Linear Regression if predicting a continuous number, Logistic Regression if predicting a category) and evaluate them using metrics like RMSE or AUC.

Data Source: https://www.kaggle.com/code/nxbfuentes/notebookf36f949a2a/edit


--- Missing Values ---
id                     0
warehouse_block        0
mode_of_shipment       0
customer_care_calls    0
customer_rating        0
cost_of_the_product    0
prior_purchases        0
product_importance     0
gender                 0
discount_offered       0
weight_in_gms          0
late_delivery          0
dtype: int64


--- Target Distribution (Late vs On Time) ---
late_delivery
1    0.59903
0    0.40097
Name: proportion, dtype: float64


--- Late Delivery Rate by Warehouse Block ---
warehouse_block
D    0.606572
C    0.604244
B    0.603116
F    0.600915
A    0.578616
Name: late_delivery, dtype: float64


--- Average Discount Offered (On Time vs Late) ---
late_delivery
0     5.487906
1    18.850746
Name: discount_offered, dtype: float64

ackages that arrive on time: ~5.49 discount.

Packages that arrive late: ~18.85 discount.

This is a massive signal. It tells us that discount_offered is going to be a very strong predictor for our model. (From a business perspective, this might mean the company is slapping high discounts on packages they already know are going to be delayed, or perhaps highly discounted items are shipped via a slower, lower-priority tier!).

Baseline Validation Accuracy: 0.6477
Baseline Validation ROC AUC:  0.7218

An ROC AUC of 0.7218 means your Logistic Regression model is doing a decent job of distinguishing between on-time and late packages, but we can definitely do better.

Phase 2: Complex Modeling (Matches Module 6)

Action: Upgrade your model to use tree-based ensembles (Random Forest, XGBoost).

Goal: Focus on feature engineering and hyperparameter tuning to beat your baseline model's performance. Export the final, best-performing model using pickle or joblib.

Phase 3: Core Deployment (Matches Module 5)

Action: Take your best trained model out of the Jupyter Notebook environment.

Goal: Write a Python script to serve the model via a Flask API. Create a Pipfile or requirements.txt to manage dependencies, and write a Dockerfile to containerize the application so it can run reliably on any machine.

Phase 4: Serverless Architecture (Matches Module 9)

Action: Adapt your inference code to run as a serverless function.

Goal: Convert your model to a lightweight format (like TF-Lite or ONNX) if necessary, package the code into an AWS Lambda deployment package, and expose it using an API Gateway.

Phase 5: Orchestration at Scale (Matches Modules 10 & 11)

Action: Prepare the model for high traffic and enterprise environments.

Goal: Write Kubernetes deployment and service YAML files to manage your containers. Finally, implement KServe to handle advanced traffic routing, auto-scaling, and health monitoring for your ML service.