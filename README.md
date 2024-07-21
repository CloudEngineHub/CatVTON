

# <center> 🐈 CatVTON: Concatenation Is All You Need for Virtual Try-On with Diffusion Models

<p align="center">
  <a href="https://github.com/Zheng-Chong/CatVTON">
    <img src='https://img.shields.io/badge/arXiv-Paper(soon)-red?style=flat&logo=arXiv&logoColor=red' alt='arxiv'>
  </a>
  <a href="http://120.76.142.206:8888">
    <img src='https://img.shields.io/badge/Demo-Gradio-orange?style=flat&logo=Gradio&logoColor=red' alt='Demo'>
  </a>
  <a href='https://huggingface.co/zhengchong/CatVTON'>
    <img src='https://img.shields.io/badge/Hugging Face-ckpts-orange?style=flat&logo=HuggingFace&logoColor=orange' alt='huggingface'>
  </a>
  <a href="https://github.com/Zheng-Chong/CatVTON">
    <img src='https://img.shields.io/badge/GitHub-Repo-blue?style=flat&logo=GitHub' alt='GitHub'>
  </a>
    <a href="https://github.com/Zheng-Chong/CatVTON/LICENCE"><img src='https://img.shields.io/badge/License-CC BY--NC--SA--4.0-lightgreen?style=flat&logo=Lisence' alt='License'>
  </a>
</p>

<div align="center">
  <img src="resource/img/teaser.jpg" width="100%" height="100%"/>
</div>

<!-- This repository is the official implementation of ***CatVTON: Concatenation Is All You Need for Virtual Try-On with Diffsuion Models***. -->

**CatVTON** is a simple and efficient virtual try-on diffusion model with ***1) Lightweight Network (899.06M parameters totally)***, ***2) Parameter-Efficient Training (49.57M parameters trainable)*** and ***3) Simplified Inference (< 8G VRAM for 1024X768 resolution)***.


## Updates
- **`2024/7/21`**: Our **Inference Code** and [**🤗Weights**](https://huggingface.co/zhengchong/CatVTON) are released.
- **`2024/7/11`**: [**Online Demo**](http://120.76.142.206:8888) is released.



## Inference
### Data Preparation
Before inference, you need to download the [VITON-HD](https://github.com/shadow2496/VITON-HD) or [DressCode](https://github.com/aimagelab/dress-code) dataset.
Once the datasets are downloaded, the folder structures should look like these:
```
├── VITON-HD
|   ├── test_pairs_unpaired.txt
│   ├── test
|   |   ├── image
│   │   │   ├── [000006_00.jpg | 000008_00.jpg | ...]
│   │   ├── cloth
│   │   │   ├── [000006_00.jpg | 000008_00.jpg | ...]
│   │   ├── agnostic-mask
│   │   │   ├── [000006_00_mask.png | 000008_00.png | ...]
...
```
For DressCode dataset, we provide [our preprocessed agnostic masks](https://drive.google.com/drive/folders/1uT88nYQl0n5qHz6zngb9WxGlX4ArAbVX?usp=share_link), download and place in `agnostic_masks` folders under each category.
```
├── DressCode
|   ├── test_pairs_paired.txt
|   ├── test_pairs_unpaired.txt
│   ├── [dresses | lower_body | upper_body]
|   |   ├── test_pairs_paired.txt
|   |   ├── test_pairs_unpaired.txt
│   │   ├── images
│   │   │   ├── [013563_0.jpg | 013563_1.jpg | 013564_0.jpg | 013564_1.jpg | ...]
│   │   ├── agnostic_masks
│   │   │   ├── [013563_0.png| 013564_0.png | ...]
...
```

### Inference on VTIONHD/DressCode
To run the inference on the DressCode or VITON-HD dataset, run the following command, checkpoints will be automaticly download from HuggingFace.

```PowerShell
CUDA_VISIBLE_DEVICES=0 python inference.py \
--dataset [dresscode | vitonhd] \
--data_root_path <path> \
--output_dir <path> 
--dataloader_num_workers 8 \
--batch_size 8 \
--seed 555 \
--mixed_precision [no | fp16 | bf16] \
--allow_tf32 \
--repaint \
--eval_pair  
```


## Acknowledgement
Our code is modified based on [Diffusers](https://github.com/huggingface/diffusers). We use [SCHP](https://github.com/GoGoDuck912/Self-Correction-Human-Parsing/tree/master) and [DensePose](https://github.com/facebookresearch/DensePose) to automaticly generate mask in our [Gradio](https://github.com/gradio-app/gradio) App. Thanks to all the contributors!
<!-- ## Citation


```
``` -->