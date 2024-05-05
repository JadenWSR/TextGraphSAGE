# CPSC 577 Project: TextGraphSAGE--Enhancing Text Classification with GraphSAGE
## Group members:
- Lang Ding(lang.ding@yale.edu)
- Weiyi You(weiyi.you@yale.edu)
- Shurui Wang(shurui.wang@yale.edu)


## Instructions on setting up the experimental environment
You have two options to run the code:
- a. Use Google Colab T4 GPU. You should be able to run the CNN, LSTM, and TextGCN notebook with no issues without a subscription. For the TextGraphSAGE notebook, you may need a paid version of Colab to avoid OutOfMemory error.
- b. Use school cluster. We have already listed all dependencies and external libraries used, along with their versions in [cpsc577_env.yaml](https://github.com/JadenWSR/TextGraphSAGE/blob/main/cpsc577_env.yaml).

**Example setup of Jupyter Lab on school cluster**:
![Yale_example](https://github.com/JadenWSR/TextGraphSAGE/blob/main/figures/Yale_Cluster_Example.png)

**Create the environment by running this code on the cluster terminal**:
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
**We used Python version `3.12.3`. Please use exactly the version we specified in [cpsc577_env.yaml](https://github.com/JadenWSR/TextGraphSAGE/blob/main/cpsc577_env.yaml)**

## Datasets
We included the Twitter asian prejudice dataset and Reuters 8 dataset in our [data folder](https://github.com/JadenWSR/TextGraphSAGE/tree/main/data).

1. Reuters R8 Dataset: This subset of the Reuters 21578 collection contains documents from 1987 newswire articles, divided into 8 categories: trade, ship, interest, earn, crude, money-fx, grain, and acquisition. The dataset consists of 5,485 training texts and 2,189 testing texts. Preprocessing involves standard text cleaning techniques such as removing stop words and infrequent words, and applying normalization steps to prepare the text for the graph-based model.

2. Twitter Asian Prejudice Dataset: Comprising 20,000 tweets related to East Asian prejudice, this dataset is categorized into five labels reflecting the nature of the tweets, including discussions on prejudice, counter-speech, and entity-directed hostility. Similar preprocessing steps are used here, tailored to handle social media text characteristics like hashtags and mentions.

Both datasets are also publicly accessible through the Text-GCN repository on  [GitHub](https://github.com/codeKgu/Text-GCN/tree/master). For our CNN and LSTM models, standard NLP data cleaning protocols are applied, including tokenization and filtering non-lexical items. For the TextGCN and TextGraphSAGE models, texts are further processed into a graph format as described in Section 4.2. This involves converting texts to nodes and edges in a graph, utilizing term frequency and document co-occurrence to weight the connections between nodes, thereby retaining semantic relationships within the data.


For a new dataset, prepare a [dataset_name]_labels.txt and [dataset_name]_sentences.txt in /data/corpus in which each line corresponds to a document and its corresponding label. Use prep_data.py to further clean [dataset_name]_sentences.txt. The script will generate a [dataset_name]_sentences_clean.txt

The following is an example of the constructed text graph for the twitter dataset from [Text-GCN repository](https://github.com/codeKgu/Text-GCN/tree/master/data/corpus). Green represents text nodes and red represents document nodes.

![graph_example](https://github.com/JadenWSR/TextGraphSAGE/blob/main/figures/Text_Graph_Example.png)
