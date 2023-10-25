# Quiz017:
 ## Question:

 Fig. 1 Image of question of Quiz 017
 ## Answer:
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
 ## Running Code:
 <img width="1179" alt="Screen Shot 2023-10-23 at 8 20 40" src="https://github.com/Yuiko-tsr/unit-1/assets/134657923/8208d60f-bec6-4487-b8de-7af808e9dd0b">

 Fig. 3 Image of code running of Quiz 017

 ## Flowchart:

 Fig. 4 Image of flowchart of Quiz 017

# Quiz018:
 ## Question:

 Fig. 5 Image of question of Quiz 018
 ## Answer:
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

 ## Running Code:
<img width="1106" alt="Screen Shot 2023-10-25 at 10 46 30" src="https://github.com/Yuiko-tsr/unit-2/assets/134657923/6684c2aa-6b1e-4330-9fae-80b63bc345da">

 Fig. 6 Image of code running of Quiz 017

 ## Flowchart:

 Fig. 7 Image of flowchart of Quiz 017
