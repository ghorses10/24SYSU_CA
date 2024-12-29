SuperLU_DIST：https://github.com/xiaoyeli/superlu_dist

PanguLU：https://github.com/SuperScientificSoftwareLaboratory/PanguLU

SuiteSparse Matrix数据集下载地址：https://sparse.tamu.edu/



### PanguLU：

首先需要安装PanguLU。

安装完成后，按需修改Makefile中对应库的位置，接下来就可以`make all`编译了。

~~~sh
LINK_METIS = /path/to/libmetis.a /path/to/libGKlib.a
OPENBLAS_LIB = /path/to/libopenblas.a
LINK_CUDA = -L/path/to/cuda/lib64 -lcudart -lcusparse -lstdc++
LINK_PANGULU = ../lib/libpangulu.a # Derictly importing static library as compiler input makes dynamic library loader searching the directory of static library.
~~~



编译完成后，可通过`run.sh`编译测试文件：

~~~sh
 bash ./run.sh path_to_mtx block_size process_count
~~~

其中：

- **process_count**: 启动 **PanguLU** 所需的 MPI 进程数；
- **block_size**: 每个非零块的块大小；
- **path_to_mtx**: 以 mtx 格式存储的矩阵文件的路径。

或者直接使用MPI编译：

~~~sh
mpirun-np process_count ./pangulu_example.elf-nb block_size-f path_to_mtx
~~~



### SuperLU_DIST

同理，首先需要按安装SuperLU_DIST。

随后可按需编译不同的程序进行测试。

~~~sh
mpiexec -n <总进程数> pddrive3d -r <行进程数> -c <列进程数> -d <Z维度进程数> g20.rua  
（例如：mpiexec -n 8 pddrive3d -r 2 -c 2 -d 2 g20.rua）  
~~~





























