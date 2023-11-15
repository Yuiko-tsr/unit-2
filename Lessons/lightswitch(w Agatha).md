'''.py
import pyfirmata
from pyfirmata import Arduino

import time

board = Arduino('/dev/cu.usbserial-110')
print("Success, Connected to Arduino")

data = pyfirmata.util.Iterator(board)
data.start()

LED_13= board.digital[13]
LED_13.mode = pyfirmata.OUTPUT
LED_13.write(0)

LED_10= board.digital[10]
LED_10.mode = pyfirmata.OUTPUT
LED_10.write(0)

LED_8= board.digital[8]
LED_8.mode = pyfirmata.OUTPUT
LED_8.write(0)

t=100
while t>0:
    LED_13.write(1)
    LED_10.write(0)
    LED_8.write(1)
    time.sleep(0.5)
    LED_13.write(0)
    LED_10.write(1)
    LED_8.write(0)
    time.sleep(0.5)


exit()
'''
