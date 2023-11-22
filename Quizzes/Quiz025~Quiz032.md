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
