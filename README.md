# tugraph-test
赛题链接 [基于TuGraph Analytics的⾼性能图模式匹配算法设计](https://www.datafountain.cn/competitions/975)
## 运行环境:Linux机器 E5-2680v4 16核 32G内存: 总耗时 12S-13S之间
## 主要优化手段
1. 参数配置，工作线程数经过实验使用8为最佳；GC策略不使用G1而使用ParallelGc，并调大新生代及Eden区空间，进而提升内存分配吞吐量
2. 预读取文件，预创建文件，并且多线程并发读取/写入，优化了阶段2/9的耗时，详见readAllData()/writeFiles()及其调用处
3. 自定义实现了高效Kryo序列化器的顶点/边/消息结构体，极大的提升了图序列化效率，在构图/计算阶段带来了20%左右的提升；详见
   PVertex/PEdge/MValue类定义
