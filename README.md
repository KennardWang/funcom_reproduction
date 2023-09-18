# funcom_reproduction

<div align="center">  

  [![description](https://img.shields.io/badge/paper-Reproduce-1F1F1F?style=for-the-badge)](https://github.com/KennardWang/funcom_reproduction)
  &nbsp;
  [![stars](https://img.shields.io/github/stars/KennardWang/funcom_reproduction?style=for-the-badge&color=FDEE21)](https://github.com/KennardWang/funcom_reproduction/stargazers)
  &nbsp;
  [![forks](https://img.shields.io/github/forks/KennardWang/funcom_reproduction?style=for-the-badge&color=white)](https://github.com/KennardWang/funcom_reproduction/forks)
  &nbsp;
  [![contributors](https://img.shields.io/github/contributors/KennardWang/funcom_reproduction?style=for-the-badge&color=8BC0D0)](https://github.com/KennardWang/funcom_reproduction/graphs/contributors)

  <img src="https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252" />
  &nbsp;
  <img src="https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue" />
  &nbsp;
  <img src="https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white" />
  &nbsp;
  <img src="https://img.shields.io/badge/Keras-FF0000?style=for-the-badge&logo=keras&logoColor=white" />
  &nbsp;
  <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white" />
</div>



## Table of Contents

- [Paper Info](#paper-info)
- [Install](#install)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)



## Paper Info

| Title | **A Neural Model for Generating Natural Language Summaries of Program Subroutines** |
|:---:|:---:|
| Publication Title | **2019 IEEE/ACM 41st International Conference on Software Engineering (ICSE)** |
| Authors | **Alexander LeClair, Siyuan Jiang, Collin McMillan** |
| Repository | [funcom](https://github.com/mcmillco/funcom) |



## Install

1. Install environment such as Google Colab env, GPU with high RAM. [Google Colab](https://colab.research.google.com/) is an online environment for machine learning and deep learning, which supports Python and Jupyter Notebook. The free version has only basic functionality. For reproduction, I use the Pro version with a high RAM GPU (monthly costs $10.88).

2. Download and unzip `Models` and `Data` at [Release](https://github.com/KennardWang/funcom_reproduction/releases), as well as the source code.

3. Upload the whole `funcom_reproduction` folder to the Google Drive root (everyone has 15GB free storage, I think maybe enough). Create a directory and make sure that the `data` folder is located at `./funcom_reproduction/scratch/funcom/data`.


## Usage

1. Before the model training, Please create `outdir` directory under `./funcom_reproduction/scratch/funcom/data`, and then create 3 directories `histories`, `models` and `predictions` respectively under `outdir`. After creation, you can execute steps 0, 0.5, 1 and 2 in the `.ipynb` file for training. The epoch suggested by the author is 5 (each epoch nearly costs more than 2 hours) because the effect will decrease if the **epoch>5**. But in my case, **ast-attendgru** model will abort exceptionally at the 4th epoch so eventually I choose **epoch=3** for comparison. The epoch value can be modified at [line 79 of `train.py`](https://github.com/KennardWang/funcom_reproduction/blob/a04196f56efeffce67df53ac04e3a0c6d9ebd887/train.py#L79). Or you can also use my models in `Models` and skip this step.

2. For comment generation and BLEU score calculation in the standard dataset, the **attendgru** model and **ast-attendgru** model have been released in `Models`. You can directly use them to generate comments for calculating BLEU scores. If you do, please start from step **iii** the following:

    1. Select `outdir_attendgru` or `outdir_ast-attendgru` in `data`, and rename the folder as `outdir`.
    2. Put the corresponding model file from `Models` under the directory `./funcom_reproduction/scratch/funcom/data/outdir/models`. For example, if you choose `outdir_attendgru`, you need to use `attendgru_E03_1633627453.h5` or `attendgru_E05_1633627453.h5`. Please do not forget to create the `models` directory.
    3. Open the corresponding `.ipynb` file under the root directory, and execute steps 0, 0.5, 1 and 3. After that, the `.txt` comment will be generated under `./funcom_reproduction/scratch/funcom/data/outdir/predictions`. Please double-check the `.h5` file name before running the code. 
    4. Calculate the BLEU score by executing step 4 in the `.ipynb` file. I leave my results here for checking:

        |Model|Ba|B1|B2|B3|B4|
        |:---:|:---:|:---:|:---:|:---:|:---:|
        |ast-attendgru, E03|19.37|38.74|21.88|14.75|11.27|
        |attendgru, E03|19.24|38.65|21.77|14.66|11.12|
        |attendgru, E05|19.14|37.88|21.4|14.66|11.3|

3. For comment generation & BLEU score calculation in the challenge dataset, please modify [line 114 of `predict.py`](https://github.com/KennardWang/funcom_reproduction/blob/a04196f56efeffce67df53ac04e3a0c6d9ebd887/predict.py#L114), and change default value from `False` to `True`. Then, redo steps **iii** and **iv** in the last point.



## Maintainers

![badge](https://img.shields.io/badge/maintenance-NO-EF2D5E) [@KennardWang](https://github.com/KennardWang)



## Contributing

Feel free to [open an issue](https://github.com/KennardWang/funcom_reproduction/issues) or submit [PRs](https://github.com/KennardWang/funcom_reproduction/pulls).



## License

[![license](https://img.shields.io/github/license/KennardWang/funcom_reproduction)](LICENSE) © Kennard Wang ( 2021.10.30 )
