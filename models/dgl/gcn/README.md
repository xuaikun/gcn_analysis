Graph Convolutional Networks (GCN)
============

- Paper link: [https://arxiv.org/abs/1609.02907](https://arxiv.org/abs/1609.02907)
- Author's code repo: [https://github.com/tkipf/gcn](https://github.com/tkipf/gcn). Note that the original code is 
implemented with Tensorflow for the paper. 

Dependencies
------------
- PyTorch 0.4.1+
- requests

``bash
pip install torch requests
``

Codes
-----
The folder contains three implementations of GCN:
- `gcn.py` uses DGL's predefined graph convolution module.
- `gcn_mp.py` uses user-defined message and reduce functions.
- `gcn_spmv.py` improves from `gcn_mp.py` by using DGL's builtin functions
   so SPMV optimization could be applied.
Modify `train.py` to switch between different implementations.

Results
-------

Run with following (available dataset: "cora", "citeseer", "pubmed")
```bash
python3 train.py --dataset cora --gpu 0 --self-loop
```

* cora: ~0.810 (0.79-0.83) (paper: 0.815)
* citeseer: 0.707 (paper: 0.703)
* pubmed: 0.792 (paper: 0.790)
* GAT Amazon2M 30GB+ GPU MemoError

| Model | Settings | GpuMemory(MB) | Acc   | Time/epoch(s) | Overall Time(s) |
| ----- | -------- | ------------- | ----- | ------------- | --------------- |
| GCN   | h=16     | 9007          | 78.20 | 0.1935        | 37.4            |
| GCN   | h=64     | 12677         | 82.48 | 0.3195        | 162.1           |
| GCN   | h=128    | 14381         | 83.42 | 0.4318        | 198.61          |

