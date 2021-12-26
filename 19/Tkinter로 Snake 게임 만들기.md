# 19. Tkinter로 Snake 게임 만들기
## 게임 기본 설정하기
* 게임에서 사용할 변수, 클래스, 함수를 만듭니다.
```python
import tkinter as tk
import random

game_width = 700
game_height = 700
speed = 50
tile_size = 50
body_parts = 3
snake_color = "green"
food_color = "red"
background_color = "black"
score = 0
direction = "down"

class Snake:
    pass

class Food:
    pass

def next_turn():
    pass

def change_direction(direction):
    pass

def check_collisions():
    pass

def game_over():
    pass
```

## Canvas 만들기
* Label과 Canvas를 만듭니다.
* Canvas에서 뱀이 움직입니다.
```python
window = tk.Tk()
window.title("Snake Game")
window.resizable(False, False)

label = tk.Label(window, text="Score:{0}".format(score), font=("aria", 20))
label.pack()
canvas = tk.Canvas(window, bg=background_color, width=game_width, height=game_height)
canvas.pack()

window.mainloop()
```

* ```window.update()```로 업데이트를 합니다. 
* 컴퓨터 화면 가운데에 창이 나오도록 합니다. 
* winfo_width()와 winfo_height()로 창의 크기를 알 수 있습니다. 
* winfo_screenwidth()와 winfo_screenheight()로 화면의 크기를 알 수 있습니다.
* 화면 가운데 좌표에서 창 너비의 반, 창 높이의 반을 뺀 좌표를 이용해서 window.geometry()를 설정합니다.
* 문자열에 변수를 넣을 때 ```"f"{변수}"```를 사용하면 편리합니다.
```python
window.update()
window_width = window.winfo_width()
window_height = window.winfo_height()
screen_width = window.winfo_screenwidth()
screen_height = window.winfo_screenheight()
x = int((screen_width/2) - (window_width/2))
y = int((screen_height/2) - (window_height/2))
window.geometry(f"{window_width}x{window_height}+{x}+{y}")
```

## 뱀과 먹이 클래스 만들기
* ```canvas.create_rectangle(x1,y1,x2,y2,fill="색깔")```로 사각형을 그립니다.
* Canvas에 뱀과 먹이 사각형을 그려서 게임을 만듭니다.
```python
canvas.create_rectangle(30,30,60,60,fill="red")
```

* 뱀과 먹이 클래스를 만듭니다.
```python
class Snake:
    def __init__(self):
        self.body_size = body_parts
        self.coordinates = []
        self.squares = []
        for i in range(body_parts):
            self.coordinates.append([0,0])
        for x, y in self.coordinates:
            sqaure = canvas.create_rectangle(x, y, x + tile_size, y + tile_size, fill=snake_color, tag="snake")
            self.squares.append(sqaure)

class Food:
    def __init__(self):
        x = random.randint(0, ((game_width/tile_size)-1) * tile_size)
        y = random.randint(0, ((game_height/tile_size)-1) * tile_size)
        self.coordinates = [x,y]
        canvas.create_rectangle(x, y, x + tile_size, y + tile_size, fill=food_color, tag="food")

snake = Snake()
food = Food()
```




