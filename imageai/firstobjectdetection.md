# FirstObjectDetection
> ref: https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/README.md

```
ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
output_path = "/Users/yuxinglee/study/xImageAi/output"
# execution_path = os.getcwd()

detector = ObjectDetection()
detector.setModelTypeAsYOLOv3()
detector.setModelPath(os.path.join(ai_models_path, "yolo.h5"))
detector.loadModel()
```

#### 辨識且用RetinaNet圈選物件然後重新輸出一張圖
```
detections = detector.detectObjectsFromImage(
  input_image=os.path.join(data_images_path, "image2.jpg"),
  output_image_path=os.path.join(output_path, "image2new.jpg"),
  minimum_percentage_probability=30
)

for eachObject in detections:
    print(eachObject["name"], " : ", eachObject["percentage_probability"],
          " : ", eachObject["box_points"])
    print("--------------------------------")
```

#### 辨識且用RetinaNet圈選物件然後重新輸出一張圖並且輸出各個物件的圖片
```
detections, objects_path = detector.detectObjectsFromImage(
    input_image=os.path.join(data_images_path, "image3.jpg"),
    output_image_path=os.path.join(output_path, "image3new.jpg"),
  minimum_percentage_probability=30,
  extract_detected_objects=True
)

for eachObject, eachObjectPath in zip(detections, objects_path):
    print(eachObject["name"], " : ", eachObject["percentage_probability"],
          " : ", eachObject["box_points"])
    print("Object's image saved in " + eachObjectPath)
    print("--------------------------------")
```

#### Custom Object Detection
```
custom_objects = detector.CustomObjects(car=True, motorcycle=True)
detections = detector.detectCustomObjectsFromImage(
  custom_objects=custom_objects,
  input_image=os.path.join(data_images_path, "image3.jpg"),
  output_image_path=os.path.join(output_path, "image3custom.jpg"),
  minimum_percentage_probability=30
)

for eachObject in detections:
    print(eachObject["name"], " : ", eachObject["percentage_probability"],
          " : ", eachObject["box_points"])
    print("--------------------------------")

```

#### Detection Speed
```
// "normal"(default), "fast", "faster" , "fastest" and "flash"
detector.loadModel(detection_speed="fast")
```

#### hide attribute
```
detections = detector.detectObjectsFromImage(input_image=os.path.join(execution_path , "image3.jpg"), output_image_path=os.path.join(execution_path , "image3new_nodetails.jpg"), minimum_percentage_probability=30, display_percentage_probability=False, display_object_name=False)
```

#### Image Input & Output Types
```
detections = detector.detectObjectsFromImage(input_type="array", input_image=image_array , output_image_path=os.path.join(execution_path , "image.jpg")) # For numpy array input type
detections = detector.detectObjectsFromImage(input_type="stream", input_image=image_stream , output_image_path=os.path.join(execution_path , "test2new.jpg")) # For file stream input type
```




