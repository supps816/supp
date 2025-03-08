# Zero-Shot Depth Estimation


Zero-shot depth estimation aims to predict depth maps for unseen scenes without requiring task-specific fine-tuning. It leverages transferable knowledge from pretrained models, enabling versatile, label-efficient solutions for applications.


## Split
The zero-shot test split is based on the sequence level. The data root folder is `interval5_nolabels/`.
```python
test_sequences = [
    '/interval5_nolabels/skip300_AMtown01_interval5',
    '/interval5_nolabels/skip300_AMvalley01_interval5',
    '/interval5_nolabels/skip300_HKairport01_interval5',
    '/interval5_nolabels/skip300_HKisland01_interval5',
]
```

## 1. DepthAnything

The code is based on the official DepthAnything Code (https://github.com/LiheYoung/Depth-Anything). 

- Requirements, which are stored in `requirements.txt`
```
torch
torchvision
gradio_imageslider
gradio==4.14.0
opencv-python
huggingface_hub
```
```
conda create -n depthanything python=3.8
conda activate depthanything
cd Depth-Anything
pip install -r requirements.txt
```


## 2. DepthAnythingV2
DepthAnythingV2 is an extended version of the vanilla DepthAnything. It is based on the code (https://github.com/DepthAnything/Depth-Anything-V2)

- Requirements
```
gradio_imageslider
gradio==4.29.0
matplotlib
opencv-python
torch
torchvision
```


## 3. GeoWizard
GeoWizard is a diffusion-based depth estimation model, which is from the code (https://github.com/fuxiao0719/GeoWizard).

- Requirements

We test the codes under the following environment: Ubuntu 22.04, Python 3.9.18, CUDA 11.8.
```
conda create -n geowizard python=3.9
conda activate geowizard
cd GeoWizard
pip install -r requirements.txt
```


## 4. Marigold
GeoWizard is a diffusion-based depth estimation model, which is from the code (https://github.com/prs-eth/Marigold).

- Requirements
```
conda create -n marigold python=3.8
conda activate marigold
cd Marigold
pip install -r requirements.txt
```

## 5. Metric3D and Metric3DV2
Metric3D and Metric3DV2 are both from the same repository (https://github.com/YvanYin/Metric3D).
- Requirements

For the ViT models, use the following environment：
```
conda create -n metric3d python=3.8
conda activate metric3d
cd Metric3D
pip install -r requirements_v2.txt
```
For ConvNeXt-L, it is
```
conda create -n metric3d python=3.8
conda activate metric3d
cd Metric3D
pip install -r requirements_v1.txt
```


## 6. ZoeDepth
ZoeDepth is based on the code (https://github.com/isl-org/ZoeDepth).
- Requirements

```
cd ZoeDepth
conda env create -n zoe --file environment.yml
conda activate zoe
```



## -1. Running

We have modified all depth estimation baselines code and provide the `draft_infer.py` in each baseline directory, which is to conduct zero-shot depth estimation evaluation on our UAVScenes dataset. You can change encoder types, input sizes, and other configurations. The ouptput visualization depth maps will be stored in `output/`. An example script is as follows
```
cd Depth-Anything
conda activate depthanything
CUDA_VISIBLE_DEVICES=0 python draft_infer.py

cd Depth-Anything-V2
conda activate depthanythingv2
CUDA_VISIBLE_DEVICES=0 python draft_infer.py

cd Metric3D
conda activate metric3d
CUDA_VISIBLE_DEVICES=0 python draft_infer.py

cd ZoeDepth
conda activate zoedepth
CUDA_VISIBLE_DEVICES=0 python draft_infer.py

cd GeoWizard/geowizard
conda activate geowizard
CUDA_VISIBLE_DEVICES=0 python draft_infer.py

cd Marigold
conda activate marigold
CUDA_VISIBLE_DEVICES=1 python draft_infer.py
```

The depth evaluation code is based from MonoDepth2 (https://github.com/nianticlabs/monodepth2/blob/master/evaluate_depth.py), which supports metric depth evaluation. We do not apply the least square alignment to fit the relative depth maps (affine-invariant depth predictions) for GeoWizard and Marigold.