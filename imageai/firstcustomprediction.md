# FirstCustomPrediction
> https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Classification/CUSTOMCLASSIFICATION.md

```
from imageai.Classification.Custom import CustomImageClassification
import os

ai_models_path = "/Users/yuxinglee/study/aiModels"
image_ai_path = "/Users/yuxinglee/study/ImageAI"
data_images_path = image_ai_path + "/data-images"
data_videos_path = image_ai_path + "/data-videos"
output_path = "/Users/yuxinglee/study/xImageAi/output"
# execution_path = os.getcwd()

prediction = CustomImageClassification()
prediction.setModelTypeAsResNet50()
prediction.setModelPath(os.path.join(
    ai_models_path, "idenprof_resnet_ex-056_acc-0.993062.h5"))
prediction.setJsonPath(os.path.join(ai_models_path, "idenprof.json"))
prediction.loadModel(num_objects=10)

predictions, probabilities = prediction.classifyImage(
    os.path.join(data_images_path, "4.jpg"), result_count=5)

for eachPrediction, eachProbability in zip(predictions, probabilities):
    print(eachPrediction, " : ", eachProbability)

```
