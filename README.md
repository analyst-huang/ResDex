# ResDex

Official code for **"Efficient Residual Learning with Mixture-of-Experts for Universal Dexterous Grasping"** *(ICLR 2025)*

![Demo](fig/demo.gif)
*For detailed information, please refer to our [paper](https://openreview.net/pdf?id=BUj9VSCoET).*


## Installation

### 1. Clone repository:
```bash
git clone https://github.com/analyst-huang/ResDex.git
cd ResDex
```

### 2. Create conda environment:
```bash
conda create -n resdex python=3.8
conda activate resdex
```

### 3. Install IsaacGym
Download Isaac Gym Preview 4 [here](https://developer.nvidia.com/isaac-gym-preview-4) and follow the installation document.

### 4. Install dependencies:
```bash
pip install -r requirements.txt
```

### 5. Install PointNet2:
You can download PointNet2 [here](https://disk.pku.edu.cn/link/AA3F49C82F397249CB83955009C32970CB).
```bash
unzip Pointnet2_PyTorch-master.zip
cd Pointnet2_PyTorch-master
pip install -e .
cd pointnet2_ops_lib
pip install -e .
```

## Data Preparation
The datasets are organized as:
```
assets/
├── datasetv4.1/
├── meshdatav3_pc_feat/
├── meshdatav3_scaled/
├── pcldata/
├── ......
```
We provide an example object in `assets`. 3200 training objects are specified in `train_set.yaml`. The testing objects are specified in `test_set_seen_cat.yaml` and `test_set_unseen_cat.yaml`. You can download the complete dataset [here](https://mirrors.pku.edu.cn/dl-release/UniDexGrasp_CVPR2023/dexgrasp_policy/assets/) for `datasetv4.1`, `meshdatav3_pc_feat` and `meshdatav3_scaled`.
After downloading `meshdatav3_scaled` and put it to the corresponding place in `assets`, you can get `pcldata` by running the following command:
```python
python script/preprocess_pcl.py
```

## Training & Evaluation

**Base Policy:**
```bash
bash script/train_blind.sh
```

**Residual Policy:**
```bash
bash script/train_residual.sh
```

**Dagger Distillation:**
```bash
bash script/train_dagger_vision.sh
```

**Evaluation:**
```bash
# Base policy
bash script/test_blind.sh

# Residual policy
bash script/test_residual.sh

# Vision policy
bash script/test_dagger_vision.sh
```

## Acknowledgement
This project is built upon [UnidexGrasp](https://github.com/PKU-EPIC/UniDexGrasp).
