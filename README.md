# smart_parking


import time
import random
import requests
import json

# Simulated IoT sensor data
def generate_sensor_data():
    vehicle_id = "Bus123"
    current_location = {
        "latitude": random.uniform(0, 90),
        "longitude": random.uniform(0, 180)
    }
    ridership = random.randint(0, 100)
    timestamp = int(time.time())

    sensor_data = {
        "vehicle_id": vehicle_id,
        "location": current_location,
        "ridership": ridership,
        "timestamp": timestamp
    }

    return sensor_data

# Simulate IoT sensor data transmission to a server
def send_sensor_data(sensor_data):
    server_url = "https://your-realtime-transit-server.com/api/sensor-data"
   
    headers = {"Content-Type": "application/json"}
   
    try:
        response = requests.post(server_url, data=json.dumps(sensor_data), headers=headers)
        if response.status_code == 200:
            print("Sensor data sent successfully.")
        else:
            print(f"Failed to send sensor data. Status code: {response.status_code}")
    except Exception as e:
        print(f"Error sending sensor data: {str(e)}")

if __name__ == "__main__":
    while True:
        sensor_data = generate_sensor_data()
        send_sensor_data(sensor_data)
        time.sleep(60)  # Simulate sending data every minute
