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
