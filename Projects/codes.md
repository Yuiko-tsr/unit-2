```.py
import requests
import time
import serial

id = "cu.usbserial-1420"

arduino = serial.Serial(port=f"/dev/{id}", baudrate=9600, timeout=0.1)
sensor_bed = {"type": "Temperature", "location": "R1-15b", "name": "sensor_bed", "unit": "2"}
sensor_desk = {"type": "Temperature", "location": "R1-15b", "name": "sensor_desk", "unit": "2"}
sensor_window = {"type": "Temperature", "location": "R1-15b", "name": "sensor_window", "unit": "2"}

sensors = [sensor_bed, sensor_desk, sensor_window]


def read():
    data = ""
    while len(data) < 1:
        data = arduino.readline()
    return data


def send_data(sensor_id, temperature, humidity):
    url = f"http://192.168.6.153/data"
    data = {"sensor_id": sensor_id, "temperature": temperature, "humidity": humidity}
    headers = {'Content-Type': 'application/json'}
    response = requests.post(url, json=data, headers=headers)
    print(f"Sent to router: {response.text}")


while True:
    for sensor in sensors:
        time.sleep(300)
        value = read()
        msg = value.decode('utf-8').strip().split(" ")
        if len(msg) == 4 and msg[0] == "Humidity:" and msg[2] == "Temperature:":
            humidity = float(msg[1])
            temperature = float(msg[3])
            send_data(sensor["name"], temperature, humidity)

hours = 24
time.sleep(300)
for hour in range(hours):
    for minute in range(0, 60, 5):
        for sensor in sensors:
            time.sleep(1)
            value = read()
            msg = value.decode('utf-8').strip().split(" ")
            if len(msg) == 4 and msg[0] == "Humidity:" and msg[2] == "Temperature:":
                humidity = float(msg[1])
                temperature = float(msg[3])
            send_data(sensor["name"], temperature, humidity)
```

Yuiko Dec 3rd
```.py
from matplotlib.gridspec import GridSpec
import matplotlib.pyplot as plt
import numpy as np
import serial
import datetime
from unit2_lib import get_sensor, smoothing
import requests

ip = "192.168.6.142"

#add user
new_user = {"username": "agatha", 'password':'1864'}

req = requests.post(f'http://{ip}/register', json=new_user)
print(req.json())

#login
user = {"username": "agatha", 'password':'1864'}

req = requests.post(f'http://{ip}/login', json=user)
access_token = req.json()["access_token"]
print(access_token)


# Function to read data from Arduino

def read():
    data = ""
    while len(data) < 1:
        data = arduino.readline()
    return data.decode('utf-8')

# Connect to Arduino
id = "cu.usbserial-10"
arduino = serial.Serial(port=f"/dev/{id}", baudrate=9600, timeout=0.1)
sensor_bed = {"type": "Temperature", "location": "R1-15b", "name": "sensor_bed", "unit": "2"}
sensor_desk = {"type": "Temperature", "location": "R1-15b", "name": "sensor_desk", "unit": "2"}
sensor_window = {"type": "Temperature", "location": "R1-15b", "name": "sensor_window", "unit": "2"}

sensors = [sensor_bed, sensor_desk, sensor_window]

# Collect data from sensors and put in csv
num_samples = 100
humidity_data = []
temperature_data = []

for i in range(num_samples):
    msg = read()
    if "hello" in msg.lower():
        print("Skipping message with 'hello'")
        continue
    humid = msg.split(",")[0:3]
    temp = msg.split(",")[3:]
    humidity_data.append(humid)
    temperature_data.append(temp)

    with open(f"humidity.csv", 'a') as myfile:
        myfile.writelines(f"{humid}\n")
    with open(f"temperature.csv", 'a') as myfile:
        myfile.writelines(f"{temp}\n")

#add data to server
access_token = r.json()["access_token"]
auth = {"Authorization": f"Bearer {access_token}"}

new_sensor ={ "type": "Temperature","location": "R2-10B", "name": "sensor_alex_bern_1","unit":"C" }

r = requests.post(f'http://{ip}/sensor/new', json=new_sensor, headers=auth)
print(r.json())

access_token = r.json()["access_token"]
auth = {"Authorization": f"Bearer {access_token}"}

new_record ={"datetime":datetime.isoformat(datetime.now()),"sensor_id":1, "value":[temp, humid]}

r = requests.post(f'http://{ip}/reading/new', json=new_record, headers=auth)
print(r.json())


#get data from server
req = requests.get(f'http://{ip}/readings')
data = req.json()
readings = data['readings'][0]
print(readings)
