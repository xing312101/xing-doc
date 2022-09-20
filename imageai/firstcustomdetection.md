# FirstCustomDetection
> https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/Custom/CUSTOMDETECTION.md

```
from imageai.Detection.Custom import CustomObjectDetection
import os

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
output_path = "/Users/yuxinglee/study/xImageAi/output"

hololensDataPath = "/Users/yuxinglee/study/aiModels/customObjectDetectionData"
detectionModelPath = os.path.join(
    hololensDataPath, "hololens-ex-60--loss-2.76.h5")
detectionConfigJsonPath = os.path.join(
    hololensDataPath, "detection_config.json")

detector = CustomObjectDetection()
detector.setModelTypeAsYOLOv3()
detector.setModelPath(detectionModelPath)
detector.setJsonPath(detectionConfigJsonPath)
detector.loadModel()
detections = detector.detectObjectsFromImage(
    input_image=os.path.join(data_images_path, "holo2.jpg"),
    output_image_path=os.path.join(output_path, "holo2-detected.jpg")
)
for detection in detections:
    print(detection["name"], " : ", detection["percentage_probability"],
          " : ", detection["box_points"])

```


#### Object Detection, Extraction and Fine-tune
```

detections, extracted_objects_array = detector.detectObjectsFromImage(
    input_image=os.path.join(data_images_path, "holo2.jpg"),
    output_image_path=os.path.join(output_path, "holo2-detected.jpg"),
    extract_detected_objects=True
)

for detection, object_path in zip(detections, extracted_objects_array):
    print(object_path)
    print(detection["name"], " : ", detection["percentage_probability"],
          " : ", detection["box_points"])
    print("---------------")

```

#### Hiding/Showing Object Name and Probability
```
detections, extracted_objects_array = detector.detectObjectsFromImage(
    input_image=os.path.join(data_images_path, "holo2.jpg"),
    output_image_path=os.path.join(output_path, "holo2-detected.jpg"),
    extract_detected_objects=True,
    minimum_percentage_probability=30,
    display_percentage_probability=False,
    display_object_name=False
)
```


### Image Input & Output Types
```
# For numpy array input type
detections = detector.detectObjectsFromImage(input_type="array", input_image=image_array , output_image_path=os.path.join(execution_path , "holo2-detected.jpg"))

# For numpy array output type
detected_image_array, detections = detector.detectObjectsFromImage(output_type="array", input_image="holo2.jpg" )

```


