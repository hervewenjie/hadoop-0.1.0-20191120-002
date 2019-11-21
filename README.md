# hadoop-0.1.0-20191120-002
init
Hadoop 0.1.0分析

LocalJobRunner是本地实现
  run方法中
  获得input文件分片
  每个分片用一个MapTask运行
  
  - 生成/tmp/hadoop/mapred/system/submit_cmpf5v/job.xml, 记录系统任务提交
  - 生成/tmp/hadoop/mapred/local/job_fj9brf.xml/localRunner
  - 每个分片FileSplit运行一个MapTask
  - MapTask运行完成生成/tmp/hadoop/mapred/local/part-0.out/map_crhuf5
  - reduce任务生成/tmp/hadoop/mapred/local/map_crhuf5.out, remove文件/tmp/hadoop/mapred/local/part-0.out/map_crhuf5
  - 运行ReduceTask
  
