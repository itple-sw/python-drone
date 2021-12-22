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
* grid에 


## 영어단어와 뜻을 입력해서 txt 파일로 저장하기


##
