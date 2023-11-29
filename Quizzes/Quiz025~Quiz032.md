# Quiz025:
 ## Question:
<img width="1068" alt="Screen Shot 2023-11-16 at 13 41 44" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/89aaec6f-52f3-434b-9d83-3e11152c629b">

 Fig. 1 Image of question of Quiz 025
 ## Answer:
 ```.py
import matplotlib.pyplot as plt
import numpy as np

sensorA = [16,24,24,9,23,26,26,23,25,14]
sensorB = [2,19,25,10,11,24,17,7,24,17]
sensorC = [15,11,24,21,6,2,18,27,1,16]

samples = []
for i in range(len(sensorA)):
    samples.append(i)

fig = plt.figure(figsize=(8,4))
plt.subplot(1,2,1)

mean = []
standard_dev = []
max_v = []
min_v = []
for i in range(len(sensorA)):
    data = [sensorA[i],sensorB[i],sensorC[i]]
    mean.append(np.mean(data))
    standard_dev.append(np.std(data))
    max_v.append(max(data))
    min_v.append(min(data))

print(mean)
print(standard_dev)
print(max_v)
print(min_v)
print(samples)

plt.fill_between(samples,max_v,min_v,alpha=.5,linewidth=0,color="#55868C")
plt.errorbar(samples,mean,standard_dev,fmt="o")
plt.show()
 ```
<img width="321" alt="Screen Shot 2023-11-16 at 15 05 23" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/c526c3de-18fe-4ba3-9f40-193bac822bd9">

Fig. 2 Image of answer of Quiz 025
 ## Running Code:
<img width="259" alt="Screen Shot 2023-11-16 at 20 22 34" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/1061049e-1904-411e-80bc-9e118ca179d9">
<img width="1064" alt="Screen Shot 2023-11-16 at 20 23 03" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/ea9ed7ed-4665-4d24-9b2d-6b9e66ac81d4">

 Fig. 3 Image of code running of Quiz 025

 # Quiz026:
 ## Question:
<img width="1058" alt="Screen Shot 2023-11-22 at 11 07 15" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/ec35df7d-0b48-4b6d-9785-0eb00a22668d">

 Fig. 4 Image of question of Quiz 026
 ## Answer:
 ```.py
import matplotlib.pyplot as plt
import numpy as np

plt.style.use('ggplot')
data = {'x': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19],
        'y': [24, 1, 2, 25, 26, 21, 23, 24, 34, 49, 2, 19, 32, 7, 17, 36, 7, 45, 28, 40]}

if "title" in data:  # asking if a key exists
    print(data["title"])
else:
    data["title"] = "quiz_data_science"
print(data)

plt.plot(data["x"], data["y"])
plt.show()
 ```
<img width="783" alt="Screen Shot 2023-11-16 at 20 03 32" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/3ccc8565-b7ac-4d78-836b-46a8f77f5c77">

Fig. 5 Image of answer of Quiz026
 ## Running Code:
<img width="432" alt="Screen Shot 2023-11-16 at 13 33 56" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/f05ef5b8-619b-4209-8232-f7f22790164e">

 Fig. 6 Image of code running of Quiz 026

# Quiz027:
 ## Question:
<img width="1069" alt="Screen Shot 2023-11-22 at 11 06 56" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/3f5b9095-7c9a-4828-87f9-5e438a5d1bf8">

 Fig. 7 Image of question of Quiz 027
 ## Answer:
 ```.py
def count_letter(my_dict, msg):
    for letter in msg:
        if letter in my_dict:
            my_dict[letter] += 1
    return my_dict

case1 = count_letter({"w":0,"l":0,"c":0},"hello world")
print(case1)

case2 = count_letter({"a":0,"e":0,"i":0,"o":0,"u":0}, "Why did I choose CS?")
print(case2)
 ```
<img width="646" alt="Screen Shot 2023-11-22 at 11 12 19" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/a577c461-4c93-4a2f-9800-471b3369ae75">

Fig. 8 Image of answer of Quiz 027

<img width="630" alt="Screen Shot 2023-11-22 at 11 14 38" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/65c51b2c-0e03-48a3-87a1-17abaa19e38a">

Fig. 9 Image of answer of Quiz 027
 ## Running Code:
 <img width="834" alt="Screen Shot 2023-11-22 at 11 10 38" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/5c1b09f3-7ea6-4840-8c07-b4440917cf67">

 Fig. 10 Image of code running of Quiz 027

# Quiz028:
 ## Question:
<img width="1077" alt="Screen Shot 2023-11-27 at 8 22 02" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/c8f8c8ca-29ce-4c61-8e6f-e93ea542205b">

 Fig. 11 Image of question of Quiz 028
 ## Answer a:
 ```.py
def sort_dict(in_dict):
    x = []
    k = []
    for i in in_dict.values():
        x += [i]
    for m in in_dict.keys():
        k += [m]
    for i in range(len(x)):
        for n in range(i+1, len(x)):
            if x[n] < x[i]:
                x[i],x[n] = x[n],x[i]
                k[i],k[n] = k[n],k[i]
    return x,k

case1 = sort_dict({"apple":5, "banana":2, "orange":8,"grape":1})
print(case1)

case2 = sort_dict({"python":3,"java":8,"c++":5,"javascript":2})
print(case2)
```
 ## Answer b:
 ```.py
 import matplotlib.pyplot as plt
import numpy as np

plt.style.use('ggplot')

plt.xlabel("X)")
plt.ylabel("Y")

def produce ():
   x_out = []
   y_out = []
   x = 0
   for _ in range(100):
       y = np.sin(2 * np.pi * x)
       x_out.append(x)
       y_out.append(y)
       x += 0.01

   return y_out, x_out

import matplotlib.pyplot as plt

plt.style.use('ggplot')
y,x =produce()
plt.plot(x,y, color = "r", marker = "o")
plt.xlabel("x", fontsize = 20)
plt.ylabel("$y=sin(2*pi*x)$", fontsize = 15)
plt.show()
```
## Running Code a: 
<img width="609" alt="Screen Shot 2023-11-23 at 9 12 21" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/6a3a3996-ca05-4cc1-a069-e3073cdcc332">

Fig.12 Image of code running for Quiz 028
## Running Code b:
<img width="541" alt="Screen Shot 2023-11-23 at 9 05 04" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/2ecd0af7-fb2e-4cf3-a676-a2b7040d8197">

Fig.13 Image of code running for Quiz 028

# Quiz029:
 ## Question:
<img width="1073" alt="Screen Shot 2023-11-27 at 8 13 08" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/4bbc4c25-19c2-45fa-bf98-ab1cb792fc1d">

 Fig. 14 Image of question of Quiz 028
 ## Answer:
 ```.py
def invert(dictionary):
    invert = {value: key for key, value in dictionary.items()}
    return invert

dict1 = {'a': 1, 'b': 2, 'c': 3}
inverted_dict = invert(dict1)
print(inverted_dict)

dict2 = {'bob':26,'alice':30,'carl':40}
inverted_dict2 = invert(dict2)
print(inverted_dict2)
```

<img width="821" alt="Screen Shot 2023-11-27 at 8 35 46" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/671da302-aa3f-4706-9473-eb8254ebe229">

Fig. 15 Answer for a 

## Running Code: 
<img width="383" alt="Screen Shot 2023-11-27 at 8 30 47" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/c1f5c80d-f863-4213-8078-8d8945f213d2">

Fig. 16 Image of code running

# Quiz030:
 ## Question:

 Fig. 17 Image of question of Quiz 028
 ## Answer:
 ```.py
import requests
import matplotlib.pyplot as plt
import numpy as np

def get_sensor(id:int=2, ip:str="192.168.6.153"):
    request = requests.get(f"http://{ip}/readings")
    data = request.json()
    sensors = data["readings"][0]
    sensor = []
    for s in sensors:
        if s["sensor_id"]==id:
            sensor.append(s["value"])

    return sensor

def smoothing(x:list,size_window:int=5):
    smooth_x = []
    t = []
    for i in range(200, 400, size_window//2):
        points = sum(x[i:i+size_window])/size_window
        smooth_x.append(points)
        t.append(i)

    return t, smooth_x


sensor2= get_sensor()
print(sensor2)

x,y = smoothing(x=sensor2)
plt.plot(x,y)
coefficients = np.polyfit(x, y, 1)
line_of_best_fit = np.polyval(coefficients, x)
plt.plot(x,line_of_best_fit)

plt.show()
```
## Running Code: 
<img width="512" alt="Screen Shot 2023-11-27 at 8 20 40" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/73d1e449-c340-41f6-bb63-921f6e1d50fe">

Fig. 18 Image of code running

# Quiz031:
 ## Question:

 Fig. 19 Image of question of Quiz 031
 ## Answer:
 ```.py
import requests
import matplotlib.pyplot as plt
def get_sensor(id:int=1, ip:str="192.168.6.153"):
    request = requests.get(f"http://{ip}/readings")
    data = request.json()
    sensors = data["readings"][0]
    sensor = []
    for s in sensors:
        if s["sensor_id"]==id:
            sensor.append(s["value"])
    return sensor


def smoothing(x:list,size_window:int=5):
    smooth_x = []
    t = []
    for i in range(0, len(x), size_window):
        points = sum(x[i:i+size_window])/size_window
        smooth_x.append(points)
        t.append(i)

    return t, smooth_x

sensor1= get_sensor()
sensor2 = get_sensor(id=2)

sensor3=[]
for i in range(len(sensor1)):
    sensor3.append(sensor1[i]+sensor2[i])

x,y = smoothing(x=sensor3)
plt.subplot(3,1,1)
plt.plot(sensor1)
plt.subplot(3,1,2)
x,y = smoothing(x=sensor2)
plt.plot(x,y)
plt.subplot(3,1,3)
plt.plot(sensor3)
plt.show()
```
## Running Code: 
<img width="528" alt="Screen Shot 2023-11-29 at 9 29 39" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/e314b6de-6614-4b64-8e03-f7ce54186b53">

Fig. 20 Image of code running
