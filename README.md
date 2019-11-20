# hadoop-0.1.0-20191120-002
init
Hadoop 0.1.0分析

LocalJobRunner是本地实现
  run方法中
  获得input文件分片
  每个分片用一个MapTask运行
