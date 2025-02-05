## DCN_movielenslatest_x1

A hands-on guide to run the DCN model on the Movielenslatest_x1 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  GPU: Tesla P100 16G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 11.4
  python: 3.6.5
  pytorch: 1.0.1.post2
  pandas: 0.23.0
  numpy: 1.18.1
  scipy: 1.1.0
  sklearn: 0.23.1
  pyyaml: 5.1
  h5py: 2.7.1
  tqdm: 4.59.0
  fuxictr: 1.1.0
  ```

### Dataset
Dataset ID: [Movielenslatest_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/MovieLens/README.md#Movielenslatest_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DCN](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DCN.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Movielens/MovielensLatest_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DCN_movielenslatest_x1_tuner_config_01](./DCN_movielenslatest_x1_tuner_config_01). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DCN_movielenslatest_x1
    nohup python run_expid.py --config ./DCN_movielenslatest_x1_tuner_config_01 --expid DCN_movielenslatest_x1_001_4810b636 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

Total 5 runs:

| Runs | AUC | logloss  |
|:--------------------:|:--------------------:|:--------------------:|
| 1 | 0.968719 | 0.215987  |
| 2 | 0.967358 | 0.214489  |
| 3 | 0.968355 | 0.213700  |
| 4 | 0.968357 | 0.208969  |
| 5 | 0.968990 | 0.215492  |
| Avg | 0.968356 | 0.213727 |
| Std | &#177;0.00055312 | &#177;0.00250770 |


### Logs
```python
2022-02-10 00:51:39,279 P6321 INFO {
    "batch_norm": "True",
    "batch_size": "4096",
    "crossing_layers": "4",
    "data_format": "csv",
    "data_root": "../data/Movielens/",
    "dataset_id": "movielenslatest_x1_cd32d937",
    "debug": "False",
    "dnn_activations": "relu",
    "dnn_hidden_units": "[400, 400, 400]",
    "embedding_dim": "10",
    "embedding_regularizer": "0.01",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user_id', 'item_id', 'tag_id'], 'type': 'categorical'}]",
    "gpu": "0",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DCN",
    "model_id": "DCN_movielenslatest_x1_001_4810b636",
    "model_root": "./Movielens/DCN_movielenslatest_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0.2",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Movielens/MovielensLatest_x1/test.csv",
    "train_data": "../data/Movielens/MovielensLatest_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Movielens/MovielensLatest_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-02-10 00:51:39,280 P6321 INFO Set up feature encoder...
2022-02-10 00:51:39,280 P6321 INFO Load feature_map from json: ../data/Movielens/movielenslatest_x1_cd32d937/feature_map.json
2022-02-10 00:51:39,280 P6321 INFO Loading data...
2022-02-10 00:51:39,282 P6321 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/train.h5
2022-02-10 00:51:39,311 P6321 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/valid.h5
2022-02-10 00:51:39,321 P6321 INFO Train samples: total/1404801, pos/467878, neg/936923, ratio/33.31%, blocks/1
2022-02-10 00:51:39,321 P6321 INFO Validation samples: total/401372, pos/134225, neg/267147, ratio/33.44%, blocks/1
2022-02-10 00:51:39,321 P6321 INFO Loading train data done.
2022-02-10 00:51:43,023 P6321 INFO Total number of parameters: 1238661.
2022-02-10 00:51:43,024 P6321 INFO Start training: 343 batches/epoch
2022-02-10 00:51:43,025 P6321 INFO ************ Epoch=1 start ************
2022-02-10 00:51:58,664 P6321 INFO [Metrics] AUC: 0.936315 - logloss: 0.286690
2022-02-10 00:51:58,664 P6321 INFO Save best model: monitor(max): 0.936315
2022-02-10 00:51:58,671 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:51:58,709 P6321 INFO Train loss: 0.380873
2022-02-10 00:51:58,709 P6321 INFO ************ Epoch=1 end ************
2022-02-10 00:52:14,606 P6321 INFO [Metrics] AUC: 0.946622 - logloss: 0.262927
2022-02-10 00:52:14,607 P6321 INFO Save best model: monitor(max): 0.946622
2022-02-10 00:52:14,615 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:52:14,665 P6321 INFO Train loss: 0.363778
2022-02-10 00:52:14,665 P6321 INFO ************ Epoch=2 end ************
2022-02-10 00:52:39,130 P6321 INFO [Metrics] AUC: 0.949533 - logloss: 0.257413
2022-02-10 00:52:39,130 P6321 INFO Save best model: monitor(max): 0.949533
2022-02-10 00:52:39,138 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:52:39,191 P6321 INFO Train loss: 0.365301
2022-02-10 00:52:39,191 P6321 INFO ************ Epoch=3 end ************
2022-02-10 00:53:09,795 P6321 INFO [Metrics] AUC: 0.951675 - logloss: 0.246543
2022-02-10 00:53:09,796 P6321 INFO Save best model: monitor(max): 0.951675
2022-02-10 00:53:09,807 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:53:09,846 P6321 INFO Train loss: 0.369061
2022-02-10 00:53:09,846 P6321 INFO ************ Epoch=4 end ************
2022-02-10 00:53:49,244 P6321 INFO [Metrics] AUC: 0.952749 - logloss: 0.245054
2022-02-10 00:53:49,245 P6321 INFO Save best model: monitor(max): 0.952749
2022-02-10 00:53:49,253 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:53:49,292 P6321 INFO Train loss: 0.373783
2022-02-10 00:53:49,293 P6321 INFO ************ Epoch=5 end ************
2022-02-10 00:54:28,777 P6321 INFO [Metrics] AUC: 0.953439 - logloss: 0.245455
2022-02-10 00:54:28,777 P6321 INFO Save best model: monitor(max): 0.953439
2022-02-10 00:54:28,786 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:54:28,854 P6321 INFO Train loss: 0.374946
2022-02-10 00:54:28,854 P6321 INFO ************ Epoch=6 end ************
2022-02-10 00:55:08,435 P6321 INFO [Metrics] AUC: 0.954142 - logloss: 0.239931
2022-02-10 00:55:08,436 P6321 INFO Save best model: monitor(max): 0.954142
2022-02-10 00:55:08,444 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:55:08,501 P6321 INFO Train loss: 0.375498
2022-02-10 00:55:08,501 P6321 INFO ************ Epoch=7 end ************
2022-02-10 00:55:48,597 P6321 INFO [Metrics] AUC: 0.954636 - logloss: 0.237659
2022-02-10 00:55:48,597 P6321 INFO Save best model: monitor(max): 0.954636
2022-02-10 00:55:48,607 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:55:48,656 P6321 INFO Train loss: 0.376406
2022-02-10 00:55:48,656 P6321 INFO ************ Epoch=8 end ************
2022-02-10 00:56:28,312 P6321 INFO [Metrics] AUC: 0.955091 - logloss: 0.242453
2022-02-10 00:56:28,312 P6321 INFO Save best model: monitor(max): 0.955091
2022-02-10 00:56:28,320 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:56:28,365 P6321 INFO Train loss: 0.375937
2022-02-10 00:56:28,365 P6321 INFO ************ Epoch=9 end ************
2022-02-10 00:57:07,997 P6321 INFO [Metrics] AUC: 0.955416 - logloss: 0.238261
2022-02-10 00:57:07,998 P6321 INFO Save best model: monitor(max): 0.955416
2022-02-10 00:57:08,006 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:57:08,043 P6321 INFO Train loss: 0.376665
2022-02-10 00:57:08,044 P6321 INFO ************ Epoch=10 end ************
2022-02-10 00:57:47,759 P6321 INFO [Metrics] AUC: 0.955511 - logloss: 0.236343
2022-02-10 00:57:47,760 P6321 INFO Save best model: monitor(max): 0.955511
2022-02-10 00:57:47,768 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:57:47,803 P6321 INFO Train loss: 0.375203
2022-02-10 00:57:47,803 P6321 INFO ************ Epoch=11 end ************
2022-02-10 00:58:23,111 P6321 INFO [Metrics] AUC: 0.956691 - logloss: 0.232197
2022-02-10 00:58:23,111 P6321 INFO Save best model: monitor(max): 0.956691
2022-02-10 00:58:23,119 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:58:23,160 P6321 INFO Train loss: 0.376660
2022-02-10 00:58:23,160 P6321 INFO ************ Epoch=12 end ************
2022-02-10 00:58:58,096 P6321 INFO [Metrics] AUC: 0.956410 - logloss: 0.233713
2022-02-10 00:58:58,097 P6321 INFO Monitor(max) STOP: 0.956410 !
2022-02-10 00:58:58,097 P6321 INFO Reduce learning rate on plateau: 0.000100
2022-02-10 00:58:58,097 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:58:58,133 P6321 INFO Train loss: 0.376230
2022-02-10 00:58:58,133 P6321 INFO ************ Epoch=13 end ************
2022-02-10 00:59:33,192 P6321 INFO [Metrics] AUC: 0.967366 - logloss: 0.207615
2022-02-10 00:59:33,192 P6321 INFO Save best model: monitor(max): 0.967366
2022-02-10 00:59:33,204 P6321 INFO --- 343/343 batches finished ---
2022-02-10 00:59:33,240 P6321 INFO Train loss: 0.273167
2022-02-10 00:59:33,240 P6321 INFO ************ Epoch=14 end ************
2022-02-10 01:00:08,668 P6321 INFO [Metrics] AUC: 0.968738 - logloss: 0.215786
2022-02-10 01:00:08,669 P6321 INFO Save best model: monitor(max): 0.968738
2022-02-10 01:00:08,677 P6321 INFO --- 343/343 batches finished ---
2022-02-10 01:00:08,715 P6321 INFO Train loss: 0.188569
2022-02-10 01:00:08,715 P6321 INFO ************ Epoch=15 end ************
2022-02-10 01:00:39,137 P6321 INFO [Metrics] AUC: 0.967290 - logloss: 0.242514
2022-02-10 01:00:39,137 P6321 INFO Monitor(max) STOP: 0.967290 !
2022-02-10 01:00:39,137 P6321 INFO Reduce learning rate on plateau: 0.000010
2022-02-10 01:00:39,137 P6321 INFO --- 343/343 batches finished ---
2022-02-10 01:00:39,184 P6321 INFO Train loss: 0.144130
2022-02-10 01:00:39,184 P6321 INFO ************ Epoch=16 end ************
2022-02-10 01:01:05,623 P6321 INFO [Metrics] AUC: 0.966740 - logloss: 0.254775
2022-02-10 01:01:05,624 P6321 INFO Monitor(max) STOP: 0.966740 !
2022-02-10 01:01:05,624 P6321 INFO Reduce learning rate on plateau: 0.000001
2022-02-10 01:01:05,624 P6321 INFO Early stopping at epoch=17
2022-02-10 01:01:05,624 P6321 INFO --- 343/343 batches finished ---
2022-02-10 01:01:05,660 P6321 INFO Train loss: 0.111467
2022-02-10 01:01:05,660 P6321 INFO Training finished.
2022-02-10 01:01:05,660 P6321 INFO Load best model: /home/XXX/FuxiCTR_github_v1.1/benchmarks/Movielens/DCN_movielenslatest_x1/movielenslatest_x1_cd32d937/DCN_movielenslatest_x1_001_4810b636.model
2022-02-10 01:01:05,701 P6321 INFO ****** Validation evaluation ******
2022-02-10 01:01:07,216 P6321 INFO [Metrics] AUC: 0.968738 - logloss: 0.215786
2022-02-10 01:01:07,254 P6321 INFO ******** Test evaluation ********
2022-02-10 01:01:07,254 P6321 INFO Loading data...
2022-02-10 01:01:07,254 P6321 INFO Loading data from h5: ../data/Movielens/movielenslatest_x1_cd32d937/test.h5
2022-02-10 01:01:07,259 P6321 INFO Test samples: total/200686, pos/66850, neg/133836, ratio/33.31%, blocks/1
2022-02-10 01:01:07,259 P6321 INFO Loading test data done.
2022-02-10 01:01:08,042 P6321 INFO [Metrics] AUC: 0.968719 - logloss: 0.215987

```
