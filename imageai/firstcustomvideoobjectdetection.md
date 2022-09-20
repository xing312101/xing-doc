# FirstCustomVideoObjectDetection
> https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/Custom/CUSTOMVIDEODETECTION.md

```
from imageai.Detection.Custom import CustomVideoObjectDetection
import os

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
# data_images_path = image_ai_path + "/data-images"
data_videos_path = image_ai_path + "/data-videos"
output_path = "/Users/yuxinglee/study/xImageAi/output"
# execution_path = os.getcwd()

hololensDataPath = "/Users/yuxinglee/study/aiModels/customVideoObjectDetectionData"
detectionModelPath = os.path.join(
    hololensDataPath, "hololens-ex-60--loss-2.76.h5")
detectionConfigJsonPath = os.path.join(
    hololensDataPath, "detection_config.json")
holoInputVideoPath = os.path.join(data_videos_path, "holo1.mp4")

video_detector = CustomVideoObjectDetection()
video_detector.setModelTypeAsYOLOv3()
video_detector.setModelPath(detectionModelPath)
video_detector.setJsonPath(detectionConfigJsonPath)
video_detector.loadModel()

video_detector.detectObjectsFromVideo(
    input_file_path=holoInputVideoPath,
    output_file_path=os.path.join(output_path, "holo1-detected3"),
    frames_per_second=20,
    minimum_percentage_probability=40,
    log_progress=True
)

```

## Camera/Streaming
> 參考前面的camera

```
camera = cv2.VideoCapture(0)

while not camera.isOpened():
    print("camera is not open")

video_detector = CustomVideoObjectDetection()
video_detector.setModelTypeAsYOLOv3()
video_detector.setModelPath(detectionModelPath)
video_detector.setJsonPath(detectionConfigJsonPath)
video_detector.loadModel()

video_detector.detectObjectsFromVideo(
    camera_input=camera,
    output_file_path=os.path.join(output_path, "holo1-detected3"),
    frames_per_second=20,
    minimum_percentage_probability=40,
    log_progress=True,
    per_frame_function=forFrame,
    return_detected_frame=True
)
```


