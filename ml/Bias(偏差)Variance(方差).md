<h1>Bias(偏差)和Variance(方差)</h1>


在机器学习中，我们用训练数据集去训练（学习）一个model（模型），通常的做法是定义一个Loss function（误差函数），通过将这个Loss（或者叫error）的最小化过程，来提高模型的性能（performance）。然而我们学习一个模型的目的是为了解决实际的问题（或者说是训练数据集这个领域（field）中的一般化问题），单纯地将训练数据集的loss最小化，并不能保证在解决更一般的问题时模型仍然是最优，甚至不能保证模型是可用的。这个训练数据集的loss与一般化的数据集的loss之间的差异就叫做generalization error。  
而generalization error又可以细分为**Bias**和**Variance**两个部分。  
  
首先如果我们能够获得所有可能的数据集合，并在这个数据集合上将loss最小化，这样学习到的模型就可以称之为“真实模型”，当然，我们是无论如何都不能获得并训练所有可能的数据的，所以“真实模型”肯定存在，但无法获得，我们的最终目标就是去学习一个模型使其更加接近这个真实模型。而bias和variance分别从两个方面来描述了我们学习到的模型与真实模型之间的差距。  

  Bias是 “用所有可能的训练数据集训练出的所有模型的输出的平均值” 与 “真实模型”的输出值之间的差异；  
  Variance则是“不同的训练数据集训练出的模型”的输出值之间的差异。  

这里需要注意的是我们能够用来学习的训练数据集只是全部数据中的一个子集。想象一下我们现在收集几组不同的数据，因为每一组数据的不同，我们学习到模型的最小loss值也会有所不同，当然，它们与“真实模型”的最小loss也是不一样的。  
假设我们现在有一组训练数据，需要训练一个模型（基于梯度的学习，不包括最近邻等方法）。在训练过程的最初，bias很大，因为我们的模型还没有来得及开始学习，也就是与“真实模型”差距很大。然而此时variance却很小，因为训练数据集（training data）还没有来得及对模型产生影响，所以此时将模型应用于“不同的”训练数据集也不会有太大差异。而随着训练过程的进行，bias变小了，因为我们的模型变得“聪明”了，懂得了更多关于“真实模型”的信息，输出值与真实值之间更加接近了。但是如果我们训练得时间太久了，variance就会变得很大，因为我们除了学习到关于真实模型的信息，还学到了许多具体的，只针对我们使用的训练集（真实数据的子集）的信息。而不同的可能训练数据集（真实数据的子集）之间的某些特征和噪声是不一致的，这就导致了我们的模型在很多其他的数据集上就无法获得很好的效果，也就是所谓的overfitting（过学习）。

南大周志华的西瓜书中写道：
```
泛化误差可分解为偏差、方差和噪声之和。  
偏差度量了学习算法的期望预测与真实结果的偏离程度，即刻画了学习算法本身的拟合能力；  
方差度量了同样大小的训练集变动所导致的学习性能变化，即刻画了数据扰动所造成的影响；  
噪声则表达了当前任务上任何学习算法所能达到的期望泛化误差的下届，即刻画了学习问题本身的难度。  

偏差-方差分解说明，泛化性能是由学习算法的能力、数据的充分性以及学习任务本身难度所共同决定的。给定学习任务，为了取得好的泛化性能，则需要使偏差较小，即能够充分拟合数据，并且使方差较小，即使得数据扰动产生的影响小。
```

