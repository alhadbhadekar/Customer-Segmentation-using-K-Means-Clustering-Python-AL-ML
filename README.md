# Customer Segmentation using K-Means Clustering

This project demonstrates customer segmentation using K-Means Clustering algorithm on a dataset of customers, aiming to group customers into segments based on their annual income and spending score. By clustering customers, we can identify patterns and target specific groups more effectively.

## Prerequisites

Before running the project, make sure you have the following Python packages installed:
- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `sklearn`

You can install these packages using pip:
```
pip install numpy pandas matplotlib seaborn scikit-learn
```

## Dataset

The dataset used in this project can be found on Kaggle: [Customer Segmentation Dataset](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python). 

The dataset contains the following columns:
- **CustomerID**: Unique identifier for each customer
- **Genre**: Gender of the customer (Male/Female)
- **Age**: Age of the customer
- **Annual Income (k$)**: The annual income of the customer in thousands of dollars
- **Spending Score (1-100)**: Spending score assigned to the customer based on their purchasing behavior

## Project Description

The goal of this project is to segment customers into distinct groups based on two features: `Annual Income (k$)` and `Spending Score (1-100)` using K-Means Clustering.

### Steps

1. **Importing Dependencies**: Required libraries like `numpy`, `pandas`, `matplotlib`, `seaborn`, and `KMeans` from `sklearn` are imported.

2. **Data Loading & Analysis**:
   - The dataset is loaded into a Pandas DataFrame from a CSV file.
   - Basic data exploration is done, such as checking the first 5 rows, inspecting the shape of the data, checking for missing values, and displaying general information.

3. **Selecting Features**: 
   - From the dataset, the columns `Annual Income (k$)` and `Spending Score (1-100)` are chosen as the features for clustering.

4. **Choosing the Optimal Number of Clusters**:
   - The **Elbow Method** is used to determine the optimal number of clusters. By plotting the Within-Cluster Sum of Squares (WCSS) for different cluster numbers, the "elbow" point is identified, indicating the best number of clusters.

5. **Training the K-Means Model**:
   - K-Means clustering is applied with the optimal number of clusters (5 in this case).
   - The model assigns a cluster label to each customer based on the two selected features.

6. **Visualizing the Clusters**:
   - A scatter plot is created to visualize the clusters. Different colors are used to represent different clusters. Additionally, the centroids of the clusters are displayed.

### Code Implementation

```python
# Importing the Dependencies
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans

# Data Collection & Analysis
customer_data = pd.read_csv('/content/Mall_Customers.csv')
customer_data.head()
customer_data.shape
customer_data.info()
customer_data.isnull().sum()

# Choosing the Annual Income Column & Spending Score Column
X = customer_data.iloc[:, [3, 4]].values
print(X)

# Choosing the number of clusters (Elbow Method)
wcss = []
for i in range(1, 11):
    kmeans = KMeans(n_clusters=i, init='k-means++', random_state=42)
    kmeans.fit(X)
    wcss.append(kmeans.inertia_)

sns.set()
plt.plot(range(1, 11), wcss)
plt.title('The Elbow Point Graph')
plt.xlabel('Number of Clusters')
plt.ylabel('WCSS')
plt.show()

# Optimum Number of Clusters = 5

# Training the K-Means Clustering Model
kmeans = KMeans(n_clusters=5, init='k-means++', random_state=0)
Y = kmeans.fit_predict(X)

# Visualizing all the Clusters
plt.figure(figsize=(8, 8))
plt.scatter(X[Y == 0, 0], X[Y == 0, 1], s=50, c='green', label='Cluster 1')
plt.scatter(X[Y == 1, 0], X[Y == 1, 1], s=50, c='red', label='Cluster 2')
plt.scatter(X[Y == 2, 0], X[Y == 2, 1], s=50, c='yellow', label='Cluster 3')
plt.scatter(X[Y == 3, 0], X[Y == 3, 1], s=50, c='violet', label='Cluster 4')
plt.scatter(X[Y == 4, 0], X[Y == 4, 1], s=50, c='blue', label='Cluster 5')

# Plotting the Centroids
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=100, c='cyan', label='Centroids')

plt.title('Customer Groups')
plt.xlabel('Annual Income')
plt.ylabel('Spending Score')
plt.show()
```

### Output

- **Elbow Method Graph**: The elbow graph helps identify the optimal number of clusters.
- **Cluster Visualization**: A scatter plot showing the customer groups, with different colors representing distinct clusters and centroids marked for reference.

### Results

- The K-Means algorithm successfully segments the customers into 5 clusters based on annual income and spending score.
- The visual representation of these clusters can help businesses tailor their marketing strategies to different customer segments.

## Conclusion

This project demonstrates how to use K-Means Clustering for customer segmentation. By dividing customers into meaningful groups, businesses can optimize their strategies and improve customer engagement. The model can be further enhanced by considering additional features like age, gender, and location for more granular segmentation.

## Future Work

- Experiment with different clustering algorithms (e.g., DBSCAN, Agglomerative Clustering) for comparison.
- Use more features from the dataset to refine customer segmentation.
- Implement a web-based dashboard for interactive visualization of customer segments.

## License

This project is open-source and available under the MIT License.

---

Feel free to adapt and extend this project to fit your specific requirements!