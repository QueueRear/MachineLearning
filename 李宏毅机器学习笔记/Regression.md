## Regression
- **基础步骤**
    - **建立模型（Model）**：含有位置参数的函数
        - 线性模型 $y = b + \sum w_i x_i$ 中 $x_i$ 是各种输入，称作 **feature**；$w_i$ 是**权重**（weight），$b$ 是**偏置**（bias）。
        - 用上标表示一个完整的对象（object）的编号，例如 $x^1$；用下标表示一个组成（component），例如 $x_1$；训练集中某一对象的函数输出值用尖（hat）表示，例如 $\hat{y}^1$，它是一个精确的、实际观测得到的值。Structure learning 中输出的 object 可能是有结构的，所以输出也可能有下标。
    - **建立损失函数（Loss Function）**：评估模型的好坏
        - 输入是一个函数，输出是这个函数有多差，也可以说是在衡量一组参数的好坏，例如 $$L(f) = L(w, b) = \sum_{n=1}^{10} (\hat{y}^n - (b + w \cdot\ x_0^n))^2 $$，即实际结果与预测结果之差的平方和。
    - **寻找最佳函数**
        - $f^* = arg \mathop{min}\limits_f L(f)$ 找到一个 $f$ 使损失函数最小。
        - $$ \begin{split} w^*, b^* ={} & arg \mathop{min}\limits_{w, b} L(w, b) \\ ={} & arg \mathop{min}\limits_{w, b} \sum_{n=1}^{10} (\hat{y}^n - (b + w \cdot\ x_0^n))^2 \end{split} $$
        找到一组参数 {w, b} 使得损失函数最小。
        - **梯度下降法**（Gradient Descent）找出最佳函数。
        对于损失函数 $L(w)$：
            - 随机选取一个初始值 $w^0$。
            - 计算损失函数在该点对 w 的微分 $ \left.\tfrac{dL}{dw}\right|_{w=w^0} $。
            - 更新 $w$ 的值。值为正说明该点左侧损失较小，$w$ 应减小；值为负应增大。
            $$ w^1 \leftarrow w^0 - η \left.\tfrac{dL}{dw}\right|_{w=w^0} $$
            - 其中 $η$ 是学习率（learning rate），也叫步长因子。
            - 重新计算新的 $w$ 对应的微分。
            - 循环往复直至得到一个局部最优解（Local Optimal）$w_T$，是一个导数为零的点，可能并非全局最优解【线性模型中不会出现局部最优解的状况】。
        - **推广到多个参数的情况**
            - 随机选取一组初始值 $\{w^0, b^0\}$。
            - 计算损失函数在该点的偏微分 $ \left.\tfrac{\partial L}{\partial w}\right|_{w=w^0, b=b^0} $ 和 $ \left.\tfrac{\partial L}{\partial b}\right|_{w=w^0, b=b^0} $。
            - 更新 $\{w^0, b^0\}$ 的值。
            $$ w^1 \leftarrow w^0 - η \left.\tfrac{\partial L}{\partial w}\right|_{w=w^0} $$
            $$ b^1 \leftarrow b^0 - η \left.\tfrac{\partial L}{\partial b}\right|_{b=b^0} $$
            - 重新计算新的 $\{w, b\}$ 对应的微分。
            - 循环往复直至得到一个局部最优解。
            > 此处的偏微分分别为
            $\tfrac{\partial L}{\partial w}=\sum\limits_n 2(\hat{y}^n - (b + w \cdot\ x_0^n))(-x_0^n) $
            $\tfrac{\partial L}{\partial w}=\sum\limits_n 2(\hat{y}^n - (b + w \cdot\ x_0^n))(-1) $
        - 在线性回归模型中的损失函数是一个凸函数，所以不会有局部最优解的情况。
    - **评估误差（Error）**
        - 在训练集上的平均误差 $\frac {1}{n} \sum\limits_{i=1}^{n} e^i$，其中 $e^i$ 是训练集中各对象与模型估测的误差
        - **泛化性能（Generalization）**：在测试集上的表现。这是更需要关心的问题。
        $\frac {1}{n} \sum\limits_{i=1}^{n} e^i$，其中 $e^i$ 是测试集中各对象与模型估测的误差。