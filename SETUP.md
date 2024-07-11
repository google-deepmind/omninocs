# OmniNOCS setup

OmniNOCS adds object NOCS annotations to 10 3D datasets: [KITTI],
[Virtual-KITTI], [nuScenes], [Waymo-OD], [Cityscapes], [Hypersim], [Objectron],
[ARKitScenes], and [NOCS-Real275].

## Download Images

The data release includes the NOCS and 3D object annotations. Users are required
to download the images from the respective datasets. We provide here the list of
sources to download data from below. Using OmniNOCS requires agreeing to the
data policy of these datasets.

Dataset            | Download Links
------------------ | --------------
KITTI              | [Images](https://s3.eu-central-1.amazonaws.com/avg-kitti/data_object_image_2.zip)
Virtual KITTI      | [Images](http://download.europe.naverlabs.com//virtual_kitti_2.0.3/vkitti_2.0.3_rgb.tar)
nuScenes           | [v1.0 trainval camera blobs](https://www.nuscenes.org/nuscenes)
Waymo open dataset | [Perception v2.0.0 images, segmentations](https://waymo.com/open/download/)
Cityscapes         | [Left camera Images](https://www.cityscapes-dataset.com/file-handling/?packageID=3)
Hypersim           | [.tonemap.jpg images](https://github.com/facebookresearch/omni3d/blob/main/DATA.md#hypersim)
Objectron          | [Images](https://github.com/google-research-datasets/Objectron/blob/master/notebooks/Download%20Data.ipynb)
ARKitScenes        | [Images](https://github.com/facebookresearch/omni3d/blob/main/DATA.md#arkitscenes)

[KITTI]: http://www.cvlibs.net/datasets/kitti/eval_3dobject.php
[Virtual-KITTI]: https://europe.naverlabs.com/research/computer-vision/proxy-virtual-worlds-vkitti-2/
[Objectron]: https://github.com/google-research-datasets/Objectron
[NOCS-Real275]: https://github.com/hughw19/NOCS_CVPR2019
[Cityscapes]: https://www.cityscapes-dataset.com/
[nuScenes]: https://www.nuscenes.org/
[Waymo-OD]: https://waymo.com/open/
[ARKitScenes]: https://github.com/apple/ARKitScenes
[Hypersim]: https://github.com/apple/ml-hypersim

## Download NOCS annotations

The NOCS annotations for each dataset are provided through the GCP buckets
below:

-   [OmniNOCS data](https://console.cloud.google.com/storage/browser/omninocs-dataset)
    (without the Waymo subset)
-   [OmniNOCS-Waymo subset](https://console.cloud.google.com/storage/browser/omni_nocs)

It is recommended to use the
[gsutil](https://cloud.google.com/storage/docs/gsutil) tool to download them.

The annotations for each data subset of OmniNOCS are provided as a separate
tar.gz file. Each tar.gz contains a folder named
`omninocs_release_<dataset_name>`, which itself contains:

-   a folder with the NOCS images and instance segmentation maps, named after
    the subset (eg: kitti_object).
-   3 metadata files `<train/val/test>_metadata.json` (one for each split) which
    contain path to images, NOCS, segmentation maps, and other object metadata
    (pose, category, size) for each example (see
    [data format](./README.md#data-format)).

Note that these annotations are released under licenses as specified in the
[README](./README.md#license-and-disclaimer).

Move the contents of each OmniNOCS subset to a common `omninocs_root` folder.
This will result in a directory structure as follows:

```
- omninocs_root
  - ARKitScenes/
    - Training
    - Validation
  - ARKitScenes_train_metadata.json
  - ARKitScenes_test_metadata.json
  - ARKitScenes_val_metadata.json
  - Objectron/
  - Objectron_train_metadata.json
  - Objectron_test_metadata.json
  - Objectron_val_metadata.json
  -
  ... (and so on for all constituent datasets)
```

The [colab notebook](./notebooks/OmniNOCS_dataset_visualization.ipynb) shows an
example of parsing OmniNOCS data once downloaded.
