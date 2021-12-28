# 18. Tkinter로 행맨 게임 만들기
## 행맨 게임 만들기
* 문제리스트를 만듭니다.
* ascii_uppercase를 사용해서 대문자로 버튼을 만듭니다.
* a//b는 a를 b로 나눴을 때 정수부분을 구합니다.
* 10//9를 하면 결과가 1이됩니다.
* grid에서 나누는 값을 다르게 해서 행과 열의 수를 바꿀 수 있습니다.
```python
import tkinter as tk
import random
from string import ascii_uppercase

word_list = ["apple", "banana", "cat"]

window = tk.Tk()

n = 0
for c in ascii_uppercase:
    tk.Button(window, text=c, width=4, font=("aria", 17)).grid(row=1+n//9, column=n%9)
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
* "banana"라면 모두 대문자로 바꾸고 리스트로 만듭니다. ```["B", "A", "N", "A", "N", "A"]```로 리스트를 만듭니다. 이 리스트가 정답(answer)이 됩니다. 
* 사용자가 선택한 것을 리스트로 저장합니다. ```your_choice```라는 리스트를 만듭니다. 
* 한 칸을 띄어서 글자를 만듭니다.
```python
def new_game():
    global number_guesses, answer, your_choice  
    number_guesses = 0
    answer = []
    your_choice = []
    img_label.config(image=images[number_guesses])
    answer = list(random.choice(word_list).upper())
    your_choice = list("-"*len(answer))
    hangman_word.set(" ".join(your_choice))
    
new_game()
```

* 글자를 클릭하면 결과를 확인합니다.
* answer에 클릭한 글자가 있는지 확인합니다.
* 리스트.count(문자)로 글자가 정답에 있는지 확인합니다.
* 글자가 있다면 인덱스를 구합니다. your_choice에서 해당 인덱스의 글자를 바꿉니다. 
* 버튼에 람다함수를 사용해서 command에 함수를 입력합니다.
```python
def guess(letter):     
    global number_guesses, answer, your_choice   
    if answer.count(letter) > 0:      
        for i in range(len(answer)):
            if answer[i] == letter:
                your_choice[i] = letter
            hangman_word.set(" ".join(your_choice))
    else:
        number_guesses += 1
        img_label.config(image=images[number_guesses])
        
n = 0
for c in ascii_uppercase:
    tk.Button(window, text=c, command=lambda letter=c:guess(letter), width=4, font=("aria", 18)).grid(row=1+n//9, column=n%9)
    n+=1    
```

* number_guesses가 11보다 작을 때까지 답을 확인합니다.
* 클릭하고 내가 선택한 것과 답을 비교해서 같은지 확인합니다.
* 정답이 같다면 메시지창으로 정답이라고 알려줍니다.
* ```import tkinter.messagebox as msgbox```로 가져옵니다.
* ```msgbox.showinfo("창제목", "메시지")```로 메시지창을 보여줍니다.
* number_guesses가 11이라면 ```msgbox.showwarning("창제목", "메시지")```로 경고창 보여줍니다.  
```python
def guess(letter):     
    global number_guesses, answer, your_choice
    if number_guesses < 11: 
        if answer.count(letter) > 0:      
            for i in range(len(answer)):
                if answer[i] == letter:
                    your_choice[i] = letter
                hangman_word.set(" ".join(your_choice))
            if your_choice ==  answer:
                msgbox.showinfo("게임 결과", "정답입니다!!")
        else:
            number_guesses += 1
            img_label.config(image=images[number_guesses])
            if number_guesses == 11:
                msgbox.showwarning("게임 결과", "틀렸습니다.")
```

* 다시 하기 버튼을 만듭니다.
* 다시 하기 버튼을 클릭하면 게임을 다시 시작합니다.
* number_guesses를 0으로 초기화합니다.
```python
tk.Button(window, text="new", command=new_game, width=4, font=("aria", 18)).grid(row=1+n//9, column=n%9)
```

* txt 파일을 읽어서 문제를 만들 수 있습니다.
* [행맨 게임 만들기](https://github.com/itple-sw/python-drone/blob/main/14/%ED%96%89%EB%A7%A8%20%EA%B2%8C%EC%9E%84%20%EB%A7%8C%EB%93%A4%EA%B8%B0.md)를 참고합니다.
