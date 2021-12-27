# 17. Tkinter로 단어퀴즈 게임 만들기
## columnconfigure와 rowconfigure 설정하기
* 레이아웃을 설정할 때 행과 열이 너비와 높이를 설정할 수 있습니다.
* columnconfigure은 너비를 정하고 rowconfigure는 높이를 정합니다. weight에 값을 입력해서 정합니다.
```python
container.columnconfigure(index, weight)
container.rowconfigure(index, weight)
```

```python
import tkinter as tk

window = tk.Tk()
window.title("범위 정하기")
window.geometry("500x500")

window.rowconfigure(0, weight=2)
window.rowconfigure(1, weight=1)
window.columnconfigure(0, weight=2)
window.columnconfigure(1, weight=1)

frame1 = tk.Frame(window, bg="yellow")
frame1.grid(row=0, column=0, sticky="news")
frame2 = tk.Frame(window, bg="red")
frame2.grid(row=0, column=1, sticky="news")
frame3 = tk.Frame(window, bg="blue")
frame3.grid(row=1, column=0, sticky="news")
frame4 = tk.Frame(window, bg="green")
frame4.grid(row=1, column=1, sticky="news")

window.mainloop()
```

* grid에 padx와 pady를 설정할 수 있습니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("범위 정하기")
window.geometry("500x500")

window.rowconfigure(0, weight=2)
window.rowconfigure(1, weight=1)
window.columnconfigure(0, weight=2)
window.columnconfigure(1, weight=1)

frame1 = tk.Frame(window, bg="yellow")
frame1.grid(row=0, column=0, padx=5, pady=5, sticky="news")
frame2 = tk.Frame(window, bg="red")
frame2.grid(row=0, column=1, padx=5, pady=5, sticky="news")
frame3 = tk.Frame(window, bg="blue")
frame3.grid(row=1, column=0, padx=5, pady=5, sticky="news")
frame4 = tk.Frame(window, bg="green")
frame4.grid(row=1, column=1, padx=5, pady=5, sticky="news")

window.mainloop()
```

## 버튼을 클릭해서 Frame 바꾸기
* pack()과 grid()를 같이 쓸 수 없습니다.
* ```tkraise()```를 사용해서 Frame을 바꿀 수 있습니다.
* 위에 버튼 3개가 있습니다.
* grid()에 같은 좌표를 입력해서 겹치게 합니다. 
```python
import tkinter as tk

window = tk.Tk()
window.title("범위 정하기")
window.geometry("500x500")

window.rowconfigure(0, weight=1)
window.rowconfigure(1, weight=4)
window.columnconfigure(0, weight=1)
    
frame_button = tk.Frame(window)
frame_button.grid(row=0, column=0, sticky="news")
button1 = tk.Button(frame_button, text="frame1")
button1.pack(side="left", padx=5)
button2 = tk.Button(frame_button, text="frame2")
button2.pack(side="left", padx=5)
button3 = tk.Button(frame_button, text="frame3")
button3.pack(side="left", padx=5)

frame1 = tk.Frame(window, bg="yellow")
frame1.grid(row=1, column=0, sticky="news")
frame2 = tk.Frame(window, bg="red")
frame2.grid(row=1, column=0, sticky="news")
frame3 = tk.Frame(window, bg="blue")
frame3.grid(row=1, column=0, sticky="news")

window.mainloop()
```

* 람다함수를 사용해서 코딩을 합니다.
* 클릭을 하면 tkraise()를 실행합니다. 
```python
import tkinter as tk

window = tk.Tk()
window.title("범위 정하기")
window.geometry("500x500")

window.rowconfigure(0, weight=1)
window.rowconfigure(1, weight=4)
window.columnconfigure(0, weight=1)

def open_frame(frame):
    frame.tkraise()
    
frame_button = tk.Frame(window)
frame_button.grid(row=0, column=0, sticky="news")
button1 = tk.Button(frame_button, text="frame1", command=lambda:open_frame(frame1))
button1.pack(side="left", padx=5)
button2 = tk.Button(frame_button, text="frame2", command=lambda:open_frame(frame2))
button2.pack(side="left", padx=5)
button3 = tk.Button(frame_button, text="frame3", command=lambda:open_frame(frame3))
button3.pack(side="left", padx=5)

frame1 = tk.Frame(window, bg="yellow")
frame1.grid(row=1, column=0, sticky="news")
frame2 = tk.Frame(window, bg="red")
frame2.grid(row=1, column=0, sticky="news")
frame3 = tk.Frame(window, bg="blue")
frame3.grid(row=1, column=0, sticky="news")

window.mainloop()
```

## 기본적인 레이아웃을 만들기
```python
import tkinter as tk
from tkinter import filedialog

window = tk.Tk()
window.title("단어 공부하기")

window.rowconfigure(0, weight=1)
window.rowconfigure(1, weight=4)
window.columnconfigure(0, weight=1)

frame_button = tk.Frame(window)
frame_button.grid(row=0, column=0, sticky="news")

button_write = tk.Button(frame_button, text="단어 입력하기")
button_write.pack(side="left", padx=5)
button_quiz = tk.Button(frame_button, text="단어 공부하기")
button_quiz.pack(side="left", padx=5)

frame_write = tk.Frame(window)
frame_write.grid(row=1, column=0, sticky="news")

add_button = tk.Button(frame_write, text="파일추가")
add_button.pack()
file_label = tk.Label(frame_write, text="파일 없음")
file_label.pack()

title_label = tk.Label(frame_write, text="단어를 입력하세요")
title_label.pack(fill="x")

word_frame = tk.Frame(frame_write)
word_frame.pack(fill="x")
word_label = tk.Label(word_frame, text="영어단어", width=10)
word_label.pack(side="left")
word_entry = tk.Entry(word_frame)
word_entry.pack(side="left", fill="x", expand=True, padx=10, pady=5)

meaning_frame = tk.Frame(frame_write)
meaning_frame.pack(fill="x")
meaning_label = tk.Label(meaning_frame, text="뜻", width=10)
meaning_label.pack(side="left")
meaning_entry = tk.Entry(meaning_frame)
meaning_entry.pack(side="left", fill="x", expand=True, padx=10, pady=5)

button_save = tk.Button(frame_write, text="저장하기")
button_save.pack()

window.mainloop()
```

## 파일을 찾아서 경로를 표시하기
* 파일을 사용하기 위해서 filedialog를 사용합니다.
* txt 파일을 열 수 있도록 합니다.
```python
def add_file():
    file = filedialog.askopenfilename(title="파일을 선택하세요", filetypes=(("txt files","*.txt"),("all files","*.*")))
    print(file)

add_button = tk.Button(frame_write, text="파일추가", command=add_file)
```
* 파일의 경로를 label에 표시해줍니다.
```python
 file_label.config(text=file)
```

## 영어단어와 뜻을 입력해서 txt 파일로 저장하기
* 저장하기 버튼을 클릭하면 txt 파일에 영어 단어와 뜻을 저장합니다.
* Label의 글자는 ```cget("text")```으로 읽어서 사용할 수 있습니다.
* Entry 글자는 ```.get())```으로 읽어서 사용할 수 있습니다.
```python
def save_file():   
    with open(file_label.cget("text"), "a") as f:        
        f.write(word_entry.get())
        f.write(":")
        f.write(meaning_entry.get())
        f.write("\n")
        
button_save = tk.Button(frame_write, text="저장하기", command=save_file)      
```

* 파일경로가 있으면 저장을 합니다.
* try와 except를 사용합니다.
```python
def save_file():
    try:
        with open(file_label.cget("text"), "a") as f:        
            f.write(word_entry.get())
            f.write(":")
            f.write(meaning_entry.get())
            f.write("\n")
    except:
        print("파일 경로를 추가하세요")
```

## 게임 관련 Frame 만들기
```python
frame_game= tk.Frame(window)
frame_game.grid(row=1, column=0, sticky="news")
```
* 버튼을 클릭하면 Frame이 바뀌도록 합니다.
* frame_game에 단어와 관련된 게임을 만듭니다.
```python
def open_frame(frame):
    frame.tkraise()
    
button_write = tk.Button(frame_button, text="단어 입력하기", command=lambda:open_frame(frame_write))
button_write.pack(side="left", padx=5)
button_quiz = tk.Button(frame_button, text="단어 공부하기", command=lambda:open_frame(frame_game))
button_quiz.pack(side="left", padx=5)
```
