# 33. OpenCV로 사람 얼굴 인식하기
## 카메라로 영상찍기
* ```cv.VideoCapture(번호)```로 카메라로 영상을 읽습니다.
```python
import cv2 as cv

capture = cv.VideoCapture(0)
#capture.set(cv.CAP_PROP_FRAME_WIDTH, 640)
#capture.set(cv.CAP_PROP_FRAME_HEIGHT, 480)

while True:
    ret, frame = capture.read()
    cv.imshow("VideoFrame", frame)
    key = cv.waitKey(10);
    if key == ord('s'):
        break
    
capture.release()
cv.destroyAllWindows()
```

## 얼굴을 인식해서 화면에 표시하기
* https://github.com/opencv/opencv/tree/master/data/haarcascades 에서 데이터를 다운로드 받습니다.
* key == 27는 ```esc```키를 누른 경우를 말합니다.
```python
import cv2 as cv

capture = cv.VideoCapture(0)
capture.set(cv.CAP_PROP_FRAME_WIDTH, 640)
capture.set(cv.CAP_PROP_FRAME_HEIGHT, 480)
face_cascade = cv.CascadeClassifier()
face_cascade.load(r'C:\opencv\haarcascade_frontalface_default.xml')

while True:
    ret, frame = capture.read()
    frame = cv.flip(frame, 1)
    grayframe = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    grayframe = cv.equalizeHist(grayframe)
    faces = face_cascade.detectMultiScale(grayframe, 1.1, 3, 0, (30, 30))
    print(faces)
    for (x,y,w,h) in faces:
        cv.rectangle(frame,(x,y),(x+w,y+h),(0,0,255),3)
    cv.imshow("Face", frame)
    key = cv.waitKey(10);
    if key == 27:
        break
    
capture.release()
cv.destroyAllWindows()
```

## 글자를 표시하기
```python
import cv2 as cv

capture = cv.VideoCapture(0)
capture.set(cv.CAP_PROP_FRAME_WIDTH, 640)
capture.set(cv.CAP_PROP_FRAME_HEIGHT, 480)
face_cascade = cv.CascadeClassifier()
face_cascade.load(r'C:\opencv\haarcascade_frontalface_default.xml')
font = cv.FONT_HERSHEY_DUPLEX

while True:
    ret, frame = capture.read()
    frame = cv.flip(frame, 1)
    grayframe = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    grayframe = cv.equalizeHist(grayframe)
    faces = face_cascade.detectMultiScale(grayframe, 1.1, 3, 0, (30, 30))
    print(faces)
    for (x,y,w,h) in faces:
        cv.rectangle(frame,(x,y),(x+w,y+h),(0,0,255),3)
        cv.putText(frame, "face", (x, y-10), font, 0.5, (255,0,0))
    cv.imshow("Face", frame)
    key = cv.waitKey(10);
    if key == 27:
        break
    
capture.release()
cv.destroyAllWindows()
```

## 눈을 인식하기
* haarcascade_eye.xml 데이터를 사용하면 눈을 인식할 수 있습니다.
```python
import cv2 as cv

capture = cv.VideoCapture(0)
capture.set(cv.CAP_PROP_FRAME_WIDTH, 640)
capture.set(cv.CAP_PROP_FRAME_HEIGHT, 480)
eye_cascade = cv.CascadeClassifier()
eye_cascade.load(r'C:\opencv\haarcascade_eye.xml')
font = cv.FONT_HERSHEY_DUPLEX

while True:
    ret, frame = capture.read()
    frame = cv.flip(frame, 1)
    grayframe = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)
    grayframe = cv.equalizeHist(grayframe)
    eyes = eye_cascade.detectMultiScale(grayframe, 1.1, 3, 0, (30, 30))
    print(eyes)
    for (x,y,w,h) in eyes:
        cv.rectangle(frame,(x,y),(x+w,y+h),(0,0,255),3)
        cv.putText(frame, "eye", (x, y-10), font, 0.5, (255,0,0))
    cv.imshow("Eyes", frame)
    key = cv.waitKey(10);
    if key == 27:
        break
    
capture.release()
cv.destroyAllWindows()


```
