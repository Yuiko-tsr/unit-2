## Code
```.py
def fromdecimal(num,base):
    result=" "
    while num > base:
        result = str(num%base)+result
        num = num//base

    if num in range(10,16):
        if num == 10: num = "A"
        if num == 11: num = "B"
        if num == 12: num = "C"
        if num == 13: num = "D"
        if num == 14: num = "E"
        if num == 15: num = "F"

    result = str(num)+result
    return result

out = fromdecimal(162,16)
print(out)
```

## Results
<img width="375" alt="Screen Shot 2023-11-02 at 9 08 48" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/3530ee85-fda8-4c4c-9817-24962aab9f1c">
Fig. 1 Image of Code running
