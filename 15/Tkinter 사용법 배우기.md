# 15. Tkinter 사용법 배우기
## Tkinter 살펴보기
* Tkinter는 버튼 등의 그래픽 기능을 제공해주는 그래픽 유저 인터페이스 모듈입니다.
* Tkinter에서 앞글자 Tk는 GUI(그래픽 유저 인터페이스)를 사용할 수 있는 레이어를 의미합니다.
* 뒷글자 inter는 interface를 의미합니다.

## Tkinter 기초 사용법
* Tkinter 모듈을 가져옵니다.
* Tkinter 객체를 만듭니다.
* mainloop()로 정의된 윈도우를 실행합니다.
```python
import tkinter as tk

window = tk.Tk()
window.mainloop()
```
* title('제목') : 윈도우 창의 제목을 정합니다.
* geometry('가로x세로') : 윈도우 창의 크기를 정합니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("파이썬")
window.geometry("900x600")
window.mainloop()
```

