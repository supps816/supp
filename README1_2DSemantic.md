# Image Semantic Segmentation

The 2D semantic segmentation codes are based on timm https://github.com/huggingface/pytorch-image-models. We use different visual backbones along with UperNet to conduct semantic segmentation evaluation.


## Splits
The splits are in sequence levels. The data root folder is `interval5_with2Dsemantic_instance_resize512/`.
```
train: [
    skip300_AMtown01_interval5, 
    skip300_AMvalley01_interval5, 
    skip300_AMtown02_interval5,
    skip300_AMvalley02_interval5, 
    skip300_HKairport01_interval5, 
    skip300_HKisland01_interval5,
    skip300_HKairport_GNSS01_interval5, 
    skip300_HKisland_GNSS01_interval5
]
test: [
    skip300_AMtown03_interval5, 
    skip300_AMvalley03_interval5, 
    skip300_HKairport_GNSS_Evening_interval5,
    skip300_HKisland_GNSS_Evening_interval5
]
```


## Requirements
Unlike other tasks that require tedious installation steps, the requirements of 2D semantic segmentation are easy to follow.
- torch (tested on torch>2.0.0)
```
pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118
```

- Others
```
shuil
pillow
tqdm
numpy
matplotlib
pyyaml

```

## Run
- Dataset preparation. 

You need to modify some arguments in `tools/options.py`. For example, you need to change the `imagedataroot` to where you store the dataset. 

- Below are some example running scripts for running ResNet, ViT (Vision Transformer), 
```
python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename resnet34

python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename resnet50

python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename resnet101

python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename vit_tiny_patch16_224

python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename vit_small_patch16_224

python train.py --machine 4090 --cuda 0 --num_epochs 30  --backbonename vit_base_patch16_224
```