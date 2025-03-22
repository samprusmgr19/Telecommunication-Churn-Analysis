# Telecommunication-Churn-Analysis
Finding and analyzing churn of a Telecommunication company.
This project aims to analyze customer churn in a telecommunications company by preprocessing data, performing clustering analysis, and identifying key factors influencing churn. The dataset used for this project contains customer information, service details, and billing history.

Dataset

Filename: Dataset_ATS_v2.csv

Rows: 7043 (after cleaning: 6741)

Columns: 21

Steps in Data Analysis

1️. Preprocessing Datasets
In this step, we prepared the dataset to ensure it's clean and ready for clustering:

Handled missing values: To maintain data integrity, we checked for and addressed any null or empty entries.

Encoded categorical variables: If there were any, such as 'Contract Type' or 'Payment Method', they were converted into a numerical format using label encoding or one-hot encoding.

Selected numerical features that are relevant to customer behavior:

tenure – how long a customer has stayed.

MonthlyCharges – monthly bill amount.

TotalServiceCost – total revenue generated from a customer.

Ensured data consistency (correct data types, realistic values).

This step ensured that the clustering algorithm would receive clean, numeric, and meaningful data to work with.

2️. Splitting Datasets
Although clustering is unsupervised, we still split the dataset to isolate the training portion:

Training data was used for clustering.

A test set was preserved for potential downstream use (e.g., validation or future supervised modeling).

This ensures our clustering model is not biased by overfitting to a single dataset and that our preprocessing pipeline can generalize.

3️. Scaling Techniques
We applied scaling to numerical features to prepare the data for distance-based clustering (like K-Means):

Used StandardScaler to transform features to have mean = 0 and standard deviation = 1.

This was crucial because:
tenure ranges from 0–70,

MonthlyCharges could range from $20–$120,

TotalServiceCost could vary drastically based on tenure.

Without scaling, features like TotalServiceCost would dominate the distance calculations, skewing the clustering results.

4️. Clustering Analysis
This is where we performed initial cluster exploration:

Chose K-Means Clustering as the algorithm due to its simplicity and efficiency.

Determined the optimal number of clusters (k) using:
The Elbow Method – plotted WCSS (Within Cluster Sum of Squares) and looked for the “elbow point” where adding more clusters didn’t significantly reduce WCSS.

The Silhouette Score – evaluated how well-separated and coherent clusters were for different values of k.
After analysis, we selected the best k (2), which represented meaningful groupings of customers.

5️. Training K-Means Clustering Models
This step involved training the K-Means model using the processed dataset:

The model was trained on the selected and scaled features: tenure, MonthlyCharges, and TotalServiceCost.

Each customer was assigned a cluster label based on their similarity to other customers (e.g., in terms of billing and loyalty).

The trained model was then saved using joblib for future reuse, so it could be applied to new customer data without retraining.

The resulting cluster labels were added back into the dataset as a new column named cluster_label.

6️. Visualising and Labeling Clusters
Once the clustering was complete, we moved to interpreting the results visually and semantically:

🔹 Visualization:
Used PCA (Principal Component Analysis) to reduce the 3D dataset (tenure, MonthlyCharges, TotalServiceCost) into 2D space.

Plotted the clusters using a scatter plot, where:
Each point represented a customer.
Color indicated the assigned cluster.
This allowed us to visually assess how well-separated and distinct the clusters were.

🔹 Cluster Analysis:
Grouped the data by cluster_label and calculated average values for each feature.

This revealed patterns such as:
One cluster had long-tenure, high-paying customers.
Another cluster had short-tenure, low-paying customers.

🔹 Labeling the Clusters:
Based on the patterns, we assigned meaningful labels to each cluster:

Cluster 0: "High-Spending Long-Term Customers"
Cluster 1: "Budget-Conscious Short-Term Customers"

These labels make the clusters actionable for business teams, such as:
Offering loyalty programs to long-term customers.
Engaging short-term customers with retention incentives.
