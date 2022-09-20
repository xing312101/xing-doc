# FirstCustomModelTraining
> ref: https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Classification/CUSTOMTRAINING.md


#### I'm tried, but there is some wrong
```
LOGO_DATA_SET_DIR = '/Users/yuxinglee/study/xImageAi/logos'
model_trainer = ClassificationModelTrainer()
model_trainer.setModelTypeAsResNet50()
model_trainer.setDataDirectory(LOGO_DATA_SET_DIR)
model_trainer.trainModel(num_objects=10, num_experiments=100,
                         enhance_data=True, batch_size=32, show_network_summary=True)

## continue train model
trainer = ClassificationModelTrainer()
trainer.setModelTypeAsResNet50()
trainer.setDataDirectory(LOGO_DATA_SET_DIR)
trainer.trainModel(
    num_objects=10,
    num_experiments=50,
    enhance_data=True,
    batch_size=8,
    show_network_summary=True,
    continue_from_model="/Users/yuxinglee/study/xImageAi/logos/models/model_ex-004_acc-0.702703.h5",
    initial_num_objects=1000
)
```





#### example: idenprof
```
from io import open
import requests
import shutil
from zipfile import ZipFile
import os
from imageai.Classification.Custom import ClassificationModelTrainer

# execution_path = os.getcwd()
execution_path = '/Users/yuxinglee/study/xImageAi/modelTrain'

ZIP_URL = "https://github.com/OlafenwaMoses/IdenProf/releases/download/v1.0/idenprof-jpg.zip"
TRAIN_ZIP_PATH = os.path.join(execution_path, "idenprof-jpg.zip")

DATASET_DIR = os.path.join(execution_path, "idenprof")

if(os.path.exists(DATASET_DIR) == False):
    os.mkdir(DATASET_DIR)

if(os.path.exists(TRAIN_ZIP_PATH) == False):
    print("Downloading idenprof-jpg.zip")
    data = requests.get(ZIP_URL, stream=True)
    with open(TRAIN_ZIP_PATH, "wb") as file:
        shutil.copyfileobj(data.raw, file)
    del data

extract1 = ZipFile(TRAIN_ZIP_PATH)
extract1.extractall(execution_path)
extract1.close()

model_trainer = ClassificationModelTrainer()
model_trainer.setModelTypeAsResNet50()
model_trainer.setDataDirectory(DATASET_DIR)
model_trainer.trainModel(num_objects=10, num_experiments=100,
                         enhance_data=True, batch_size=32, show_network_summary=True)

```

#### continue train model
```
from imageai.Classification.Custom import ClassificationModelTrainer
import os

trainer = ClassificationModelTrainer()
trainer.setModelTypeAsDenseNet121()
trainer.setDataDirectory("idenprof")
trainer.trainModel(num_objects=10, num_experiments=50, enhance_data=True, batch_size=8, show_network_summary=True, continue_from_model="idenprof_densenet-0.763500.h5")

```

#### Transfer Learning (Training from a pre-trained model)
```
from imageai.Classification.Custom import ClassificationModelTrainer
import os

trainer = ClassificationModelTrainer()
trainer.setModelTypeAsResNet50()
trainer.setDataDirectory("idenprof")
trainer.trainModel(num_objects=10, num_experiments=50, enhance_data=True, batch_size=32, show_network_summary=True,transfer_from_model="resnet50_imagenet_tf.2.0.h5", initial_num_objects=1000)
```



