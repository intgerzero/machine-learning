# machine-learning
参照《统计学习方法》实现了大部分的机器学习算法。  

下面简要叙述一下设计这个工程的思路。  

对于一条机器学习的pipeline来说，从读入数据到展示结果，必然包含了许多作为独立学习算法的子过程，将每个机器学习算法写成一个类结构，并尝试封装出普遍的接口，对于自由组合这些机器学习算法来说
是十分必要的。  
首先，数据被定义为具有如下特点的4种类型：
- 基于数值数据的监督分类数据
- 基于字符数据的监督分类数据
- 基于数值数据的监督回归数据
- 基于数值数据的无监督数据  

数据类和算法类是分离的，在每个算法类中都有一个智能指针shared_ptr<data>来实现数据的共享。我们希望在传入数据时，必须先有一个数据类保存了数据，而算法类的构造函数传入shared_ptr<data>参数，来实现在算法类的成员函数中自由调用数据的目的，同时避免数据的拷贝。

每个算法类都有类似的组成，都包括一个训练函数，一个预测函数，预测函数的输入是4中数据类的一种特征类型，输出也是监督数据类的一种类标类型。类似的组成为后面的归一化设计逻辑做铺垫，但目前还未实现基于继承和多态的体系。

