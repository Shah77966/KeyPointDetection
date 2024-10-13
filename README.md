````markdown
# Keypoint Detection Model

This repository contains a keypoint detection model using PyTorch and a custom dataset. The model is based on the `KeypointRCNN` architecture and detects keypoints and bounding boxes for objects in images.

## Table of Contents

- [Key Features](#key-features)
- [Installation](#installation)
- [Dataset Structure](#dataset-structure)
- [Training and Evaluation](#training-and-evaluation)
- [Visualization](#visualization)
- [File Structure](#file-structure)
- [Requirements](#requirements)
- [Usage](#usage)
- [Model](#model)
- [Acknowledgements](#acknowledgements)

## Key Features

- **Custom Keypoint Detection:** Detects keypoints and bounding boxes of objects in images.
- **Augmentation:** Uses `Albumentations` for image and keypoint augmentations.
- **Visualization:** Provides utilities for visualizing predictions and original annotations.
- **Pretrained Backbone:** Utilizes a pretrained ResNet50 backbone with customizable RPN anchor sizes.

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/Shah77966/KeyPointDetection.git
   ```
2. Navigate to the project directory:
   ```bash
   cd KeyPointDetection
   ```
3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Dataset Structure

Your dataset should be structured as follows:

```bash
Dataset/
    ├── train/
    │   ├── images/
    │   └── annotations/
    └── test/
        ├── images/
        └── annotations/
```
````

- **images/**: Contains all the images for training and testing.
- **annotations/**: JSON files containing bounding boxes and keypoints for each image.

## Training and Evaluation

To train the model, adjust the training loop parameters inside `main.py`, such as number of epochs and learning rate. The training loop can be activated by uncommenting the respective code.

```python
for epoch in range(num_epochs):
    train_one_epoch(model, optimizer, data_loader_train, device, epoch, print_freq=1000)
    lr_scheduler.step()
    evaluate(model, data_loader_test, device)
```

## Visualization

You can visualize both original and transformed images with bounding boxes and keypoints by using the `visualize()` function in `main.py`.

The function will save the output to a specified path:

```python
visualize(image, bboxes, keypoints, save_path="output/transformed_image.jpg")
```

### Example Visualization:

Transformed and original images are saved side by side, with keypoints and bounding boxes drawn in different colors.

## File Structure

Here’s a breakdown of the key files:

- **main.py**: Contains the core logic for data loading, model creation, training, and visualization.
- **coco_eval.py**: COCO evaluation utilities.
- **coco_util.py**: Helper functions for COCO datasets.
- **engine.py**: Training and evaluation logic.
- **group_by_aspect.py**: Groups images by aspect ratio for better batching.
- **presets.py**: Contains preset configurations for training.
- **train.py**: Training utilities.
- **transforms.py**: Data augmentation and transformation utilities.
- **utils.py**: General utilities such as collate functions.

## Requirements

To set up the environment, install the following dependencies listed in the `requirements.txt` file:

```bash
albumentations==1.4.18
matplotlib==3.7.2
numpy==2.1.2
opencv_python_headless==4.10.0.84
Pillow==9.3.0
Pillow==10.4.0
pycocotools==2.0.8
torch==2.0.1+cu117
torchvision==0.15.2+cu117
```

You can install all dependencies using the following command:

```bash
pip install -r requirements.txt
```

## Usage

### Training the Model

1. Make sure your dataset is structured as described above.
2. Run the `main.py` script to start training:

   ```bash
   python main.py
   ```

3. To visualize results after training, use the `visualize()` function.

### Model Weights

After training, the model weights are saved to the `SavedModel/weights` folder:

```bash
torch.save(model.state_dict(), 'SavedModel/weights/keypointsrcnn_weights_initial.pth')
```

To load the weights for evaluation:

```python
model.load_state_dict(torch.load('SavedModel/weights/keypointsrcnn_weights_initial.pth', weights_only=False))
```

## Model

The model is based on the `KeypointRCNN` architecture with a ResNet50 backbone. You can create the model by calling:

```python
model = get_model(num_keypoints=2)
```

This function allows you to specify the number of keypoints you want the model to predict. The default is set to 2 keypoints per object.

## Acknowledgements

- **PyTorch Team**: For the robust and flexible PyTorch framework.
- **Albumentations**: For providing advanced augmentation utilities.
- **COCO Dataset**: For the evaluation scripts and utility functions.

---

Feel free to reach out with any issues or feature requests!

```

This `README.md` file includes all the key aspects of your project, such as installation instructions, dataset structure, file breakdowns, and how to use the model for training, evaluation, and visualization.

Let me know if you need further modifications!
```
