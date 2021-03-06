#  Defending Against Universal Attacks Through Selective Feature Regeneration (CVPR 2020)
<img src="https://github.com/tsborkar/Selective-feature-regeneration/blob/master/fig/5625-teaser.gif" width="330" height="330"> [<img src="fig/teaser_frame0.PNG" height="330" width="480">](https://youtu.be/wMWhb7xqubg)

## Introduction
<p align="justify">
Deep neural network (DNN) predictions have been shown to be vulnerable to carefully crafted adversarial perturbations. Specifically, image-agnostic (universal adversarial) perturbations added to any image can fool a target network into making erroneous predictions. Departing from existing defense strategies that work mostly in the image domain, we present a novel defense which operates in the DNN feature domain and effectively defends against such universal perturbations. Our approach identifies pre-trained convolutional features that are most vulnerable to adversarial noise and deploys trainable feature regeneration units which transform these DNN filter activations into resilient features that are robust to universal perturbations. Regenerating only the top 50% adversarially susceptible activations in at most 6 DNN layers and leaving all remaining DNN activations unchanged, we outperform existing defense strategies across different network architectures by more than 10% in restored accuracy. We show that without any additional modification, our defense trained on ImageNet with one type of universal attack examples effectively defends against other types of unseen universal attacks. 

A complete description of our CVPR 2020 work can be found on [CVF Open access](https://openaccess.thecvf.com/content_CVPR_2020/html/Borkar_Defending_Against_Universal_Attacks_Through_Selective_Feature_Regeneration_CVPR_2020_paper.html) or on [ArXiv](https://arxiv.org/abs/1906.03444) and on the [Project page](https://ivulab.asu.edu/project/selectivefeatureregeneration/). </p>
For questions/comments, please email [Tejas Borkar](mailto:tsborkar@asu.edu)

## Proposed Defense

<img align="center" src="fig/intro_fig.png" height="400">

<p align="justify"><em><b>
Defending Against Adversarial Attacks by Selective Feature Regeneration: Convolutional filter activations in the baseline DNN (top) are first sorted in order of vulnerability to adversarial noise using their respective filter weight norms (see Manuscript). For each considered layer, we use a feature regeneration unit, consisting of a residual block with a single skip connection (4 layers), to regenerate only the most adversarially susceptible activations into resilient features that restore the lost accuracy of the baseline DNN, while leaving the remaining filter activations unchanged. We train these units on both clean and perturbed images in every mini-batch using the same target loss as the baseline DNN such that all parameters of the baseline DNN are left unchanged during training. </b></em></p>

### Feature Regeneration Unit (FRU)
<p align="center">
<img src="fig/FRU.PNG" align="center" height="200"></p>

<p align="justify"><em><b>
FRU acting on the activations of the N most susceptible filters in a DNN layer. D represents the FRU kernel depth and
has a default value of N. All convolutional layers except the final 1×1 layer are also followed by batch normalization and a ReLU
non-linearity. # parameters per FRU ≈ 18D^2 + 2ND.
 </em></b></p>

<p align="left"><b>Trainable parameters for DNN models:</b></p>

|   Methods        |  [CaffeNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)        |    [VGG-F](https://arxiv.org/abs/1405.3531)  |   [GoogLeNet](https://arxiv.org/abs/1409.4842)  |  [VGG-16](https://arxiv.org/abs/1409.1556)   |  [Res152](https://arxiv.org/abs/1512.03385)  |
| :-----------:  | :--------------: | :---------: |   :----------: |   :---------:  | :---------: |
|  Baseline      |   61M         | 61M      |      6.9M    |       131M   |   60M    |
|  *Ours*        |   **2.2M**      | **1.7M**   |      **1.4M** |     **1.6M**  |  **2.5M**  | 


### Robust Feature Regeneration

<img src="fig/feat_regen.PNG" align="center">

<p align="justify"><em><b>
Effectiveness of feature regeneration units at masking adversarial perturbations in DNN feature maps for images perturbed by universal perturbations (UAP, NAG, GAP and sPGD). Perturbation-free feature map (clean), different adversarially perturbed feature maps (Row 1) and corresponding feature maps regenerated by feature regeneration units (Row 2) are obtained for a single filter channel in conv1 1 layer of VGG-16, along with an enlarged view of a small region in the feature map (yellow box). Feature regeneration units are only trained on UAP attack examples but are very effective at suppressing adversarial artifacts generated by unseen attacks (e.g., NAG, GAP and sPGD).</em></b></p>



## Citation

If you use our code, models or need to refer to our results, please use the following:

```
@inproceedings{selectivefeatadvdef,
 author = {Tejas Borkar and Felix Heide and Lina Karam},
 booktitle = {Proceedings of the {IEEE} Conference on Computer Vision and Pattern Recognition ({CVPR})},
 title = {Defending Against Universal Attacks Through Selective Feature Regeneration},
 year = {2020}
}
```

## Key Results on ILSVRC2012 Validation Set

### Restoration accuracy for [Universal Adversarial Peturbations](https://arxiv.org/abs/1610.08401) (UAP)

|   Methods        |  [CaffeNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)        |    [VGG-F](https://arxiv.org/abs/1405.3531)  |   [GoogLeNet](https://arxiv.org/abs/1409.4842)  |  [VGG-16](https://arxiv.org/abs/1409.1556)   |  [Res152](https://arxiv.org/abs/1512.03385)  |
| :-----------:  | :--------------: | :---------: |   :----------: |   :---------:  | :---------: |
|  Baseline      |   0.596          | 0.628       |      0.691     |       0.681    |   0.670     |
|  *Ours*        |   **0.976**      | **0.967**   |      **0.970** |     **0.963**  |  **0.982**  | 

Please refer to Table 2. in our paper for additional details.


### Restoration accuracy for unseen stronger UAP attack perturbations against CaffeNet

|  Method    |  Attack Strength = 15    |   Attack Strength = 20    |   Attack Strength = 25      |
| :---------:|  :--------:  |:---------:|:----------:|
| Baseline   |     0.543    |    0.525  |     0.519   |
| *Ours*     |     **0.952**    |    **0.896**  |     **0.854**   |

Our defense is trained on attack examples with an attack strength of 10. Please refer to Table 4. in our paper for additional details. 

### Restoration accuracy for other types of unseen universal attacks 

Our defense is trained only one UAP attack examples. Please refer to Table 5. in our paper for additional details.

<table>
<thead>
<tr>  
 <th align="center" rowspan="2"> Method </th>
 <th align="center" colspan="3"> CaffeNet</th>
 <th align="center" colspan="3"> Res152 </th>
</tr> 
 <tr>
  <th align="center"><a href="https://arxiv.org/abs/1707.05572"> FFF </a></th>
  <th align="center"><a href="https://arxiv.org/abs/1712.03390"> NAG </a></th>
  <th align="center"><a href="https://arxiv.org/abs/1709.03582"> S.Fool </a></th>
   <th align="center"><a href="https://arxiv.org/abs/1712.02328"> GAP </a></th>
  <th align="center"><a href="https://arxiv.org/abs/1801.08092"> G-UAP </a></th>
  <th align="center"><a href="https://arxiv.org/abs/1812.03705"> sPGD </a></th>
</thead>
 
 <tbody>
 <tr>
 <td align="center"> Baseline </td>
 <td align="center">  0.645 </td>
 <td align="center">  0.670 </td>
 <td align="center">  0.815 </td>
 <td align="center">  0.640 </td>
 <td align="center">  0.726 </td>
 <td align="center">  0.671 </td>
 </tr>
  
 <tr>
 <td align="center"> <em> Ours </em> </td>
 <td align="center"> <b> 0.941 </b> </td>
 <td align="center"> <b> 0.840 </b> </td>
 <td align="center"> <b> 0.914 </b> </td>
 <td align="center"> <b> 0.922 </b> </td>
 <td align="center"> <b> 0.914 </b> </td>
 <td align="center"> <b> 0.976 </b> </td>
 </tr>
 
 </tbody>
 
 </table>

## Dependencies
- [Python-2.7](https://www.python.org/download/releases/2.7/)
- [Caffe](https://caffe.berkeleyvision.org/) with python bindings and GPU support
- [h5py](http://www.h5py.org/) 
- [numpy](http://www.numpy.org/)
- [matplotlib](https://matplotlib.org/) for displaying images
- MATLAB (needed only for organizing ImageNet image files)

## Trained Defense Models
Download our trained models from the table below:
<table>
<thead>
 <tr>
  <th align="center" colspan="5"> Baseline (Click for download/details) </th>
 </tr>
</thead> 
 <tbody>
  <tr>
   <td align="center"> CaffeNet <a href="https://drive.google.com/file/d/1XD55nDLl3VzigJ5CueCtCcF-tMJL12b7/view?usp=sharing"> :arrow_down: </a> </td> 
   <td align="center"> VGG-F <a href="https://drive.google.com/file/d/1q8Nu6hR4Eihgvqs--hw4wJ4eAFCuPqrS/view?usp=sharing"> :arrow_down: </a> </td> 
 <td align="center"> GoogLeNet <a href="https://drive.google.com/file/d/1jKo5qlBKy8338InhGm4JRZmPKG2BJRYe/view?usp=sharing"> :arrow_down: </a> </td> 
 <td align="center"> VGG16 <a href="https://drive.google.com/file/d/1HbgHHj2YDCX8gPrm_b6nAscPnoh6tPqA/view?usp=sharing"> :arrow_down: </a> </td> 
 <td align="center"> ResNet152 <a href="https://drive.google.com/file/d/1vfXX-moSs9K7Qe3A8WObf3zm3R1-4ZCR/view?usp=sharing"> :arrow_down: </a> </td> 
  </tr>
  <tr>
   <td align="center" colspan="5"> <b>Selective Feature Regeneration (Click for download/details) </b></td>  
  </tr>
  <tr>
   <td align="center"><details><summary> CaffeNet </summary> 
    <ul>
     <li>Primary attack defense <a href="https://drive.google.com/file/d/1noTb00HNQNVcQ6MmHQawqhXVRdoyVA0U/view?usp=sharing"> :arrow_down: </a></li> 
     <li>Secondary attack defense <a href="https://drive.google.com/file/d/1AVaXbEXnlldX-HBFv50rOigO_7yEbkxI/view?usp=sharing"> :arrow_down: </a></li>
    </ul></details></td>   
      <td align="center"> VGG-F <a href="https://drive.google.com/file/d/1ceCHTHrTR3eykE8aCrbgcdyvv-cccXIj/view?usp=sharing"> :arrow_down: </a> </td> 
 <td align="center"> GoogLeNet <a href="https://drive.google.com/file/d/1wXZM80xRgfBoHJBCw8j7DlEEgnSORCrC/view?usp=sharing"> :arrow_down: </a> </td> 
 <td align="center"> VGG16 <a href="https://drive.google.com/file/d/1UaUbqFLgQnGS7X7buduX6W5m7hORcfQW/view?usp=sharing"> :arrow_down: </a> </td> 
      <td align="center"><details><summary> ResNet152 </summary> 
    <ul>
     <li>Primary attack defense <a href="https://drive.google.com/file/d/1Di5r_jt_gOstUWLeg4ullrGillXnrds6/view?usp=sharing"> :arrow_down: </a></li> 
     <li>Secondary attack defense <a href="https://drive.google.com/file/d/1SpLkYTGr7vvhg43WvKZvwptiH8pAKpHT/view?usp=sharing"> :arrow_down: </a></li>
    </ul></details></td>  
  </tr>
 </tbody> 
</table>

Note:  We use a pruned [VGG16](https://github.com/yihui-he/channel-pruning) model for computational efficiency. 
       Secondary attack defense models are trained to defend against new white-box attacks computed using gradient information for the baseline DNN + FRUs. Refer to Section 5.2.5 in our paper for additional details.
 

## Install Selective Feature Regeneration Defense
Get the source code by cloning the repository :
```
git clone https://github.com/tsborkar/Selective-feature-regeneration.git
```

## Setting up ImageNet (ILSVRC2012) validation data
1. Change to the source directory: ``` cd Selective-feature-regeneration ```
2. Create folder for validation data ``` mkdir ILSVRC_data ```
3. Download [ILSVRC2012](http://image-net.org/challenges/LSVRC/2012/index) validation data files
4. Extract validation set files to ```ILSVRC_data``` folder.
5. Change to ```misc``` folder in the ```Selective-feature-regeneration``` source directory: ``` cd Selective-feature-regeneration/misc ```
6. Start MATLAB ```matlab``` and run ```ILSVRC_data_org.m```
```
>> ILSVRC_data_org
```
Note: The Matlab code creates a class folder for each object class and moves images to their corresponding class folders. The ImageNet evaluation codes provided in this repository assume the image files to be ordered by class in their own subfolder. The class_id to human readable label mapping used by our models can be found here: https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a

## ImageNet Evaluation (ILSVRC2012)
Code is provided to reproduce our results published in Tables 2,3 and 5 of our paper.

### Same-norm evaluation (Table 2 in our paper)

Example 1: Evaluating our CaffeNet defense against an L_inf UAP attack
```
python samenorm_ilsvrc_eval.py --input /path/to/imagenet_val/root_folder --dnn CaffeNet --load caffenet_FRU.caffemodel --defense True

```
Example 2: Evaluating baseline CaffeNet (no defense) against an L_inf UAP attack
```
python samenorm_ilsvrc_eval.py --input /path/to/imagenet_val/root_folder --dnn CaffeNet --load caffenet.caffemodel --defense False

```

For a detailed list of usage options see below:
```
python samenorm_ilsvrc_eval.py --help
```

### Cross-norm evaluation (Table 3 in our paper)


Example 1: Evaluating our ResNet152 defense against an L_2 UAP attack
```
python crossnorm_ilsvrc_eval.py --input /path/to/imagenet_val/root_folder --dnn ResNet152 --load resnet152_FRU.caffemodel --defense True

```
Example 2: Evaluating baseline ResNet152 (no defense) against an L_2 UAP attack
```
python crossnorm_ilsvrc_eval.py --input /path/to/imagenet_val/root_folder --dnn ResNet152 --load resnet152.caffemodel --defense False

```

For a detailed list of usage options see below:
```
python crossnorm_ilsvrc_eval.py --help
```

### Unseen attacks against CaffeNet (Table 5 in our paper)

Example 1: Evaluating our defense against an unseen NAG attack
```
python unseencaffenet_ilsvrc.py --input /path/to/imagenet_val/root_folder --load caffenet_FRU.caffemodel --attack NAG --defense True

```
Example 2: Evaluating our defense against an FFF attack
```
python unseencaffenet_ilsvrc.py --input /path/to/imagenet_val/root_folder --load caffenet_FRU.caffemodel --attack FFF --defense True
```

For a detailed list of usage options see below:
```
python unseencaffenet_ilsvrc.py --help
```

### Unseen attacks against ResNet152 (Table 5 in our paper)

Example 1: Evaluating our defense against an unseen GAP attack
```
python unseenresnet152_ilsvrc.py --input /path/to/imagenet_val/root_folder --load resnet152_FRU.caffemodel --attack GAP --defense True

```
Example 2: Evaluating our defense against an sPGD attack
```
python unseenresnet152_ilsvrc.py --input /path/to/imagenet_val/root_folder --load resnet152_FRU.caffemodel --attack sPGD --defense True
```

For a detailed list of usage options see below:
```
python unseenresnet152_ilsvrc.py --help
```





## General Usage

Sample code is provided in [defense_example.py](https://github.com/tsborkar/Selective-feature-regeneration/blob/master/defense_example.py) for evaluating our proposed defense against various types of universal attack examples.

Example 1: Evaluate proposed defense for ResNet152 against a UAP attack on an input image.
```
python defense_example.py --input /path/to/input_image --dnn ResNet152 
    --load /path/to/trained/model_weights --attack UAP --defense True
```

Example 2: Evaluate proposed defense for CaffeNet against an unseen NAG attack on a default image.
```
python defense_example.py --dnn CaffeNet --load /path/to/trained/model_weights --attack NAG --defense True
```

Example 3: Evaluate baseline ResNet152 (no defense) against a UAP attack.
```
python defense_example.py --dnn ResNet152 --load /path/to/trained/model_weights --attack UAP --defense False
```

For a detailed list of usage options see below:
``` 
python defense_example.py --help
```

