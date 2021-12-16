# 37. Tesseract로 숫자와 문자 인식하기
## Tesseract 이해하기
* Tesseract는 구글에서 만든 AI 프로그램입니다.
* 사진 속에서 글자를 인식할 수 있습니다.
* Tesseract 프로그램을 다운로드 받습니다.
* 윈도우는 https://github.com/UB-Mannheim/tesseract/wiki 사이트에 들어가서 운영체제에 맞는 exe 파일을 다운로드 받습니다.
* 맥은 https://brew.sh/ 사이트에 들어가서 명령어를 복사해서 homebrew를 설치합니다. 그리고 ```brew install tesseract-lang``으로 설치합니다.  
* ```pip install pytesseract Pillow```로 pytesseract와 Pillow를 설치합니다.


## Tesseract 사용법
* pytesseract와 Pillow 모듈을 가져옵니다.
* PTL는 Pillow 모듈입니다. 여기에서 Image라는 함수를 사용하겠습니다.
* pytesseract.pytesseract.tesseract_cmd에 Tesseract 프로그램 경로를 지정합니다.
```python
import pytesseract
from PTL import Image

pytesseract.pytesseract.tesseract_cmd = r"Tesseract 프로그램 경로"
```
