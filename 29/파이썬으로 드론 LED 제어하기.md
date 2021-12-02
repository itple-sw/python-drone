# 29.파이썬으로 드론 LED 제어하기
## LED 계속 색깔 바꾸기
```python
import random
from time import sleep
from e_drone.drone import *
from e_drone.protocol import *

if __name__ == '__main__':
    drone = Drone(True, True, True, True, True)
    drone.open("com3")
    while True:
        drone.sendLightDefaultColor(LightModeDrone.BodyDimming, 1, 255, 0, 0)
        sleep(2)
        drone.sendLightDefaultColor(LightModeDrone.BodyDimming, 1, 0, 255, 0)
        sleep(2)
        drone.sendLightDefaultColor(LightModeDrone.BodyDimming, 1, 0, 0, 255)
        sleep(2)
    drone.close()
```

## LED 색깔 랜덤으로 바꾸기
```python
import random
from time import sleep
from e_drone.drone import *
from e_drone.protocol import *

if __name__ == '__main__':
    drone = Drone(True, True, True, True, True)
    drone.open("com3")
    for i in range(0, 10, 1):
        r = int(random.randint(0, 255))
        g = int(random.randint(0, 255))
        b = int(random.randint(0, 255))
        dataArray = drone.sendLightDefaultColor(LightModeDrone.BodyDimming, 1, r, g, b)
        print(" {0} / {1}".format(i, convertByteArrayToString(dataArray)))
        sleep(2)
    drone.close()
```

* ```convertByteArrayToString```는 특정 함수들은 타입의 포맷이 정해져 있어서 타입의 형을 변환하는 함수를 사용합니다.
