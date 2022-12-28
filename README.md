# AAI2022Fall-Project
AAI Project: Text-Independent Speaker Identification

**Warning: This repo is only for clean voices, which do not include noises.**

## Main Dependencies

* python 3.8
* torch 1.12.1
* torchaudio 0.12.1
* torchvision 0.13.1

## Forwarding Pipeline
```
.flac -> torchaudio.load -> tensor
tensor -> silding window -> n tensor fragments, same length
fragments -> MFCC transformation -> n spectral tensors, size: H * W
spectral tensors -> CNN models: MFCCNN or ResNet18 -> n predicted labels
predicted labels -> most frequent label -> y_pred

MFCCNN: H=W=64; ResNet18: H=W=224
```

## Usage

```bash
cd model-dz/

# Train
python -u train.py -m mfccnn -g <GPUID> > mfccnn.log 2>&1
python -u train.py -m resnet -g <GPUID> > resnet.log 2>&1

# MFCCNN 0.96 test acc
# ResNet 0.99 test acc

# Inference
python train.py -m mfccnn/resnet -g <GPUID> -f <file_path>.flac
python train.py -m mfccnn/resnet -g <GPUID> # all test files
```
