```.py
from matplotlib.gridspec import GridSpec
import matplotlib.pyplot as plt
import numpy as np
from datetime import datetime, timedelta
import serial
from time import sleep
import requests
import pandas as pd
from matplotlib.gridspec import GridSpec

import matplotlib.pyplot as plt
import matplotlib
import requests
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

def get_sensor(id: int, ip: str = "192.168.6.153"):
     request = requests.get(f"http://{ip}/readings")
     data = request.json()
     sensors = data["readings"][0]
     sensor = []
     for s in sensors:
         if s["sensor_id"] == id:
             sensor.append(s["value"])

     return sensor

def smoothing(x: list, size_window: int = 5):
    smooth_x = []
    t = []
    for i in range(200, 400, size_window // 2):
        points = sum(x[i:i + size_window]) / size_window
        smooth_x.append(points)
        t.append(i)
    return t, smooth_x

sensor1 = get_sensor(1)
print(sensor1)
sensor2 = get_sensor(2)
print(sensor2)
sensor3 = get_sensor(3)
print(sensor3)
sensor4= get_sensor(4)
print(sensor4)
sensor5 = get_sensor(5)
print(sensor5)
sensor0 = get_sensor(0)
print(sensor0)

fig = plt.figure(figsize=(40, 10))
grid = GridSpec(2,7,figure=fig)
x, y = smoothing(x=sensor0)
x2, y2 = smoothing(x=sensor2)
x4, y4 = smoothing(x=sensor4)
box1 = fig.add_subplot(grid[0,0])
plt.plot(x, y, label="sensor 0")
plt.plot(x2, y2, label="sensor 2")
plt.plot(x4, y4, label="sensor 4")
plt.title("Outdoor humidity")
plt.legend()
x1, y1 = smoothing(x=sensor1)
x3, y3 = smoothing(x=sensor3)
x5, y5 = smoothing(x=sensor5)
box2 = fig.add_subplot(grid[1,0])
plt.subplots_adjust(hspace=0.5)
plt.plot(x1, y1, label="sensor 1")
plt.plot(x3, y3, label="sensor 3")
plt.plot(x5, y5, label="sensor 5")
plt.title("Outdoor temperature")
plt.legend()


mean_humid = []
z_values = []
temp = 0
for a, b in zip(sensor2, sensor4):
    z_values.append(temp)
    temp += 1
    mean_humid.append((a + b)/ 2)
# Calculate statistics for outdoor humidity
std_humid = np.std([sensor2, sensor4], axis=0)
max_humid = np.max([sensor2, sensor4], axis=0)
min_humid = np.min([sensor2, sensor4], axis=0)

# Calculate statistics for outdoor temperature
mean_temp = np.mean([sensor1[:len(sensor5)], sensor5], axis=0)
std_temp = np.std([sensor1, sensor5], axis=0)
max_temp = np.max([sensor1, sensor5], axis=0)
min_temp = np.min([sensor1, sensor5], axis=0)


samples = []
for i in range(len(sensor1)):
   samples.append(i)
# Plot statistics for outdoor humidity
box3 = fig.add_subplot(grid[0, 1])
plt.fill_between(samples, max_humid, min_humid, alpha=.5, linewidth=0, color="#55868C")
plt.plot(mean_humid, label="mean")
plt.plot(max_humid, label="maximum")
plt.plot(min_humid, label="minimum")
plt.title("Outdoor Humidity Statistics (N=2)")
plt.legend()

# Plot statistics for outdoor temperature
box4 = fig.add_subplot(grid[1, 1])
plt.fill_between(samples, max_temp, min_temp, alpha=.5, linewidth=0, color="#55868C")
plt.plot(mean_temp, label="mean")
plt.plot(max_temp, label="maximum")
plt.plot(min_temp, label="minimum")
plt.title("Outdoor Temperature Statistics (N=2)")
plt.legend()

df = pd.read_csv('reading_sw.csv')

window_humid = df.iloc[:, 1].tolist()
window_temp = df.iloc[:, 2].tolist()

dt = pd.read_csv('reading_st.csv')

table_humid = dt.iloc[:, 1].tolist()
table_temp = dt.iloc[:, 2].tolist()

db = pd.read_csv('reading_sb.csv')

bed_humid = db.iloc[:, 1].tolist()
bed_temp = db.iloc[:, 2].tolist()

box5 = fig.add_subplot(grid[0,2])
plt.plot(window_humid)
plt.title("Window Sensor Humidity")
box6 = fig.add_subplot(grid[1,2])
plt.plot(window_temp)
plt.title("Window Sensor Temperature")
box7 = fig.add_subplot(grid[0,3])
plt.plot(table_humid)
plt.title("Table Sensor Humidity")
box8 = fig.add_subplot(grid[1,3])
plt.plot(table_temp)
plt.title("Table Sensor Temperature")
box9 = fig.add_subplot(grid[0,4])
plt.plot(bed_humid)
plt.title("Bed Sensor Humidity")
box10 = fig.add_subplot(grid[1,4])
plt.plot(bed_temp)
plt.title("Bed Sensor Temperature")

mean_inside_humid = []
standard_dev_inside_humid = []
max_v_inside_humid = []
min_v_inside_humid = []
for i in range(len(table_humid)):
    data = [table_humid[i], bed_humid[i], window_humid[i]]
    mean_inside_humid.append(np.mean(data))
    standard_dev_inside_humid.append(np.std(data))
    max_v_inside_humid.append(max(data))
    min_v_inside_humid.append(min(data))
mean_inside_temp = []
standard_dev_inside_temp = []
max_v_inside_temp = []
min_v_inside_temp = []
for i in range(len(table_temp)):
    data = [table_temp[i], bed_temp[i], window_temp[i]]
    mean_inside_temp.append(np.mean(data))
    standard_dev_inside_temp.append(np.std(data))
    max_v_inside_temp.append(max(data))
    min_v_inside_temp.append(min(data))

x_values=range(0,len(table_temp))
box11 = fig.add_subplot(grid[0,5])
plt.fill_between(x_values, max_v_inside_humid, min_v_inside_humid, alpha=.5, linewidth=0, color="#55868C")
plt.plot(max_v_inside_humid, label="minimum")
plt.plot(min_v_inside_humid, label="maximum")
plt.plot(mean_inside_humid, label="mean")
plt.title("Indoor humidity average (N=3)")
plt.legend()
box12 = fig.add_subplot(grid[1,5])
plt.fill_between(x_values, max_v_inside_temp, min_v_inside_temp, alpha=.5, linewidth=0, color="#55868C")
plt.plot(mean_inside_temp, label="mean")
plt.plot(max_v_inside_temp, label="minimum")
plt.plot(min_v_inside_temp, label="maximum")
plt.title("Indoor temperature average (N=3)")
plt.legend()

# Assuming x_values and y_values are your data for temperature and humidity
# Replace these with your actual data or load them as needed
x_values_temp = np.array(x_values)
y_values_temp = np.array(mean_inside_temp)
x_values_humid = np.array(x_values)
y_values_humid = np.array(mean_inside_humid)

# Quadratic regression for temperature
poly_features_temp = PolynomialFeatures(degree=2)
x_poly_temp = poly_features_temp.fit_transform(x_values_temp.reshape(-1, 1))
reg_temp = LinearRegression().fit(x_poly_temp, y_values_temp)
pred_temp = reg_temp.predict(x_poly_temp)

# Plot temperature line of best fit and prediction
box13 = fig.add_subplot(grid[0, 6])
plt.plot(mean_inside_temp, label="Actual Temperature")
x,y = smoothing(x=mean_inside_temp)# Split the data into two parts based on the condition x < 300
x_part1 = np.array(x)[np.array(x) < 300]
y_part1 = np.array(y)[np.array(x) < 300]

# Split the data into two parts based on the condition x >= 300
x_part2 = np.array(x)[np.array(x) >= 300]
y_part2 = np.array(y)[np.array(x) >= 300]

# Calculate coefficients and line fits for each part
coefficients_part1 = np.polyfit(x_part1, y_part1, 1)
line_of_best_fit_part1 = np.polyval(coefficients_part1, x_part1)

coefficients_part2 = np.polyfit(x_part2, y_part2, 1)
line_of_best_fit_part2 = np.polyval(coefficients_part2, x_part2)

# Plot the data and line fits
plt.plot(x_part1, line_of_best_fit_part1, label="Line of Best Fit (Part 1)", color="blue")
plt.plot(x_part2, line_of_best_fit_part2, label="Line of Best Fit (Part 2)", color="red")
plt.title("Temperature Line of Best Fit (Quadratic Regression) and Prediction")
box13.legend()

x_values_humid = np.array(x_values)
y_values_humid = np.array(mean_inside_humid)

poly_features_humid = PolynomialFeatures(degree=2)
x_poly_humid = poly_features_humid.fit_transform(x_values_humid.reshape(-1, 1))
reg_humid = LinearRegression().fit(x_poly_humid, y_values_humid)
pred_humid = reg_humid.predict(x_poly_humid)

# Plot humidity line of best fit and prediction
box14 = fig.add_subplot(grid[1, 6])
plt.plot(mean_inside_humid, label="Actual Humidity")
plt.title("Humidity Line of Best Fit (Quadratic Regression) and Prediction")
box14.legend()

plt.show()

# ip = "192.168.6.153"
# id = "cu.usbserial-10"
#
# def createuser(user, ip="192.168.6.153"):
#     req = requests.post(f'http://{ip}/register', json=user)
#     print(req.json())
#
#
# def smoothing(x, smoothing_win=5, overlap=1):
#     smooth_x = []
#     t = []
#     for i in range(0, len(x), int(smoothing_win * overlap)):
#         smooth_x.append(sum(x[i:i + smoothing_win]) / smoothing_win)
#         t.append(i)
#     return t, smooth_x
#
# def login(user, ip="192.168.6.153"):
#     req = requests.post(f'http://{ip}/login', json=user)
#     access_token = req.json()["access_token"]
#     return access_token
#
#
# def create_sensor(sensor,token, ip="192.168.6.153"):
#
#     auth = {"Authorization": f"Bearer {token}"}
#     r = requests.post(f'http://{ip}/sensor/new', json=sensor, headers=auth)
#     print(r.json())
#
# def add_data(value,token, id, ip="192.168.6.153"):
#
#     auth = {"Authorization": f"Bearer {token}"}
#     new_record = {"datetime": datetime.isoformat(datetime.now()), "sensor_id": id, "value": value}
#
#     r = requests.post(f'http://{ip}/reading/new', json=new_record, headers=auth)
#     print(r.json())
# def read_arduino():
#     arduino = serial.Serial(port=f"/dev/{id}", baudrate=9600, timeout=0.1)
#     msg = ""
#     while len(msg) < 1 :
#         msg = arduino.readline()
#     data = msg.decode("utf-8").strip()
#
#     return data
#
# def main():
#     start_time = datetime.now()
#     total_duration = timedelta(hours=48)  # Total duration for data collection
#
#     while datetime.now() - start_time < total_duration:
#         # Collect data for 5 minutes
#         end_time = datetime.now() + timedelta(minutes=5)
#         while datetime.now() < end_time:
#             measure(49, 50, 48, 51, 52, 53, token)
#             sleep(300)  # Sleep for 10 seconds between readings
#
#     print("Data collection complete.")
#
# def save_csv(data, file_name):
#     print("Raw data:", data)  # Add this line to print the raw data
#     timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
#     with open(file_name, "a") as f:
#         f.write(f"{timestamp},{data}\n")
#
# def measure(stt, swt, sbt,sbh,sth,swh, token):
#     data = read_arduino()
#     print(data)
#     h1,t1,h2,t2,h3,t3 = data.split(",")
#     save_csv(data=f"{h1},{t1}", file_name="reading_st.csv")
#     save_csv(data=f"{h2},{t2}", file_name="reading_sw.csv")
#     save_csv(data=f"{h3},{t3}", file_name="reading_sb.csv")
#
#     add_data(float(h1), token, id=sbt)
#     add_data(float(t1), token, id=sbh)
#     add_data(float(h2), token, id=swh)
#     add_data(float(t2), token, id=swt)
#     add_data(float(h3), token, id=sth)
#     add_data(float(t3), token, id=stt)
# #
# # new_user = {"username": "yuiko", 'password':'1234'}
# #
# # req = requests.post('http://{ip}}/register', json=new_user)
# # print(req.json())
# #
# # x = create_sensor("tryout", type="temperature", location="Bed", ip="192.168.6.153")
# # print(x)
# agatha={"username": "agatha_unit2", 'password': 'a1b2c3'}
# # createuser(user=agatha)
# token=login(user=agatha)
# # sensor_bed = {"type": "Temperature", "location": "R1-15", "name": "sensor_bed", "unit": "C"}
# # sensor_desk = {"type": "Temperature", "location": "R1-15", "name": "sensor_desk", "unit": "C"}
# # sensor_window = {"type": "Temperature", "location": "R1-15", "name": "sensor_window", "unit": "C"}
# # sensor_bed = {"type": "Humidity", "location": "R1-15", "name": "sensor_bed_humidity", "unit": "%"}
# # sensor_desk = {"type": "Humidity", "location": "R1-15", "name": "sensor_desk_humidity", "unit": "%"}
# # sensor_window = {"type": "Humidity", "location": "R1-15", "name": "sensor_window_humidity", "unit": "%"}
# # create_sensor(sensor_bed,token)
# # create_sensor(sensor_desk, token)
# # create_sensor(sensor_window, token)
#
# # add_data(25,token,48)
#
# main()
#
#
