# 33. OpenCV로 사람 얼굴 인식하기
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
        cv.rectangle(frame,(x,y),(x+w,y+h),(0,0,255),3,4,0)
    cv.imshow("Face", frame)
    key = cv.waitKey(10);
    if key == 27:
        break
    
capture.release()
cv.destroyAllWindows()
```

