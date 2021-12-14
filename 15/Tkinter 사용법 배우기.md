# 15. Tkinter 사용법 배우기
## Tkinter 살펴보기
* Tkinter는 버튼 등의 그래픽 기능을 제공해주는 그래픽 유저 인터페이스 모듈입니다.
* Tkinter에서 앞글자 Tk는 GUI(그래픽 유저 인터페이스)를 사용할 수 있는 레이어를 의미합니다.
* 뒷글자 inter는 interface를 의미합니다.

## Tkinter 기초 사용법
* Tkinter 모듈을 가져옵니다.
* Tkinter 객체를 만듭니다.
* Tk객체.mainloop()로 정의된 윈도우를 실행합니다.
```python
import tkinter as tk

window = tk.Tk()
window.mainloop()
```
* Tk객체.title('제목') : 윈도우 창의 제목을 정합니다.
* Tk객체.geometry('가로x세로') : 윈도우 창의 크기를 정합니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("파이썬")
window.geometry("300x300")
window.mainloop()
```
* Tk객체.resizable(False, False)로 창 크기를 변경못하게 설정할 수 있습니다. (X크기, Y크기)순으로 설정합니다.  
* 라벨, 버튼, 입력 등을 위젯을 추가해서 사용합니다.
* 위젯 이름을 대문자로 입력합니다.
* 위젯객체.pack()으로 geometry manager에 등록을 해야 합니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("파이썬")
window.geometry("300x300")
a = tk.Label(window, text="라벨")
a.pack()
b = tk.Button(window, text="버튼")
b.pack()
c = tk.Entry(window)
c.pack()
window.mainloop()
```
* 버튼에서 padx와 pady로 padding 값을 줄 수 있습니다.
```python
b = tk.Button(window, padx=20, pady=20, text="버튼")
```
* 버튼에서 width, height로 크기를 지정할 수 있습니다.
```python
b = tk.Button(window, width=10, heigh=3, text="버튼")
```
