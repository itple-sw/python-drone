# 17. Tkinter로 행맨 게임 만들기
## 행맨 게임 만들기
```python
#람다함수는 익명함수(이름이 없는 함수)입니다.
#파이썬에서 람다함수를 사용해서 간단하게 함수를 만들어서 사용할 수 있습니다.
#(lambda x : x+1)(3)
#func = lambda x : x + 1
#func(4)
#(lambda x,y: x + y)(10, 20)
#list(map(lambda x: x ** 2, range(5)))
#변수값이 바뀔 때 화면에 즉시 바뀌기 원하는 경우 tk.StringVar()를 사용한다. set으로 값을 지정한다.
#

import tkinter as tk
import os
# 대문자 하려고
from string import ascii_uppercase

os.chdir(r"C:\file")
pictures = os.listdir("img")
window = tk.Tk()
photos = []
for i in range(len(pictures)):
    photos.append(tk.PhotoImage(file=r"img/hang"+str(i)+".png"))
print(photos)

word_list = ["russia", "morocco"]

imgLabel = tk.Label(window)
imgLabel.grid(row=0, column=0, columnspan=3, padx=10, pady=40)
imgLabel.config(image=photos[0])

lblWord = tk.StringVar()
lblWord.set("------")
tk.Label(window, textvariable=lblWord, font=("Consolas 24 bold")).grid(row=0, column=3, columnspan=6, padx=10, pady=40)
def guess(c):
    print(c)
    lblWord.set("-")
    print(lblWord.get())
def newGame():
    pass    
#버튼을 만들기
n = 0
for c in ascii_uppercase:
    tk.Button(window, text=c, command=lambda c=c : guess(c), width=4, font=("Helvetica 18")).grid(row=1+n//8, column=n%8)
    n+=1
    
newGame()
window.mainloop()
```
