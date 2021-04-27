# Scientific Knowledge Graph Generator



This repository contains the source code developed to build a hybrid architecture generates a Scientific Knowledge Graph about the Semantic Web domain. The results of this research work have been published in: 

This work has been described in:
```
Generating Knowledge Graphs by Employing Natural Language Processing and Machine Learning Techniques within the Scholarly Domain. (2019). Authored by Danilo Dessi', Francesco Osborne, Diego Reforgiato Recupero, Davide Buscaldi, and Enrico Motta.
```

## Repository Description

- **data-preparation/** contains the scripts used to model the data downloaded from MAG dataset about the Semantic Web into a format that can be mined by the Luan Yi et al. tool. 

- **luanyi-extractor/** contains the scripts we have changed from the original project for adapting the Luan Yi et al. tool to our data. (**ATTENTION**: they have to be copied into the Luan Yi et al. project after that it works and its models have been built.)

- **cso-openie-extractor/** contains the scripts that have been used to enrich the Luan Yi et al. result wirh CSO topics and Stanford Core NLP relations (i.e., OpenIE and verbs detected by the PoS tagger).

- **skg-generator/** contains the scripts for performing all operations to clean entities and relations and making triples. Its final step is the generation of our scientific knowledge graph triples.

- **evaluation/** contains the scripts we used to generate the sample of triples about the semantic web and evaluate our approach.

Some files have been removed form the repository for github limitations on big files. Send an email to danilo_dessi@unica.it (Danilo Dessì) to get a copy of them.


## Usage
Please follow this guide to run the code and reproduce our results. Please contact us because we need to provide extra files that cannot be pushed into the github reporsitory for files limit of 100 MB.

### Environments
Our project uses both Python 2.7 and Python 3.6 (ensure you have Python 3.6 or above installed.). Python2.7 is used to run the Luan Yi et al. tool.

### download

please add 

./CS8750/skg/luanyi-extractor/master/data/processed_data/elmo/test.hdf5

./CS8750/scierc/data/processed_data/elmo/test.hdf5

./CS8750/skg/luanyi-extractor/master/data/processed_data/elmo/train.hdf5

./CS8750/scierc/data/processed_data/elmo/train.hdf5

./CS8750/skg/luanyi-extractor/master/embeddings/glove.840B.300d.txt

./CS8750/scierc/embeddings/glove.840B.300d.txt

./CS8750/cc/skg/luanyi-extractor/master/embeddings/glove_50_300_2.txt

./CS8750/cc/scierc/embeddings/glove_50_300_2.txt

./CS8750/cc/skg/stanford-corenlp-full-2018-10-05/stanford-corenlp-4.2.0-models.jar

and all 20 file_0_input_luanyi.hdf5

### Extraction with Luan Yi et al. tool

To extract entities and relations from scientific publications our work has been built on top of https://arxiv.org/abs/1808.09602
1. Go to the directory luanyi-extractor/
2. Please be sure you have already downloaded and tested the files coming from https://bitbucket.org/luanyi/scierc/src/master/

#### for training and testing LuanYi evaluate ./scierc/singleton.py and ./scierc/evaluator.py

donot execuate those two files which under master/ folder

3. Under master/ create the directories paths data/processed_data/json/ and data/processed_data/elmo/
4. From data-preparation/ copy the directory **luanyi_input/** to master/data/processed_data/json/
5. Create an empty directory luanyi_input/ (same name of above) also under master/data/processed_data/elmo/
6. Go to master/
7. Copy the files from the directory use/ to the directory master/
8. Run 
```
python generate_elmo.py
```

9. Run
```
python3 run_luanyi.py
```

The execution will produce a csv file called *luanyi_output.csv* under the luanyi-extractor/ directory.

The execution will also produce the directory **csv_e_r/** that contains files where for each sentence a list of entities and a list of relations are associated. 

We suggest to run above commands in background since they are very time consuming.










