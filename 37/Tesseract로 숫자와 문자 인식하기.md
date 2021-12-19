# 37. Tesseract로 숫자와 문자 인식하기
## Tesseract 이해하기
* Tesseract는 구글에서 만든 AI 프로그램입니다.
* 사진 속에서 글자를 인식할 수 있습니다.
* Tesseract 프로그램을 다운로드 받습니다.
* 윈도우는 https://github.com/UB-Mannheim/tesseract/wiki 사이트에 들어가서 운영체제에 맞는 exe 파일을 다운로드 받습니다.
* 다운로드 받은 파일을 실행합니다.
* 설치할 때 언어 데이터를 선택해야 합니다.
* Additional script data에서 Hangul을 선택합니다.
* Additional language data에서 Korean을 선택합니다.
* 한글이 설치가 안 되면 https://github.com/tesseract-ocr/tessdata/ 에서 Hangul과 kor와 관련된 데이터를 다운로드 받아서 tessdata 폴더에 저장합니다.
* 맥은 https://brew.sh/ 사이트에 들어가서 명령어를 복사해서 homebrew를 설치합니다. 그리고 ```brew install tesseract-lang```으로 설치합니다.  
* ```pip install pytesseract Pillow```로 pytesseract와 Pillow를 설치합니다.

## Tesseract 사용법
* pytesseract와 Pillow 모듈을 가져옵니다.
* PTL는 Pillow 모듈입니다. 여기에서 Image 객체를 사용하겠습니다.
* pytesseract.pytesseract.tesseract_cmd에 Tesseract 프로그램 경로를 지정합니다.
```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"tesseract.exe 경로"
```

* ```Image.open("경로")```로 사진을 엽니다.
* ```pytesseract.image_to_string(이미지)```로 사진 속 글자를 텍스트로 바꿔줍니다.
* 한국어라면 ```lang='kor'``` 옵션을 입력합니다.
* ```print()```로 결과를 확인합니다.
* 에러가 나면 환경변수에 ```C:\Program Files\Tesseract-OCR```를 추가합니다.
```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
img = Image.open("english.png")
result = pytesseract.image_to_string(img)
print(result)
```

* result는 문자열입니다. ```\n```을 기준으로 split으로 나눠서 사용할 수 있습니다.
```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
img = Image.open("english.png")
result = pytesseract.image_to_string(img)
print(result.split("\n"))
```
* 인식한 글자를 파일로 저장할 수 있습니다.
```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
img = Image.open("english.png")
result = pytesseract.image_to_string(img)
with open("tesseract.txt", "w") as f:
    f.write(result)
```
## 글자를 사각형으로 표시하기
* ```pytesseract.image_to_boxes```로 글자와 좌표를 확인합니다.
```python
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
img = Image.open("english.png")
result = pytesseract.image_to_boxes(img)
print(result)
```

* ```splitlines()```로 나눕니다.
```python
for boxes in result.splitlines():
    print(boxes)
```  
* boxes에 들어있는 값을 x,y,w,h에 저장합니다.
```python
for boxes in result.splitlines():
    boxes = boxes.split(' ')
    x,y,w,h = int(boxes[1]), int(boxes[2]), int(boxes[3]), int(boxes[4])
    print(x, y, w, h)
```
* 전체 이미지의 높이와 너비에서 y와 h를 뺀 값으로 사각형을 그립니다.
* y, h는 아래를 기준으로 값이 정해지기 때문에 빼야 합니다. 
![image](https://user-images.githubusercontent.com/76088532/146682612-b63eeec4-2eb6-4aa9-87fe-175aae3a23e0.png)

```python
import cv2 as cv
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
img = Image.open("english.png")
imgBox = pytesseract.image_to_boxes(img)
img = cv.imread("english.png")
img_h, img_w, channel = img.shape

for boxes in imgBox.splitlines():
    boxes = boxes.split(' ')
    x,y,w,h = int(boxes[1]), int(boxes[2]), int(boxes[3]), int(boxes[4])
    cv.rectangle(img, (x, img_h-y), (w, img_h-h), (0,0,255), 2)

cv.imshow("pytesseract", img)
```

## 영상에서 글자 인식하기
* capture.read()로 영상을 읽고 결과가 없다면 continue로 while문에 처음부터 코드를 다시 실행합니다. 
```python
import cv2 as cv
import pytesseract
from PIL import Image

pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"

capture = cv.VideoCapture(0)
font = cv.FONT_HERSHEY_DUPLEX

while True:      
    ret, frame = capture.read()
    if not ret:
        continue
    frame_h, frame_w, channel = frame.shape      
    text = pytesseract.image_to_string(frame)
    imgBox = pytesseract.image_to_boxes(frame)
    for boxes in imgBox.splitlines():
        boxes = boxes.split(' ')
        x,y,w,h = int(boxes[1]), int(boxes[2]), int(boxes[3]), int(boxes[4])
        cv.rectangle(frame, (x, frame_h-y), (w, frame_h-h), (0,0,255), 2)
    cv.putText(frame, text, org=(30, 30), fontFace=font, fontScale=0.5, color=(255,0,0), thickness=2)    
    cv.imshow("pytesseract", frame)
    if cv.waitKey(1) == 27:
        break

capture.release()
cv.destroyAllWindows()
```
