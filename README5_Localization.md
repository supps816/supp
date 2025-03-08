# 6-DoF Visual Localization


## 0. Preprocess
Please perform data preprocessing first and replace the path with the corresponding scenes in each UAVScenes. This data preprocessing is based on the data processed by the NVS task. Then, load the path to the SCR task according to the region name.
```
python setup_uavscenes.py
```
### Split
The data split is based on the sequence level. 
```
Train: 
    AMtown01
    AMtown02   
Test: 
    AMtown03

Train: 
    AMvalley01
    AMvalley02   
Test: 
    AMvalley03

Train: 
    HKairport01
    HKairport02   
Test: 
    HKairport03

Train: 
    HKisland01
    HKisland02   
Test: 
    HKisland03
```


## 1. ACE
---- 
Accelerated Coordinate Encoding: Learning to Relocalize in Minutes using RGB and Poses. ACE, a scene coordinate regression system that maps a new scene in 5 minutes. Previous state-of-the-art scene coordinate regression systems require hours of mapping to achieve comparable relocalization accuracy.

#### Conda Environment

Please refer to the original ACE code

#### UAVScences

Running:

```
./train_ace.py /AMtown/ output/AMtown.pt --epochs 320
```

```
./test_ace.py /AMtown/ output/AMtown.pt
```


## 2. GLACE
---- 
GLACE: Global Local Accelerated Coordinate Encoding. GLACE is the first attempt of an SCR method to achieve state-of-the-art performance on large-scale scenes without using an ensemble of networks or 3D model supervision.

#### Conda Environment

Please refer to the original GLACE code

#### UAVScences

Running:

```
./train_ace.py /AMtown/ output/AMtown.pt --max_iterations 60000
```

```
./test_ace.py /AMtown/ output/AMtown.pt
```


## 3. FocusTune
---- 
FocusTune: Tuning Visual Localization through Focus-Guided Sampling. FocusTune, a focus-guided heuristic sampling strategy to avoid optimizing parts of the scene that are non-informative and instead leveraging geometrical constraints. FocusTune incurs minimal computational overhead.

#### Conda Environment

Please refer to the original FocusTune code

#### UAVScences

Running:

```
./train_ace.py /AMtown/ output/AMtown.pt --epochs 320
```

```
./test_ace.py /AMtown/ output/AMtown.pt
```


## 4. PoseNet
---- 
Posenet: A convolutional network for real-time 6-dof camera relocalization. 

#### Conda Environment

Please refer to the original PoseNet code

#### UAVScences

Running:

```
python train.py --image_path /AMtown

```

```
python test.py --image_path /AMtown
```


## 5. AtLoc
---- 
Atloc: Attention guided camera localization.

#### Conda Environment

Please refer to the original AtLoc code

#### UAVScences

Running:

```
python train.py --image_path /AMtown

```

```
python test.py --image_path /AMtown
```


## 6. RobustLoc
---- 
RobustLoc: Robust camera pose regression in challenging driving environments. 

#### Conda Environment

Please refer to the original RobustLoc code

#### UAVScences

Running:

```
python train.py --image_path /AMtown

```

```
python test.py --image_path /AMtown
```