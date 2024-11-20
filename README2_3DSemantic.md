# 3D Semantic Segmentation Baseline

## 1. PVKD
---- 
The Point-to-Voxel Knowledge Distillation (PVD) is a framework designed to compress LiDAR semantic segmentation models by transferring knowledge from a large teacher model to a compact student model. PVD integrates both point-level and voxel-level distillation and employs difficulty-aware sampling and supervoxel partitioning to efficiently capture structural and semantic information, achieving state-of-the-art results on benchmarks like SemanticKITTI and nuScenes.

#### Conda Environment

```bash
conda create -n pvkd python=3.7
conda activate pvkd
pip install torch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 --index-url https://download.pytorch.org/whl/cu121
pip install spconv-cu120
pip install Cython==3.0.11
pip install yaml
pip install torch-scatter 
```
>  Note:  Make sure that the `torch-scatter` version matches your CUDA, PyTorch, and Python versions. Incompatible versions may cause errors.

#### UAVScences

#### Please ensure that the data_path variable is correctly set in the configuration file located at `/Codes-for-PVKD/config/uavscenes.yaml`. This should point to the root directory of your dataset.

Running:

```
python -u train_cyl_sem.py
```





## 2. Cylinder3D
----

 The source code of our work **"Cylindrical and Asymmetrical 3D Convolution Networks for LiDAR Segmentation**
![img|center](./img/pipeline.png)

Cylinder3D is a 3D deep learning framework for outdoor LiDAR segmentation, utilizing **cylindrical partition** and **asymmetrical 3D convolution networks** to address the challenges of point cloud sparsity and varying density. The method achieves state-of-the-art performance on SemanticKITTI and nuScenes datasets, demonstrating strong generalization capability to tasks such as LiDAR panoptic segmentation and 3D object detection.


#### Conda Environment

```bash
conda create -n cylinder python=3.7
conda activate cylinder
pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
pip install spconv-cu114
pip install Cython==3.0.11
pip install yaml
pip install torch-scatter 
```
>  Note:  Make sure that the `torch-scatter` version matches your CUDA, PyTorch, and Python versions. Incompatible versions may cause errors.

#### UAVScences

#### Please ensure that the data_path variable is correctly set in the configuration file located at `/Cylinder3D/config/uavscenes.yaml`. This should point to the root directory of your dataset.

Running:

```
sh train.sh
```





## 3. PointCept (PTv2)

#### Installation

#### Requirements
- Ubuntu: 18.04 and above.
- CUDA: 11.3 and above.
- PyTorch: 1.10.0 and above.

#### Conda Environment

```bash
conda create -n pointcept python=3.8 -y
conda activate pointcept
conda install ninja -y
# Choose version you want here: https://pytorch.org/get-started/previous-versions/
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch -y
conda install h5py pyyaml -c anaconda -y
conda install sharedarray tensorboard tensorboardx yapf addict einops scipy plyfile termcolor timm -c conda-forge -y
conda install pytorch-cluster pytorch-scatter pytorch-sparse -c pyg -y
pip install torch-geometric

# spconv (SparseUNet)
# refer https://github.com/traveller59/spconv
pip install spconv-cu113

# PPT (clip)
pip install ftfy regex tqdm
pip install git+https://github.com/openai/CLIP.git

# PTv1 & PTv2 or precise eval
cd libs/pointops
# usual
python setup.py install
# docker & multi GPU arch
TORCH_CUDA_ARCH_LIST="ARCH LIST" python  setup.py install
# e.g. 7.5: RTX 3000; 8.0: a100 More available in: https://developer.nvidia.com/cuda-gpus
TORCH_CUDA_ARCH_LIST="7.5 8.0" python  setup.py install
cd ../..

# Open3D (visualization, optional)
pip install open3d
```

**PTv2 mode2**

The original PTv2 was trained on 4 * RTX a6000 (48G memory). Even enabling AMP, the memory cost of the original PTv2 is slightly larger than 24G. Considering GPUs with 24G memory are much more accessible, I tuned the PTv2 on the latest Pointcept and made it runnable on 4 * RTX 3090 machines.

`PTv2 Mode2` enables AMP and disables _Position Encoding Multiplier_ & _Grouped Linear_. During our further research, we found that precise coordinates are not necessary for point cloud understanding (Replacing precise coordinates with grid coordinates doesn't influence the performance. Also, SparseUNet is an example). As for Grouped Linear, my implementation of Grouped Linear seems to cost more memory than the Linear layer provided by PyTorch. Benefiting from the codebase and better parameter tuning, we also relieve the overfitting problem. The reproducing performance is even better than the results reported in our paper.

#### UAVScences


#### Please ensure that the data_root variable is correctly set in the configuration file located at `/Pointcept/configs/uavscenes`. This should point to the root directory of your dataset.

Running:

```
sh scripts/train.sh -g 3 -d uavscenes -c semseg-pt-v2m2-0-base -n semseg-pt-v2m2-0-base
```
Parameter Explanation

-g: Specifies the number of GPUs to use during training. For example, -g 3 indicates that 3 GPUs will be utilized.

-d: Indicates the dataset name (e.g., uavscenes).

-c: Specifies the configuration file to use for training (e.g., semseg-pt-v2m2-0-base).

-n: Name of the training job or experiment, used for logging purposes.





## 4. WaffleIron

[**Using a Waffle Iron for Automotive Point Cloud Semantic Segmentation**](http://arxiv.org/abs/2301.10100)  
[*Gilles Puy*<sup>1</sup>](https://sites.google.com/site/puygilles/home),
[*Alexandre Boulch*<sup>1</sup>](http://boulch.eu),
[*Renaud Marlet*<sup>1,2</sup>](http://imagine.enpc.fr/~marletr/)  
<sup>1</sup>*valeo.ai, France* and <sup>2</sup>*LIGM, Ecole des Ponts, Univ Gustave Eiffel, CNRS, France*.

#### Model Overview

- **48 layers (L)**: The model consists of 48 layers, each performing a **token-mixing** and **channel-mixing** operation. Token-mixing utilizes dense 2D convolutions to extract spatial features, while channel-mixing uses MLPs to mix features across channels.
- **256-dimensional tokens (F)**: Each point in the input point cloud is represented by a 256-dimensional feature vector, updated iteratively through the 48 layers.
- **Grid Resolution (ρ)**: Points are projected onto 2D grids with a default resolution of 40–60 cm during 2D convolution operations.

#### Installation

We use the following environment:
```
conda create -n waffleiron
conda activate waffleiron
conda install pytorch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 pytorch-cuda=12.1 -c pytorch -c nvidia
pip install pyaml==23.12.0 tqdm==4.63.0 scipy==1.13.1 tensorboard==2.16.2
git clone https://github.com/valeoai/WaffleIron
cd WaffleIron
pip install -e ./
```


#### UAVScences
Running:

To retrain the WaffleIron-48-256 backbone, type
```

python launch_train.py \
--dataset uavscenes \
--path_dataset /UAVScenes/ \
--log_path /log \
--config ./configs/uavscenes.yaml \
--multiprocessing-distributed \
--fp16 

```