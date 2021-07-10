# 车辆和硬件传感器
自动驾驶使用线控车辆，区别于传统车辆使用方向盘、油门和刹车控制车辆  
- 控制器区域网络（CAN)  
- GPS
- LIDAR：360度扫描车身周围的障碍物
- 惯性导航装置IMU
- 相机：例如感知中使用相机区分红绿灯的颜色
- radar：分辨率较低，无法用于区分障碍物类型，擅长于测量其他车辆的速度
---
# 软件架构
## 实时操作系统RTOS
real-time operating system  
确保在给定时间内完成指定任务    
Apollo RTOS = Ubuntu Linux + Apollo内核 
原生的Ubuntu系统并非RTOS    
## 运行时框架
定制版的ROS：机器人实时操作系统  
ROS系统内部的模块相互独立，是最广泛的机器人系统框架     
Apollo的改进    
- 共享内存  
降低了需要访问不同模块时的数据复制需求  
基于共享内存，实现了一次写入，多次读取的模式    
- 去中心化  
解决了单点故障的问题    
现成的ROS需要有单个ROS主节点来控制其他模块的所有节点，主节点出问题系统就失效    
Apollo使用公共域（Domain），所有节点都放在公共域内，域中每个节点都保存有其他节点的信息
- 数据兼容性    
使用protobuf替代了原生ROS消息协议   
序列化的消息    
增加字段后不影响后向兼容性  
## 应用程序模块层
- MAP engine
- Localization
- Perception
- Planning
- Control
- End-to-End
- HMI
