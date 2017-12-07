Eureka
=====
[![Build Status](https://netflixoss.ci.cloudbees.com/job/NetflixOSS/job/eureka/job/eureka-snapshot/badge/icon)](https://netflixoss.ci.cloudbees.com/job/NetflixOSS/job/eureka/job/eureka-snapshot/)

Eureka is a REST (Representational State Transfer) based service that is primarily used in the AWS cloud for locating services for the purpose of load balancing and failover of middle-tier servers.

At Netflix, Eureka is used for the following purposes apart from playing a critical part in mid-tier load balancing.

* For aiding Netflix Asgard - an open source service which makes cloud deployments easier, in  
    + Fast rollback of versions in case of problems avoiding the re-launch of 100's of instances which 
      could take a long time.
    + In rolling pushes, for avoiding propagation of a new version to all instances in case of problems.

* For our cassandra deployments to take instances out of traffic for maintenance.

* For our memcached caching services to identify the list of nodes in the ring.

* For carrying other additional application specific metadata about services for various other reasons.


Building
----------
The build requires java8 because of some required libraries that are java8 (servo), but the source and target compatibility are still set to 1.7.


Support
----------
[Eureka Google Group](https://groups.google.com/forum/?fromgroups#!forum/eureka_netflix)


Documentation
--------------
Please see [wiki](https://github.com/Netflix/eureka/wiki) for detailed documentation.

同步原作者的代码
--------------
    进入刚才clone的文件目录下，然后增加源分支地址到你项目远程分支列表中，命令是
    git remote add Netflix https://github.com/Netflix/eureka.git
    fetch源分支到本地，命令是：
    git fetch Netflix
    合并两个版本的代码
    git merge Netflix/master
    最后一步，把合并后的代码push到你的Github项目上去，这步需要你输入你的账户名和密码
    git push origin master
 eureka-core 模块包含了功能的核心实现: 
 --------------     
    1. com.netflix.eureka.cluster - 与peer节点复制(replication)相关的功能 
    2. com.netflix.eureka.lease - 即”租约”, 用来控制注册信息的生命周期(添加、清除、续约) 
    3. com.netflix.eureka.registry - 存储、查询服务注册信息 
    4. com.netflix.eureka.resources - RESTful风格中的”R”, 即资源。相当于SpringMVC中的Controller 
    5. com.netflix.eureka.transport - 发送HTTP请求的客户端，如发送心跳 
    6. com.netflix.eureka.aws - 与amazon AWS服务相关的类
    
  eureka-client模块: 
  --------------   
    Eureka客户端，微服务通过该客户端与Eureka进行通讯，屏蔽了通讯细节
    
  eureka-server模块: 
  --------------   
    包含了 servlet 应用的基本配置，如 web.xml。构建成功后在该模块下会生成可部署的war包。
   其他
   -----