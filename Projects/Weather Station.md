
![Screen Shot 2023-11-27 at 9 06 34](https://github.com/Yuiko-tsr/unit-2/assets/142757977/5197c956-1981-4c54-a813-4b4cad738ce8)

# Unit 2: A Distributed Weather Station for ISAK

## Criteria A: Planning

## Problem definition
Many students visit the nurses' office due to sore throat and we believe this may be caused from lack of humidification. As a result of the student rooms' poor humidity and temperature, ISAK students have been seeing nurses far more frequently for sore throat-related problems. The nurses think that the humidity and warmth in the student rooms are to blame for the sore throats that students are experiencing. 

## Proposed Solution
Considering the client requirements an adequate solution includes a low cost sensing device for humidity and temperature and a custom data script that process and anaysis the samples acquired. For a low cost sensing device an adequate alternative is the DHT11 sensor[^1] which is offered online for less than 5 USD and provides adequare precision and range for the client requirements (Temperature Range: 0°C to 50°C, Humidity Range: 20% to 90%). Similar devices such as the DHT22, AHT20 or the AM2301B [^2] have higher specifications, however the DHT11 uses a simple serial communication (SPI) rather than more eleborated protocols such as the I2C used by the alternatives. For the range, precision and accuracy required in this applicaiton the DHT11 provides the best compromise. Connecting the DHT11 sensor to a computer requires a device that provides a Serial Port communication. A cheap and often used alternative for prototyping is the Arduino UNO microcontroller [^3]. "Arduino is an open-source electronics platform based on easy-to-use hardware and software"[^4]. In additon to the low cost of the Arduino (< 6USD), this devide is programable and expandable[^1]. Other alternatives include diffeerent versions of the original Arduino but their size and price make them a less adequate solution.

Considering the budgetary constrains of the client and the hardware requirements, the software tool that I proposed for this solution is Python. Python's open-source nature and platform independence contribute to the long-term viability of the system. The use of Python simplifies potential future enhancements or modifications, allowing for seamless scalability without the need for extensive redevelopment [^5][^6]. In comparison to the alternative C or C++, which share similar features, Python is a High level programming language (HLL) with high abstraction [^7]. For example, memory management is automatic in Python whereas it is responsability of the C/C++ developer to allocate and free up memory [^7], this could result in faster applications but also memory problems. In addition a HLL language will allow me and future developers extend the solution or solve issues proptly.  

## Design statement

The nurses want a remote server that they can access online to monitor the temperature and humidity in the student dorms at various times of the day and compare it with the ideal levels as well as the outside temperature and humidity. Therefore, we plan to measure the humidity of campus and compare with the necessary humidity to maintain health. Therefore, we will create a program that will calculate the average of the humidity and temperature of a room using three sensors during the 48 hours the program runs. After measuring the average we will create a graph using these data to compare with the optimal humidity/temperature so the nurses can use this data to improve the students' living environments. We will do this by using python and three DHT_11 sensors to collect the humidity and temperature. The program will store the data to a csv file and upload this data to the "192.168.6.153" server to prevent the loss of information

## Success Criteria

[^1]: Industries, Adafruit. “DHT11 Basic Temperature-Humidity Sensor + Extras.” Adafruit Industries Blog RSS, https://www.adafruit.com/product/386. 
[^2]: Nelson, Carter. “Modern Replacements for DHT11 and dht22 Sensors.” Adafruit Learning System, https://learn.adafruit.com/modern-replacements-for-dht11-dht22-sensors/what-are-better-alternatives.   
[^3]:“How to Connect dht11 Sensor with Arduino Uno.” Arduino Project Hub, https://create.arduino.cc/projecthub/pibots555/how-to-connect-dht11-sensor-with-arduino-uno-f4d239.  
[^4]:Team, The Arduino. “What Is Arduino?: Arduino Documentation.” Arduino Documentation | Arduino Documentation, https://docs.arduino.cc/learn/starting-guide/whats-arduino.  
[^5]:Tino. “Tino/PyFirmata: Python Interface for the Firmata (Http://Firmata.org/) Protocol. It Is Compliant with Firmata 2.1. Any Help with Updating to 2.2 Is Welcome. the Capability Query Is Implemented, but the Pin State Query Feature Not Yet.” GitHub, https://github.com/tino/pyFirmata. 
[^6]:Python Geeks. “Advantages of Python: Disadvantages of Python.” Python Geeks, 26 June 2021, https://pythongeeks.org/advantages-disadvantages-of-python/. 
[^7]: Real Python. “Python vs C++: Selecting the Right Tool for the Job.” Real Python, Real Python, 19 June 2021, https://realpython.com/python-vs-cpp/#memory-management. 

1. The solution provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours. 
1. The local variables will be measure using a set of 3 sensors around the dormitory.
2. The solution provides a mathematical modelling for the Humidity and Temperature levels for each Local and Remote locations. (Non-lineal model)
3. The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standad deviation, minimum, maximum, and median.
4.  Posted to the remote server as a backup.
5. The solution provides a prediction for the subsequent 12 hours for both temperature and humidity.
6. The solution includes a poster summarizing the visual representations, model and analysis created. The poster includes a recommendation about healthy levels for Temperature and Humidity.

_TOK Connection: To what extent does ```the use of data science``` in climate research influence our understanding of environmental issues, and what knowledge questions arise regarding the ```reliability, interpretation, and ethical implications``` of data-driven approaches in addressing climate change_

1. How does our use of technology shape our understanding of the environment
2. What responsibilities do we have as technologists when it comes to handling personal data related to our living spaces?
3. What cultural and contextual factors might impact our interpretation of the results, especially when comparing our local readings with those from the campus? 

# Criteria B: Design

## System Diagram 

![Screen Shot 2023-11-29 at 10 01 54](https://github.com/Yuiko-tsr/unit-2/assets/142757977/e3c4b668-ce9c-466b-b991-fb31415cf15e)



**Fig.2** shows the system diagram for the proposed solution. The indoor variables will be measured using an Arduino and three DHT11 sensors located inside a room. Three sensors are used to determine more precisely the physical values and include measurement uncertainty. The outdoor variables will be requested to the remote server using a GET request to the API of the server at ```192.168.6.153/readings```. The local values are stored in a CSV database locally and a backup copy will be store in the remote server using the **Weather API**. 

## Flow Charts
<img width="377" alt="Screen Shot 2023-12-10 at 16 29 03" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/5eeca73a-d292-455f-bd9c-0e87e8034e50">

**Fig 1** Flow chart of the smoothing function (Easiest function)
This function allows us to make the graphs we make more smooth by taking the average of 5 data values for every 2 points.

<img width="346" alt="Screen Shot 2023-12-10 at 16 34 56" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/d926544b-7314-4cb6-8f4c-58f5e8b8791f">

**Fig 2** Flow chart of the main funciton (Medium level function)
This function allows us to collect data every 5 minutes by using the measure function every five minutes.

<img width="246" alt="Screen Shot 2023-12-10 at 16 39 29" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/d4f452e9-24c8-43d0-80d3-ac80fa3cf577">

**Fig 3** Flow chart of the create_sensor funciton (Most important function)
This function allows us to create new sensors so we can store our data in the servers.

## Record of Tasks
| Task No | Planned Action                                                | Planned Outcome                                                                                                 | Time estimate | Target completion date | Criterion |
|---------|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------|------------------------|-----------|
|1| Write the Problem context | Wrote the Problem context| 10min         | Nov 22                 | A         |
|2|Write the Proposed Solution | Write the Proposed Solution                        | 20min         | Nov 24                 | A         |
|3|Writng code |Started to write a code which collects data and sends it to the server and csv file|30 min|Nov 29|C|
|4|Writing code|Continued to write code |2 hours|Dec 2|C|
|5|Arduino  board |installed all the necessary elements on the Arduino board|40 min|Dec 3|C|
|6|Writing code |Continued to write code |2 hours 30 min|Dec 3|C|
|7|Making scheme for placing the sensors|Chose the best locations to put every sensor and reflected on the map of the room|20 min|Dec 3|A, C|
|8|End the code|To end writing code which gets information from 3 sensors, sends this data to the server and csv file|30 min|Dec 5|C|
|9|Correcting the code |To find the reasons of all mistakes and eliminate errors|1 hour|Dec 5|C|
|10|Work woth sensors|Install sensors throughout the room|20 min|Dec 5|C|
|11|Getting data|Got information about humidity and temperature in the room for 2 days|48 hour|Dec 5|C|
|12|Video planning|Identified the main ideas for the final video|25 min|Dec 7|D|
|13|Writing code|Wrote the code to display the received data in the form of graphs|1,5 hours|Dec 8|C|
|14|Writing code|Wrote the code to display the received data in the form of graphs|1 hour|Dec 9|C|
|15|Writing code|Ended the code to display the received data in the form of graphs|40 min|Dec 10|C|
|16|Making poster|Replased the main objects in the poster|30 min|Dec 10|C|
|17|Making system diagram|Made the system diagram of the code|1 hour|Dec 10|B|
|18|Studing of norms|Studied norms of humidity and temperature level of favorable conditions using variable researches and articles from different countries|1.5 hours|Dec 10|D|
|19|Analyzing the data|Analyzed the received information and compared it with the norms|40 min|Dec 11|C|
|20|Making poster|Continued to make the poster|1 hour|Dec 11|C|
|21|TOK questions|Wrote 2 answers to TOK questions|40 min|Dec 11|A|
|22|Text for the video|Wrote the text for final video|30 min|Dec 11|D|
|23|Success Criteria|Wrote about 1-3 success criteria and attached parts of the code and schemes|40 min|Dec 11|A, C|
|24|Making poster|Wrote conclusion and recommendation and put in on the poster|20 min|Dec 12|A, C|
|25|Code writing| Wrote the code to predict Humidity and Temperature level in 12 hours|2 hours|Dec 13|C|
|26|Making video|Made speaking of the text, screen video and added some video from process of getting data, writing subtitles, edited the video with project presentation|5 hours|Dec 13|D|
|27|Finishing work with the banner|Added all the details and graphics to the banner, uploaded it to the project|30 min|Dec 13|C|
|28|Checking| Checked all points of the project and added all the unfinished ones|1.5 hours|Dec 14|A, B, C, D|

## Test Plan

# Criteria C: Development

## List of techniques used

## Development

### 1. The solution provides a visual representation of the Humidity and Temperature values inside a dormitory (Local) and outside the house (Remote) for a period of minimum 48 hours.

### 2.The local variables will be measure using a set of 3 sensors around the dormitory.
We used 3 sensors to collect data about humidity and temperature around the room (Fig. C.2.1).. The sensors were attached to the bed, desk and place near the window, which lets the client see conditions in locations where students spend more of their time, and compare the average indicator with norms.

![Web_Photo_Editor](https://github.com/Yuiko-tsr/unit-2/assets/142757977/7c4e5410-04ae-46ff-8ebc-7f4d74ff2b37)

*Fig. C.2.1* The sensors location
### 3. The solution provides a mathematical modeling for the Humidity and Temperature levels for each Local and Remote locations. (Non-lineal model)
All data from 3 sensors inside the room and outside is used to create variable graphs. They provide levels of Humidity and Temperature in 6 different zones. We used csv file as a source of data for graphs of indoor sensors (code.C.3.1)
The next part of the code provides modeling for the Hum/Tem level using outside sensors, so it gets information from the local network (code.C.3.2). Then we used “smoothing” to improved visualization (code.C.3.3). Then we created a 2x7 grid of subplots using Matplotlib and add all graphs here (code.C.3.4)

```.py
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

```

*Code C.3.1*

```.py
def get_sensor(id: int, ip: str = "192.168.6.153"):
     request = requests.get(f"http://{ip}/readings")
     data = request.json()
     sensors = data["readings"][0]
     sensor = []
     for s in sensors:
         if s["sensor_id"] == id:
             sensor.append(s["value"])

     return sensor
```

*Code.C.3.2*

```.py
def smoothing(x: list, size_window: int = 5):
    smooth_x = []
    t = []
    for i in range(200, 400, size_window // 2):
        points = sum(x[i:i + size_window]) / size_window
        smooth_x.append(points)
        t.append(i)
    return t, smooth_x
```

*Code C.3.3*


```.py
fig = plt.figure(figsize=(100, 10))
grid = GridSpec(2,7,figure=fig)
x, y = smoothing(x=sensor0)
x2, y2 = smoothing(x=sensor2)
x4, y4 = smoothing(x=sensor4)
box1 = fig.add_subplot(grid[0,0])
plt.plot(x, y, label="sensor 0")
plt.plot(x2, y2, label="sensor 2")
plt.plot(x4, y4, label="sensor 4")
plt.title("Outdoor \n humidity")
plt.legend()
x1, y1 = smoothing(x=sensor1)
x3, y3 = smoothing(x=sensor3)
x5, y5 = smoothing(x=sensor5)
box2 = fig.add_subplot(grid[1,0])
plt.subplots_adjust(hspace=0.5)
plt.subplots_adjust(wspace=0.5)
plt.plot(x1, y1, label="sensor 1")
plt.plot(x3, y3, label="sensor 3")
plt.plot(x5, y5, label="sensor 5")
plt.title(f"Outdoor \n temperature")
plt.legend()
```
*Code C.3.4*

### 4.The solution provides a comparative analysis for the Humidity and Temperature levels for each Local and Remote locations including mean, standard deviation, minimum, maximum, and median.

We analyzed some sources of information and got the solution that the perfect temperature for the room is 23-24C. 21-25C is an acceptable norm. The best level of humidity is 40-50%. 35-55% also is considered an admissible index. As we can in in the fig.C.4.1, C.4.2 and C.4.3, the norms are observed not always. The green line is ideal level, the yellow one is permissible indices


![Image_20231214_095946_261](https://github.com/Yuiko-tsr/unit-2/assets/142757977/c97f60fd-2efb-4664-824a-d2b24c253c6f)


*Fig. C.4.1* Graph with data about the Humidity and Temperature levels from desk zone


![Image_20231214_095946_345](https://github.com/Yuiko-tsr/unit-2/assets/142757977/c5bbea51-977d-4bb1-9a7f-b1d348985bfe)


*Fig. C.4.2* Graph with data about the Humidity and Temperature levels from window zone


![Image_20231214_095946_305 (1)](https://github.com/Yuiko-tsr/unit-2/assets/142757977/52239818-d87a-4a13-b987-0c5f1c80bb75)



*Fig. C.4.3* Graph with data about the Humidity and Temperature levels from bed zone


### 5. Posted to the remote server as a backup.

All data about humidity and temperature from 3 sensors are sent to csv file and remote server (Fig. C.5.1). Information saved here is a backup option in case of csv file problems and can be used by the clients, if they are ​​authorized.


![Screen Shot 2023-12-14 at 10 55 00](https://github.com/Yuiko-tsr/unit-2/assets/142757977/43a0dcde-06dd-442b-86f7-63221a60ee33)


*Fig.C.5.1* 

#### The part of code, which creates sensors 
```.py
def create_sensor(sensor,token, ip="192.168.6.153"):

    auth = {"Authorization": f"Bearer {token}"}
    r = requests.post(f'http://{ip}/sensor/new', json=sensor, headers=auth)
    print(r.json())
```

#### List of the sensors 
```.py
sensor_bed = {"type": "Temperature", "location": "R1-15", "name": "sensor_bed", "unit": "C"}
sensor_desk = {"type": "Temperature", "location": "R1-15", "name": "sensor_desk", "unit": "C"}
sensor_window = {"type": "Temperature", "location": "R1-15", "name": "sensor_window", "unit": "C"}
sensor_bed = {"type": "Humidity", "location": "R1-15", "name": "sensor_bed", "unit": "%"}
sensor_desk = {"type": "Temperature", "location": "R1-15", "name": "sensor_desk", "unit": "C"}
sensor_window = {"type": "Temperature", "location": "R1-15", "name": "sensor_window", "unit": "C"}
```

#### The part of code, which sent data to the server
```.py

def add_data(value, token, id, ip="192.168.6.153"):
    auth = {"Authorization": f"Bearer {token}"}
    new_record = {"datetime": datetime.isoformat(datetime.now()), "sensor_id": id, "value": value}

    r = requests.post(f'http://{ip}/reading/new', json=new_record, headers=auth)
    print(r.json())
```



### 6. The solution provides a prediction for the subsequent 12 hours for both temperature and humidity.
After getting all data about temperature level in the room
and graphs, we are able to make predictions for the next 12 hours using code.C.6.3 
Also it proved almost impossible to predict accurate humidity levels because of permanent changes, as you can see in the fig.C.6.2


![Image_20231214_103524_779](https://github.com/Yuiko-tsr/unit-2/assets/142757977/69abc542-2a69-4f8d-82fa-6d40849eec21)


*Fig.C.6.1* temperature prediction 

![Image_20231214_103524_701](https://github.com/Yuiko-tsr/unit-2/assets/142757977/b0a41516-7192-49c6-bc54-19aee015ccd9)


*Fig.C.6.2* humidity prediction 
```.py
poly_features_temp = PolynomialFeatures(degree=2)
x_poly_temp = poly_features_temp.fit_transform(x_values_temp.reshape(-1, 1))
reg_temp = LinearRegression().fit(x_poly_temp, y_values_temp)
pred_temp = reg_temp.predict(x_poly_temp)


box13 = fig.add_subplot(grid[0, 6])
plt.plot(mean_inside_temp, label="Actual Temperature")


temp=0
x1=[]
y1=[]
for _ in range (100):
    x1.append(temp)
    y1.append(0.026*temp+21)
    temp+=2.5
temp=250
x2=[]
y2=[]
for _ in range (100):
    x2.append(temp)
    y2.append(-0.0111*(temp-250)+27.5)
    temp+=2.7
temp=550
x3=[]
y3=[]
for _ in range(100):
    x3.append(temp)
    y3.append(0.0625*(temp-550)+24.5)
    temp+=0.24

temp = 574
x4=[]
y4=[]
for _ in range(100):
    x4.append(temp)
    y4.append(-0.1*(temp-574)+26)
    temp+=0.1
temp=584
x5=[]
y5=[]
for _ in range(100):
    x5.append(temp)
    y5.append(0.0417*(temp-584)+25)
    temp+=0.6

plt.plot(x1, y1, label="Line of Best Fit", color="blue")
plt.plot(x2, y2, color="blue")
plt.plot(x3, y3, color="blue")
plt.plot(x4, y4, color="blue")
plt.plot(x5, y5, color="red",label="Prediction")
plt.title("Temperature\n Line of Best Fit \nand Prediction")
plt.xlim([0,650])
box13.legend()

x_values_humid = np.array(x_values)[np.array(x_values)>500]
y_values_humid = np.array(mean_inside_humid)[np.array(x_values)>500]
coefficients_humid = np.polyfit(x_values_humid,y_values_humid,1)

line_of_best_fit_humid =np.polyval(coefficients_humid,x_values_humid)


box14 = fig.add_subplot(grid[1, 6])
plt.plot(mean_inside_humid, label="Actual Humidity")
plt.plot(x_values_humid, line_of_best_fit_humid,label="Line of Best Fit")
plt.title("Humidity\n Line of Best Fit \nand Prediction")
plt.xlim([500,650])
box14.legend()

plt.show()
```
*Code.C.6.3* 


### 7. The solution includes a poster summarizing the visual representations, model and analysis created. The poster includes a recommendation about healthy levels for Temperature and Humidity.
To summarize all the information we got and present our research to the clients we made a banner. It contains all the information about our methods and materials, 14 graphs of indoor and outdoor sensors, our conclusion and some recommendation about remedial measures to improve living conditions 
![Screen Shot 2023-12-14 at 8 04 57](https://github.com/Yuiko-tsr/unit-2/assets/142757977/0aa081f9-8406-4f60-8c00-baca627534f0)
https://www.canva.com/design/DAF2dSGzz78/WDoAuLG9kkOW7O9i_ROZDA/edit?utm_content=DAF2dSGzz78&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton


## TOK questions

### 1). How does our use of technology shape our understanding of the environment?

Using technology in research enables people efficient data collection and analysis of temperature and humidity. Continuous monitoring over a 48-hour period allows us to observe variations in temperature and humidity levels throughout the day and promptly identify deviations from favorable norms. The ability to receive real-time information enables us to take immediate action, implementing necessary measures to address any anomalies as soon as they arise. Using technology let us to get to know the level of quality of our living conditions for their improvement if required                                 
### 2). What responsibilities do we have as technologists when it comes to handling personal data related to our living spaces?

Handling everyone’s personal data should be conducted with full assurance of anonymity. We as technologists must provide guarantee of this. Results of research about any living room have a big importance, because changes will also be made in case of non-compliance. Accordingly, all information must be 100% authentic and the analysis carried out as diligently as possible

### 3). What cultural and contextual factors might impact our interpretation of the results, especially when comparing our local readings with those from the campus?
Since the average temperature and humidity indicators differ greatly from each other in various countries and climates, the comfortable conditions for the researcher may stand apart from the average norms for the research area. In connection with this all conclusions and recommendations must be as unbiased as possible. Technologists should use varied articles and research to study average indicators of comfortable conditions, but not their own experience.





# Criteria D: Functionality

A 7 min video demonstrating the proposed solution with narration

