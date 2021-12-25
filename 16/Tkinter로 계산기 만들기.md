# 16. Tkinter로 계산기 만들기
## 계산기 레이아웃 만들기
![image](https://user-images.githubusercontent.com/76088532/145950261-96760e52-9371-408a-b8ec-3377f1da5504.png)
* 5행 5열로 grid 레이아웃을 만듭니다.
* %를 /로 바꿔서 나눗셈 계산을 할 수 있도록 합니다.
* ```button_1 = tk.Button(window, text="7")```과 ```button_1.grid(row=1, column=0)```를 합쳐서 ```button_1 = tk.Button(window, text="7").grid(row=1, column=0)```로 코딩할 수 있습니다.
```python
import tkinter as tk

window = tk.Tk()
window.title("계산기")

label_result = tk.Label(window, text="0")
label_result.grid(row=0, column=0, columnspan=5)
button_1 = tk.Button(window, text="7").grid(row=1, column=0)
button_2 = tk.Button(window, text="8").grid(row=1, column=1)
button_3 = tk.Button(window, text="9").grid(row=1, column=2)
button_4 = tk.Button(window, text="/").grid(row=1, column=3)
button_5 = tk.Button(window, text="4").grid(row=2, column=0)
button_6 = tk.Button(window, text="5").grid(row=2, column=1)
button_7 = tk.Button(window, text="6").grid(row=2, column=2)
button_8 = tk.Button(window, text="X").grid(row=2, column=3)
button_9 = tk.Button(window, text="1").grid(row=3, column=0)
button_10 = tk.Button(window, text="2").grid(row=3, column=1)
button_11 = tk.Button(window, text="3").grid(row=3, column=2)
button_12 = tk.Button(window, text="-").grid(row=3, column=3)
button_13 = tk.Button(window, text="000").grid(row=4, column=0)
button_14 = tk.Button(window, text="0").grid(row=4, column=1)
button_15 = tk.Button(window, text=".").grid(row=4, column=2)
button_16 = tk.Button(window, text="+").grid(row=4, column=3)

window.mainloop()
```
