# 32. OpenCV 기초 사용법 알기
## OpenCV 살펴보기
* OpenCV는 Open Source Computer Vision의 약자입니다.
* 실시간 컴퓨터 비전을 목적으로 한 프로그래밍 라이브러리입니다.
* 실시간으로 이미지 프로세싱을 쉽게 할 수 있도록 인텔에서 만들었습니다.
* OpenCV는 영상으로 사물의 특성을 분석하여 인식할 수 있습니다.
* 라이브러리화하여 우리가 쉽게 영상인식에 활용할 수 있습니다.
* 주자창의 번호판 인식, 자동차의 불법단속, CCTV등 다양한 서비스로 활용됩니다.

## OpenCV 관련 패키지 설치하기
* OpenCV 관련 패키지를 설치합니다.
* ```pip install opencv-python``` : OpenCV의 메인 모듈을 설치합니다.
* ```pip install opencv-contrib-python``` : contrib 모듈(래퍼 패키지)을 설치합니다.
* ```pip install numpy``` : 데이터 분석 환경에서 많이 사용되는 행렬 연산을 위한 라이브러리를 설치합니다.
* ```pip install matplotlib``` : 도표, 차트, 그래프 등을 구현할 수 있도록 해주는 그래픽 라이브러리를 설치합니다.
* 문제없이 설치가 되었는지 확인합니다.
```python
import cv2 as cv
print(cv.__version__)
```

## 이미지에서 원하는 것을 인식하기
* imread(경로)로 이미지를 읽습니다.
* 경로를 설정할 때 문자열 앞에 r을 붙이면 raw 문자열이 됩니다.
* raw 문자열은 이스케이프 시퀀스를 그대로 저장할 때 사용합니다.
* shape로 Y축, X축, 채널을 확인합니다.
* imshow(제목, 이미지객체)로 이미지를 창으로 보여줍니다.
* waitKey()는 키보드 입력을 대기하는 함수로 0이면 key 입력이 있을 때까지 계속 기다립니다.
* destroyAllWindows()으로 화면에 나타난 창을 종료합니다.
```python
import cv2 as cv
img = cv.imread(r'C:\img\codrone.jpg')
print(img.shape) #shape로 크기를 확인
cv.imshow('window_title',img)
cv.waitKey(0)
cv.destroyAllWindows()
```
* 이미지에서 원하는 것을 인식하기 위해서 사진을 gray 스케일로 바꿉니다.
* cv.cvtColor(이미지객체, cv.COLOR_BGR2GRAY)로 gray 스케일로 바꿉니다.
```python
import cv2 as cv
img = cv.imread(r'C:\img\codrone.jpg')
print(img.shape)
img_gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('window_title',img_gray)
cv.waitKey(0)
cv.destroyAllWindows()
```
* 












