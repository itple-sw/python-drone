# 20. turtle 사용법 배우기
## turtle 사용법
* ```import turtle as t```로 모듈을 가져옵니다.
* turtle을 t로 줄여서 사용하면 좋습니다.
* t.Turtle() : turtle 객체를 만듭니다.
* t.bgcolor("색깔") : 배경 색깔을 정합니다.
* t.color("색깔") : 펜색깔을 정합니다.
* t.speed(숫자) : 펜이 움직이는 속도를 정합니다.
* t.penup() : 펜을 들어서 그리는 것을 멈춥니다.
* t.pendown() : 펜을 내려서 그립니다.
* t.forward(숫자) : 입력한 숫자만큼 앞으로 갑니다.
* t.left(숫자) : 입력한 숫자만큼 왼쪽으로 회전합니다.
* t.right(숫자) : 입력한 숫자만큼 오른쪽으로 회전합니다.
* t.circle(숫자) : 입력한 숫자크기로 원을 그립니다.
* t.goto(x좌표, y좌표) : 입력한 좌표로 이동합니다.

## 4각형 그리기
![image](https://user-images.githubusercontent.com/76088532/145509000-cf8f7e68-9bbd-4733-8976-3214dd153e85.png)
* 반복문을 사용해서 코딩할 수 있습니다.
```python
import turtle as t

t.Turtle()
t.bgcolor("black")
t.color("yellow")
t.speed(50)

for i in range(4):
    t.forward(100)
    t.left(90)
```

## n각형 그리기
* 360/각의 수만큼 회전합니다.
```python
for i in range(angle):
    t.forward(length)
    t.left(360/angle)
```    
* n각형을 연속해서 그립니다.
* 이중 for문을 사용합니다.

![image](https://user-images.githubusercontent.com/76088532/145509610-e7630b87-2be6-42ee-86fa-86fd74806144.png)

## 여러 모양의 그림 그리기

![image](https://user-images.githubusercontent.com/76088532/145509713-dcf86009-3d9e-4624-a629-a30221fd0b49.png)

![image](https://user-images.githubusercontent.com/76088532/145509782-39a529be-b7ce-4ecc-a998-a5a94f674347.png)
