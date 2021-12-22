# 16. Tkinter로 단어퀴즈 게임 만들기
## columnconfigure와 rowconfigure 설정하기
* 레이아웃을 설정할 때 행과 열이 너비를 설정할 수 있습니다.
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
## 버튼을 클릭해서 Frame 바꾸기
* columnconfigure와 rowconfigure 설정했다면 pack()과 grid()를 같이 쓸 수 없습니다.
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

## 영어단어와 뜻을 입력해서 txt 파일로 저장하기


##
