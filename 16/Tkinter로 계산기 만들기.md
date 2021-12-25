# 16. Tkinter로 계산기 만들기
## 계산기 레이아웃 만들기
![image](https://user-images.githubusercontent.com/76088532/145950261-96760e52-9371-408a-b8ec-3377f1da5504.png)
* 5행 5열로 grid 레이아웃을 만듭니다.
* %를 /로 바꿔서 나눗셈 계산을 할 수 있도록 합니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("계산기")

label_result = tk.Label(window, text="0")
label_result.grid(row=0, column=0, columnspan=5)
button_1 = tk.Button(window, text="7")
button_1.grid(row=1, column=0)
button_2 = tk.Button(window, text="8")
button_2.grid(row=1, column=1)
button_3 = tk.Button(window, text="9")
button_3.grid(row=1, column=2)
button_4 = tk.Button(window, text="/")
button_4.grid(row=1, column=3)
button_5 = tk.Button(window, text="4")
button_5.grid(row=2, column=0)
button_6 = tk.Button(window, text="5")
button_6.grid(row=2, column=1)
button_7 = tk.Button(window, text="6")
button_7.grid(row=2, column=2)
button_8 = tk.Button(window, text="X")
button_8.grid(row=2, column=3)
button_9 = tk.Button(window, text="1")
button_9.grid(row=3, column=0)
button_10 = tk.Button(window, text="2")
button_10.grid(row=3, column=1)
button_11 = tk.Button(window, text="3")
button_11.grid(row=3, column=2)
button_12 = tk.Button(window, text="-")
button_12.grid(row=3, column=3)
button_13 = tk.Button(window, text="000")
button_13.grid(row=4, column=0)
button_14 = tk.Button(window, text="0")
button_14.grid(row=4, column=1)
button_15 = tk.Button(window, text=".")
button_15.grid(row=4, column=2)
button_16 = tk.Button(window, text="+")
button_16.grid(row=4, column=3)
button_result = tk.Button(window, text="=")
button_result.grid(row=1, column=4, rowspan=2)
button_clear=tk.Button(window, text="C")
button_clear.grid(row=3, column=4, rowspan=2)

window.mainloop()
```

* sticky로 버튼의 크기를 키웁니다.
* 위젯을 리스트에 저장해서 for문을 사용해서 코딩하면 편리합니다.
```python
buttons = [button_1, button_2, button_3, button_4, button_5, button_6, button_7, button_8, button_9, button_10, button_11, button_12, button_13, button_14, button_15, button_16, button_result, button_clear]
for button in buttons:
    button.grid(sticky="news")
```

* 폰트를 설정할 수 있습니다.
* family에 폰트를 정하고 size에 크기를 정합니다. 
* ```위젯.config(font=font옵션)```으로 폰트를 정할 수 있습니다.
```python
import tkinter.font

font=tkinter.font.Font(family="맑은 고딕", size=20)

for button in buttons:
    button.config(font=font)
```

* width, height, padx, pady 등을 설정합니다.
```python
for button in buttons:
    button.grid(sticky="news", padx=5, pady=5)
    button.config(font=font, width=5, height=2)
   

label_result.config(font=font, width=5, height=2)
```


