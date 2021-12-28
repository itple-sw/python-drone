# 18. Tkinter로 행맨 게임 만들기
## 행맨 게임 만들기
* 문제리스트를 만듭니다.
* ascii_uppercase를 사용해서 대문자로 버튼을 만듭니다.
```python
import tkinter as tk
import random
from string import ascii_uppercase

word_list = ["apple", "banana", "cat"]

window = tk.Tk()

n = 0
for c in ascii_uppercase:
    tk.Button(window, text=c, width=4, font=("aria", 18)).grid(row=1+n//9, column=n%9)
    n+=1    

window.mainloop()
```

* 행맨 사진이 나오도록 합니다.
* 깃허브에서 사진을 행맨 파이썬 파일과 같은 폴더에 다운로드 받습니다.
* ```tk.PhotoImage```로 사진을 사용합니다.
* ```image``` 옵션에 tk.PhotoImage객체를 넣습니다.
```pyhon
images = [tk.PhotoImage(file="images/hang0.png"),
          tk.PhotoImage(file="images/hang1.png"),
          tk.PhotoImage(file="images/hang2.png"),
          tk.PhotoImage(file="images/hang3.png"),
          tk.PhotoImage(file="images/hang4.png"),
          tk.PhotoImage(file="images/hang5.png"),
          tk.PhotoImage(file="images/hang6.png"),
          tk.PhotoImage(file="images/hang7.png"),
          tk.PhotoImage(file="images/hang8.png"),
          tk.PhotoImage(file="images/hang9.png"),
          tk.PhotoImage(file="images/hang10.png"),
          tk.PhotoImage(file="images/hang11.png")]

img_label = tk.Label(window)
img_label.grid(row=0, column=0, columnspan=3, padx=10, pady=40)
img_label.config(image=images[0])
```

* 행맨 글자를 나타내는 라벨을 만듭니다.
* StringVar()로 글자를 나타냅니다.
* StringVar() 값이 변하면 위젯의 글자도 변합니다. 
```python
hangman_word = tk.StringVar()
word_label = tk.Label(window, textvariable = hangman_word, font=("aria", 30))
word_label.grid(row=0, column=3, columnspan=6, padx=10)
```

* new_game() 함수를 만들어서 게임을 시작합니다.
* 한 칸을 띄어서 글자를 만듭니다.
```python
number_guesses = 0
word_choice = ""

def new_game():
    global number_guesses, word_choice
    img_label.config(image=images[0])
    word_choice = random.choice(word_list)   
    hangman_word.set(" ".join("_"*len(word_choice)))

new_game()
```

* 글자를 클릭하면 
```python
def guess(letter):
    letter = letter.lower()
    global number_guesses, word_choice
    choice_list = list(word_choice)   
    guesse_word = list(hangman_word.get())
    if choice_list.count(letter.lower()) > 0:      
        for i in range(len(choice_list)):
            if choice_list[i] == letter:
                guesse_word[i] = letter.upper()
                print(guesse_word)
            hangman_word.set("".join(guesse_word))
    else:
        number_guesses += 1
        img_label.config(image=images[number_guesses])
```

