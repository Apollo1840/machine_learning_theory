# Computer vision

- references: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E8%AE%A1%E7%AE%97%E6%9C%BA%E8%A7%86%E8%A7%89.one%7Ce62dec13-74a6-4848-8bf4-bcd47aeaba78%2F%E6%9C%BA%E5%99%A8%E8%A7%86%E8%A7%89%E6%9C%89%E5%93%AA%E4%BA%9B%E5%AD%90%E9%A2%86%E5%9F%9F%7Ce071607e-6287-403b-ad40-c4c9cebdd804%2F%29&wdorigin=NavigationUrl

## Fields

- Core Vision tasks
    - Image classification/clustering
    - Image segmentation
    - Image caption
    - VQA
- Extractive tasks
    - Object detection
    - Keypoint detection
    - OCR
- Generative tasks
    - Image generation
    - Image restoration & super resolution
- Hyper-media tasks
    - 3D Vision
    - Video (see `video.md`)

### Image classification
Task: Assigns a category label to an image.

Representative Methods:
- AlexNet (2012)
- VGGNet (2014)
- GoogLeNet/Inception (2014)
- ResNet (2015)
- EfficientNet (2019)
- Vision Transformers (ViTs) (2020)
- ConvNeXt (2022)


### Image segmentation
a) Semantic Segmentation
Task: Assigns a class label to each pixel in an image.

Representative Methods:
- FCN (Fully Convolutional Network) (2015)
- U-Net (2015)
- DeepLab series (2017–2019)
- PSPNet (2017)
- Segment Anything Model (SAM) (2023)

b) Instance Segmentation
Task: Identifies and segments each object instance separately.

Representative Methods:
- Mask R-CNN (2017)
- YOLACT (2019)
- SOLO (Segmenting Objects by Locations) (2020)

Others: Image Matting/visual saliency detection

### Image caption
Task: Generates natural language descriptions for images.

Representative Methods:
- Show and Tell (2015)
- Show, Attend and Tell (2016)
- Transformer-based models (e.g., ViT+GPT)
- BLIP, BLIP-2 (2022)
- Flamingo (DeepMind) (2023)

### Visual Question Answering (VQA)
Task: Answers textual questions based on image content.

Representative Methods:
- SAN (Stacked Attention Network) (2016)
- Bottom-Up & Top-Down Attention (2018)
- LXMERT (2019)
- VisualBERT (2019)
- PaLI, PaLI-X (2022)
- LLaVA (Large Language and Vision Assistant) (2023)

### Object detection

Task: Identifies and localizes objects in an image with bounding boxes.

Representative Methods:
- R-CNN, Fast R-CNN, Faster R-CNN (2014–2015)
- SSD (Single Shot MultiBox Detector) (2016)
- YOLO (You Only Look Once) series (2016–2023)
- RetinaNet (2017)
- DETR (DEtection TRansformer) (2020)
- DINO (2022)

### Keypoint detection
Task: Detects key landmarks (e.g., body joints, face landmarks, hand keypoints).

Representative Methods:
- OpenPose (2017)
- HRNet (2019)
- BlazePose (Google) (2020)
- PoseFormer (2021)


### OCR

### Generative Vision Models
a) Image Generation
Task: Generates realistic images from noise or text descriptions.

Representative Methods:
- GANs (Generative Adversarial Networks) (2014)
- StyleGAN (2018–2020)
- BigGAN (2018)
- DALL·E series (2021–2023)
- Stable Diffusion (2022)

b) Style Transfer
Task: Transfers the artistic style of one image to another.

Representative Methods:
- Neural Style Transfer (2015)
- CycleGAN (2017)
- AdaIN (Adaptive Instance Normalization) (2017)

### Image Restoration & Super-Resolution 
Task: Enhances image quality, resolution, or removes noise.

Representative Methods:
- SRCNN (2014)
- EDSR (Enhanced Deep Super-Resolution) (2017)
- ESRGAN (Enhanced Super-Resolution GAN) (2018)
- SwinIR (2021)

### 3D Vision & Depth Estimation
Task: Estimates depth or reconstructs 3D structures from 2D images.

Representative Methods:
- SfM (Structure from Motion)
- MonoDepth (2017)
- NeRF (Neural Radiance Fields) (2020)
- Instant NeRF (2022)

### Video Analysis & Action Recognition
Task: Detects, classifies, and analyzes human actions in videos.

Representative Methods:
- C3D (Convolutional 3D Network) (2015)
- Two-Stream Network (2016)
- I3D (Inflated 3D Network) (2017)
- SlowFast Networks (2019)
- TimeSformer (2021)

## Models

see `cnn.md` adn `cnn_variants.md`.