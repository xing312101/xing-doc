# FirstVideoObjectDetection
> ref: https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/VIDEO.md


```
from imageai.Detection import VideoObjectDetection
import os

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
data_videos_path = image_ai_path + "/data-videos"
output_path = "/Users/yuxinglee/study/xImageAi/output"

detector = VideoObjectDetection()
detector.setModelTypeAsRetinaNet()
detector.setModelPath(os.path.join(ai_models_path, "resnet50_coco_best_v2.1.0.h5"))
detector.loadModel()

```

```
video_path = detector.detectObjectsFromVideo(
  input_file_path=os.path.join(data_videos_path, "traffic-mini.mp4"),
  output_file_path=os.path.join(output_path, "traffic_detected"),
  frames_per_second=20,
  log_progress=True
)
```


#### Custom Video Object Detection
```
custom_objects = detector.CustomObjects(
    person=True, bicycle=True, motorcycle=True)

video_path = detector.detectCustomObjectsFromVideo(
    custom_objects=custom_objects,
    input_file_path=os.path.join(data_videos_path, "traffic-mini.mp4"),
    output_file_path=os.path.join(output_path, "traffic_custom_detected"),
    frames_per_second=26, log_progress=True)

```

#### customize function
```
def forFrame(frame_number, output_array, output_count)

def forSeconds(second_number, output_arrays, count_arrays, average_output_count)

def forMinute(minute_number, output_arrays, count_arrays, average_output_count)

video_path = detector.detectCustomObjectsFromVideo(
    custom_objects=custom_objects,
    input_file_path=os.path.join(data_videos_path, "traffic-mini.mp4"),
    output_file_path=os.path.join(output_path, "traffic_custom_detected"),
    frames_per_second=26,
    log_progress=True,

    per_second_function=forSeconds,
    per_frame_function=forFrame,
    per_minute_function=forMinute,
)

```
## Camera / Live Stream Video Detection

```
import cv2
from imageai.Detection import VideoObjectDetection
import os
import numpy as np


def forFrame(frame_number, output_array, output_count, returned_frame):
    # 2764800
    newFrameNp = returned_frame.reshape(720, 1280, 3)

    cv2.imshow("return_frame", newFrameNp)
    cv2.waitKey(100)
    print("------------END OF A FRAME --------------")

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
data_videos_path = image_ai_path + "/data-videos"
output_path = "/Users/yuxinglee/study/xImageAi/output"

print("@@ init camera")
camera = cv2.VideoCapture(0)

detector = VideoObjectDetection()
detector.setModelTypeAsRetinaNet()
detector.setModelPath(os.path.join(
    ai_models_path, "resnet50_coco_best_v2.1.0.h5"))
detector.loadModel()

while not camera.isOpened():
    print("camera is not open")

print("@@ start detect")
video_path = detector.detectObjectsFromVideo(
    camera_input=camera,
    output_file_path=os.path.join(output_path, "camera_detected_video"),
    frames_per_second=20,
    log_progress=True,
    minimum_percentage_probability=40,
    # detection_timeout=10,
    per_frame_function=forFrame,
    # per_second_function=forSeconds,
    return_detected_frame=True
)


```

