# ann-benchmark
Benchmarks of artificial neural network library for Spark MLlib

##Prerequisites
### OpenBLAS
  - Download, compile and install OpenBLAS https://github.com/xianyi/OpenBLAS
  - Add OpenBLAS to your library path:
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/your/openblas
```
  - Create symlink to OpenBLAS within its folder
```
ln -s libopenblas.so libblas.so.3
```
  - You need to have gcc libs not less than v.4.8 in your library path `gcc -v`
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/your/openblas:/gcc-4.8.2/lib
```

## Benchmark
### Spark
  - Clone Spark from https://github.com/avulanov/spark/tree/ann-interface-gemm
  - Compile Spark with `-Pnetlib-lgpl` flag to use native BLAS
  - Deploy Spark on N-node cluster
  - Download mnist dataset: http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass/mnist.scale.bz2 

### Caffe
  - Download Caffe
  - Configure `Makefile.config` to point to the same OpenBLAS lib (and CUDA) as for Spark
  - Compile Caffe
  - Set environment variable:
```    
export $CAFFE=/your/caffe/
```
  - Download mnist dataset and convert it to lmdb: 
```
$CAFFE/data/mnist/get_mnist.sh
$CAFFE/examples/mnist/create_mnist.sh
```
  - Run the benchmark with the model provided:
```
$CAFFE/build/tools/caffe train --solver=mnist-lmdb-5h.solver
```
