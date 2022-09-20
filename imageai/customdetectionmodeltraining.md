# CustomDetectionModelTraining
> https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/Custom/CUSTOMDETECTIONTRAINING.md

## Training on your custom dataset
> https://github.com/OlafenwaMoses/ImageAI/releases/tag/essential-v4

```
from imageai.Detection.Custom import DetectionModelTrainer
import os

hololensDataPath = "/Users/yuxinglee/study/hololensData"
hololensImagesDirPath = os.path.join(hololensDataPath, "hololens")
pretrainedModelPath = os.path.join(hololensDataPath, "pretrained-yolov3.h5")


trainer = DetectionModelTrainer()
trainer.setModelTypeAsYOLOv3()
trainer.setDataDirectory(data_directory=hololensImagesDirPath)
trainer.setTrainConfig(object_names_array=[
                       "hololens"], batch_size=4, num_experiments=200, train_from_pretrained_model=pretrainedModelPath)
# In the above,when training for detecting multiple objects,
# set object_names_array=["object1", "object2", "object3",..."objectz"]
trainer.trainModel()

```


## Evaluating your saved detection models' mAP
```
from imageai.Detection.Custom import DetectionModelTrainer
import os

hololensDataPath = "/Users/yuxinglee/study/hololensData"
hololensImagesDirPath = os.path.join(hololensDataPath, "hololens")
# pretrainedModelPath = os.path.join(hololensDataPath, "pretrained-yolov3.h5")
detectionModelPath = os.path.join(
    hololensDataPath, "hololens-ex-60--loss-2.76.h5")
detectionConfigJsonPath = os.path.join(
    hololensDataPath, "detection_config.json")

trainer = DetectionModelTrainer()
trainer.setModelTypeAsYOLOv3()
trainer.setDataDirectory(data_directory=hololensImagesDirPath)
metrics = trainer.evaluateModel(
    model_path=detectionModelPath,
    json_path=detectionConfigJsonPath,
    iou_threshold=0.5,
    object_threshold=0.3,
    nms_threshold=0.5
)

```


#### Multi Model Evaluation:
```
metrics = trainer.evaluateModel(model_path="hololens/models", json_path="hololens/json/detection_config.json", iou_threshold=0.5, object_threshold=0.3, nms_threshold=0.5)

```
