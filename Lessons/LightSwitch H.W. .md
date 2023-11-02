## Code
```.py
def lightswitch(num):
    result=" "
    while num > 4:
        result = str(num%4)+result
        num = num//4

    result = str(num)+result
    new_result = int(result)
    res = int('{:03d}'.format(new_result))

    hundreds = res//100
    tens = (res-((res//100)*100))//10
    ones = res-((res//10)*10)

    a, b, c, d, e, f, g, h, i = 0, 0, 0, 0, 0, 0, 0, 0, 0

    if hundreds % 4 == 0:
        a, b, c = 0, 0, 0
    elif hundreds % 4 == 1:
        a, b, c = 0, 0, 1
    elif hundreds % 4 == 2:
        a, b, c = 0, 1, 1
    else:
        a, b, c = 1, 1, 1

    if tens % 4 == 0:
        d, e, f = 0, 0, 0
    elif tens % 4 == 1:
        d, e, f = 0, 0, 1
    elif tens % 4 == 2:
        d, e, f = 0, 1, 1
    else:
        d, e, f = 1, 1, 1

    if ones % 4 == 0:
        g, h, i = 0, 0, 0
    elif ones % 4 == 1:
        g, h, i = 0, 0, 1
    elif ones % 4 == 2:
        g, h, i = 0, 1, 1
    else:
        g, h, i = 1, 1, 1

    out = (a, b, c, d, e, f, g, h, i)
    return out

light = lightswitch(15)
print(light)
```

## Code Running
<img width="1124" alt="Screen Shot 2023-11-02 at 9 34 41" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/3556b909-9c0e-4fcf-9125-214881297916">
Fig. 1 Image of Code Running
