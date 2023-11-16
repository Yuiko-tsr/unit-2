# Quiz017:
 ## Question:
<img width="1079" alt="Screen Shot 2023-10-28 at 15 47 18" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/0dedeeb3-e330-4402-85da-a4051ede5bb4">

 Fig. 1 Image of question of Quiz 017
 ## Answer a:
 ```.py
 def get_l3tt3r(msg=str):
     message =" "
     vowels = ["a","e","i","o", " "]
     numbers = ["4","3","1","0","_"]
     for letter in msg:
         if letter in vowels:
             v = vowels.index(letter)
             message += numbers[v]

         else:
             message += letter
     return message

 case1 = get_l3tt3r("Hello World")
 print(case1)
 case1 = get_l3tt3r("Why did I choose CS?")
 print(case1)
 case1 = get_l3tt3r("Remember the Figure Caption")
 print(case1)
 ```
 <img width="435" alt="Screen Shot 2023-10-23 at 8 21 18" src="https://github.com/Yuiko-tsr/unit-1/assets/134657923/f50a1ccc-25c9-4b5b-9c79-608df24f4627">

 Fig. 2 Image of answer of Quiz 017
 ## Answer b:
 <img width="885" alt="Screen Shot 2023-11-16 at 14 43 09" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/5aa555cf-de9a-4b6f-ab7d-a88ce49c3b79">

Fig.3 Image of answer of Quiz 017
 ## Running Code:
 <img width="1179" alt="Screen Shot 2023-10-23 at 8 20 40" src="https://github.com/Yuiko-tsr/unit-1/assets/134657923/8208d60f-bec6-4487-b8de-7af808e9dd0b">

 Fig. 4 Image of code running of Quiz 017

 ## Flowchart:
<img width="583" alt="Screen Shot 2023-10-28 at 15 46 40" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/363a9ca6-9a96-4312-9da6-615dcf0f5456">

 Fig. 5 Image of flowchart of Quiz 017

# Quiz018:
 ## Question:
<img width="1073" alt="Screen Shot 2023-11-01 at 11 06 41" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/d0c1242a-6ee8-4ac0-a2c4-8ffff1e8872e">

 Fig. 6 Image of question of Quiz 018
 ## Answer a:
```.py
def get_table():
    header = ["|", "A", "|", "B", "|", "C", "|"]
    out = ""

    for item in header:
        out += item
    out += "\n"

    for i in range(8):
        a = (i // 4) % 2
        b = (i // 2) % 2
        c = i % 2
        out += "|" + str(a) + "|" + str(b) + "|" + str(c) + "|\n"
    return out

table = get_table()
print(table)
```
## Answer b:
<img width="799" alt="Screen Shot 2023-11-16 at 14 50 42" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/798d2b00-d835-4654-9e4b-f6e830b93685">

Fig. 7: Image of answer of b
 ## Running Code:
<img width="1106" alt="Screen Shot 2023-10-25 at 10 46 30" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/6684c2aa-6b1e-4330-9fae-80b63bc345da">

 Fig. 8 Image of code running of Quiz 018

 ## Flowchart:
<img width="621" alt="Screen Shot 2023-10-28 at 15 54 00" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/83a7b401-c9d4-472f-bfba-84ee4d94c98f">

 Fig. 9 Image of flowchart of Quiz 018
 
# Quiz019:
 ## Question:
<img width="1063" alt="Screen Shot 2023-11-16 at 12 51 24" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/6da984c3-e183-40d3-8648-fc1074e9b7ac">

 Fig. 10 Image of question of Quiz 019
 ## Answer a:
```.py
def get_table():
    header = ["|", "A", "|", "B", "|", "C", "|","AB + not B + not CB", "|"]
    out = ""

    for item in header:
        out += item
    out += "\n"

    for i in range(8):
        a = (i // 4) % 2
        b = (i // 2) % 2
        c = i % 2
        eq = int((a and b) or (not b) or (not (c and b)))
        out += "|" + str(a) + "|" + str(b) + "|" + str(c) + "|" + str(eq) + "|\n"
    return out

table = get_table()
print(table)
```
## Answer b:
<img width="687" alt="Screen Shot 2023-11-16 at 14 45 21" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/62937226-a6f1-45a9-9eff-6559da033c74">

Fig. 11 Image of answer of Quiz 019
 ## Running Code:
<img width="1132" alt="Screen Shot 2023-11-01 at 11 03 15" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/af678c3d-daca-4614-8c4f-0b2e89621819">

 Fig. 12 Image of code running of Quiz 019

 ## Flowchart:
<img width="561" alt="Screen Shot 2023-11-01 at 11 06 00" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/179bbac0-8cee-4963-8372-626de99e9f8c">

 Fig. 13 Image of flowchart of Quiz 019

# Quiz020:
 ## Question:
<img width="1076" alt="Screen Shot 2023-11-16 at 12 51 04" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/a0fbdc78-45bf-4ac4-9186-154d4a2a302a">

 Fig. 14 Image of question of Quiz 020
 ## Answer a:
 ```.py
 def produce(n=int, m=int, s=int):
    print("|x|y(x)|")
    import random
    random.seed(1234)
    for i in range(n):
        x=random.randint(0,100)
        y=x**(1/2*((m/s)**1/2))
        ans = print(f"|{str(x)}|{str(y)}|\n")
    return ans

sample = produce(n =5, m=3, s=2)
print(sample)
```
## Answer b:
<img width="539" alt="Screen Shot 2023-11-16 at 14 48 12" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/dc5bd2e1-66ab-4f98-b446-02f2b1ca23bb">

Fig. 15 Image of answer of Quiz 020
 ## Running Code:
<img width="234" alt="Screen Shot 2023-11-02 at 9 03 44" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/344d7f7a-7eef-4d50-be76-bf677583b016">

 Fig. 16 Image of code running of Quiz 020

 ## Flowchart:

 Fig. 17 Image of flowchart of Quiz 020

# Quiz021:
 ## Question:
<img width="1076" alt="Screen Shot 2023-11-16 at 12 55 47" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/fabaf78d-c17c-4451-9f0e-cec1ec13fc0e">

 Fig. 18 Image of question of Quiz 021
 ## Answer:
 ```.py
import random

random.seed(1234)
def produce (n:int, m:int, s:int):
    x_out = []
    y_out = []
    for _ in range(n):
        x = random.randint(0,100)
        y = x ** (0.5*((m/s)**2))
        x_out.append(x)
        y_out.append(y)

    return y_out, x_out

import matplotlib.pyplot as plt

plt.style.use('ggplot')

y, x = produce(n=10, m=5, s=2)

plt.plot(x,y, color = "r", marker = "o")
plt.xlabel("x", fontsize = 20)
plt.ylabel("$y=x^{(1/2)(m/s)^2}$", fontsize = 20)
plt.show()
```
<img width="650" alt="Screen Shot 2023-11-16 at 14 53 08" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/d1088150-d5eb-4ab8-aa07-1cb7d3949912">

Fig. 19 Image of answer of Quiz 021

 ## Running Code:
<img width="472" alt="Screen Shot 2023-11-16 at 12 57 15" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/ab8630bc-cd09-442e-a36d-5b181525ed10">

 Fig. 20 Image of code running of Quiz 021

 ## Flowchart:

 Fig. 21 Image of flowchart of Quiz 020

# Quiz022:
 ## Question:
<img width="1082" alt="Screen Shot 2023-11-16 at 12 56 44" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/88f61ea5-67a0-4be2-ae47-93901f97b091">

 Fig. 22 Image of question of Quiz 022
 ## Answer:
 ```.py
import random

random.seed(1234)
def produce ():
    x_out = []
    y_out = []
    x = -10
    for _ in range(100):
        y = 2*((x+5)**2)
        x_out.append(x)
        y_out.append(y)
        x += 0.2

    return y_out, x_out

import matplotlib.pyplot as plt

plt.style.use('ggplot')
y,x =produce()
plt.plot(x,y, color = "r", marker = "o")
plt.xlabel("x", fontsize = 20)
plt.ylabel("$y=2(x+5)^2$", fontsize = 20)
plt.show()
```

## Answer b:
Fig. 23 Image of answer of Quiz 022
 ## Running Code:
<img width="469" alt="Screen Shot 2023-11-16 at 12 56 29" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/5616f065-4bdc-4e86-bd6e-2c1f2e1a78b8">

 Fig. 24 Image of code running of Quiz 022

 ## Flowchart:

 Fig. 25 Image of flowchart of Quiz 022

# Quiz023:
 ## Question:
<img width="1082" alt="Screen Shot 2023-11-16 at 12 56 44" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/88f61ea5-67a0-4be2-ae47-93901f97b091">

 Fig. 26 Image of question of Quiz 023
 ## Answer:
 ```.py
def produce():
    st = -10
    len=10
    x = []
    y = []
    for i in range(101):
        x.append(st)
        y_out = abs(st)
        y.append(y_out)
        st += 0.2
    return x, y

data_x, data_y = produce()
from matplotlib import pyplot as plt
plt.plot(data_x, data_y, color="red", marker= '.')
plt.ylabel("$f(x)=|x|$")
plt.show()
```
 Fig. 27 Image of question of Quiz 023

 ## Running Code:
<img width="469" alt="Screen Shot 2023-11-16 at 12 56 29" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/5616f065-4bdc-4e86-bd6e-2c1f2e1a78b8">

 Fig. 28 Image of code running of Quiz 023

 ## Flowchart:

 Fig. 29 Image of flowchart of Quiz 023
