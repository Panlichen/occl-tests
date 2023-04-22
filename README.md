Tests for both [NCCL](https://github.com/NVIDIA/nccl) and [OCCL](https://github.com/Oneflow-Inc/occl).

## Compiling

```shell
make src.build -j<n> NCCL_HOME=path-to-occl/build
make src_simple.build -j<n> NCCL_HOME=path-to-occl/build
make src_chaos_order.build -j<n> NCCL_HOME=path-to-occl/build
```
and for experiments with MPI:
```shell
make src.build -j<n> MPI=1 MPI_HOME=path-to-mpi NCCL_HOME=path-to-occl/build
make src_simple.build -j<n> MPI=1 MPI_HOME=path-to-mpi NCCL_HOME=path-to-occl/build
```
> Using `-gencode=arch=compute_86,code=sm_86` for `NVCC_GENCODE` by default. Set the `NVCC_GENCODE` environment variable when needed.

## Running
```shell
bash nccl_tests.sh <NUM_GPUS> <COLL_FUNC> <BUFFER_SIZE>
bash occl_tests.sh <NUM_GPUS> <COLL_FUNC> <BUFFER_SIZE>
```
- Supported `COLL_FUNC` includes `AR`, `AG`, `RS`, `R`, and `B`, representing all-reduce, all-gather, reduce-scatter, reduce, and broadcast.

and for experiments with MPI:
```shell
bash mpi_nccl_tests.sh <NUM_GPUS_PER_NODE> <COLL_FUNC> <BUFFER_SIZE>
bash mpi_occl_tests.sh <NUM_GPUS_PER_NODE> <COLL_FUNC> <BUFFER_SIZE>
```

To demonstrate OCCL's deadlock-prevention capability:
```shell
export BINARY=CHAOS
bash occl_tests.sh 8
```
