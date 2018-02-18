# 软件体系结构
## 4+1 View
* 逻辑视图：{部件，连接件，配置}   
    * UML表示需要进行一定的调整
        * 部件：以构造型`<<component>>`扩展了的类来描述
        * 连接件：以构造型`<<connector>>`扩展了的类来描述
        * 部件/连接件的特征：以构造型`<<property>>`扩展了的属性来描述
        *  规则：以协议状态机来描述
    * Viewer：End-user
    * 作用：功能分布，需求分配
* 开发视图：系统的物理模块划分
    * UML表示：构件图，是物理包
    * Viewer：程序员、开发管理者
    * 分模块，任务分配，判定可复用性和可修改性
* 进程视图：适用于多进程系统
    * UML表示：进程：以UML主动类（Active Class）来描述
    * Viewer：系统综合考虑者
* 物理视图：与硬件资源相关
    * UML表示：部署图（体现进程的部署，体现开发构件的部署）
    * Viewer：系统工程师
* Scenarios：需求做，联系4个视图
    * 展现合理性，帮助设计和验证

## 物理包的6个设计原则
* REP重用发布原则：Release Reuse Equivalency Principle，重用的粒度就是发布的粒度
* ADP无环依赖原则：Acyclic Dependencies Principle，不存在循环依赖
* SAP稳定抽象原则：Stable Abstractions Principle，包的抽象程度与其稳定程度一致
* SDP稳定依赖原则：Stable Dependencies Principle，包要依赖的包要比自己更具稳定性
* CCP共同封闭原则：Common Closure Principle，保证所有类对于同一性质的变化应该是共同封闭的
* CRP共同重用原则：Common Reuse Principle，一个包中所有类应该是共同重用的