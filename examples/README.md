# Examples for the use of DAG/GTN network 

Demonstrate how to build the DAG/GTN network by combining the Node Data (`n_data.m`) and the Transformers (`tf_xxx`) for your own task, i.e., how to wrap the APIs in the directory `./matlab_dag`. The GTN can be as simple as 
the common feed forward neural network, or as complicated as the TODO. The wrapping we demonstrate in this directory is similar to how `./examples/cnn_train.m` and `./matlab/vl_simplenn.m` wrap the `vl_nnxxx` APIs. 

## Desgin Concept
- The whole DAG is viewed as a big transformer, derived from `tfw_i`, i.e., a DAG (transformer) can be the composition of many small DAGs (transformers). 
- Explicit CPU version or GPU version
- The class `convdag.m` is thin wrapper of the DAG, managing the training and testing
- An auxiliary class `convdag_peek.m` probes the state of `convdag.m` and does the job like printing/plotting/saving (the Observer Design Pattern).  

## Purposes of the Examples
It is suggested that the following examples are read sequentially:

- `tfw_lenetDropout` and `mnist_small_tr_lenetDropout`. The "LeNet" for mnist dataset and its caller, which demonstrate how to:
  - switch between CPU or GPU computation
  - set the connection of a network
  - initialize the parameters with customized strategies, e.g., Gaussian with std involving number of fan-in and fan-out
  - apply a certain numeric optimization, e.g., SGD with different step size at each layer
  - set the observer and plot, save model, etc. 

- `tfw_MLP` and `mnist_small_tr_MLP`. A two hidden layers MLP for mnist and its caller, which demonstrate how to
  - Build the DAG recursively using `tfw_xxx`

- `tfw_lenetTriCon`, `mnist_small_lenetTriCon`: The modified "LeNet" with triangular connection (i.e., a non-trivial directed acyclic connection) at the second last layer and its caller, which demonstrate how to:
  - set the triangular connection

- `tfw_cifar` and `cifar_tr.m`. The same network structure with that of `vlfeat/matconvnet/examples/cnn_cifar.m` for cifar-10 dataset. They demonstrate:
  - The Abstraction Penalty of the DAG class hierarchy in this project is negligible 
