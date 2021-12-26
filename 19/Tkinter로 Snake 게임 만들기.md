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

def change_direction():
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

## 뱀과 먹이 만들기
* ```canvas.create_rectangle(x1,y1,x2,y2,fill="색깔")```로 사각형을 그립니다.
* Canvas에 뱀과 먹이 사각형을 그려서 게임을 만듭니다.
```python
canvas.create_rectangle(30,30,60,60,fill="red")
```

* 뱀과 먹이 클래스를 만듭니다.
* 뱀 클래스에 자신의 좌표와 그린 사각형을 저장하는 리스트를 만듭니다.
* 먹이 클래스에 랜덤한 곳에 먹이 사각형을 그리도록 합니다.
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
        x = random.randint(0, (game_width/tile_size)-1) * tile_size
        y = random.randint(0, (game_height/tile_size)-1) * tile_size
        self.coordinates = [x,y]
        canvas.create_rectangle(x, y, x + tile_size, y + tile_size, fill=food_color, tag="food")

snake = Snake()
food = Food()
```
* next_turn 함수를 만듭니다.
* 방향에 따라서 뱀 머리의 좌표를 다르게 합니다.
* 새로운 좌표를 insert로 추가합니다.
* 인덱스 0은 뱀 머리 좌표를 나타냅니다.
* 그리고 꼬리는 지웁니다.
* window.after로 speed 시간마다 next_turn 함수를 호출합니다.
```python
def next_turn(snake, food):
    x, y = snake.coordinates[0]
    if direction == "up":
        y -= tile_size
    elif direction == "down":
        y += tile_size
    elif direction == "right":
        x += tile_size
    elif direction == "left":
        x -= tile_size
        
    snake.coordinates.insert(0,(x,y))
    square = canvas.create_rectangle(x, y, x + tile_size, y + tile_size, fill=snake_color, tag="snake")
    snake.squares.insert(0, square)
    del snake.coordinates[-1]
    canvas.delete(snake.squares[-1])
    del snake.squares[-1]
    window.after(speed, next_turn, snake, food)

snake = Snake()
food = Food()
next_turn(snake, food)
```

* ```window.bind```로 키 입력을 받습니다.
```python
window.bind('<Left>', lambda event : print("left"))
```    
    
* 화살표 키를 누르면 방향이 바뀌도록 코딩을 합니다.
```python
def change_direction(new_direction):
    global direction
    if new_direction == "left":
        if direction != "right":
            direction = new_direction
    elif new_direction == "right":
        if direction != "left":
            direction = new_direction
    elif new_direction == "up":
        if direction != "down":
            direction = new_direction
    elif new_direction == "down":
        if direction != "up":
            direction = new_direction        

window.bind('<Left>', lambda event : change_direction("left"))
window.bind('<Right>', lambda event : change_direction("right"))
window.bind('<Up>', lambda event : change_direction("up"))
window.bind('<Down>', lambda event : change_direction("down"))
```

* 먹이를 먹으면 뱀이 점점 커지도록 합니다.
* 뱀 머리 좌표와 먹이 좌표가 같으면 먹이를 먹은 것입니다. 
* 뱀 좌표에 새로운 좌표를 추가합니다.
* 먹이를 태그를 사용해서 지웁니다.
* 먹이를 먹으면 점수를 더해줍니다.
```python
snake.squares.insert(0, square)
if x == food.coordinates[0] and y == food.coordinates[1]:
    global score
    score += 1
    label.config(text="Score:{0}".format(score))
    canvas.delete("food")
    food = Food()
else:
    del snake.coordinates[-1]
    canvas.delete(snake.squares[-1])
    del snake.squares[-1]
window.after(speed, next_turn, snake, food)
```

* 뱀이 자신이나 벽에 닿았는지 확인하는 함수를 만듭니다.
* 닿았다면 게임이 끝나도록 코딩을 합니다.
* ```snake.coordinates[1:]```는 머리를 빼고 몸통을 말합니다.
* ```canvas.create_text```로 글자를 나타냅니다.
```python
def check_collisions(snake):
    x, y = snake.coordinates[0]
    if x < 0 or x >= game_width:
        return True
    if y < 0 or y > game_height:
        return True
    for body_part in snake.coordinates[1:]:
        if x == body_part[0] and y == body_part[1]:
            return True
        
def game_over():
    canvas.delete("snake")
    canvas.delete("food")
    canvas.create_text(canvas.winfo_width()/2, canvas.winfo_height()/2,
                       font=("aria", 70), text="GAME OVER", fill="red", tag="gameover")

def next_turn(snake, food):
    x, y = snake.coordinates[0]
    if direction == "up":
        y -= tile_size
    elif direction == "down":
        y += tile_size
    elif direction == "right":
        x += tile_size
    elif direction == "left":
        x -= tile_size
        
    snake.coordinates.insert(0,(x,y))
    square = canvas.create_rectangle(x, y, x + tile_size, y + tile_size, fill=snake_color, tag="snake")
    snake.squares.insert(0, square)
    if x == food.coordinates[0] and y == food.coordinates[1]:
        global score
        score += 1
        label.config(text="Score:{0}".format(score))
        canvas.delete("food")
        food = Food()
    else:
        del snake.coordinates[-1]
        canvas.delete(snake.squares[-1])
        del snake.squares[-1]
    if check_collisions(snake):
        game_over()
    else:
        window.after(speed, next_turn, snake, food)
```     
        


