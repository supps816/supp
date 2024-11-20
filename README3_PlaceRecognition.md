# Placer Recognition

The place recognition basic framework is based on DVGLB (https://github.com/gmberton/deep-visual-geo-localization-benchmark). 

## Requirements

- torch
```
pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118

```

- MinkowskiEngine (ME), to support 3D voxel processing
```
pip install numpy==1.22.4
pip install setuptools==59.8.0

conda install openblas-devel -c anaconda -y
pip install pip==22.3.1
pip install -U git+https://github.com/NVIDIA/MinkowskiEngine -v --no-deps --install-option="--blas_include_dirs=${CONDA_PREFIX}/include" --install-option="--blas=openblas"
```

- Others
```
pip install laspy pytest addict pytorch-metric-learning==0.9.97 yapf==0.40.1 bitarray h5py transforms3d open3d
pip install tqdm setuptools==59.5.0 einops
pip install bagpy utm pptk
pip install pyexr pyntcloud
pip install torchdiffeq
pip install torchsde
pip install torchcde
pip install git+https://github.com/openai/CLIP.git
pip install faiss-cpu

pip install transformers
pip install googledrivedownloader
pip install timm
pip install fast-pytorch-kmeans
pip install kornia opencv-python  
pip install spconv-cu118
pip install transformers timm
pip install nuscenes-devkit utm
pip install tabulate

pip install huggingface-hub==0.24.2
pip install timm==1.0.11
pip install transformers==4.43.3
pip install albumentations
```

## Running
The training codes are in `train.py`, and you need to modify some arguments in `tools/options.py` to ensure right configutations. For example, you need to modify `--dataroot` to the path that you store the UAVScenes dataset.Below we list some demo scripts to conduct training and evaluation.

```
python train.py --cuda 0 --machine 4090 --epochs_num 20 --train_batch_size 16 --final_l2 True --modelq qvanilla2d --qvanilla2d_pool cosplace  --features_dim 256 --db_jitter 0.5  --q_jitter 0.5;

python train.py --cuda 0 --machine 4090 --epochs_num 20 --train_batch_size 16 --final_l2 True --modelq qvanilla2d --qvanilla2d_pool convap  --features_dim 256 --db_jitter 0.5  --q_jitter 0.5;

python train.py --cuda 0 --machine 4090 --epochs_num 20 --train_batch_size 16 --final_l2 True --modelq minklocpp --minklocpp_fusetype add --features_dim 256 --db_jitter 0.5  --q_jitter 0.5;

python train.py --cuda 0 --machine 4090 --epochs_num 20 --train_batch_size 16 --final_l2 True --modelq minkloc3dv2 --features_dim 256 --minkloc3dv2_layers 1_1_1 --db_jitter 0.5  --q_jitter 0.5;
```