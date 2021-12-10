# 23. turtle로 단어 깜박이 만들기
## turtle로 글자 그리는 법 알기
* turtle.write("글자", move=False, align="center", font=("폰트", 크기, "폰트형태")로 글자를 그립니다. 
* move를 False로 해서 움직이지 않도록 합니다. 
* turtle.clear()를 하면 화면에서 그렸던 것이 지워집니다.
* turtle.color("색깔")로 글자색을 정합니다.
```python
import turtle as t

t.write("파이썬", move=False, align="center", font=("Arial", 100, "normal"))
```

## 파이썬 깜박이 만들기
* 영어 단어와 뜻이 정리된 word.txt를 사용합니다.
* 영어 단어와 뜻을 딕셔너리로 정리해서 깜박이를 만듭니다.
```python
import os
import random
import turtle as t
import time

os.chdir(r'C:\file')

word_dict = {} 

def find_word_meaning():
    with open("word.txt", "r") as f:
        lines = f.readlines()

    for line in lines:
        key = line.split("\n")[0].split(":")[0]
        value = line.split("\n")[0].split(":")[1]
        word_dict[key] = value 
    return(word_dict)

my_dict = find_word_meaning()
print(my_dict)
```
* show_word_meaning이라는 함수를 만듭니다.
* 인자로 들어오는 딕셔너리에서 키만 모아서 리스트로 만듭니다. 
```python
def show_word_meaning(dictionary):
    key_list = list(dictionary.keys()) 
    while True:
        for i in range(len(key_list)):
            key = key_list[i]
            value = dictionary[key]

            t.color("black")
            t.write(key, move=False, align="center", font=("Arial", 100, "normal"))
            time.sleep(1)
            t.clear()

            t.color("orange")
            t.write(value, move=False, align="center", font=("Arial", 100, "normal"))
            time.sleep(1)
            t.clear()
```
* 전체코드입니다.
```python
import os
import random
import turtle as t
import time

os.chdir(r'C:\file')

word_dict = {}

def find_word_meaning():
    with open("word.txt", "r") as f:
        lines = f.readlines()

    for line in lines:
        key = line.split("\n")[0].split(":")[0]
        value = line.split("\n")[0].split(":")[1]
        word_dict[key] = value
    return(word_dict)

def show_word_meaning(dictionary):
    key_list = list(dictionary.keys())
    while True:
        for i in range(len(key_list)):
            key = key_list[i]
            value = dictionary[key]
            t.color("black")
            t.write(key, move=False, align="center", font=("Arial", 100, "normal"))
            time.sleep(1)
            t.clear()
            t.color("orange")
            t.write(value, move=False, align="center", font=("Arial", 100, "normal"))
            time.sleep(1)
            t.clear()
            
my_dict = find_word_meaning()
show_word_meaning(my_dict)
```
