# FirstPrediction
> ref: https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Classification/README.md

```
from imageai.Classification import ImageClassification
import os

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
# execution_path = os.getcwd()

print(ai_models_path)
print(os.path.join(ai_models_path, "resnet50_imagenet_tf.2.0.h5"))

prediction = ImageClassification()
prediction.setModelTypeAsResNet50()
prediction.setModelPath(os.path.join(ai_models_path, "resnet50_imagenet_tf.2.0.h5"))
prediction.loadModel(classification_speed="normal")

predictions, probabilities = prediction.classifyImage(os.path.join(data_images_path, "1.jpg"), result_count=5 )
for eachPrediction, eachProbability in zip(predictions, probabilities):
    print(eachPrediction , " : " , eachProbability)


```

## speed
```
// "normal"(default), "fast", "faster" and "fastest"
prediction.loadModel(prediction_speed="fast")
```

## Image Input Types
```
predictions, probabilities = prediction.classifyImage(image_array, result_count=5 , input_type="array" ) # For numpy array input type
predictions, probabilities = prediction.classifyImage(image_stream, result_count=5 , input_type="stream" ) # For file stream input type
```



