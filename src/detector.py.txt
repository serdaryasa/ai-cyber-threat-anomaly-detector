import numpy as np
import pandas as pd
from sklearn.ensemble import IsolationForest

class AnomalyDetector:
    def __init__(self):
        self.model = IsolationForest(contamination=0.05, random_state=42)
        self.is_trained = False

    def train(self, normal_data_list):
        df = pd.DataFrame(normal_data_list)
        features = df[['response_size', 'request_count_per_min', 'status_code']]
        self.model.fit(features)
        self.is_trained = True

    def predict(self, log_entry):
        if not self.is_trained:
            return "Normal (Model Not Trained Yet)"

        df = pd.DataFrame([log_entry])
        features = df[['response_size', 'request_count_per_min', 'status_code']]

        prediction = self.model.predict(features)[0]
        return "ANOMALY/THREAT" if prediction == -1 else "NORMAL"