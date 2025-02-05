## CrossNet_frappe_x1

A hands-on guide to run the DCN model on the Frappe_x1 dataset.

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
Dataset ID: [Frappe_x1](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Frappe/README.md#Frappe_x1). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/tree/v1.1.0) for this experiment. See the model code: [DCN](https://github.com/xue-pai/FuxiCTR/blob/v1.1.0/fuxictr/pytorch/models/DCN.py).

Running steps:

1. Download [FuxiCTR-v1.1.0](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.1.0.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Frappe/Frappe_x1`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [CrossNet_criteo_x1_tuner_config_02](./CrossNet_criteo_x1_tuner_config_02). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd CrossNet_frappe_x1
    nohup python run_expid.py --config ./CrossNet_criteo_x1_tuner_config_02 --expid DCN_frappe_x1_005_880c69b8 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| AUC | logloss  |
|:--------------------:|:--------------------:|
| 0.959427 | 0.271483  |


### Logs
```python
2022-01-23 11:30:07,469 P14924 INFO {
    "batch_norm": "False",
    "batch_size": "4096",
    "crossing_layers": "6",
    "data_format": "csv",
    "data_root": "../data/Frappe/",
    "dataset_id": "frappe_x1_04e961e9",
    "debug": "False",
    "dnn_activations": "relu",
    "dnn_hidden_units": "None",
    "embedding_dim": "10",
    "embedding_regularizer": "0.0001",
    "epochs": "100",
    "every_x_epochs": "1",
    "feature_cols": "[{'active': True, 'dtype': 'float', 'name': ['user', 'item', 'daytime', 'weekday', 'isweekend', 'homework', 'cost', 'weather', 'country', 'city'], 'type': 'categorical'}]",
    "gpu": "0",
    "label_col": "{'dtype': 'float', 'name': 'label'}",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['AUC', 'logloss']",
    "min_categr_count": "1",
    "model": "DCN",
    "model_id": "DCN_frappe_x1_005_880c69b8",
    "model_root": "./Frappe/DCN_frappe_x1/",
    "monitor": "AUC",
    "monitor_mode": "max",
    "net_dropout": "0",
    "net_regularizer": "0",
    "num_workers": "3",
    "optimizer": "adam",
    "partition_block_size": "-1",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2021",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Frappe/Frappe_x1/test.csv",
    "train_data": "../data/Frappe/Frappe_x1/train.csv",
    "use_hdf5": "True",
    "valid_data": "../data/Frappe/Frappe_x1/valid.csv",
    "verbose": "1",
    "version": "pytorch"
}
2022-01-23 11:30:07,470 P14924 INFO Set up feature encoder...
2022-01-23 11:30:07,470 P14924 INFO Load feature_map from json: ../data/Frappe/frappe_x1_04e961e9/feature_map.json
2022-01-23 11:30:07,470 P14924 INFO Loading data...
2022-01-23 11:30:07,472 P14924 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/train.h5
2022-01-23 11:30:07,483 P14924 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/valid.h5
2022-01-23 11:30:07,487 P14924 INFO Train samples: total/202027, pos/67604, neg/134423, ratio/33.46%, blocks/1
2022-01-23 11:30:07,487 P14924 INFO Validation samples: total/57722, pos/19063, neg/38659, ratio/33.03%, blocks/1
2022-01-23 11:30:07,487 P14924 INFO Loading train data done.
2022-01-23 11:30:11,779 P14924 INFO Total number of parameters: 55191.
2022-01-23 11:30:11,779 P14924 INFO Start training: 50 batches/epoch
2022-01-23 11:30:11,780 P14924 INFO ************ Epoch=1 start ************
2022-01-23 11:30:15,238 P14924 INFO [Metrics] AUC: 0.925258 - logloss: 0.493493
2022-01-23 11:30:15,239 P14924 INFO Save best model: monitor(max): 0.925258
2022-01-23 11:30:15,241 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:15,299 P14924 INFO Train loss: 0.610261
2022-01-23 11:30:15,299 P14924 INFO ************ Epoch=1 end ************
2022-01-23 11:30:18,588 P14924 INFO [Metrics] AUC: 0.938497 - logloss: 0.283559
2022-01-23 11:30:18,589 P14924 INFO Save best model: monitor(max): 0.938497
2022-01-23 11:30:18,591 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:18,642 P14924 INFO Train loss: 0.324486
2022-01-23 11:30:18,642 P14924 INFO ************ Epoch=2 end ************
2022-01-23 11:30:21,926 P14924 INFO [Metrics] AUC: 0.939884 - logloss: 0.279683
2022-01-23 11:30:21,926 P14924 INFO Save best model: monitor(max): 0.939884
2022-01-23 11:30:21,929 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:21,981 P14924 INFO Train loss: 0.272526
2022-01-23 11:30:21,981 P14924 INFO ************ Epoch=3 end ************
2022-01-23 11:30:25,196 P14924 INFO [Metrics] AUC: 0.940792 - logloss: 0.278836
2022-01-23 11:30:25,197 P14924 INFO Save best model: monitor(max): 0.940792
2022-01-23 11:30:25,199 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:25,244 P14924 INFO Train loss: 0.267627
2022-01-23 11:30:25,244 P14924 INFO ************ Epoch=4 end ************
2022-01-23 11:30:28,368 P14924 INFO [Metrics] AUC: 0.941275 - logloss: 0.278673
2022-01-23 11:30:28,369 P14924 INFO Save best model: monitor(max): 0.941275
2022-01-23 11:30:28,373 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:28,421 P14924 INFO Train loss: 0.265717
2022-01-23 11:30:28,421 P14924 INFO ************ Epoch=5 end ************
2022-01-23 11:30:31,503 P14924 INFO [Metrics] AUC: 0.941801 - logloss: 0.278119
2022-01-23 11:30:31,503 P14924 INFO Save best model: monitor(max): 0.941801
2022-01-23 11:30:31,505 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:31,548 P14924 INFO Train loss: 0.263771
2022-01-23 11:30:31,548 P14924 INFO ************ Epoch=6 end ************
2022-01-23 11:30:34,599 P14924 INFO [Metrics] AUC: 0.942304 - logloss: 0.277400
2022-01-23 11:30:34,599 P14924 INFO Save best model: monitor(max): 0.942304
2022-01-23 11:30:34,601 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:34,644 P14924 INFO Train loss: 0.263061
2022-01-23 11:30:34,644 P14924 INFO ************ Epoch=7 end ************
2022-01-23 11:30:37,654 P14924 INFO [Metrics] AUC: 0.942626 - logloss: 0.277860
2022-01-23 11:30:37,655 P14924 INFO Save best model: monitor(max): 0.942626
2022-01-23 11:30:37,657 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:37,698 P14924 INFO Train loss: 0.261910
2022-01-23 11:30:37,698 P14924 INFO ************ Epoch=8 end ************
2022-01-23 11:30:40,702 P14924 INFO [Metrics] AUC: 0.942826 - logloss: 0.278284
2022-01-23 11:30:40,702 P14924 INFO Save best model: monitor(max): 0.942826
2022-01-23 11:30:40,704 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:40,755 P14924 INFO Train loss: 0.261192
2022-01-23 11:30:40,755 P14924 INFO ************ Epoch=9 end ************
2022-01-23 11:30:43,727 P14924 INFO [Metrics] AUC: 0.942972 - logloss: 0.278064
2022-01-23 11:30:43,727 P14924 INFO Save best model: monitor(max): 0.942972
2022-01-23 11:30:43,730 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:43,775 P14924 INFO Train loss: 0.260360
2022-01-23 11:30:43,775 P14924 INFO ************ Epoch=10 end ************
2022-01-23 11:30:46,581 P14924 INFO [Metrics] AUC: 0.943308 - logloss: 0.277826
2022-01-23 11:30:46,582 P14924 INFO Save best model: monitor(max): 0.943308
2022-01-23 11:30:46,584 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:46,631 P14924 INFO Train loss: 0.259994
2022-01-23 11:30:46,631 P14924 INFO ************ Epoch=11 end ************
2022-01-23 11:30:49,148 P14924 INFO [Metrics] AUC: 0.943474 - logloss: 0.277954
2022-01-23 11:30:49,149 P14924 INFO Save best model: monitor(max): 0.943474
2022-01-23 11:30:49,151 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:49,200 P14924 INFO Train loss: 0.259240
2022-01-23 11:30:49,200 P14924 INFO ************ Epoch=12 end ************
2022-01-23 11:30:51,604 P14924 INFO [Metrics] AUC: 0.943540 - logloss: 0.278348
2022-01-23 11:30:51,605 P14924 INFO Save best model: monitor(max): 0.943540
2022-01-23 11:30:51,607 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:51,652 P14924 INFO Train loss: 0.258791
2022-01-23 11:30:51,652 P14924 INFO ************ Epoch=13 end ************
2022-01-23 11:30:54,290 P14924 INFO [Metrics] AUC: 0.943893 - logloss: 0.278089
2022-01-23 11:30:54,290 P14924 INFO Save best model: monitor(max): 0.943893
2022-01-23 11:30:54,293 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:54,339 P14924 INFO Train loss: 0.257718
2022-01-23 11:30:54,340 P14924 INFO ************ Epoch=14 end ************
2022-01-23 11:30:57,291 P14924 INFO [Metrics] AUC: 0.944149 - logloss: 0.277914
2022-01-23 11:30:57,292 P14924 INFO Save best model: monitor(max): 0.944149
2022-01-23 11:30:57,295 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:30:57,342 P14924 INFO Train loss: 0.257244
2022-01-23 11:30:57,342 P14924 INFO ************ Epoch=15 end ************
2022-01-23 11:31:00,242 P14924 INFO [Metrics] AUC: 0.944393 - logloss: 0.278139
2022-01-23 11:31:00,243 P14924 INFO Save best model: monitor(max): 0.944393
2022-01-23 11:31:00,245 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:00,286 P14924 INFO Train loss: 0.256611
2022-01-23 11:31:00,286 P14924 INFO ************ Epoch=16 end ************
2022-01-23 11:31:02,384 P14924 INFO [Metrics] AUC: 0.944793 - logloss: 0.278126
2022-01-23 11:31:02,385 P14924 INFO Save best model: monitor(max): 0.944793
2022-01-23 11:31:02,387 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:02,427 P14924 INFO Train loss: 0.255430
2022-01-23 11:31:02,427 P14924 INFO ************ Epoch=17 end ************
2022-01-23 11:31:04,512 P14924 INFO [Metrics] AUC: 0.945119 - logloss: 0.278179
2022-01-23 11:31:04,513 P14924 INFO Save best model: monitor(max): 0.945119
2022-01-23 11:31:04,515 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:04,565 P14924 INFO Train loss: 0.254041
2022-01-23 11:31:04,565 P14924 INFO ************ Epoch=18 end ************
2022-01-23 11:31:06,698 P14924 INFO [Metrics] AUC: 0.945648 - logloss: 0.277367
2022-01-23 11:31:06,699 P14924 INFO Save best model: monitor(max): 0.945648
2022-01-23 11:31:06,701 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:06,742 P14924 INFO Train loss: 0.252674
2022-01-23 11:31:06,742 P14924 INFO ************ Epoch=19 end ************
2022-01-23 11:31:09,058 P14924 INFO [Metrics] AUC: 0.946376 - logloss: 0.275705
2022-01-23 11:31:09,059 P14924 INFO Save best model: monitor(max): 0.946376
2022-01-23 11:31:09,061 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:09,102 P14924 INFO Train loss: 0.251028
2022-01-23 11:31:09,102 P14924 INFO ************ Epoch=20 end ************
2022-01-23 11:31:11,550 P14924 INFO [Metrics] AUC: 0.946863 - logloss: 0.275998
2022-01-23 11:31:11,550 P14924 INFO Save best model: monitor(max): 0.946863
2022-01-23 11:31:11,552 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:11,593 P14924 INFO Train loss: 0.249175
2022-01-23 11:31:11,593 P14924 INFO ************ Epoch=21 end ************
2022-01-23 11:31:14,312 P14924 INFO [Metrics] AUC: 0.947821 - logloss: 0.275299
2022-01-23 11:31:14,313 P14924 INFO Save best model: monitor(max): 0.947821
2022-01-23 11:31:14,315 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:14,356 P14924 INFO Train loss: 0.246534
2022-01-23 11:31:14,357 P14924 INFO ************ Epoch=22 end ************
2022-01-23 11:31:17,283 P14924 INFO [Metrics] AUC: 0.948791 - logloss: 0.274817
2022-01-23 11:31:17,284 P14924 INFO Save best model: monitor(max): 0.948791
2022-01-23 11:31:17,286 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:17,346 P14924 INFO Train loss: 0.243329
2022-01-23 11:31:17,346 P14924 INFO ************ Epoch=23 end ************
2022-01-23 11:31:19,638 P14924 INFO [Metrics] AUC: 0.949880 - logloss: 0.272579
2022-01-23 11:31:19,638 P14924 INFO Save best model: monitor(max): 0.949880
2022-01-23 11:31:19,640 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:19,685 P14924 INFO Train loss: 0.239416
2022-01-23 11:31:19,685 P14924 INFO ************ Epoch=24 end ************
2022-01-23 11:31:22,098 P14924 INFO [Metrics] AUC: 0.951025 - logloss: 0.273192
2022-01-23 11:31:22,099 P14924 INFO Save best model: monitor(max): 0.951025
2022-01-23 11:31:22,101 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:22,141 P14924 INFO Train loss: 0.235274
2022-01-23 11:31:22,141 P14924 INFO ************ Epoch=25 end ************
2022-01-23 11:31:24,589 P14924 INFO [Metrics] AUC: 0.952513 - logloss: 0.271535
2022-01-23 11:31:24,589 P14924 INFO Save best model: monitor(max): 0.952513
2022-01-23 11:31:24,591 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:24,632 P14924 INFO Train loss: 0.230387
2022-01-23 11:31:24,632 P14924 INFO ************ Epoch=26 end ************
2022-01-23 11:31:27,323 P14924 INFO [Metrics] AUC: 0.953973 - logloss: 0.271341
2022-01-23 11:31:27,324 P14924 INFO Save best model: monitor(max): 0.953973
2022-01-23 11:31:27,326 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:27,387 P14924 INFO Train loss: 0.224959
2022-01-23 11:31:27,387 P14924 INFO ************ Epoch=27 end ************
2022-01-23 11:31:30,340 P14924 INFO [Metrics] AUC: 0.955540 - logloss: 0.265948
2022-01-23 11:31:30,340 P14924 INFO Save best model: monitor(max): 0.955540
2022-01-23 11:31:30,342 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:30,388 P14924 INFO Train loss: 0.219448
2022-01-23 11:31:30,389 P14924 INFO ************ Epoch=28 end ************
2022-01-23 11:31:33,261 P14924 INFO [Metrics] AUC: 0.957064 - logloss: 0.263775
2022-01-23 11:31:33,261 P14924 INFO Save best model: monitor(max): 0.957064
2022-01-23 11:31:33,263 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:33,322 P14924 INFO Train loss: 0.214112
2022-01-23 11:31:33,322 P14924 INFO ************ Epoch=29 end ************
2022-01-23 11:31:36,204 P14924 INFO [Metrics] AUC: 0.957772 - logloss: 0.260482
2022-01-23 11:31:36,205 P14924 INFO Save best model: monitor(max): 0.957772
2022-01-23 11:31:36,207 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:36,255 P14924 INFO Train loss: 0.210238
2022-01-23 11:31:36,255 P14924 INFO ************ Epoch=30 end ************
2022-01-23 11:31:39,223 P14924 INFO [Metrics] AUC: 0.958628 - logloss: 0.259289
2022-01-23 11:31:39,223 P14924 INFO Save best model: monitor(max): 0.958628
2022-01-23 11:31:39,225 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:39,270 P14924 INFO Train loss: 0.206837
2022-01-23 11:31:39,270 P14924 INFO ************ Epoch=31 end ************
2022-01-23 11:31:42,168 P14924 INFO [Metrics] AUC: 0.959118 - logloss: 0.258971
2022-01-23 11:31:42,169 P14924 INFO Save best model: monitor(max): 0.959118
2022-01-23 11:31:42,171 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:42,234 P14924 INFO Train loss: 0.204589
2022-01-23 11:31:42,234 P14924 INFO ************ Epoch=32 end ************
2022-01-23 11:31:45,149 P14924 INFO [Metrics] AUC: 0.959461 - logloss: 0.259702
2022-01-23 11:31:45,149 P14924 INFO Save best model: monitor(max): 0.959461
2022-01-23 11:31:45,151 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:45,191 P14924 INFO Train loss: 0.202308
2022-01-23 11:31:45,191 P14924 INFO ************ Epoch=33 end ************
2022-01-23 11:31:48,197 P14924 INFO [Metrics] AUC: 0.959501 - logloss: 0.261371
2022-01-23 11:31:48,197 P14924 INFO Save best model: monitor(max): 0.959501
2022-01-23 11:31:48,199 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:48,244 P14924 INFO Train loss: 0.200215
2022-01-23 11:31:48,244 P14924 INFO ************ Epoch=34 end ************
2022-01-23 11:31:51,175 P14924 INFO [Metrics] AUC: 0.959842 - logloss: 0.259422
2022-01-23 11:31:51,175 P14924 INFO Save best model: monitor(max): 0.959842
2022-01-23 11:31:51,178 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:51,224 P14924 INFO Train loss: 0.198999
2022-01-23 11:31:51,224 P14924 INFO ************ Epoch=35 end ************
2022-01-23 11:31:54,071 P14924 INFO [Metrics] AUC: 0.960057 - logloss: 0.261712
2022-01-23 11:31:54,071 P14924 INFO Save best model: monitor(max): 0.960057
2022-01-23 11:31:54,073 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:54,114 P14924 INFO Train loss: 0.197197
2022-01-23 11:31:54,114 P14924 INFO ************ Epoch=36 end ************
2022-01-23 11:31:56,915 P14924 INFO [Metrics] AUC: 0.960154 - logloss: 0.268735
2022-01-23 11:31:56,915 P14924 INFO Save best model: monitor(max): 0.960154
2022-01-23 11:31:56,917 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:56,957 P14924 INFO Train loss: 0.196637
2022-01-23 11:31:56,957 P14924 INFO ************ Epoch=37 end ************
2022-01-23 11:31:59,033 P14924 INFO [Metrics] AUC: 0.960150 - logloss: 0.263972
2022-01-23 11:31:59,033 P14924 INFO Monitor(max) STOP: 0.960150 !
2022-01-23 11:31:59,033 P14924 INFO Reduce learning rate on plateau: 0.000100
2022-01-23 11:31:59,033 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:31:59,073 P14924 INFO Train loss: 0.195083
2022-01-23 11:31:59,073 P14924 INFO ************ Epoch=38 end ************
2022-01-23 11:32:01,115 P14924 INFO [Metrics] AUC: 0.960356 - logloss: 0.265173
2022-01-23 11:32:01,116 P14924 INFO Save best model: monitor(max): 0.960356
2022-01-23 11:32:01,118 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:01,164 P14924 INFO Train loss: 0.186806
2022-01-23 11:32:01,164 P14924 INFO ************ Epoch=39 end ************
2022-01-23 11:32:03,384 P14924 INFO [Metrics] AUC: 0.960412 - logloss: 0.265927
2022-01-23 11:32:03,384 P14924 INFO Save best model: monitor(max): 0.960412
2022-01-23 11:32:03,386 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:03,431 P14924 INFO Train loss: 0.186056
2022-01-23 11:32:03,431 P14924 INFO ************ Epoch=40 end ************
2022-01-23 11:32:05,674 P14924 INFO [Metrics] AUC: 0.960407 - logloss: 0.266463
2022-01-23 11:32:05,674 P14924 INFO Monitor(max) STOP: 0.960407 !
2022-01-23 11:32:05,675 P14924 INFO Reduce learning rate on plateau: 0.000010
2022-01-23 11:32:05,675 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:05,720 P14924 INFO Train loss: 0.185187
2022-01-23 11:32:05,720 P14924 INFO ************ Epoch=41 end ************
2022-01-23 11:32:08,753 P14924 INFO [Metrics] AUC: 0.960422 - logloss: 0.266707
2022-01-23 11:32:08,753 P14924 INFO Save best model: monitor(max): 0.960422
2022-01-23 11:32:08,756 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:08,803 P14924 INFO Train loss: 0.184113
2022-01-23 11:32:08,803 P14924 INFO ************ Epoch=42 end ************
2022-01-23 11:32:11,804 P14924 INFO [Metrics] AUC: 0.960425 - logloss: 0.266917
2022-01-23 11:32:11,805 P14924 INFO Save best model: monitor(max): 0.960425
2022-01-23 11:32:11,808 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:11,855 P14924 INFO Train loss: 0.184426
2022-01-23 11:32:11,855 P14924 INFO ************ Epoch=43 end ************
2022-01-23 11:32:14,843 P14924 INFO [Metrics] AUC: 0.960427 - logloss: 0.266888
2022-01-23 11:32:14,843 P14924 INFO Save best model: monitor(max): 0.960427
2022-01-23 11:32:14,845 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:14,886 P14924 INFO Train loss: 0.184690
2022-01-23 11:32:14,886 P14924 INFO ************ Epoch=44 end ************
2022-01-23 11:32:17,825 P14924 INFO [Metrics] AUC: 0.960425 - logloss: 0.267132
2022-01-23 11:32:17,825 P14924 INFO Monitor(max) STOP: 0.960425 !
2022-01-23 11:32:17,825 P14924 INFO Reduce learning rate on plateau: 0.000001
2022-01-23 11:32:17,825 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:17,871 P14924 INFO Train loss: 0.184493
2022-01-23 11:32:17,871 P14924 INFO ************ Epoch=45 end ************
2022-01-23 11:32:20,456 P14924 INFO [Metrics] AUC: 0.960425 - logloss: 0.267137
2022-01-23 11:32:20,456 P14924 INFO Monitor(max) STOP: 0.960425 !
2022-01-23 11:32:20,457 P14924 INFO Reduce learning rate on plateau: 0.000001
2022-01-23 11:32:20,457 P14924 INFO Early stopping at epoch=46
2022-01-23 11:32:20,457 P14924 INFO --- 50/50 batches finished ---
2022-01-23 11:32:20,498 P14924 INFO Train loss: 0.184094
2022-01-23 11:32:20,498 P14924 INFO Training finished.
2022-01-23 11:32:20,498 P14924 INFO Load best model: /home/XXX/FuxiCTR/benchmarks/Frappe/DCN_frappe_x1/frappe_x1_04e961e9/DCN_frappe_x1_005_880c69b8.model
2022-01-23 11:32:20,504 P14924 INFO ****** Validation evaluation ******
2022-01-23 11:32:20,872 P14924 INFO [Metrics] AUC: 0.960427 - logloss: 0.266888
2022-01-23 11:32:20,918 P14924 INFO ******** Test evaluation ********
2022-01-23 11:32:20,918 P14924 INFO Loading data...
2022-01-23 11:32:20,918 P14924 INFO Loading data from h5: ../data/Frappe/frappe_x1_04e961e9/test.h5
2022-01-23 11:32:20,921 P14924 INFO Test samples: total/28860, pos/9536, neg/19324, ratio/33.04%, blocks/1
2022-01-23 11:32:20,921 P14924 INFO Loading test data done.
2022-01-23 11:32:21,209 P14924 INFO [Metrics] AUC: 0.959427 - logloss: 0.271483

```
