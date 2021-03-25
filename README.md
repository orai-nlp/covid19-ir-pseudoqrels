# covid-19-IR with neural Reranking using Pseudo-qrels from the target collection.

**Wide perspective query system focused on COVID-19
**

System that offers integral consultation of scientific papers on COVID-19 through search at document and passage level and with auxiliary visualization of the results.

Developed for the [CORD-19](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge/) challenge.

Kaggle notebook available at : https://www.kaggle.com/isanvi/covid-19-ir-system-elhuyar

Also there is an initial interactive demo that provides navigation of the challenge questions and results at http://covid19kaggle.elhuyar.eus/


The system has the following features:
* Simultaneous and complementary retrieval of documents (coarse grain) and passages (fine grain) relevant to queries.
* Visual representation of relevant documents and paragraphs according to their semantic content.
* Hybrid retrieval of paragraphs and answers.

Techniques:
* Recovery of documents through language models (Indri).
* Recovery of passages by combining language models (Indri) and re-ranking based on fine-tuned BERT.
* Visualization by means of embeddings and reduction of dimensions.

Contributions:
* Results and visualization according to different techniques that offer an enriched and wide perspective consultation.
* Fine-tuning by trainset built from titles and abstracts.


## Dependencies
* python 3.6+ required (tested with 3.6.9)
* [Indri](https://www.lemurproject.org/indri.php) - Latest version can be found at (https://sourceforge.net/projects/lemur/files/lemur/)
* [BERT](https://github.com/google-research/bert)
* [Flair] (https://github.com/zalandoresearch/flair)

All Python dependencies are automatically installed by creating a virtual environment using the venv.requirements file provided here.


### INDRI (testing don on ubuntu 18.04, INDRI v5.17)

Building the document index requires antlr2.7.7 and compiling INDRI with the following configure command:

CXXFLAGS=-std=c++17 ./configure --with-antlr=/usr/local/antlr2

However if compiled so, IndriBuildIndex command works and index is built correctly, but pyndri fails to import indri library. So in orderr to make pyndri work, once the index is built Indri must be recompiled with the following configure command:

./configure CXX="g++ -D_GLIBCXX_USE_CXX11_ABI=0"


Therefore there are two versions of Indri. We installed the one used by pyndri to acces the index in the default path, while the one used to build indexes was kept in our home "/home/youruser/indri-5.17" (the reason is the index is built only once). Hence in order to build an index do as follows:

$cd /home/youruser/indri-5.17 
$./buildindex/IndriBuildIndex /path/your/indri/parameter.file



# Pseudo training datasets

The following datasets are made available

* title: [Title-abstract dataset (1:2 positive:negative ratio) https://storage.googleapis.com/elhuyar/datasets/titles_1%3A2_cord19-20200719.tsv.gz]

* cites: [sentence-citedAbstract dataset (1:2 positive:negative ratio) https://storage.googleapis.com/elhuyar/datasets/cites_1%3A2_cord19-20200719.tsv.gz]


# Reranking models

* [Clinical Bert (CBERT) fine-tuned on title dataset https://storage.googleapis.com/elhuyar/models/cbert-cord19-silver2.tgz]:
* [Clinical Bert (CBERT) fine-tuned on cites dataset https://storage.googleapis.com/elhuyar/models/cbert-cord19-cites2.tgz]:
* [Clinical Bert (CBERT) fine-tuned on title+sites combined dataset https://storage.googleapis.com/elhuyar/models/cbert-cord19-silver2-cites2.tgz]: 





# Source code(ongoing work)
Scripts order:

1 - Filter papers talking about covid-19:
'''shell
src/filter_dataset_with_kwords.py
'''

2 - Fine-tuning models:

Fine tuning is done using google BERT original code

3 - Fine tuning for passage reranking
3.1 - Prepare dataset for finetuning:
'''shell
src/createPassagePseuTrain-reranking.py
'''
3.2 - Finetuning

4 - Index collections with Indri

5 - Retrieval

6 - Visualization



# Citations

If you use any of the resources provided by this repository please cite the following paper:

