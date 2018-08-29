# Paxos
* 容错的分布式一致性算法
* 角色：proposer 提出者，acceptor 参与投票者，leader 执行者；
* 过程(每一轮仅讨论一个值)
    1. 客户端发送请求给proposer；
    2. proposer决定成为leader，向acceptor发送proposal N；acceptor：如果N大于之前最大的，则返回 past proposal中最大的N和值V；
    3. leader依据返回值V判断实际该讨论的值应是返回值V还是new value，再将值发给learner执行；
    4. 将结果反馈给 Client；
* 算法两阶段
    1. 阶段 1：
        * a）Proposer：选择议案编号n，向acceptor的多数派发送prepare请求；
        * b）Acceptor：如果接收到的prepare请求编号n 大于它已回应的任何prepare请求，则回应已批准的编号最高的议案，并承诺不再回应编号小于n的议案；
    2. 阶段 2：
        * a） Proposer：如果收到多数acceptor对 prepare请求（编号为 n）的回应，则向这些 acceptor发送议案{n,v}的accept请求，v是所有回应中编号最高的议案的决议，或如果回应中没有议案，则是proposer选择的值； 
        * b）Acceptor：如果收到了议案{n,v}的accept请求，就批准该议案；