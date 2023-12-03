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

    with open(f"humidity.csv", 'w') as myfile:
        myfile.writelines(f"{humid}\n")
    with open(f"temperature.csv", 'w') as myfile:
        myfile.writelines(f"{temp}\n")

#add data to server
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

#humidity

#local sensors' (data from arduino) graphs for humidity
# Calculate average
average = np.mean(humidity_data, axis=0)

# Calculate statistics for humidity_data
mean_humidity = np.mean(humidity_data, axis=0)
std_dev_humidity = np.std(humidity_data, axis=0)
max_humidity = np.max(humidity_data, axis=0)
min_humidity = np.min(humidity_data, axis=0)
median_humidity = np.median(humidity_data, axis=0)

# Create subplots
fig = plt.figure(figsize=(12, 8))
grid = GridSpec(6, 3, figure=fig)
plt.subplots_adjust(hspace=0.5)

box1 = fig.add_subplot(grid[0:2, 0:2])
box2 = fig.add_subplot(grid[0, 2])
box3 = fig.add_subplot(grid[1, 2])
box4 = fig.add_subplot(grid[2, 0])

# Plotting data
box1.plot(average, color="red", label="Average")
box1.fill_between(range(num_samples), max_humidity, min_humidity, alpha=0.5, linewidth=0, label='Range')
box1.errorbar(range(num_samples), mean_humidity, std_dev_humidity, fmt="o", label='Mean with SD')
box1.legend()

box2.plot(humidity_data[0], color="black", label="Sensor 1")
box2.set_title("Sensor 1")
box2.legend()

box3.plot(humidity_data[1], color="black", label="Sensor 2")
box3.set_title("Sensor 2")
box3.legend()

box4.plot(humidity_data[2], color="black", label="Sensor 3")
box4.set_title("Sensor 3")
box4.legend()

# Find line of best fit and plot
coefficients = np.polyfit(range(num_samples), average, 1)
line_of_best_fit = np.polyval(coefficients, range(num_samples))
box1.plot(line_of_best_fit, color="blue", linestyle="--", label="Line of Best Fit")
box1.legend()

# Plotting predicted values for the next 12 hours
next_x = np.arange(num_samples, num_samples + 12)
predicted_values = np.polyval(coefficients, next_x)
box1.plot(next_x, predicted_values, color="green", marker="o", linestyle="--", label="Predicted Values")
box1.legend()

# remote sensors'(data from server) graphs for humidity
sensors = []
for s in [0, 1, 2]:
    data = get_sensor(id=s)
    sensors.append(data)
    print(f"Sensor {s} obtained with {len(data)} samples")

num_samples_remote = len(sensors[0])  # Assuming all sensors have the same number of samples
average_remote = []

for i in range(num_samples_remote):
    total = 0
    for s in sensors:
        total += s[i]
    average_remote.append(total / len(sensors))

fig = plt.figure(figsize = (10,8))
grid = GridSpec(3,3,figure=fig)
plt.subplots_adjust(hspace=0.5)
box5 = fig.add_subplot(grid[3:5,0:2])
plt.plot(average, color="red")
plt.title("Average of all remote sensors")

box6 = fig.add_subplot(grid[3,2])
plt.plot(sensors[0],color="black")
plt.title("Sensor 1")
box7 = fig.add_subplot(grid[4,2])
plt.plot(sensors[1],color="black")
plt.title("Sensor 2")
box8 = fig.add_subplot(grid[5,0])
plt.plot(sensors[2],color="black")
plt.title("Sensor 3")

plt.show()

#temperature
# Calculate statistics for temperature_data
mean_temperature = np.mean(temperature_data, axis=0)
std_dev_temperature = np.std(temperature_data, axis=0)
max_temperature = np.max(temperature_data, axis=0)
min_temperature = np.min(temperature_data, axis=0)
median_temperature = np.median(temperature_data, axis=0)

# Create subplots for local temperature sensors
fig_temp_local = plt.figure(figsize=(12, 8))
grid_temp_local = GridSpec(6, 3, figure=fig_temp_local)
plt.subplots_adjust(hspace=0.5)

box10 = fig_temp_local.add_subplot(grid_temp_local[0:2, 0:2])
box11 = fig_temp_local.add_subplot(grid_temp_local[0, 2])
box12 = fig_temp_local.add_subplot(grid_temp_local[1, 2])
box13 = fig_temp_local.add_subplot(grid_temp_local[2, 0])

# Plotting data for local temperature sensors
box10.plot(average, color="red", label="Average")
box10.fill_between(range(num_samples), max_temperature, min_temperature, alpha=0.5, linewidth=0, label='Range')
box10.errorbar(range(num_samples), mean_temperature, std_dev_temperature, fmt="o", label='Mean with SD')
box10.legend()

box11.plot(temperature_data[0], color="black", label="Sensor 1")
box11.set_title("Sensor 1")
box11.legend()

box12.plot(temperature_data[1], color="black", label="Sensor 2")
box12.set_title("Sensor 2")
box12.legend()

box13.plot(temperature_data[2], color="black", label="Sensor 3")
box13.set_title("Sensor 3")
box13.legend()

# Find line of best fit and plot for local temperature sensors
coefficients_temp_local = np.polyfit(range(num_samples), average, 1)
line_of_best_fit_temp_local = np.polyval(coefficients_temp_local, range(num_samples))
box10.plot(line_of_best_fit_temp_local, color="blue", linestyle="--", label="Line of Best Fit")
box10.legend()

# Plotting predicted values for the next 12 hours for local temperature sensors
next_x_temp_local = np.arange(num_samples, num_samples + 12)
predicted_values_temp_local = np.polyval(coefficients_temp_local, next_x_temp_local)
box10.plot(next_x_temp_local, predicted_values_temp_local, color="green", marker="o", linestyle="--",
           label="Predicted Values")
box10.legend()

# Remote sensors' (data from server) graphs for temperature
sensors_temp = []
for s in [1, 2, 3]:
    data_temp = get_sensor(id=s, sensor_type="Temperature")
    sensors_temp.append(data_temp)
    print(f"Sensor {s} obtained with {len(data_temp)} samples")

num_samples_remote_temp = len(sensors_temp[0])
average_remote_temp = np.mean(sensors_temp, axis=0)
std_dev_remote_temp = np.std(sensors_temp, axis=0)

fig_temp = plt.figure(figsize=(12, 8))
grid_temp = GridSpec(3, 3, figure=fig_temp)
plt.subplots_adjust(hspace=0.5)

box9 = fig_temp.add_subplot(grid_temp[2, :])
box9.plot(range(num_samples_remote_temp), average_remote_temp, color="red", label="Average")
box9.fill_between(range(num_samples_remote_temp), average_remote_temp - std_dev_remote_temp,
                  average_remote_temp + std_dev_remote_temp, alpha=0.5, linewidth=0, label='Range')
box9.legend()
box9.set_title("Average of all remote sensors (Temperature)")

for i, ax_temp in enumerate([grid_temp[0, 0], grid_temp[0, 1], grid_temp[0, 2]]):
    box_temp = fig_temp.add_subplot(ax_temp)
    box_temp.plot(sensors_temp[i], color="black", label=f"Sensor {i + 1}")
    box_temp.legend()
    box_temp.set_title(f"Sensor {i + 1} (Temperature)")

plt.show()
