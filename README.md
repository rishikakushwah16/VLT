Steps to Recreate the code :  create Conda env with python 3.8 and then installing : conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 -c pytorch, then doing pip install -r requirements.txt.

Dataset Prepration : Dowload MSCOCO : http://images.cocodataset.org/zips/train2014.zip  - Train
http://images.cocodataset.org/zips/val2014.zip - Val
karpathy split - Karpathy Split 

Structre : root

├── train2014            
│   ├── COCO_train2014_000000000009.jpg                
|   └── ...
├── val2014              
|   ├── COCO_val2014_000000000042.jpg
|   └── ...          
└── karpathy
    └── dataset_coco.json 

Convert the dataset into pyarrow format and save it to the /home/ViLT/data2/dsets/dataset 
from vilt.utils.write_coco_karpathy import make_arrow
make_arrow(root, arrows_root)

Run the comand for evaluation : CUDA_VISIBLE_DEVICES=0,1 python '/ViLT/run.py' with data_root='/home/ViLT/data2/dsets/dataset/make_arrow' num_gpus=2 num_nodes=1 task_finetune_irtr_coco_randaug per_gpu_batchsize=4 load_path="/weights/vilt_200k_mlm_itm.ckpt"

Reference :
@InProceedings{pmlr-v139-kim21k,
  title = 	 {ViLT: Vision-and-Language Transformer Without Convolution or Region Supervision},
  author =       {Kim, Wonjae and Son, Bokyung and Kim, Ildoo},
  booktitle = 	 {Proceedings of the 38th International Conference on Machine Learning},
  pages = 	 {5583--5594},
  year = 	 {2021},
  editor = 	 {Meila, Marina and Zhang, Tong},
  volume = 	 {139},
  series = 	 {Proceedings of Machine Learning Research},
  month = 	 {18--24 Jul},
  publisher =    {PMLR},
  pdf = 	 {http://proceedings.mlr.press/v139/kim21k/kim21k.pdf},
  url = 	 {http://proceedings.mlr.press/v139/kim21k.html},
  
}
