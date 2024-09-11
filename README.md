# Fraud Detection in Medical claims using Anomaly Detection
An anomaly detection system for Medicare insurance claims data. Built this project using Python3 along with various scientific computing and machine learning packages (numpy, scikit-learn, and many others).

# Structure
* `data/`: Contains a CSV file displaying the outlier count data generated by the anomaly labeling engine.
* `notebooks/`: Jupyter notebooks demonstrating various aspects of FraudHacker's workflow, including the outlier detection, physician ranking, and hyperparameter sweeping.
* `src/`: The actual source code for FraudHacker and the Flask app that displays its results to users.

# Workflow

The PandasDBReader class (implemented in database_tools.py) is responsible for reading data from a PostgreSQL database, with the connection details specified in an external YAML file. It then loads the data into a Pandas DataFrame. This dataframe is passed to a subclass of AnomalyDetector (depending on the chosen algorithm, implemented in anomaly_tools.py), which handles the clustering and outlier detection. Each record gets an outlier score, and based on a defined threshold, certain records are labeled as outliers. Additionally, the AnomalyDetector aggregates the outlier counts for each physician.

Currently, the next step is done semi-manually, but there’s room for improvement in the future. I export the outlier counts per physician to a CSV file (examples of which are available in the data folder). This data is then imported into another PostgreSQL database, which is ultimately accessed by the Flask app. This process is managed by the OutlierCountDBReader class (also implemented in database_tools.py). The OutlierCountDBReader generates the values that are displayed in the Flask app.
