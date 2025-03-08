
# Frame-wise LiDAR Poinc Cloud Semantic Segmentation
This task is conducted using the Pointcept package (https://github.com/Pointcept/Pointcept), which already supports MinkUNet, SPUNet, and PTv2.


## Split
The split is based on the sequence level. The data root folder is `UAVScenes_ICCVv1/`.
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
The requirement installation instructions are as follows.
```
pip install spconv-cu118

pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118

pip install torch-scatter -f https://data.pyg.org/whl/torch-2.0.0+cu118.html


pip install pyyaml Cython strictyaml tqdm open3d
pip install addict yapf tensorboardX sharedarray scipy timm
pip install torch_geometric
pip install pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-2.0.0+cu118.html
pip install einops open3d tomli platformdirs

pip install numpy==1.22.4
pip install setuptools==59.8.0
conda install openblas-devel -c anaconda -y
pip install pip==22.3.1
pip install -U git+https://github.com/NVIDIA/MinkowskiEngine -v --no-deps --install-option="--blas_include_dirs=${CONDA_PREFIX}/include" --install-option="--blas=openblas"

pip install open3d tomli platformdirs numpy==1.24.4

```





## Running
You need to change the data root folder in each config file, e.g., `configs/uavscenes/semseg-minkunet34c-0-base.py`. 
```bash
sh scripts/train.sh -p python -d uavscenes -c semseg-pt-v2m2-0-base -n semseg-pt-v2m2-0-base --g 2

sh scripts/train.sh -p python -d uavscenes -c semseg-spunet-v1m1-0-base -n semseg-spunet-v1m1-0-base --g 2

sh scripts/train.sh -p python -d uavscenes -c semseg-minkunet34c-0-base -n semseg-minkunet34c-0-base --g 2

```