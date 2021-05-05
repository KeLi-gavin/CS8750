# Scientific Knowledge Graph Generator



This repository contains the source code developed to build a hybrid architecture generates a Scientific Knowledge Graph about the Semantic Web domain. The results of this research work have been published in: 

This work has been described in:
```
Generating Knowledge Graphs by Employing Natural Language Processing and Machine Learning Techniques within the Scholarly Domain. (2019). Authored by Danilo Dessi', Francesco Osborne, Diego Reforgiato Recupero, Davide Buscaldi, and Enrico Motta.
```

Reference code : https://github.com/danilo-dessi/skg (Thanks to Danilo Dessì)



![Scientific Knowledge Graph Generator Schema](https://github.com/KeLi-gavin/CS8750/blob/master/skg_schema.png)
**Figure 1**: Scientific Knowledge Graph Generator Schema

## Repository Description

- **data-preparation/** contains the scripts used to model the data downloaded from MAG dataset about the Semantic Web into a format that can be mined by the Luan Yi et al. tool. 

- **luanyi-extractor/** contains the scripts we have changed from the original project for adapting the Luan Yi et al. tool to our data. (**ATTENTION**: they have to be copied into the Luan Yi et al. project after that it works and its models have been built.)

- **cso-openie-extractor/** contains the scripts that have been used to enrich the Luan Yi et al. result wirh CSO topics and Stanford Core NLP relations (i.e., OpenIE and verbs detected by the PoS tagger).

- **skg-generator/** contains the scripts for performing all operations to clean entities and relations and making triples. Its final step is the generation of our scientific knowledge graph triples.

- **evaluation/** contains the scripts we used to generate the sample of triples about the semantic web and evaluate our approach.

Some files have been removed form the repository for github limitations on big files. Send an email to danilo_dessi@unica.it (Danilo Dessì) to get a copy of them.


## Usage

### Environments
Our project uses both Python 2.7 and Python 3.7. Python2.7 is used to run the Luan Yi et al. tool.

![Requirements List for python2.7 (Luan Yi)](https://github.com/KeLi-gavin/CS8750/blob/master/env_python27.png)
**Figure 2**: Requirements List for python2.7 (Luan Yi)

![Requirements List for python3.7 (CSO & SKG)](https://github.com/KeLi-gavin/CS8750/blob/master/env_python37.png)
**Figure 3**: Requirements List for python3.7 (CSO & SKG)

### Downloads

Please add 

```
./CS8750/luanyi-extractor/master/data/processed_data/elmo/test.hdf5

./CS8750/luanyi-extractor/master/data/processed_data/elmo/train.hdf5

./CS8750/luanyi-extractor/master/embeddings/glove.840B.300d.txt

./CS8750/luanyi-extractor/master/embeddings/glove_50_300_2.txt

./CS8750/stanford-corenlp-full-2018-10-05/stanford-corenlp-4.2.0-models.jar

All 20 file_x_input_luanyi.hdf5
```

### Extraction with Luan Yi et al. tool

To extract entities and relations from scientific publications our work has been built on top of https://arxiv.org/abs/1808.09602
1. Go to the directory luanyi-extractor/
2. Go to master/
3. Run 

```
python generate_elmo.py
```

4. Run
```
python3 run_luanyi.py
```

The execution will produce a csv file called *luanyi_output.csv* under the luanyi-extractor/ directory.

The execution will also produce the directory **csv_e_r/** that contains files where for each sentence a list of entities and a list of relations are associated. 

We suggest to run above commands in background since they are very time consuming.


### Extraction of CSO entities and Stanford Core NLP relations
1. Go to the cso-openie-extractor
2. Copy here the *luanyi_output.csv* previously generated in the directory luanyi-extractor/

#### Delete *cso_result.pkl* (if applicable) 

3. Run
```
python3 run_extractors.py
```

4. The result is a csv file called *csv_e_r_full.csv* which contains all entities and relations extracted by the used tools


### Toward the SKG
This code generates heristic based relations through the window of verbs, and validates entities based on CSO topics, Semantic Web Keywords and statistics. Finally it maps all relations following the taxonomy "SKG_predicates" we defined. 

1. Go to skg-generator
2. Copy the *csv_e_r_full.csv* in this directory

#### Delete */resources/300model.bin* and */resources/statistics.pickle* (if applicable) 

3. Run
```
python3 run.py
```
4. At the end the files *selected_triples.csv* and *kg.graphml* will be generated.  The file *selected_triples.csv* contains all triples with other information generated with our method. The file *triples.csv* contains all triples generated without details. The script *to_rdf.py* can be used to generate the rdf and nt files.


### Evaluation

The directory evalution contains the scripts we used for performing our evaluation and the manually annotated gold standard.

