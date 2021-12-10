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
* 
