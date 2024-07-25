# MPI-InfiniBand-Benchmark

## Description

This repository contains a benchmark tool designed to test the bandwidth of an InfiniBand network using MPI (Message Passing Interface). The program measures the data transfer rate between two nodes within an MPI environment equipped with InfiniBand connectivity.

### Prerequisites
- InfiniBand hardware
- Open MPI installed

### Compilation
To compile the program, use the following command:
```bash
mpicc -o mpi-infiniband-benchmark mpi-infiniband-benchmark.c
```

###Execution
To run the benchmark, use the following command:
```bash
mpirun -np 2 --host [node1],[node2] ./mpi-infiniband-benchmark [time(s)]
```
ex.
```bash
mpirun -np 2 --host hpc1,hpc2 ./mpi-infiniband-benchmark 60
```


---

## 說明

這個倉庫包含了一個用於測試使用 MPI（訊息傳遞介面）的 InfiniBand 網絡帶寬的基準測試工具。該程式用於測量裝備 InfiniBand 連接的 MPI 環境中兩個節點之間的數據傳輸速率。

### 前提條件
- InfiniBand 硬件
- 已安裝 Open MPI

### 編譯
使用以下命令來編譯程式：
```bash
mpicc -o mpi-infiniband-benchmark mpi-infiniband-benchmark.c
```

###執行
使用以下命令來執行基準測試：
```bash
mpirun -np 2 --host [node1],[node2] ./mpi-infiniband-benchmark [time(s)]
```

ex.
```bash
mpirun -np 2 --host hpc1,hpc2 ./mpi-infiniband-benchmark 60
```




---
output:
```
hpc@hpc1:~/shared$ mpirun -np 2 --host hpc1,hpc2 ./mpi-infiniband-benchmark 10
Average bandwidth: 5726.45 MB/s (45.81 Gbps)
Total data transferred: 57266.00 MB
Number of iterations: 28633
Total time: 10.00 seconds
```
