# EPIC-Survival 

This repository provides training and testing scripts for the article *EPIC-Survival: End-to-end Part Inferred Clustering for Survival Analysis with Prognostic Stratification Boosting* by **Muhammad and Xie et al. 2021**.

## How to Use
The main training script is `train.py`. Please use `python train.py --help` to see complete set of training parameters and their descriptions.

The tile library (csv) should have the following format:

SlideID | x | y | Duration | Event | Split
------------ | ------------- | -------------| -------------| ------------- | -------------
1 | 24521 | 23426 | 16.2 | 0 | 'train'
1 | 6732 | 3323 | 16.2 | 0 | 'train'
1 | 1232 | 5551 | 16.2 | 0| 'train'
... | ... | ... | ... | ... 
324 | 34265 | 122 | 3.0 | 1 | 'val'
... | ... | ... | ... | ... 
556 | 2264 | 2436 | 174.0 | 1 | 'test'

In short, this tile library should be a record of all tile coordinates with associated slide level information (duration, event, training split, slide name).

The dataloader will load all `.svs` images located at `args.slide_path` during initiation, and pull tiles on-the-fly using the `(x,y)` coordinates during training.

The following will be generated in the output folder:
* convergence.csv
  * a file containing training loss, training concordance index, and validation condorance index over training epochs
* /clustering_grid_top
  * a folder where a clustering visualization for top 20 tiles of each cluster is displayed and saved as a `.png` 

## Python Dependencies
* torch 1.8.1
  * torchvision 0.9.1
* lifelines 0.23.8
* openslide 1.1.1
  * *Note: We recommend modifying openslide to correct for memory leak issue. Please see https://github.com/openslide/openslide-python/issues/24 for more information.*

## License
This project is under the CC-BY-NC 4.0 license. See [LICENSE](LICENSE.md) for details. (c) MSK

## Cite
If you find our work useful, please consider citing our [EPIC-Survival Paper](https://openreview.net/pdf?id=JSSwHS_GU63):
```
@inproceedings{muhammad2021epic,
  title={EPIC-Survival: End-to-end Part Inferred Clustering for Survival Analysis, with Prognostic Stratification Boosting},
  author={Muhammad, Hassan and Xie, Chensu and Sigel, Carlie S and Doukas, Michael and Alpert, Lindsay and Simpson, Amber Lea and Fuchs, Thomas J},
  booktitle={Medical Imaging with Deep Learning},
  year={2021}
}
```
