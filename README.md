# EDA-ECommerce-Shipping-Data

Phase 1: Exploration and Baselines (Matches Modules 1 - 4)

Action: Source our dataset and perform extensive EDA. Set up a robust validation framework (train/val/test splits).

Goal: Train baseline models (Linear Regression if predicting a continuous number, Logistic Regression if predicting a category) and evaluate them using metrics like RMSE or AUC.

Data Source: https://www.kaggle.com/code/nxbfuentes/notebookf36f949a2a/edit


🚀 Phase 1: Data Exploration and Baseline Model
Objective: Establish a robust validation framework, uncover initial data insights without data leakage, and train a baseline linear model to predict e-commerce shipping delays.

📊 Dataset & Validation Setup
Domain: Supply Chain & Logistics (E-Commerce Shipping)

Target Variable: late_delivery (Engineered from reached_on_time_y_n where 1 = Late, 0 = On Time)

Validation Framework: Implemented a strict 60% / 20% / 20% (Train / Validation / Test) split using Scikit-Learn to ensure the model is evaluated on entirely unseen data.

🔍 Exploratory Data Analysis (EDA) Highlights
Data Quality: The dataset is exceptionally clean with 0 missing values across all columns.

Target Distribution: The data is slightly imbalanced, with a baseline late delivery rate of ~59.9%.

Key Signal (discount_offered): Identified a massive behavioral signal regarding discounts. Packages arriving on time had an average discount of ~5.49, whereas delayed packages featured an average discount of ~18.85.

Categorical Trends: Warehouse Block 'D' exhibited the highest rate of late deliveries (~60.6%).

🤖 Baseline Model Performance
To establish a performance floor, a baseline LogisticRegression model was trained using the liblinear solver. Scikit-Learn's DictVectorizer was utilized to handle the automatic One-Hot Encoding of all categorical features (e.g., mode_of_shipment, warehouse_block).

Baseline Validation Accuracy: 0.6477

Baseline Validation ROC AUC: 0.7218

Note: These metrics serve as our foundational benchmark. Advanced tree-based ensembles introduced in Phase 2 must reliably exceed an ROC AUC of 0.7218 to justify their added complexity.

Phase 2: Complex Modeling (Matches Module 6)

Action: Upgrade your model to use tree-based ensembles (Random Forest, XGBoost).

Goal: Focus on feature engineering and hyperparameter tuning to beat your baseline model's performance. Export the final, best-performing model using pickle or joblib.

Here is a beautifully formatted recap for Phase 2, styled to match your Phase 1 update. It perfectly captures your progression into complex modeling, your metric improvements, and the final engineering steps taken to prepare the model for production.

You can copy and paste this directly into your GitHub Pull Request description or your `README.md`:

---

#### 🚀 Phase 2: Complex Modeling and Model Export

**Objective:** Upgrade from the baseline linear model by implementing tree-based ensembles to capture non-linear relationships, improve predictive performance, and package the final model for production deployment.

##### 🌳 Models Evaluated

Transitioned from a linear baseline to advanced ensemble methods capable of handling complex, conditional decision rules (e.g., combining high discount rates with specific warehouse blocks).

* **Random Forest:** Trained using `scikit-learn`'s `RandomForestClassifier` with constraints on tree depth and estimators to prevent overfitting.
* **XGBoost:** Trained using `XGBClassifier`, leveraging gradient boosting to build trees sequentially and minimize errors from previous iterations.

##### 📊 Performance Comparison

Models were evaluated using the isolated validation set (20%) via the ROC AUC metric.

* **Baseline (Logistic Regression):** 0.7218 ROC AUC
* **Random Forest:** 0.7224 ROC AUC
* **XGBoost:** **0.7309 ROC AUC 🏆**

XGBoost emerged as the clear champion, successfully outperforming both the linear baseline and the Random Forest model on tabular data.

##### 📦 Model Export & Artifacts

To prepare the champion model for Phase 3 (Core Deployment), the model and its preprocessing pipeline were serialized and exported out of the Jupyter Notebook environment.

* **Serialization:** Used Python's native `pickle` library to export the components.
* **Artifact:** Saved both the fitted `DictVectorizer` and the trained `XGBoost` model together as a tuple into a binary file (`xgboost_model.bin`).
* **Engineering Note:** Bundling the `DictVectorizer` with the model is critical; it ensures the future Flask web service can accurately translate raw JSON text inputs (like `warehouse_block: 'D'`) into the exact numerical arrays the model expects.

Phase 3: Core Deployment (Matches Module 5)

Action: Take your best trained model out of the Jupyter Notebook environment.

Goal: Write a Python script to serve the model via a Flask API. Create a Pipfile or requirements.txt to manage dependencies, and write a Dockerfile to containerize the application so it can run reliably on any machine.

Phase 4: Serverless Architecture (Matches Module 9)

Action: Adapt your inference code to run as a serverless function.

Goal: Convert your model to a lightweight format (like TF-Lite or ONNX) if necessary, package the code into an AWS Lambda deployment package, and expose it using an API Gateway.

Phase 5: Orchestration at Scale (Matches Modules 10 & 11)

Action: Prepare the model for high traffic and enterprise environments.

Goal: Write Kubernetes deployment and service YAML files to manage your containers. Finally, implement KServe to handle advanced traffic routing, auto-scaling, and health monitoring for your ML service.