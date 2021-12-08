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






