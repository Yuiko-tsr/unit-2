```.py
from matplotlib.gridspec import GridSpec
import matplotlib.pyplot as plt
import numpy as np
import serial
from datetime import datetime
import requests

ip = "192.168.6.153"
id = "cu.usbserial-10"


def createuser(user, ip="192.168.6.153"):
    req = requests.post(f'http://{ip}/register', json=user)
    print(req.json())


def smoothing(x, smoothing_win=5, overlap=1):
    smooth_x = []
    t = []
    for i in range(0, len(x), int(smoothing_win * overlap)):
        smooth_x.append(sum(x[i:i + smoothing_win]) / smoothing_win)
        t.append(i)
    return t, smooth_x


def login(user, ip="192.168.6.153"):
    req = requests.post(f'http://{ip}/login', json=user)
    access_token = req.json()["access_token"]
    return access_token


def create_sensor(sensor,token, ip="192.168.6.153"):

    auth = {"Authorization": f"Bearer {token}"}
    r = requests.post(f'http://{ip}/sensor/new', json=sensor, headers=auth)
    print(r.json())


def add_data(value,token,id, ip="192.168.6.153"):

    auth = {"Authorization": f"Bearer {token}"}
    new_record = {"datetime": datetime.isoformat(datetime.now()), "sensor_id": id, "value": value}

    r = requests.post(f'http://{ip}/reading/new', json=new_record, headers=auth)
    print(r.json())


#
# new_user = {"username": "yuiko                              ", 'password':'1234'}
#
# req = requests.post('http://{ip}}/register', json=new_user)
# print(req.json())
#
# x = create_sensor("tryout", type="temperature", location="Bed", ip="192.168.6.153")
# print(x)
agatha={"username": "agatha_unit2", 'password': 'a1b2c3'}
# createuser(user=agatha)
token=login(user=agatha)
sensor_bed = {"type": "Temperature", "location": "R1-15", "name": "sensor_bed", "unit": "C"}
sensor_desk = {"type": "Temperature", "location": "R1-15", "name": "sensor_desk", "unit": "C"}
sensor_window = {"type": "Temperature", "location": "R1-15", "name": "sensor_window", "unit": "C"}
sensor_bed = {"type": "Humidity", "location": "R1-15", "name": "sensor_bed", "unit": "%"}
sensor_desk = {"type": "Temperature", "location": "R1-15", "name": "sensor_desk", "unit": "C"}
sensor_window = {"type": "Temperature", "location": "R1-15", "name": "sensor_window", "unit": "C"}
# create_sensor(sensor_bed,token)
# create_sensor(sensor_desk, token)
# create_sensor(sensor_window, token)

add_data(25,token,48)
```
