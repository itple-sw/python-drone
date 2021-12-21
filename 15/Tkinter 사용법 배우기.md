# 15. Tkinter 사용법 배우기
## Tkinter 살펴보기
* Tkinter는 버튼 등의 그래픽 기능을 제공해주는 그래픽 유저 인터페이스 모듈입니다.
* Tkinter에서 앞글자 Tk는 GUI(그래픽 유저 인터페이스)를 사용할 수 있는 레이어를 의미합니다.
* 뒷글자 inter는 interface를 의미합니다.

## Tkinter 기초 사용법
### 기초 위젯 
* Tkinter 모듈을 가져옵니다.
* Tkinter 객체를 만듭니다.
* ```mainloop()```로 정의된 윈도우를 실행합니다.
```python
import tkinter as tk

window = tk.Tk()
window.mainloop()
```
* ```title('제목')``` : 윈도우 창의 제목을 정합니다.
* ```geometry('가로x세로')``` : 윈도우 창의 크기를 정합니다.
* ```geometry('가로x세로+x좌표+y좌표')``` : 창의 나오는 좌표를 정합니다. 왼쪽 위를 기준으로 좌푯값을 정합니다. 
```python
import tkinter as tk

window = tk.Tk()
window.title("파이썬")
window.geometry("300x300")
window.mainloop()
```
* ```resizable(False, False)```로 창 크기를 변경못하게 설정할 수 있습니다. (X크기, Y크기)순으로 설정합니다.  
* 레이블, 버튼, 입력 등을 위젯을 추가해서 사용합니다.
* 위젯 이름을 대문자로 입력합니다.
* ```pack()```으로 geometry manager에 등록을 해야 보입니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("파이썬")
window.geometry("300x300")
label = tk.Label(window, text="라벨")
label.pack()
button = tk.Button(window, text="버튼")
button.pack()
entry = tk.Entry(window)
entry.pack()
window.mainloop()
```

* padx와 pady로 padding 값을 줄 수 있습니다.
```python
button = tk.Button(window, padx=20, pady=20, text="버튼")
```

* 버튼에서 width, height로 크기를 지정할 수 있습니다.
```python
button = tk.Button(window, width=10, heigh=3, text="버튼")
```

* 버튼에서 fg로 글자색을, bg로 배경색을 정합니다.
```python
button = tk.Button(window, fg="red", bg="yellow", text="버튼")
```

* 버튼에 사진을 추가할 수 있습니다. 
* ```tk.PhotoImage(file="경로")```로 이미지를 가져옵니다. 그리고 image옵션에 이미지 객체를 입력합니다.
```python
img = tk.PhotoImage(file="img.png")
button = tk.Button(window, image=img)
```

* 버튼을 클릭했을 때 실행할 함수를 command에 정합니다.
* 함수이름을 따옴표 없이 입력합니다.
```python
def click_button():
    print("버튼을 클릭했습니다")

button = tk.Button(window, text="버튼", command=click_button)
```

* ```config```를 사용해서 위젯의 속성 값을 바꿀 수 있습니다.
``` python
def click_button():
    button.config(text="클릭했습니다")
    
button = tk.Button(window, text="버튼", command=click_button)
```
* 글자를 입력하는 텍스트 위젯을 만들 수 있습니다.
* 엔트리 위젯은 한 줄로만 입력할 수 있고, 텍스트 위젯은 여러 줄로 입력할 수 있습니다.  
* Text로 만듭니다.
* width와 height로 크기를 정합니다.
* ```텍스트객체.insert(tk.END, "글자")```로 텍스트 위젯에 표시할 글자를 나타낼 수 있습니다.
* ```엔트리객체.insert(0, "글자")```로 엔트리 위젯에 표시할 글자를 나타낼 수 있습니다.
``` python
text = tk.Text(window, width=100, height=3)
text.insert(tk.END, "글자를 입력하세요")
text.pack()
```
* ```텍스트객체.get("1.0", tk.END)```로 텍스트 위젯에 있는 첫문장부터 끝까지 글자를 가져옵니다.
* ```엔트리객체.get()```으로 엔트리 위젯에 잇는 문장을 가져옵니다.
* ```텍스트객체.delete("1.0", tk.END)```로 텍스트 위젯에 있는 글자를 지웁니다.
* ```엔트리객체.delete(0, tk.END)```로 엔트리 위젯에 있는 글자를 지웁니다.
``` python
def click_button():
    label.config(text=text.get("1.0", tk.END))

text = tk.Text(window, width=50, height=3)
text.insert(tk.END, "글자를 입력하세요")
text.pack()

button = tk.Button(window, text="버튼", command=click_button)    
button.pack()

label = tk.Label(window, text="입력한 내용")
label.pack()
```

* 메시지창을 사용할 수 있습니다.
* ```import tkinter.messagebox as msgbox```로 가져옵니다.
* ```msgbox.showinfo("창제목", "메시지")```로 메시지창을 보여줍니다. 
```python
import tkinter.messagebox as msgbox

def click_button():
    msgbox.showinfo("알림", "버튼을 클릭했습니다.")
```

* 프레임을 사용해서 레이아웃을 정할 수 있습니다.
* 프레임에 여러 위젯을 넣어서 사용할 수 있습니다. 
* ```Tk객체.Frame(window, 옵션)```으로 사용합니다.
* ```relief="solid", bd=값```으로 테두리를 정합니다.
* 위젯을 만들 때 넣고 싶은 frame 객체를 정합니다.
```python
frame1 = tk.Frame(window, relief="solid", bd=1, padx=5, pady=5)
frame1.pack()
button1 = tk.Button(frame1, text="frame1")
button1.pack()
button2 = tk.Button(frame1, text="frame1")
button2.pack()
button3 = tk.Button(frame1, text="frame1")
button3.pack()

frame2 = tk.Frame(window, relief="solid", bd=1, padx=5, pady=5)
frame2.pack()
button4 = tk.Button(frame2, text="frame2")
button4.pack()
button5 = tk.Button(frame2, text="frame2")
button5.pack()
button6 = tk.Button(frame2, text="frame2")
button6.pack()
```
* pack() 옵션에 padx, pady를 설정할 수 있습니다.
* 위젯 중에 pack() 옵션에 padx, pady를 설정해야 되는 것이 있습니다.
 

### pack에 옵션 사용하기
* side : 어느 방향에 놓을지 정합니다. left, right, top, buttom과 같이 방향을 입력합니다.
* fill : 어느 방향으로 채울지 정합니다. x, y, both와 같이 입력합니다. ```expand=True```를 입력해서 공간을 채우도록 할 수 있습니다.
```python
frame1 = tk.Frame(window, relief="solid", bd=1, padx=5, pady=5)
frame1.pack(side="left", fill="both", expand=True)

frame2 = tk.Frame(window, relief="solid", bd=1, padx=5, pady=5)
frame2.pack(side="right", fill="both", expand=True)
```

### grid를 사용해서 위젯 배치하기
* ```위젯.grid(row=값, column=값)```로 위젯을 배치합니다.
* 행와 열의 위치를 정합니다. 0부터 시작합니다.
```python
button1 = tk.Button(window, text="1")
button1.grid(row=0, column=0)
button2 = tk.Button(window, text="2")
button2.grid(row=0, column=1)
button2 = tk.Button(window, text="3")
button2.grid(row=0, column=2)
```
* columnspan과 rowspan으로 몇 칸을 차지할지 정할 수 있습니다.
* columnspan는 가로방향, rowspan는 세로방향입니다.
```python
button1 = tk.Button(window, text="1")
button1.grid(row=0, column=0, columnspan=2)
button2 = tk.Button(window, text="2")
button2.grid(row=1, column=0)
button2 = tk.Button(window, text="3")
button2.grid(row=1, column=1)
```
* ```sticky=방향```으로 크기를 늘릴 수 있습니다.
* sticky=tk.N+tk.E+tk.W+tk.S와 같이 +를 사용해서 방향을 추가합니다.
```python
button1.grid(row=0, column=0, columnspan=2, sticky=tk.N+tk.E+tk.W+tk.S)
```

### 계산기 모양 만들기
![image](https://user-images.githubusercontent.com/76088532/145950261-96760e52-9371-408a-b8ec-3377f1da5504.png)
