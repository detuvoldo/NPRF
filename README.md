# NPRF
NPRF: A Neural Pseudo Relevance Feedback Framework for Ad-hoc Information Retrieval [[pdf]](http://aclweb.org/anthology/D18-1478)

<p align="center"> 
<img src="https://github.com/ucasir/NPRF/blob/master/NPRF-arch.jpg" width="600" align="center">
</p>

If you use the code, please cite the following paper: 

```
@inproceedings{li2018nprf,
  title={NPRF: A Neural Pseudo Relevance Feedback Framework for Ad-hoc Information Retrieval},
  author={Li, Canjia and Sun, Yingfei and He, Ben and Wang, Le and Hui, Kai and Yates, Andrew and Sun, Le and Xu, Jungang},
  booktitle={Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing},
  year={2018}
}
```

## Requirement

* Tensorflow
* Keras
* gensim
* numpy

## Getting started

### Training data preparation
To capture the top-k terms from top-n documents, one needs to extract term document frequency from index. Afterwards, you are required to generate the similarity matrix upon the query and document given the pre-trained word embedding (e.g. word2vec). Related functions can be found in preprocess/prepare_d2d.py.

### Training meta data preparation
We introduce two classes for the ease of training. The class **Relevance** incorporates the relevance information from the baseline and qrels file. The class **Result** simplify the write/read operation on standard TREC result file. Other information like query idf is dumped as a pickle file.


### Model training
Configure the MODEL_config.py file, then run 
```
python MODEL.py --fold fold_number temp_file_path
```
You need to run 5-fold cross valiation, which can be automatically done by running the *runfold.sh* script. The temp file is a temporary file to write the result of the validation set in TREC format. A training log sample on the first fold of TREC 1-3 dataset is provided for reference, see [sample_log](https://github.com/ucasir/NPRF/blob/master/sample_log).
### Evaluation
After training, the evaluation result of each fold is retained in the result path as you specify in the MODEL_config.py file. One can simply run `cat *res >> merge_file` to merge results from all folds. Thereafter, run the [trec_eval](https://trec.nist.gov/trec_eval/) script to evaluate your model.


## Reference

Some snippets of the code follow the implementation of [K-NRM](https://github.com/AdeDZY/K-NRM), [MatchZoo](https://github.com/faneshion/MatchZoo).
