# Quiz033
## Question

**Fig 1** Image of the Question 033
## Answer
```.py
import matplotlib.pyplot as plt
import numpy as np

plt.style.use('ggplot')
x1 = [-2,-1.8,-1.6,-1.4,-1.2,-1.0,-0.8,-0.6,-0.4,-0.2,0,0.2,0.4,0.6,0.8,1.0,1.2,1.4,1.6,1.8,2.0]
y1 = [4,3.24,2.56,1.96,1.44,1, 0.64,0.36,0.16,0.04,0,0.04,0.16,0.36,0.64,1,1.44,1.96,2.56,3.24,4]
x2 = [4,3.24,2.56,1.96,1.44,1, 0.64,0.36,0.16,0.04,0,0.04,0.16,0.36,0.64,1,1.44,1.96,2.56,3.24,4]
y2 = [-2,-1.8,-1.6,-1.4,-1.2,-1.0,-0.8,-0.6,-0.4,-0.2,0,0.2,0.4,0.6,0.8,1.0,1.2,1.4,1.6,1.8,2.0]
x3 = [-4,-3.24,-2.56,-1.96,-1.44,-1, -0.64,-0.36,-0.16,-0.04,-0,-0.04,-0.16,-0.36,-0.64,-1,-1.44,-1.96,-2.56,-3.24,-4]
y3 = [-2,-1.8,-1.6,-1.4,-1.2,-1.0,-0.8,-0.6,-0.4,-0.2,0,0.2,0.4,0.6,0.8,1.0,1.2,1.4,1.6,1.8,2.0]
x4 = [-2,-1.8,-1.6,-1.4,-1.2,-1.0,-0.8,-0.6,-0.4,-0.2,0,0.2,0.4,0.6,0.8,1.0,1.2,1.4,1.6,1.8,2.0]
y4 = [-4,-3.24,-2.56,-1.96,-1.44,-1, -0.64,-0.36,-0.16,-0.04,-0,-0.04,-0.16,-0.36,-0.64,-1,-1.44,-1.96,-2.56,-3.24,-4]



plt.plot(x1, y1, label='y=x^2', color='red')
plt.plot(x2, y2, label='y=-x^2', color='purple')
plt.plot(x3, y3, label='x=-y^2', color='black')
plt.plot(x4, y4, label='x=y^2', color='blue')


# Set labels and title
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Four Parabolas Aligned with Axes")
plt.legend()
plt.show()

```

## Proof of Code
<img width="643" alt="Screen Shot 2023-12-04 at 8 29 15" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/c1a5f210-2407-4b98-8ab6-551ee36925f3">

**Fig. 2** Image of code running

# Quiz034
## Question

**Fig 3** Image of the Question 034
## Answer
```.py
import xmlrpc.server

import matplotlib.pyplot as plt
plt.style.use("dark_background")

# x1=-2
# for i in range (-2,2,1):
#     x1+=0.2
#     y1=x1**2
# plt.plot(x1, y1, color = "red")
# plt.title("Four Parabolas Aligned with axes")
# plt.xlabel('X-axis')
# plt.ylabel('Y-axis')
temp=0
x1=[]
y1=[]
for _ in range (150):
    x1.append(temp)
    y1.append((temp-2)**2)
    temp+=0.04
plt.plot(x1, y1, color = "blue")
plt.title("Four Funny Parabolas")
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.xlim([-15,15])

temp =-6
x2=[]
y2=[]
for _ in range (150):
    x2.append(temp)
    y2.append((temp + 2) ** 2)
    temp+=0.04
plt.plot(x2,y2, color = "red")
plt.title("Four Funny Parabolas")
plt.xlabel('X-axis')
plt.ylabel('Y-axis')


temp=-6
x3=[]
y3=[]
for _ in range (150):
    x3.append(temp)
    y3.append(-(temp + 2) ** 2)
    temp+=0.04
plt.plot(x3, y3, color = "purple")
plt.title("Four Funny Parabolas")
plt.xlabel('X-axis')
plt.ylabel('Y-axis')

temp=0
x4=[]
y4=[]
for _ in range (150):
    x4.append(temp)
    y4.append(-(temp - 2) ** 2)
    temp+=0.04
plt.plot(x4, y4, color = "white")
plt.title("Four Funny Parabolas")
plt.xlabel('X-axis')
plt.ylabel('Y-axis')

#
# x3=0
# for i in range (0,4,1):
#     x3+=0.2
#     y3=x3//2
# plt.plot(x3, y3, color = "purple")
# plt.title("Four Parabolas Aligned with axes")
# plt.xlabel('X-axis')
# plt.ylabel('Y-axis')
#
# x4=0
# for i in range (-4,0,1):
#     x4+=0.2
#     y4 = -x4 // 2
# plt.plot(x4, y4, color = "black")
# plt.title("Four Parabolas Aligned with axes")
# plt.xlabel('X-axis')
# plt.ylabel('Y-axis')



plt.xlabel('X-axis')
plt.ylabel('Y-axis')

plt.show()

```

## Proof of Code
<img width="607" alt="Screen Shot 2023-12-13 at 11 10 18" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/a28e1b12-378b-4c5c-bd61-308b592d07c2">

**Fig. 4** Image of code running


# Quiz035
## Question

**Fig 5** Image of the Question 035
## Answer
```.py
import xmlrpc.server

import matplotlib.pyplot as plt
plt.style.use("dark_background")

# x1=-2
# for i in range (-2,2,1):
#     x1+=0.2
#     y1=x1**2
# plt.plot(x1, y1, color = "red")
# plt.title("Four Parabolas Aligned with axes")
# plt.xlabel('X-axis')
# plt.ylabel('Y-axis')
temp=-1.0
x1=[]
y1=[]
for _ in range (100):
    x1.append(temp)
    y1.append(-1*((temp)**2)+2)
    temp+=0.04
x2=[-1.00,-0.75,-0.50,-0.25,0.00]
y2=[1.0,0.5,0.0,-0.5,-1.0]
x3=[0.00,0.25,0.50,0.75,1.00]
y3=[-1.0,-0.5,0.0,0.5,1.0]
plt.plot(x1, y1, color = "green",label="parabola")
plt.plot(x2,y2,color="red", label="left line")
plt.plot(x3,y3,color="blue",label="right line")
plt.title("Cone Shape Graph with Parabolas and Lines")
plt.xlabel('X-axis')
plt.ylabel('Y-axis')

plt.xlim([-1.00,1.00])
plt.ylim([-1.2,2.2])
plt.legend()
plt.show()
```

## Proof of Code
<img width="614" alt="Screen Shot 2023-12-13 at 11 09 54" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/d1b697ce-f5e1-4158-b5da-b04f9aa00560">

**Fig. 6** Image of code running



