import random
from datetime import datetime

class LogSimulator:
    def __init__(self):
        self.ip_pool = ["192.168.1.10", "10.0.0.5", "172.16.0.2", "192.168.1.15"]
        self.methods = ["GET", "POST", "HEAD"]
        self.endpoints = ["/home", "/login", "/api/v1/data", "/profile"]

    def generate_normal_log(self):
        return {
            "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "ip": random.choice(self.ip_pool),
            "method": random.choice(self.methods),
            "endpoint": random.choice(self.endpoints),
            "response_size": random.randint(200, 4000),
            "request_count_per_min": random.randint(5, 30),
            "status_code": 200
        }

    def generate_anomaly_log(self):
        anomaly_type = random.choice(["ddos", "exfiltration"])
        if anomaly_type == "ddos":
            return {
                "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
                "ip": "185.220.101.5",
                "method": "POST",
                "endpoint": "/login",
                "response_size": 150,
                "request_count_per_min": random.randint(800, 1500),
                "status_code": 429
            }
        else:
            return {
                "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
                "ip": "94.23.45.12",
                "method": "GET",
                "endpoint": "/api/v1/backup",
                "response_size": random.randint(500000, 900000),
                "request_count_per_min": 2,
                "status_code": 200
            }