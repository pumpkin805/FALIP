# FALIP: Visual Prompt as Foveal Attention Boosts CLIP Zero-Shot Performance
This repository contains the code for the paper [FALIP: Visual Prompt as Foveal Attention Boosts CLIP Zero-Shot Performance](https://arxiv.org/abs/2407.05578)
(ECCV 2024).

## Data Download
Download preprocessed data files via `gsutil cp gs://reclip-sanjays/reclip_data.tar.gz`, and extract the data using `tar -xvzf reclip_data.tar.gz`. This data
does not include images.
Download the images for RefCOCO/g/+ from [http://images.cocodataset.org/zips/train2014.zip](http://images.cocodataset.org/zips/train2014.zip).

## Results with CLIP
The following format can be used to run experiments:
```
pip install -r requirements.txt
python main.py --input_file INPUT_FILE --image_root IMAGE_ROOT --method baseline --box_method_aggregator sum --clip_model ViT-B/16 --box_representation_method box --detector_file PATH_TO_DETECTOR_FILE
```

`--input_file`: should be in `.jsonl` format (we provide these files for the datasets discussed in our paper; see the Data Download information above).

`--image_root`: the top-level directory containing all images in the dataset. For RefCOCO/g/+, this is the `train2014` directory.

`--detector_file`: if not specified, ground-truth proposals are used. For RefCOCO/g/+, the detection files are in `reclip_data.tar.gz` and have the format `{refcoco/refcocog/refcoco+}_dets_dict.json`.

Choices for `method`: "parse" is the full version of ReCLIP that includes isolated proposal scoring and the heuristic-based relation handling system. "baseline" is the version of ReCLIP using only isolated proposal scoring. "gradcam" uses GradCAM, and "random" selects one of the proposals uniformly at random. (default: "baseline")

Choices for `clip_model`: The choices are the same as the model names used in the CLIP repository except that the model names can be concatenated with a comma between consecutive names. (default: "ViT-B/16")

Choices for `box_representation_method`: This argument dictates which of the following methods is used to score proposals: CPT-adapted, cropping, blurring, or some combination of these. For CPT-adapted, choose "shade". To use more than one method, concatenate them with a comma between consecutive methods. (default: "box")

To see explanations of other arguments see the `main.py` file.

## Acknowledgements
Thanks to the codebase [ReCLIP](https://github.com/allenai/reclip).

## Citation
If you find this repository useful, please cite our paper:
```
@article{zhuang2024falip,
  title={FALIP: Visual Prompt as Foveal Attention Boosts CLIP Zero-Shot Performance},
  author={Zhuang, Jiedong and Hu, Jiaqi and Mu, Lianrui and Hu, Rui and Liang, Xiaoyu and Ye, Jiangnan and Hu, Haoji},
  journal={arXiv preprint arXiv:2407.05578},
  year={2024}
}
```
