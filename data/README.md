# Dataset

The raw dataset is not stored in this repository.

The notebook downloads the LGG MRI Segmentation dataset automatically with KaggleHub:

```python
kagglehub.dataset_download("mateuszbuda/lgg-mri-segmentation")
```

Dataset page: https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation

Do not commit downloaded MRI images, masks, Kaggle credentials, or local cache files to this directory.
