# Cascade R-CNN: Delving into High Quality Object Detection

by Zhaowei Cai and Nuno Vasconcelos

This repository is written by Zhaowei Cai at UC San Diego, on the base of [Detectron](https://github.com/facebookresearch/Detectron) @ [e8942c8](https://github.com/facebookresearch/Detectron/tree/e8942c882abf6e28fe68a626ec55028c9bdfe1cf).

## Introduction

This repository re-implements Cascade R-CNN on the base of [Detectron](https://github.com/facebookresearch/Detectron). Very consistent gains are available for all tested models, regardless of baseline strength.

Please follow [Detectron](https://github.com/facebookresearch/Detectron) on how to install and use Detectron-Cascade-RCNN.

It is also recommended to use our original implementation, [cascade-rcnn](https://github.com/zhaoweicai/cascade-rcnn) based on Caffe, and the third-party implementation, [mmdetection](https://github.com/open-mmlab/mmdetection) based on PyTorch and [tensorpack](https://github.com/tensorpack/tensorpack/tree/master/examples/FasterRCNN) based on TensorFlow.

## Citation

If you use our code/model/data, please cite our paper:

```
@inproceedings{cai18cascadercnn,
  author = {Zhaowei Cai and Nuno Vasconcelos},
  Title = {Cascade R-CNN: Delving into High Quality Object Detection},
  booktitle = {CVPR},
  Year  = {2018}
}
```

or its extension:

```
@article{cai2019cascadercnn,
  author = {Zhaowei Cai and Nuno Vasconcelos},
  title = {Cascade R-CNN: High Quality Object Detection and Instance Segmentation},
  journal = {arXiv preprint arXiv:1906.09756},
  year = {2019}
}
```

and Detectron:

```
@misc{Detectron2018,
  author =       {Ross Girshick and Ilija Radosavovic and Georgia Gkioxari and
                  Piotr Doll\'{a}r and Kaiming He},
  title =        {Detectron},
  howpublished = {\url{https://github.com/facebookresearch/detectron}},
  year =         {2018}
}
```

## Benchmarking

### End-to-End Faster & Mask R-CNN Baselines

<table><tbody>
<!-- START E2E FASTER AND MASK TABLE -->
<!-- TABLE HEADER -->
<!-- Info: we use wrap text in <sup><sub></sub><sup> to make is small -->
<th valign="bottom"><sup><sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;backbone&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</sub></sup></th>
<th valign="bottom"><sup><sub>type</sub></sup></th>
<th valign="bottom"><sup><sub>lr<br/>schd</sub></sup></th>
<th valign="bottom"><sup><sub>im/<br/>gpu</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>download<br/>links</sub></sup></th>
<!-- TABLE BODY -->
<tr>
<td align="left"><sup><sub>R-50-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>36.7</sub></sup></td>
<td align="right"><sup><sub>58.4</sub></sup></td>
<td align="right"><sup><sub>39.6</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/35857345/12_2017_baselines/e2e_faster_rcnn_R-50-FPN_1x.yaml.01_36_30.cUF7QR7I/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35857345/12_2017_baselines/e2e_faster_rcnn_R-50-FPN_1x.yaml.01_36_30.cUF7QR7I/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>40.9</sub></sup></td>
<td align="right"><sup><sub>59.0</sub></sup></td>
<td align="right"><sup><sub>44.6</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/R50-FPN-cascade-rcnn.pkl">model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R50-FPN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>39.4</sub></sup></td>
<td align="right"><sup><sub>61.2</sub></sup></td>
<td align="right"><sup><sub>43.4</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/35857890/12_2017_baselines/e2e_faster_rcnn_R-101-FPN_1x.yaml.01_38_50.sNxI7sX7/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35857890/12_2017_baselines/e2e_faster_rcnn_R-101-FPN_1x.yaml.01_38_50.sNxI7sX7/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>42.8</sub></sup></td>
<td align="right"><sup><sub>61.4</sub></sup></td>
<td align="right"><sup><sub>46.1</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/R101-FPN-cascade-rcnn.pkl">model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R101-FPN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-64x4d-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>41.5</sub></sup></td>
<td align="right"><sup><sub>63.8</sub></sup></td>
<td align="right"><sup><sub>44.9</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/35858015/12_2017_baselines/e2e_faster_rcnn_X-101-64x4d-FPN_1x.yaml.01_40_54.1xc565DE/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35858015/12_2017_baselines/e2e_faster_rcnn_X-101-64x4d-FPN_1x.yaml.01_40_54.1xc565DE/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-64x4d-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>45.4</sub></sup></td>
<td align="right"><sup><sub>64.0</sub></sup></td>
<td align="right"><sup><sub>49.8</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_X101-64x4d-FPN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-32x8d-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>41.3</sub></sup></td>
<td align="right"><sup><sub>63.7</sub></sup></td>
<td align="right"><sup><sub>44.7</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/36761737/12_2017_baselines/e2e_faster_rcnn_X-101-32x8d-FPN_1x.yaml.06_31_39.5MIHi1fZ/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/36761737/12_2017_baselines/e2e_faster_rcnn_X-101-32x8d-FPN_1x.yaml.06_31_39.5MIHi1fZ/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-32x8d-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>44.7</sub></sup></td>
<td align="right"><sup><sub>63.7</sub></sup></td>
<td align="right"><sup><sub>48.8</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_X101-32x8d-FPN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>37.7</sub></sup></td>
<td align="right"><sup><sub>59.2</sub></sup></td>
<td align="right"><sup><sub>40.9</sub></sup></td>
<td align="right"><sup><sub>33.9</sub></sup></td>
<td align="right"><sup><sub>55.8</sub></sup></td>
<td align="right"><sup><sub>35.8</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/35858933/12_2017_baselines/e2e_mask_rcnn_R-50-FPN_1x.yaml.01_48_14.DzEQe4wC/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35858933/12_2017_baselines/e2e_mask_rcnn_R-50-FPN_1x.yaml.01_48_14.DzEQe4wC/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35858933/12_2017_baselines/e2e_mask_rcnn_R-50-FPN_1x.yaml.01_48_14.DzEQe4wC/output/test/coco_2014_minival/generalized_rcnn/segmentations_coco_2014_minival_results.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>41.3</sub></sup></td>
<td align="right"><sup><sub>59.6</sub></sup></td>
<td align="right"><sup><sub>44.9</sub></sup></td>
<td align="right"><sup><sub>35.4</sub></sup></td>
<td align="right"><sup><sub>56.2</sub></sup></td>
<td align="right"><sup><sub>37.8</sub></sup></td>
<td align="left"><sup><sub><a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/R50-FPN-cascade-rcnn-mask.pkl">model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R50-FPN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_R50-FPN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>40.0</sub></sup></td>
<td align="right"><sup><sub>61.8</sub></sup></td>
<td align="right"><sup><sub>43.7</sub></sup></td>
<td align="right"><sup><sub>35.9</sub></sup></td>
<td align="right"><sup><sub>58.3</sub></sup></td>
<td align="right"><sup><sub>38.0</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/35861795/12_2017_baselines/e2e_mask_rcnn_R-101-FPN_1x.yaml.02_31_37.KqyEK4tT/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35861795/12_2017_baselines/e2e_mask_rcnn_R-101-FPN_1x.yaml.02_31_37.KqyEK4tT/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/35861795/12_2017_baselines/e2e_mask_rcnn_R-101-FPN_1x.yaml.02_31_37.KqyEK4tT/output/test/coco_2014_minival/generalized_rcnn/segmentations_coco_2014_minival_results.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>43.3</sub></sup></td>
<td align="right"><sup><sub>61.7</sub></sup></td>
<td align="right"><sup><sub>47.2</sub></sup></td>
<td align="right"><sup><sub>37.1</sub></sup></td>
<td align="right"><sup><sub>58.6</sub></sup></td>
<td align="right"><sup><sub>39.8</sub></sup></td>
<td align="left"><sup><sub><a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/R101-FPN-cascade-rcnn-mask.pkl">model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R101-FPN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_R101-FPN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-64x4d-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>42.4</sub></sup></td>
<td align="right"><sup><sub>64.3</sub></sup></td>
<td align="right"><sup><sub>46.4</sub></sup></td>
<td align="right"><sup><sub>37.5</sub></sup></td>
<td align="right"><sup><sub>60.6</sub></sup></td>
<td align="right"><sup><sub>39.9</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/36494496/12_2017_baselines/e2e_mask_rcnn_X-101-64x4d-FPN_1x.yaml.07_50_11.fkwVtEvg/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/36494496/12_2017_baselines/e2e_mask_rcnn_X-101-64x4d-FPN_1x.yaml.07_50_11.fkwVtEvg/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/36494496/12_2017_baselines/e2e_mask_rcnn_X-101-64x4d-FPN_1x.yaml.07_50_11.fkwVtEvg/output/test/coco_2014_minival/generalized_rcnn/segmentations_coco_2014_minival_results.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-64x4d-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>45.9</sub></sup></td>
<td align="right"><sup><sub>64.4</sub></sup></td>
<td align="right"><sup><sub>50.2</sub></sup></td>
<td align="right"><sup><sub>38.8</sub></sup></td>
<td align="right"><sup><sub>61.3</sub></sup></td>
<td align="right"><sup><sub>41.6</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_X101-64x4d-FPN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_X101-64x4d-FPN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-32x8d-FPN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>42.1</sub></sup></td>
<td align="right"><sup><sub>64.1</sub></sup></td>
<td align="right"><sup><sub>45.9</sub></sup></td>
<td align="right"><sup><sub>37.3</sub></sup></td>
<td align="right"><sup><sub>60.3</sub></sup></td>
<td align="right"><sup><sub>39.5</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/36761843/12_2017_baselines/e2e_mask_rcnn_X-101-32x8d-FPN_1x.yaml.06_35_59.RZotkLKI/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/36761843/12_2017_baselines/e2e_mask_rcnn_X-101-32x8d-FPN_1x.yaml.06_35_59.RZotkLKI/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/36761843/12_2017_baselines/e2e_mask_rcnn_X-101-32x8d-FPN_1x.yaml.06_35_59.RZotkLKI/output/test/coco_2014_minival/generalized_rcnn/segmentations_coco_2014_minival_results.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-101-32x8d-FPN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>45.8</sub></sup></td>
<td align="right"><sup><sub>64.1</sub></sup></td>
<td align="right"><sup><sub>50.3</sub></sup></td>
<td align="right"><sup><sub>38.6</sub></sup></td>
<td align="right"><sup><sub>60.6</sub></sup></td>
<td align="right"><sup><sub>41.5</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_X101-32x8d-FPN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_X101-32x8d-FPN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<!-- END E2E FASTER AND MASK TABLE -->
</tbody></table>

### Mask R-CNN with Bells & Whistles

<table><tbody>
<!-- START BELLS TABLE -->
<!-- TABLE HEADER -->
<!-- Info: we use wrap text in <sup><sub></sub><sup> to make is small -->
<th valign="bottom"><sup><sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;backbone&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</sub></sup></th>
<th valign="bottom"><sup><sub>type</sub></sup></th>
<th valign="bottom"><sup><sub>lr<br/>schd</sub></sup></th>
<th valign="bottom"><sup><sub>im/<br/>gpu</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>download<br/>links</sub></sup></th>
<!-- TABLE BODY -->
<tr>
<td align="left"><sup><sub>X-152-32x8d-FPN-IN5k-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>s1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>48.1</sub></sup></td>
<td align="right"><sup><sub>68.3</sub></sup></td>
<td align="right"><sup><sub>52.9</sub></sup></td>
<td align="right"><sup><sub>41.5</sub></sup></td>
<td align="right"><sup><sub>65.1</sub></sup></td>
<td align="right"><sup><sub>44.7</sub></sup></td>
<td align="left"><sup><sub><a href="https://s3-us-west-2.amazonaws.com/detectron/37129812/12_2017_baselines/e2e_mask_rcnn_X-152-32x8d-FPN-IN5k_1.44x.yaml.09_35_36.8pzTQKYK/output/train/coco_2014_train%3Acoco_2014_valminusminival/generalized_rcnn/model_final.pkl">model</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/37129812/12_2017_baselines/e2e_mask_rcnn_X-152-32x8d-FPN-IN5k_1.44x.yaml.09_35_36.8pzTQKYK/output/test/coco_2014_minival/generalized_rcnn/bbox_coco_2014_minival_results.json">boxes</a>&nbsp;|&nbsp;<a href="https://s3-us-west-2.amazonaws.com/detectron/37129812/12_2017_baselines/e2e_mask_rcnn_X-152-32x8d-FPN-IN5k_1.44x.yaml.09_35_36.8pzTQKYK/output/test/coco_2014_minival/generalized_rcnn/segmentations_coco_2014_minival_results.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>[above without test-time aug.]</sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub>45.2</sub></sup></td>
<td align="right"><sup><sub>66.9</sub></sup></td>
<td align="right"><sup><sub>49.7</sub></sup></td>
<td align="right"><sup><sub>39.7</sub></sup></td>
<td align="right"><sup><sub>63.5</sub></sup></td>
<td align="right"><sup><sub>42.4</sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>X-152-32x8d-FPN-IN5k-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>s1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>50.2</sub></sup></td>
<td align="right"><sup><sub>68.2</sub></sup></td>
<td align="right"><sup><sub>55.0</sub></sup></td>
<td align="right"><sup><sub>42.3</sub></sup></td>
<td align="right"><sup><sub>65.4</sub></sup></td>
<td align="right"><sup><sub>45.8</sub></sup></td>
<td align="left"><sup><sub><a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/X152-32x8d-FPN-cascade-rcnn-mask-aug.pkl">model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_X152-32x8d-FPN-cascade-rcnn-mask-aug.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_X152-32x8d-FPN-cascade-rcnn-mask-aug.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>[above without test-time aug.]</sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
<td align="right"><sup><sub>48.1</sub></sup></td>
<td align="right"><sup><sub>66.7</sub></sup></td>
<td align="right"><sup><sub>52.6</sub></sup></td>
<td align="right"><sup><sub>40.7</sub></sup></td>
<td align="right"><sup><sub>63.7</sub></sup></td>
<td align="right"><sup><sub>43.8</sub></sup></td>
<td align="right"><sup><sub></sub></sup></td>
</tr>
<!-- END BELLS TABLE -->
</tbody></table>

### Faster & Mask R-CNN with GN

<table><tbody>
<!-- START E2E FASTER AND MASK TABLE -->
<!-- TABLE HEADER -->
<!-- Info: we use wrap text in <sup><sub></sub><sup> to make is small -->
<th valign="bottom"><sup><sub>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;backbone&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</sub></sup></th>
<th valign="bottom"><sup><sub>type</sub></sup></th>
<th valign="bottom"><sup><sub>lr<br/>schd</sub></sup></th>
<th valign="bottom"><sup><sub>im/<br/>gpu</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>box<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP50</sub></sup></th>
<th valign="bottom"><sup><sub>mask<br/>AP75</sub></sup></th>
<th valign="bottom"><sup><sub>download<br/>links</sub></sup></th>
<!-- TABLE BODY -->
<tr>
<td align="left"><sup><sub>R-50-FPN-GN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>38.4</sub></sup></td>
<td align="right"><sup><sub>59.9</sub></sup></td>
<td align="right"><sup><sub>41.7</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-GN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>42.2</sub></sup></td>
<td align="right"><sup><sub>60.6</sub></sup></td>
<td align="right"><sup><sub>45.8</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R50-FPN-GN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-GN-baseline</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>39.9</sub></sup></td>
<td align="right"><sup><sub>61.3</sub></sup></td>
<td align="right"><sup><sub>43.3</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-GN-cascade</sub></sup></td>
<td align="left"><sup><sub>Faster</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>43.8</sub></sup></td>
<td align="right"><sup><sub>62.2</sub></sup></td>
<td align="right"><sup><sub>47.6</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="right"><sup><sub>-</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R101-FPN-GN-cascade-rcnn.json">boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-GN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>39.2</sub></sup></td>
<td align="right"><sup><sub>60.5</sub></sup></td>
<td align="right"><sup><sub>42.9</sub></sup></td>
<td align="right"><sup><sub>34.9</sub></sup></td>
<td align="right"><sup><sub>57.1</sub></sup></td>
<td align="right"><sup><sub>36.9</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;boxes</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-50-FPN-GN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>42.9</sub></sup></td>
<td align="right"><sup><sub>60.7</sub></sup></td>
<td align="right"><sup><sub>46.6</sub></sup></td>
<td align="right"><sup><sub>36.6</sub></sup></td>
<td align="right"><sup><sub>57.7</sub></sup></td>
<td align="right"><sup><sub>39.2</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R50-FPN-GN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_R50-FPN-GN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-GN-baseline</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>2</sub></sup></td>
<td align="right"><sup><sub>41.1</sub></sup></td>
<td align="right"><sup><sub>62.1</sub></sup></td>
<td align="right"><sup><sub>45.1</sub></sup></td>
<td align="right"><sup><sub>36.3</sub></sup></td>
<td align="right"><sup><sub>58.9</sub></sup></td>
<td align="right"><sup><sub>38.5</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;boxes</a>&nbsp;|&nbsp;masks</a></sub></sup></td>
</tr>
<tr>
<td align="left"><sup><sub>R-101-FPN-GN-cascade</sub></sup></td>
<td align="left"><sup><sub>Mask</sub></sup></td>
<td align="left"><sup><sub>1x</sub></sup></td>
<td align="right"><sup><sub>1</sub></sup></td>
<td align="right"><sup><sub>44.8</sub></sup></td>
<td align="right"><sup><sub>62.8</sub></sup></td>
<td align="right"><sup><sub>48.8</sub></sup></td>
<td align="right"><sup><sub>38.0</sub></sup></td>
<td align="right"><sup><sub>59.8</sub></sup></td>
<td align="right"><sup><sub>40.8</sub></sup></td>
<td align="left"><sup><sub>model</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/bbox_coco_2014_minival_results_R101-FPN-GN-cascade-rcnn-mask.json">boxes</a>&nbsp;|&nbsp;<a href="http://www.svcl.ucsd.edu/projects/cascade-rcnn/results/segmentations_coco_2014_minival_results_R101-FPN-GN-cascade-rcnn-mask.json">masks</a></sub></sup></td>
</tr>
<!-- END E2E FASTER AND MASK TABLE -->
</tbody></table>
