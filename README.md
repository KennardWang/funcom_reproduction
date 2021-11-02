# funcom_reproduction

### Credit

| Paper | **A Neural Model for Generating Natural Language Summaries of Program Subroutines** |
|:---:|:---:|
| Conference | **2019 IEEE/ACM 41st International Conference on Software Engineering (ICSE)** |
| Author | **Alexander LeClair, Siyuan Jiang, Collin McMillan** |
| Repository | [funcom](https://github.com/mcmillco/funcom) |

------
### How to Reproduce
#### Step 0 : Environment Preparation
+ Google Colab env, GPU with high RAM. [Google Colab](https://colab.research.google.com/) is an online environment for machine learning and deep learning, which supports Python and Jupyter Notebook. The free version has only basic functionality. For the reproduction I use the Pro version with high RAM GPU ( monthly costs $10.88 ).

#### Step 0.5 : Data Preparation
+ Please download and unzip ***Models*** and ***Data Set*** at [Release](https://github.com/KennardWang/funcom_reproduction/releases), as well as the source code.

#### Step 1 : Directory Setting
+ Create directory and make sure that ***data*** file is located at `./funcom_reproduction/scratch/funcom/data`.

#### Step 2 : Model Training
+ Please create `outdir` directory under `./funcom_reproduction/scratch/funcom/data`, and then create 3 directories `histories`, `models` and `predictions` respectively under `outdir`. After creation, you can execute step 0, 0.5, 1 and 2 in *.ipynb* file for training.
+ ***Attention :*** The epoch suggested by the author is 5 ( each epoch nearly costs more than 2 hours ) because the effect will decrease if epoch > 5. But in my case, ast-attendgru model will abort exceptionally at 4th epoch so that eventually I choose epoch = 3 for comparison. The epoch value can be modified at [line 79 in ***train.py***](https://github.com/KennardWang/funcom_reproduction/blob/a04196f56efeffce67df53ac04e3a0c6d9ebd887/train.py#L79). Or you can also use my models in ***Models*** and skip this step because everything will be explained in Step 3.

#### Step 3 : Comment Generation & BLEU Score Calculation ( standard data set )
+ The ***attendgru*** model and ***ast-attendgru*** model has been released in ***Models***. You can directly use them to generate comment for calculating BLEU score. If you have done Step 2, please start from point 3 following.

1. Select ***outdir_attendgru*** or ***outdir_ast-attendgru*** in ***data*** file, and rename the file as ***outdir***.
2. Put corresponding model file from ***Models*** under directory `./funcom_reproduction/scratch/funcom/data/outdir/models`. For example, if you choose ***outdir_attendgru***, you need to use ***attendgru_E03_1633627453.h5*** or ***attendgru_E05_1633627453.h5***. Please do not forget to create ***models*** directory.
3. Now open corresponding *.ipynb* file under root directory, execute step 0, 0.5, 1 and 3. After that, the *.txt* comment will be generated under `./funcom_reproduction/scratch/funcom/data/outdir/predictions`. Please double check the *.h5* file name before running the code. 
4. Calculating BLEU score by executing step 4 in *.ipynb* file.

I give my results for you guys to check:

|Model|Ba|B1|B2|B3|B4|
|:---:|:---:|:---:|:---:|:---:|:---:|
|ast-attendgru, E03|19.37|38.74|21.88|14.75|11.27|
|attendgru, E03|19.24|38.65|21.77|14.66|11.12|
|attendgru, E05|19.14|37.88|21.4|14.66|11.3|

#### Step 4 : Comment Generation & BLEU Score Calculation ( challenge data set )
+ Modify [line 114 in ***predict.py***](https://github.com/KennardWang/funcom_reproduction/blob/a04196f56efeffce67df53ac04e3a0c6d9ebd887/predict.py#L114), change default value from `False` to `True`.
+ Redo point 3 and 4 in Step 3.

------
### License
+ [MIT License](https://github.com/KennardWang/funcom_reproduction/blob/master/LICENSE)
------
### Author
+ Kennard Wang ( 2021.10.30 )
------
