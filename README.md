# CPSC 577 Project: TextGraphSAGE--Enhancing Text Classification with GraphSAGE
## Group members:
- Lang Ding(lang.ding@yale.edu)
- Weiyi You(weiyi.you@yale.edu)
- Shurui Wang(shurui.wang@yale.edu)


## Instructions on setting up the experimental environment
You have two options to run the code:
- a. Use Google Colab T4 GPU. You should be able to run the CNN, LSTM, and TextGCN notebook with no issues without a subscription. For the TextGraphSAGE notebook, you may need a paid version of Colab to avoid OutOfMemory error.
- b. Use school cluster. We have already listed all dependencies and external libraries used, along with their versions in env.yml. Create the environment by running this code:
```
salloc -t 2:00:00 --mem=16G

module load miniconda

# create conda environment
$ conda env create -f cpsc577_env.yaml

# update conda environment
$ conda env update -n cpsc577 --file cpsc577_env.yaml

# after you have installed the environment, install below libraries
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia

pip install torch-scatter torch-geometric -f https://data.pyg.org/whl/torch-2.2.2+cu121.html
```
