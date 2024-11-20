# Novel View Synthesis


## 0. Preprocess
Please perform data preprocessing first and replace the path with the corresponding scenes in each UAVScenes.
```
python prepare_uavscenes.py
```


## 1. 3DGS
---- 
3D Gaussian Splatting for Real-Time Radiance Field Rendering. The introduction of anisotropic 3D Gaussians as a high-quality, unstructured representation of radiance fields. An optimization method of 3D Gaussian properties, interleaved with adaptive density control that creates high-quality representations for captured scenes. A fast, differentiable rendering approach for the GPU, which is visibility-aware, allows anisotropic splatting and fast backpropagation to achieve high-quality novel view synthesis.

#### Conda Environment

Please refer to the original 3DGS code

#### UAVScences

Running:

```
CUDA_VISIBLE_DEVICES=0 python train.py \
    -s /HKairport_processed/HKairport01 \
    -m debug/MaRS/HKairport01 \
    --data_device cpu \
    --position_lr_init 0.000016 \
    --scaling_lr 0.001 \
    --percent_dense 0.005 \
    --eval && \
CUDA_VISIBLE_DEVICES=0 python render.py \
    -m debug/HKairport01 && \
CUDA_VISIBLE_DEVICES=0 python metrics.py \
    -m debug/HKairport01
```


## 2. GaussianPro
---- 
GaussianPro: 3D Gaussian Splatting with Progressive Propagation. GaussianPro is a novel Gaussian propagation strategy that guides the densification to produce more compact and accurate Gaussians, particularly in low-texture regions.

#### Conda Environment

Please refer to the original GaussianPro code

#### UAVScences

Running:

```
CUDA_VISIBLE_DEVICES=0 python train.py \
    -s /HKairport_processed/HKairport01 \
    -m debug/MaRS/HKairport01 \
    --data_device cpu \
    --position_lr_init 0.000016 \
    --scaling_lr 0.001 \
    --percent_dense 0.005 \
    --eval && \
CUDA_VISIBLE_DEVICES=0 python render.py \
    -m debug/HKairport01 && \
CUDA_VISIBLE_DEVICES=0 python metrics.py \
    -m debug/HKairport01
```


## 3. DCGaussian
---- 
DC-Gaussian: Improving 3D Gaussian Splatting for Reflective Dash Cam Videos. DC-Gaussian, a method for modeling high-fidelity obstruction-free 3D Gaussian Splatting from dash cam videos. 

#### Conda Environment

Please refer to the original DCGaussian code

#### UAVScences

Running:

```
CUDA_VISIBLE_DEVICES=0 python train.py \
    -s /HKairport_processed/HKairport01 \
    -m debug/MaRS/HKairport01 \
    --data_device cpu \
    --position_lr_init 0.000016 \
    --scaling_lr 0.001 \
    --percent_dense 0.005 \
    --eval && \
CUDA_VISIBLE_DEVICES=0 python render.py \
    -m debug/HKairport01 && \
CUDA_VISIBLE_DEVICES=0 python metrics.py \
    -m debug/HKairport01
```


## 4. Pixel-GS
---- 
Pixel-GS: Density Control with Pixel-aware Gradient for 3D Gaussian Splatting. Pixel-GS analyzed the reason for the blurry artifacts in 3DGS and propose to optimize the number of points from the perspective of pixels, thereby enabling effectively growing points in areas with insufficient initial points.

#### Conda Environment

Please refer to the original Pixel-GS code

#### UAVScences

Running:

```
CUDA_VISIBLE_DEVICES=0 python train.py \
    -s /HKairport_processed/HKairport01 \
    -m debug/MaRS/HKairport01 \
    --data_device cpu \
    --position_lr_init 0.000016 \
    --scaling_lr 0.001 \
    --percent_dense 0.005 \
    --eval && \
CUDA_VISIBLE_DEVICES=0 python render.py \
    -m debug/HKairport01 && \
CUDA_VISIBLE_DEVICES=0 python metrics.py \
    -m debug/HKairport01
```


## 5. Instant-NGP
---- 
Instant Neural Graphics Primitives with a Multiresolution Hash Encoding. Instant-NGP breaks NeRF training into 3 pillars and proposes improvements to each to enable real-time training of NeRFs.

#### Conda Environment

Please refer to the original Instant-NGP code

#### UAVScences

Running:

```
ns-train instant-ngp --data data/nerfstudio/xxx
```