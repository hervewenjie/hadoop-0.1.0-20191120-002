# hadoop-0.1.0-20191120-002
init
Hadoop 0.1.0分析

# 本地模式

LocalJobRunner是本地实现JobSubmissionProtocol
  run方法中
  获得input文件分片
  每个分片用一个MapTask运行
  
  - 生成/tmp/hadoop/mapred/system/submit_cmpf5v/job.xml, 记录系统任务提交
  - 生成/tmp/hadoop/mapred/local/job_fj9brf.xml/localRunner
  - 每个分片FileSplit运行一个MapTask
  - MapRunner对于每个记录
      - 运行map函数, 写入Collector
      - Collector根据partition数量创建SequenceFile.Writer, 写入partition
      - 写入路径/tmp/hadoop/mapred/local/part-0.out/map_8cqxob
  - CombiningCollector缓存一个key对于一个list, 在被发送到reducer之前, 减少网络传输
  - MapTask运行完成生成/tmp/hadoop/mapred/local/part-0.out/map_crhuf5
  - reduce任务生成/tmp/hadoop/mapred/local/map_crhuf5.out, remove文件/tmp/hadoop/mapred/local/part-0.out/map_crhuf5
  - ReduceTask
      - 把map的输出copy到一个文件中
      - sort这个文件的key对应的value
      - 运行reduce函数
  
# 集群模式

JobTracker是集群模式实现JobSubmissionProtocol
